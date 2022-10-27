参考 rollup [入门指南]([rollup.js (rollupjs.org)](https://rollupjs.org/guide/en/#tutorial))

全局安装rollup
```shell
npm install --global rollup
```

创建一个JavaScript文件
```js
import foo from "./foo.js"
export default function () {
	console.log(foo);
}
```

```js
export default "hello world"
```

现在利用rollup 可以把ESM转换为commonjs格式的代码
```shell
rollup main.js -f cjs
```
这里的`f`选项是"format"的意思，这个命令会自动将main.js转换为commonjs格式的代码

output
```js
'use strict';

var foo = "hello world";

function f () {
	console.log(foo);
}

exports.f = f;
```

如果我们要添加更多配置，这显然是很麻烦的，所以rollup为用户提供了配置文件，每次打包的时候，指定读取该配置文件里面内容即可，默认该配置文件为 "rollup.config.js"
```js
// rollup.config.js
export default {
  input: 'src/main.js',
  output: {
    file: 'bundle.js',
    format: 'cjs'
  }
};
```
注意到这里的rollup配置文件使用的ESM导出，也就意味着，你使用的node版本至少应该支持ES Module

配置好文件之后，就不必再次输入繁琐的命令，直接
```shell
rollup -c
```
也可以通过传递命令行选项的方式，覆写配置文件里面的选项
```shell
rollup -c -o new-bundle.js
```
 这里的`-o`等价于配置文件里面的`file`选项
 也可以通过 --config 指定不同的配置文件
```shell
rollup --config rollup.dev.config
rollup --config rollup.prod.config
```
### 局部安装rollup
for npm 
```shell
npm install rollup --save-dev
```
for yarn
```shell
yarn add -D rollup
```
for pnpm 
```shell
pnpm add -D rollup
```
安装完成之后，通常的操作是在`package.json`当中添加一个build命令，用以指定rollup来进行构建代码
```json
{
  "name": "rollup-tutorial",
  "version": "1.0.0",
  "scripts": {
    "build": "rollup -c"
  }
}
```