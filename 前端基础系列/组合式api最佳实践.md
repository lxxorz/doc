# 组合式函数最佳实践
## Ref 作为函数参数传递

关于 `ref() ` 函数， 如果参数本身是 Ref ，那么会原样返回，如果是纯值，则会被包装为一个 ref 变量
```js
const foo = ref("123");
cont bar = ref(foo);
console.log(bar === foo) // true
```

关于 `unref()`，如果是 Ref 变量，则会返回 `.value`，如果是纯值，则直接返回。

总而言之，不管是 Ref 还是普通 variable，都可以直接使用 `ref` 和 `unref `

为了函数的普遍性，可以构造一个 `MaybeRef<T>` 类型
```ts
type MaybeRef<T> = Ref<T>|T
```

一个典型的响应式函数是
```js
function useTimeAgo(time: MaybeRef<Date | time | string>) {
	return computed(() => format(unref(time)))
}
```

不仅参数可以传递 `Ref` 还可以传递一个 `ComputedRef`
```js
const tite = computed(() => isDark.value ? "Good Eveningst🌙" : "Good Morning ☀")
useTitle(title);
```

在进一步使用直接使用一个 getter 函数
```js
useTitle(() => isDark.value ? "Good Eveningst🌙" : "Good Morning ☀")
```

## 构造一个普适的响应式变量
根据上文，函数的参数可能是如下几种类型
1. 响应式变量（Ref）
2. 纯值
3. ComputedRef
4. getter 函数

vue 提供了开箱即用的 `toRef` 函数，用以将以上几种类型的参数归一为 Ref 变量 (3.3+)
```ts
function useSomething<T>(arg: MabeRefOrGetter<T>) {
	const arg_ref = toRef(arg);
}
```

同样的如果想要获取纯值，也可以用 toValue 将其归一化为非响应式变量
```ts
function useSomething<T>(arg: MabeRefOrGetter<T>) {
	const raw_value = toValue(arg);
}
```


unref 也可以获取纯值，但是 toValue 和 toRef 都考虑了参数是 getter 函数的情况



