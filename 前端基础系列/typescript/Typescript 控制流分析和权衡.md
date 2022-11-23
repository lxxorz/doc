在 TS 中，
```ts
let a = false;
doSomething();

if(a === true){
	//error
}
```
这里 TS 会提示类型错误，因为 TS 会对我们的程序流程进行分析，它发现从 `let a = false` 声明开始 a 并没有被重新赋值，所以理应是不变的，是的, TS 忽视了 `doSomething` 函数可能存在的副作用，比如：
```ts
function doSomething(){
	a = true;
}
```



















参考
- [TypeScript - 控制流分析中的权衡 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/143789846)