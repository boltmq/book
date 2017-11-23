# 通讯包结构

BoltMQ中通讯包的结构如下：

![Alt text](https://static.oschina.net/uploads/space/2017/1122/151656_c2sl_3724856.jpg "设计")

* length域: 报文的长度。
* header length域: 报文头部长度。
* header域: 报文头部。
* body域: 报文内容。

header和body域的数据解析后是RemotingCommand这个结构，通信时将RemotingCommand序列化成byte[]字节数组通信层进行传输。

### RemotingCommand结构

| 字段名           | 请求                                             | 响应 |
| :---:            | :---                                             | :--- |
| **code**         | 请求操作代码，请求接收方根据不同的代码有不同操作 | 应答结果代码，0表示成功，非0表示各种错误 |
| **Language**     | 请求发起方实现语言                               | 响应方实现语言 | 
| **Version**      | 请求方程序版本                                   | 响应方程序版本 |
| **Opaque**       | 请求标识代码，多线程，连接复用使用               | 应答方不做修改，直接返回 |
| **Flag**         | 通信层的标志位                                   | 通信层的标志位 |
| **Remark**       | 传输自定文本信息                                 | 错诨详细描述信息 |
| **ExtFields**    | 请求自定义字段                                   | 响应自定义字段 |
| **CustomHeader** | 自定义结构，传输时将其转换为extFields型数据      | 自定义结构，传输时将其转换为extFields型数据 |
| **Body**         | 请求body                                         | 响应body |
