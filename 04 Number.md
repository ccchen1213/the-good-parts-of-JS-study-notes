* Object and ...(all objects)
	* Number
	* Boolean
	* String
	* Array
	* Date
	* RegExp
	* Function

* Only one number type
	* No integer types

* 64-bit binary floating point

* IEEE-754 (aka double)

* Integers under 9 quadrillion are ok

* Decimal fractions are approximate

* NaN: Not a Number
	* NaN === NaN is false
	* isNaN(NaN) is true
	* isNaN does **type coercion**: isNaN('hello') is true
		* convert string into a number
		* number 'hello' turns into NaN