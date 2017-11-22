# 背景及介绍

BoltMQ在网络层面使用TCP长连接作为通讯方式，RocketMQ使用Netty库为基础网络开发库，netty是事件驱动的网络编程框架和工具，它的强大毋庸置疑。而Golang目前还没有和Netty类似的实现库，所有需要构建一个性能优异的网络基础库。

### IO模型
Netty是基于NIO(Non-blocking I/O)的实现，NIO的多路复用select/epoll默认使用epoll，可以在不同操作系统有不同选择。BoltMQ同样选择了epoll，Golang的net包标准库底层使用了epoll，在runtime层面，是用epoll/kqueue实现的非阻塞io，为性能提供了保障。不同的是开发者层面任然是阻塞的，配合Golang的线程模型CSP能达到高性能。

### 连接管理
BoltMQ的netm包提供的统一的连接管理功能，将所有连接统一管理，简化使用者维护连接。该功能讲会在之后去除，由事情通知功能代替，连接维护交由使用者维护。

### 事件通知
提供类似于Netty的事情通知功能，但目前只支持少数几类事情，提供代码的重用行。

### 粘包
这里的粘包是业务粘包，标准net包在底层提供了粘包保证了报文的正确性。业务报文是否完整，将进行粘包处理。

### 报文协议
BoltMQ中报文格式定义分为header和body，这两部分都定义了格式来进行通信。这部分将介绍具体的格式以及含义。