在 Typescript4.9 当中，新增了一个 feature, 即 `satisfies`
出现的场景
### 提供安全的向上转换
```ts
let a = false;

upd();

if(a === true) {
	// error
}

function upd(){
	if(some_condition) 
		a = true;
}

```
通常的做法是使用类型断言
```ts
let a = false as boolean
```

这样做是有效的，但如果是对象呢
```ts
type Animal = { kind: "cat", meows: true } | { kind: "dog", barks: true };
let p = { kind: "cat" } as Animal; // Missing meows!
upd();
if (p.kind === "dog") {

} else {
    p.meows; // Reported 'true', actually 'undefined'
}
function upd() {
    if (Math.random() > 0.5) p = { kind: "dog", barks: true };
}
```

可以看到，对于上述代码的错误并没有提示，在 4.9 可以这样写
```ts
let p = { kind: "cat" } satisfies Animal as Animal;
```

### 约束属性名
想要让 p 中的键全部来源于某个集合
```ts
type Keys = 'a' | 'b' | 'c' | 'd';

const p = {
    a: 0,
    b: "hello",
    c: true
    // Should error because 'd' is missing
};
// Should be OK
const t: boolean = p.c;
```
使用 satisfies 可以这样:
```ts
const p = {
    a: 0,
    b: "hello",
    c: true
} satisfies Record<Keys, unkown>;
```