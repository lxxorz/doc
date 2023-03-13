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
