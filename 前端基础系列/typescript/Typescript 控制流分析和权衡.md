在 TS 中，CFA 几乎总是接受一个联合体，并且基于代码中的逻辑减少 union type 的中类型数量，
大多数类型收缩发生在 `if` 条件语句之中

### if statement
- 使用 `typeof` 类型收缩类型
```ts
const input = getUserInput();
input;// string | number
if(typeof input === "string") {
	input; // string
}
```

- 使用 `instanceof` 收缩类型
```ts
const input = getUserInput();
input; // number | number[];
if(input instanceof Array) {
	input; // number[]
}
```

- 使用 `property in object`
```ts
 const input = getUserInput();
 input; // string | {"error": ...}
 if("error" in input) {
	 input; // {"error": ...}
 }
```

- 类型守卫函数
```ts
const input = getUserInput();
input;  // number | number[];

if(Array.isArray(input)) {
	input; // number[];
}
```


### expression
类型收缩也随着代码做布尔操作的同时发生在同一行
```ts
const input = getUserInput();
input; // number | string;

const inputLength = 
	  (typeof input === "string" && input.length /*string*/) || input

```

### discriminated unions
[标签联合 - 维基百科，自由的百科全书 (wikipedia.org)](https://zh.wikipedia.org/wiki/%E6%A0%87%E7%AD%BE%E8%81%94%E5%90%88)
能够区分中所有成员的共同属性 `status`
```ts
type response = 
	  | {status: 200, data: any}
	  | {status: 301, to: string}
	  | {status: 400, error: Error}

const response = getResponse();
switch(response.status) {
	case 200: return response.data;
	case 301: return redirect(to);
	case 400: return return reponse.error
}
```

### type guards
类型守护函数能够收缩类型
```ts
const isErrorResponse(obj:Response) {
	return obj instanceof ErrorResponse
}

const response = getResponse();
response; //Response;

if(isErrorResponse(obj)) {
	obj;// ErrorResponse;
}
```

CFA 也会导致一些问题

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