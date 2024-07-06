* Inherit from Object

* sort

* delete elements
	* splice(index, 1)
	* avoid use `delete`
```javascript
		var array = [1, 2, 3, 4];
		delete array[1]
		// array = [1, undefined, 3, 4];
```

+ Arrays vs Objects
	+ Use objects when the names are arbitrary strings.
	+ Use arrays when the names are sequential integers.

