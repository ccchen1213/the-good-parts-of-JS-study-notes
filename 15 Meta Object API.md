* Meta Object API
	* Data properties
	* Accessor properties

* Attributes 
	* A property is a named collection of attributes.
	* value: any JS value
	* writeable: boolean
	* enumerable: boolean
	* configurable: boolean
	* get: `function() {... return value;}`
	* set: `function(value) {...}`

* Meta Object API
	* `Object.defineProperty(object, key, descriptor)`
	* `Object.defineProperties(object, object_of_descriptors)`
	* `Object.getOwnPropertyDescriptor(object, key)`
	* `object.getOwnPropertyNames(object)`
	* `Object.getProtorypeOf(object)`