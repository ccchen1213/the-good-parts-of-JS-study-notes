```javascript
function constructor(init) {
	var that = other_constructor(init),
		member,
		method = function() {
			// init, member, method
		}
	that.method = method;
	return that;
}
```