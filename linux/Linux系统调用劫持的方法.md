### Linux函数调用劫持的方法总结

> 参考文章：
>
> https://www.cnblogs.com/LittleHann/p/3854977.html
>
> https://lwn.net/Articles/132196/
>
> https://blog.csdn.net/andy205214/article/details/77148573
>
> https://www.cnblogs.com/arnoldlu/p/9752061.html

#### 1.概览

- Ring3中劫持

  1. 基于环境变量LD_PRELOAD的动态库劫持

- Ring0中劫持

  1.  Kernel Inline Hook

  2.  syscall table修改
  3. 内核调试机制Kprobe

#### 2. Ring3函数调用劫持

​	在Linux中，动态库加载的时候，会按照以下顺序进行搜索：LD_PRELOAD  >LD_LIBRARY_PATH >/etc/ld.so.cache>/lib>/usr/lib

​	方法原理：通过LD_PERELOAD设置编写自己的so库函数在原正常函数前执行

**例子：劫持gets()函数**

```sequence
程序-->hook.so:LD_PRELOAD优先链接
Note Right of hook.so:(此处执行额外的操作)
hook.so-->libc.so:dlsym调用原函数
libc.so-->hook.so:正常执行，返回值
hook.so-->程序:执行完成，返回值


```

###### 1. 编写自定义的动态链接库源码hook.c

```C
#include<stdio.h>
#include<dlfcn.h> //用于搜索原函数

/* 要求：函数的形式必须和原函数一样（返回类型，函数名，函数参数）*/
char* gets(char* str){
    
    /* 自定义的操作区域 */
    printf("hook gets! str: %s\n ",str);
    
    /* 调用原函数*/
    typeof(gets)  *func;//函数指针
    func=dlsym(RTLD_NEXT,"gets");//查找malloc函数位置  dlsym:在打开的动态库里找一个函数
    return (*func)(str); //调用原函数执行
}
```

###### 2.编译成共享库

```shell
gcc hook.c -fPIC -shared -ldl -D_GNU_SOURCE -o hook.so
```

- -fPIC: 编译器就输出位置无关目标码.适用于动态连接
- -shared: 生成共享目标文件

###### 3.设置LD_PRELOAD

> 通过设置环境变量的方法
>
> - 临时设置  export LD_PRELOAD=$PWD/hook.so
> - 永久设置 
>   - 修改profile文件  加入 export LD_PRELOAD=${YOUR PATH}/hook.so
>   - 修改.bashrc文件  加入 export LD_PRELOAD=${YOUR PATH}/hook.so

- 编写一个测试程序test.c

  ```c
  #include <stdio.h>
  
  int main(){
      char str[20]="\0";
      printf("请输入\n");
      gets(str);
      return 0;
  }
  ```


- 函数调用劫持效果

  ![](http://images.htmonster.xyz/img/20200520/HS1XJhwK65vU.png?imageslim)

  

#### 3.Ring0系统调用劫持

##### 3.1 Kernel Inline Hook

原理：一个系统调用会调用子函数的，这是通过<u>段内偏移</u>的方式完成的，我们可以通过设置这个偏移指向我们Hook的原函数

**例子：劫持sys_read系统调用**

![](http://images.htmonster.xyz/img/20200520/Hj1p3uvm9cwP.png?imageslim)

##### 3.2 sys_call_table修改方法进行系统调用劫持

原理：将系统调用表中对应的服务例程修改为自己Hook函数的地址

**例子：劫持fork()**

![](http://images.htmonster.xyz/img/20200520/7LWfqxcGHkgI.png?imageslim)

###### 查找syscall_table位置的方法

1. 代码模拟出call *sys_call_table(,%eax,4)，然后查看机器码查找
2. 通过/boot/System.map-2.6.32-358.el6.i686文件查找
3. 通过/proc/kallsyms进行搜索

##### 3.3 内核调试机制kprobe进行系统调用劫持

###### Kprobe介绍

- 轻量级内核调试机制

###### Kprobe两种使用方法

- 模块加载
- debugfs接口

###### Kprobe三种探测手段

- kprobe  基本的探测手段 基础  可以在函数内任意位置放置探测点
- jprobe  探测在函数的入口，可以方便的获得函数参数，但是每个函数只能有一个探针
- Kretprobe 探测在函数的返回值

**例子:劫持execve()**

```c

#include <linux/kernel.h>
#include <linux/module.h>
#include <linux/kprobes.h>

int jsys_execve(const char __user *filename,
		const char __user *const __user *__argv,
		const char __user *const __user *__envp)
{
  	pr_info("jprobe: execve: %s\n", filename);

	/* Always end with a call to jprobe_return(). */
  	jprobe_return();
  	return 0;
}

static struct jprobe jprobe_execve = {
	.entry= jsys_execve,
	.kp = {
		.symbol_name	= "sys_execve",
	},
};

static int __init mymodule_init(void){
    int ret;

	/* 挂载 hook */
	ret = register_jprobe(&jprobe_execve);
	if (ret < 0) {
		pr_info("register_jprobe failed, returned %d\n", ret);
		return -1;
	}
	pr_info("Planted jprobe execve at %p, handler addr %p\n",
	       jprobe_execve.kp.addr, jprobe_execve.entry);
    
    return 0;
}

static void __exit mymodule_exit(void)
{
	unregister_jprobe(&jprobe_execve);
}


module_init(mymodule_init)
module_exit(mymodule_exit)
MODULE_LICENSE("GPL");
```

运行效果：

![](http://images.htmonster.xyz/img/20200520/VBuDxCximadA.png?imageslim)

##### 4.总结

| 方法               | 优点                        | 缺点                                                         |
| ------------------ | --------------------------- | ------------------------------------------------------------ |
| LD_PRELOAD         | 针对函数调用，简单          | 1.容易发生循环调用问题 2. 部分情况不适用（文件的SUID或SGID位被置1，加载的时候会**忽略**LD_PRELOAD） |
| Kernel Inline Hook |                             | 实现比较难                                                   |
| sys_call_table修改 | 负载小                      | 需要查找系统调用表地址                                       |
| kprobe             | 内核支持  使用简单 安全性高 | 需要内核特性keprobe特性支持，一些系统需要重新编译内核        |

