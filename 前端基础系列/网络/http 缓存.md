Vite 的重新加载
> Vite 同时利用 HTTP 头来加速整个页面的重新加载（再次让浏览器为我们做更多事情）：源码模块的请求会根据 `304 Not Modified` 进行协商缓存，而依赖模块请求则会通过 `Cache-Control: max-age=31536000,immutable` 进行强缓存，因此一旦被缓存它们将不需要再次请求。


1. 私有缓存，绑定到特定客户端不和其他客户端共享
2. 共享缓存，共享缓存位于客户端和服务器之间进一步分为代理缓存和托管缓存
```mermaid
graph BT
	z[私有缓存] ==> cache[缓存]
	a[代理缓存] ==> b[共享缓存] ==> cache
	c[托管缓存] ==> b[共享缓存]
```

![[http-cache.png]]


### 缓存方式

#### 基于 max-age 的缓存
响应的状态分为两种, 未过时和过时客户端会根据响应头中的 cache-control 当中的 max-age 进行缓存，超过了 max-age 指定的时间会将响应的状态设置为过时的
```http
HTTP/1.1 200 OK
Content-Length: 409259
Last-Modified: Fri, 28 Oct 2022 02:39:47 GMT
Cache-Control: max-age=0
Content-Type: application/json; charset=utf-8
Date: Tue, 01 Nov 2022 09:31:49 GMT
Connection: keep-alive
Keep-Alive: timeout=5
```

#### 启发式缓存
即使没有给出 cache-control 在满足一定条件之后，浏览器也会主动的缓存响应，比如
```http
HTTP/1.1 200 OK
Content-Type: text/html
Content-Length: 1024
Date: Tue, 22 Feb 2022 22:22:22 GMT
Last-Modified: Tue, 22 Feb 2021 22:22:22 GMT
```
根据 Date 和 Last-Modified 可以看出该响应已经一年没有修改，可以猜想在今后的一段时间，也不会更改此响应。这个“今后的一段时间”到底多长，取决于实现，http 的规范建议存储至少 10% 的时间

### 缓存验证


### 奇怪的现象
使用 curl 请求已缓存的资源显示 304 Not Modified
```sh
curl http://192.168.13.76/EHCommon/resources/map/Scene_1/Building_1/Floor_2d_1_1666927127.json --header 'If-None-Match: "216cd7b-5ec0fb74c9898"' -I
HTTP/1.1 304 Not Modified
Date: Tue, 01 Nov 2022 09:25:59 GMT
Server: Apache
ETag: "216cd7b-5ec0fb74c9898"
```
但是实际在浏览器中根本就没有带 `If-None-Match` 这个header，响应的状态码一直是 200 Ok
* 第一次请求
![[etag-1.png]]
* 第二次请求（已缓存）
* ![[etag-2.png]]