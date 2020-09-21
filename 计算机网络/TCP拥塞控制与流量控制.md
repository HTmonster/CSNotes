# TCP拥塞控制与流量控制

#### 拥塞控制与流量控制区别

- **拥塞控制**防止过多的数据到达网咯中  全局性
- **流量控制**点对点通信量控制（主要是 抑制发送端发送速率）端到端

#### 流量控制——滑动窗口

![img](http://up.2cto.com/2013/0923/20130923092130492.jpeg)

- **接收窗口 rwnd**

  - 接收端缓冲区大小  TCP报文首部发送给发送端

- **拥塞窗口 cwnd**

  -  发送端的缓冲区大小

- **发送窗口 swnd**

  - $$
    swnd=Min[rwnd,cwnd]
    $$

    

#### 拥塞控制

![img](http://up.2cto.com/2013/0923/20130923092139371.jpeg)

![å¢å å¿"éä¼ ä¸å¿"æ¢å¤](https://img-blog.csdn.net/20180610195515179?2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3NodXhuaHM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

1. **慢开始**

   - ![æ¯ç"è¿ä¸ä¸ªä¼ è¾è½®æ¬¡ï¼cnwdææ°å¢é¿](https://img-blog.csdn.net/20180610191717379?2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3NodXhuaHM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

   - cwnd = 1(MSS最大报文端 字节为单位)
   - 指数增长
   - cwnd<ssthresh（慢开始门限）
   - ssthresh不变

2. **拥塞避免**

   - 【加法增大】线性增 ssthresh++ cwnd++
   - 【乘法减小】出现超时 ：cwnd=1, ssthresh=ssthresh/2

3. **快重传**

   ![å¿"éä¼ ç¤ºæå¾](https://img-blog.csdn.net/20180610195854523?2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3NodXhuaHM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

   - 一连收到三个重复确认 不必等到重传计时器时间到期

4. **快恢复**

   - 【乘法减小】三个重复确认 cwnd=ssthresh=ssthresh/2

