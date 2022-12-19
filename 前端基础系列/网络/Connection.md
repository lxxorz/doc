# http 连接
## Connection 首部
Connection 首部是用于指定 http 连接相关的参数，Connection 首部只会应用于两个两个相邻的 http 应用程序，比如客户端和代理之间，他们共享一组连接，由于 Connection 是只用于逐跳连接的参数，所以不能将其转发出去

## 连接优化
如果 http 只采用串行连接，是十分低效的，在 http 中有如下优化
1. 并行连接，采用多个 TCP，按序请求，适用于无副作用的或者说『幂等』的方法
2. 持久化连接，http 可以通过 `keep-alive` (http/1.0) 或者 `persistent` (http/1.1) 建立持久化的连接，避免 TCP 连接的关闭和开启造成等待时间
3. **在持久连接的基础上**，可以选用*请求管道*，在响应达到之前将多条请求放入队列

```ad-note
HTTP/1.0中如果Connection中存在`keep-alive`可能造成**哑代理**问题
```