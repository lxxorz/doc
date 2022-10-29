roll的插件机制比较优秀，故单独提出来讲一下

### 如何使用插件
首先用官网的例子来介绍rollup的插件是如何使用
1. 初始化一个项目
```sh
pnpm init
```
2. 局部安装 rollup
```sh
pnpm add -D rollup
```
3. 安装 @rollup/plugin-json
```sh
pnpm add -D @rollup/plugin-json
```

4. 在**main.js**当中键入以下内容
```js
import {version} from "./foo.js"
export default function  () {
	console.log("version" + version)
}
module.exports = main
```
5. 在配置文件**rollup.config.js**当中添加以下配置
```js
// rollup.config.js
import json from '@rollup/plugin-json';

export default {
  input: 'src/main.js',
  output: {
    file: 'bundle.js',
    format: 'cjs'
  },
  plugins: [json()]
};
```
然后执行`rollup -c`，输出以下内容
```js
'use strict';

var version = "1.0.0";

function main$1  () {
  console.log("version" + version);
}

module.exports = main;

module.exports = main$1;
```

可以看到, rollup 只导入了version字段，其余没有用到的内容都被忽略了,这实际上就是**tree-shaking**

