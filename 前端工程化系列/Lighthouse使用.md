## 简介
lighthouse 是 goggle 开源的一个性能测试工具，它收集并且分析 web 应用和 web 网页的现代性能指标，并且提供一系列的有帮助的优化建议
主要有四种方式使用 lighthouse
- 通过 chrome 开发者工具
- 通过 chrome 扩展
- 作为 Node Module 使用
- 作为 Node CLI 程序使用

主要介绍作为 node module 时如何使用 Puppeteer


## 生成报告
lighthouse 可以生成两种文件格式的报告
- JSON
- HTML
用 output 配置项指定

## 基础配置
为什么保证每次测试的一致性，需要自定义 lighthouse 的一些配置
### 网络一致性
需要保证网络上传下载的带宽一致

### 性能一致性
指定客户机使用的 CPU 和内存能力

### 客户端一致性
使用相同的客户端（移动端和桌面端）
屏幕大小

使用如下配置
```js
const constants = require("lighthouse/lighthouse-core/config/constants")
module.exports = {
  extends: 'lighthouse:default',
  settings: {
    onlyCategory: ["performance"],
    onlyAudits: [
      "first-contentful-paint",
      "interactive",
      "speed-index",
      "total-blocking-time",
      "largest-contentful-paint",
      "cumulative-layout-shift",
    ],
    maxWaitForFcp: 15 * 1000,
    maxWaitForLoad: 35 * 1000,
    formFactor: 'desktop',
    throttling: constants.throttling.desktopDense4G,
    screenEmulation: constants.screenEmulationMetrics.desktop,
    emulatedUserAgent: constants.userAgents.desktop
  }
}
```

## 配合 Puppeteer 使用
