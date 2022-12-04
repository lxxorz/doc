TCP 是面向数据流（Data Stream Oriented ）的协议，特点是
- 按照顺序发送
- 可靠
TCP 建立连接并且发送数据的过程如下
![[net-tcp-procedure.png]]

建立 TCP 连接的三个步骤
- 客户端发送一个 TCP 分组，里面包含一个 SYN 标记，用来说明这是一个连接请求