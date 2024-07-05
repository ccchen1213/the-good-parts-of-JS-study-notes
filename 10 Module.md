* Function as module
```
(function() {
	var ...
	function ...
	function ...
}());
```

* Module pattern is easily transformed into a powerful constructor pattern.

* Power Constructors
	* Make an object: Object literal, new, Object.create, call...
	* Define some variables and functions to become private members.
	* Augment the object with privileged methods.
	* Return the object.

```
// step one
function constructor(spec) {
	var that = otherMaker(spec),
		member,
		method = function () {
			// spec, member, method
		};
	that.method = method;
	return that;
}
```