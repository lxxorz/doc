## 简介
lighthouse 是 goggle 开源的一个性能测试工具，它收集并且分析 web 应用和 web 网页的现代性能指标，并且提供一系列的有帮助的优化建议
主要有四种方式使用 lighthouse
- 通过 chrome 开发者工具
- 通过 chrome 扩展
- 作为 Node Module 使用
- 作为 Node CLI 程序使用

主要介绍 lighthouse 作为 Javascript 库如何配合 Puppeteer 使用


## 生成报告
lighthouse 可以生成两种文件格式的报告
- JSON
- HTML
用 output 配置项指定
```js
  const { lhr, report } = await lighthouse(page, {
    port: port,
    output: 'html',
    logLevel: 'error',
    locale: "en-US",
  }, CONFIG);
```
## 基本架构
![[lighthouse-arch.png]]
需要理解以下概念
驱动（driver）使用 puppeteer 和 chrome debugging protocol 的接口
收集器 (gatherers) 使用驱动收集有关页面的信息，最小化推送处理

## 基础配置
为了保证每次测试的一致性，需要自定义 lighthouse 的一些配置

### 网络一致性
lighthouse 提供了两种不同形式的网络节流
- simulate 根据请求的数据计算得来
- devtools 设置开发者工具里面的网络带宽限制，在请求层次去限制网络速度
| simulate       | devtools   |
| -------------- | ---------- |
| 快但准确性欠缺 | 慢但更准确 |
通过配置 `throttlingMethod:'devtools'` 来设置节流的方法，在 lighthouse 的配置里面, 指定 `settings.throttling` 对象，来配置网络相关的具体参数
**注意,  如果使用 ` simulate ` 方式的网络节流方式，那么需要在 throttling 对象里面配置 ` throughputKbps `，如果使用 `devtools` 方式则对应的配置`downloadThroughputKbps` 来限制网络带宽**
```js
{
    rttMs: 40,
    throughputKbps: 2 * 1024,
    cpuSlowdownMultiplier: 1,
    requestLatencyMs: 0, // 0 means unset
    downloadThroughputKbps: 2048,
    uploadThroughputKbps: 2048,
}
```
具体细节参考[lighthouse/throttling.md at main · GoogleChrome/lighthouse (github.com)](https://github.com/GoogleChrome/lighthouse/blob/main/docs/throttling.md)

### 性能一致性
跟网络节流不一样的是，, lighthouse 对性能的设置都是基于当前机器的性能, 没有一个绝对的标准，因此要保证一致性不太容易，除非保证每台计算机的性能是相同的，在 lighthouse 产生的报告页最下面有一个计算机性能的估测。
![[lighthouse-cpu-throttling.png]]

### 客户端一致性
使用相同的客户端（移动端和桌面端）
屏幕大小，通过指定 `settings.screenEmulation` 配置项指定
使用如下配置
```js
const desktop = {
  mobile: false,
  width: 1920,
  height: 1080,
  deviceScaleFactor: 1,
  disabled: false,
};
```

## 注意事项
有些 lighthouse 的配置是文档没有列出或者很难找到
 - 设置缓存 `setting.disableStorageReset` 



参考
- [lighthouse/docs at main · GoogleChrome/lighthouse (github.com)](https://github.com/GoogleChrome/lighthouse/tree/main/docs)