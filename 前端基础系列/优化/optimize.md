

### 缓存
关于 http 缓存的前置知识可以参考
[[HTTP-Cache]]
在项目中，基本上所有的静态文件都是放置在 public 文件夹下，但是 vue-cli 的文档中存在这样一句话「任何放置在 public 文件夹的静态资源都会被简单的复制，而不经过 webpack，注意我们推荐将资源作为你的模块依赖图的一部分导入」这是因为生成的文件名包含了内容哈希，所以可以通过一种叫做 [Cache Busting](https://developer.mozilla.org/en-US/docs/Web/HTTP/Caching#cache_busting) 技术设置缓存

当然，对于我们的入口文件 `index.html` 则永远不应该对他缓存

### 文本压缩




### 新格式的图片


