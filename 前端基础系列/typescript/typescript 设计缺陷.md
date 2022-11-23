列出遇到过的由于 TS 的设计限制而导致不一致的地方
- [error TS2365: Operator '+' cannot be applied to types 'string | number' and 'string | number'. · Issue #49661 · microsoft/TypeScript (github.com)](https://github.com/microsoft/TypeScript/issues/49661)
```ts
function add(a: string | number, b: string | number) {
	return a + b;
	//Should be string | number, but error
}
```

