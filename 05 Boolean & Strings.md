* Boolean
	* true
	* false

* Strings
	* Strings are immutable
	* Similar strings are equal (`===`)
	* Use " for external strings
	* Use ' for internal strings and characters

* Convert a number to a string
	* Use `toString`: `str = num.toString();`
	* Use string function: `str = String(num);`

* Convert a string to a number
	* Use `Number()`: `num = Number(str);`
	* Use the + prefix operator: `num = +str;`
	* Use the `parseInt` function
		* It stops at the first non-digit character: `parseInt("12emas") === 12;`
		* The radix(10) should always be used. If the string starts with a 0, it would be parsed as base-8: (**It fixed in ES5**)
			* `parseInt("08") === 0;`
			* `parseInt("08", 10) === 8`