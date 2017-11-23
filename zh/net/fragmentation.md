# 粘包处理

粘包指的是业务粘包，标准net包在底层提供了粘包保证了报文的正确性。业务报文是否完整，将进行粘包处理。BoltMQ采用length-field的方式传输报文。length占用4个字节，存储之后的报文长度。粘包就是将接收的报文进行验证，先验证length域，在根据length域的值取得field域。如果length长度不够，会将报文进行缓存，等待下一个报文的到来。粘包必须是针对单个连接进行，保证传输报文的不乱序。

![Alt text](https://static.oschina.net/uploads/space/2017/1122/151627_R0wl_3724856.jpg "报文")

* length域: 报文的长度。
* field域: 报文内容。
