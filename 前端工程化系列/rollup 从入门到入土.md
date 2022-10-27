参考 rollup [入门指南]([rollup.js (rollupjs.org)](https://rollupjs.org/guide/en/#tutorial))

全局安装rollup
```shell
npm install --global rollup
```

创建一个JavaScript文件
```js
import foo from "./foo.js"
export function () {
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
```

```


