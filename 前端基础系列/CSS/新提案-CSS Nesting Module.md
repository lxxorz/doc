## 为什么要使用嵌套
即使是适度复杂度的网络应用，CSS 样式规则也会有一定的重复，使用嵌套规则可以消除重复，并且提升 CSS 的可读性和可维护性

## 嵌套样式规则
### 直接嵌套 directing nested
直接嵌套要求嵌套的樣式規則必須以嵌套前綴 `&` 开头
```css
:is(div) {
	& :is(div) {
		color: red;
	}
}
```
这种是错误的
```css
.div{
	.bar {
		color: red
	}
}
```









### 提前使用新提案的方法

目前提案还在 (stage 1)[ https://cssdb.org/#stage-1-experimental ] ，还是实验性质的，可以通过 `postcss` 插件 `postcss-nesting` 来提前使用提案
