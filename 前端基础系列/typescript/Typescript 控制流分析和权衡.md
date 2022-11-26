## 什么是控制流
	

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
也许能做到根据函数调用来检查变量是否被重新赋值，但是目前 TS 实现起来比较困难，
所以目前针对函数调用，有两种可行的策略
- 乐观策略
乐观策略认为函数永远不会修改外部的变量，因此以下代码就会报错
```
let a = false;
doSomething();

if(a === true){
	//error
}
```

- 悲观策略
悲观策略认为，所有函数调用都存在将可达的变量修改的可能性。所以会将所有类型收缩的变量的类型重置
```ts
let a = "hello world";
doSomething();
a.toUpperCase();
//Should be error

```


参考
- [TypeScript - 控制流分析中的权衡 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/143789846)  