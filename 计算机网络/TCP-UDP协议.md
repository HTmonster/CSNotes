# TCP/UDP

#### 计算机网络图

![æ¥çæºå¾å](https://images2015.cnblogs.com/blog/731716/201606/731716-20160621162533006-795255031.png)

#### TCP与UDP对比



|                     TCP                     |                 UDP                  |
| :-----------------------------------------: | :----------------------------------: |
| 传输控制协议(Tranmission Control Protocols) | 用户数据报协议（User Data Protocols) |
|                  面向连接                   |                非连接                |
|                  可靠传输                   |       非可靠传输（依赖应用层）       |
|                   有确认                    |                无确认                |
|           面向字节流（字节排序）            |               面向报文               |
|               20字节固定TCP头               |              8字节UDP头              |
|             流量控制和拥塞控制              |                  无                  |
|                   一对一                    |         一对一 一对多 多对多         |

#### TCP建立连接与释放连接

- **建立连接（**三次握手）

  - A机向B机发送建立连接请求（SYN=1 seq=x)

  - B机向A机发送回应信息 （SYN=1 ACK=1 seq=y ack=x+1)

  - A机向B机进行回应确认  （ACK=1 seq=x+1 ack=y+1)  

    ![image](https://images0.cnblogs.com/blog/385532/201308/30193702-7287165c73e7440382207309e07fcbb5.png)

  - **三次握手必要性**：

    - A第一个请求在网络中延迟（失效）
    - B接受到建立连接（对失效连接建立）
    - 浪费资源

- **解除连接**（四次握手）

  - A向B发送解除连接请求 （FIN=1 seq=x)

  - B向A发送已经确认接受信息 （ACK=1 seq=y ack=x+1)

  - B处理好后对A发送已经关闭信息 （FIN=1 ACK=1 seq=w ack=x+1)

  - A向B发送接受确认信息 （ACK=1 seq=x+1 ack=w+1)

    ![img](https://images0.cnblogs.com/blog/385532/201308/30193703-63640062b79a4fc8b8ed31e95fd87bd8.png)

  - **TIME-WAIT状态**

    - 等待2MSL(Maximum Segment Lifetime)最大报文生存时间
    - 确保服务器端已经收到ACK信号
    - 避免资源浪费

#### TCP传输数据

![img](http://c.biancheng.net/cpp/uploads/allimg/151106/1-151106134A4196.jpg)

- **超时重传时间（RTO retransmission Time OUT)**
  -  **过大**：不必要的等待
  -  **过小**：不必要的重传
  - **理论最佳**：RTT（Round-Trip Time) 往返时间 发送-接受到ACK确认包
  - **实际应用**：自适应动态算法（Jacobson算法 Karn算法）
- **重传次数**
  - 根据系统设置的不同有所区别
  - 重传三次

#### 常见应用

- ![img](https://images0.cnblogs.com/blog/385532/201308/30193704-d65f24c7ddea474ab3236bd701650059.png)
