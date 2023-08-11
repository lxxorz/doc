## JS 的除法不会自动取整
```js
		getRuleList(search_flag) {
			let obj = {
				begin: this.area_rule_search.date[0] / 1000,
				end: this.area_rule_search.date[1] / 1000,
			};
			this.getAreaAlarmRuleList(obj);
		},
```