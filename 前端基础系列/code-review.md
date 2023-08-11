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


## JS 的对象是引用传递 (pass by reference)而非值传递 (pass by value)
```js
    updateChange(data) {
      if (data["getTotalAlarm"] && data["getTotalAlarm"].result !== {}) 
	      this.processAlarmData(data["getTotalAlarm"]);

      if (data["getHelp"] && data["getHelp"].result !== {}) 
	      this.processSOSData(data["getHelp"]);

      if (data["getFaultAlarm"] && data["getFaultAlarm"]?.result?.length > 0) 
	      this.processEquipData(data["getFaultAlarm"]);
    },
```
这里的错误之处在于 `data["getTotalAlarm"].result !== {}` 将变量和对象进行相等判断，将会永远返回 true 


[[前端基础系列/assets/b472f9e05188e0adb2b24c11e85fce55_MD5.png|Open file:]]
![[前端基础系列/assets/b472f9e05188e0adb2b24c11e85fce55_MD5.png]]
