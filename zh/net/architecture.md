# 设计与流程

![Alt text](https://static.oschina.net/uploads/space/2017/1109/170753_f0T7_3724856.jpg "设计")

图中是整个网络层的设计以及报文的处理流程。分为client和server端，client负责创建连接，报文的封包和拆包。服务器除此之外还要维护客户端连接，保证连接能接收数据。缓存队列可以缓存突发流程的，保证程序的可靠性。

客户端首先创建连接，连接创建成功，发送消息并等待响应消息。发送消息前会将报文进行编码，接收到消息后也会将消息进行解码。

服务器端会启动端口监听，接收来自客户端的连接。当有连接连上的时候，服务端用一个新的Goroutine接收客户端连接。当接收到一个客户端发送的消息时，会将消息发到队列中，然后会从队列中取出消息进行粘包。最后将完整的报文交给业务进行处理并响应。这里说明一点的是，队列和粘包都针对的单个连接，减少资源的竞争。
