# 事件通知

当连接状态发送变化时，将该事件通知给用户。支持事件:

* Active: 当接收到一个新创建的连接时，被动接收通常作为服务端。
* Connect: 当新创建一个新连接时，通常主动创建连接的客户端。
* Disconnet: 当连接时断开时，通常被动断开。
* Closed: 当连接时断开时，通常主动关闭。
* Error: 当连接使用中发生错误时。

实现接口方法可以接收到事件通知：
```go
type ContextEvent interface {
	OnContextActive(ctx Context)
	OnContextConnect(ctx Context)
	OnContextClosed(ctx Context)
	OnContextDisconnect(ctx Context)
	OnContextError(ctx Context)
}
```
