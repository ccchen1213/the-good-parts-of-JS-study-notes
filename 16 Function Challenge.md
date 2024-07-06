#### Function 1
```javascript
// Write an identity function that takes an argument and returns that argument.
// eg: identity(3) -> 3

function identity(id) {
	return id;
}

```

#### Quiz 1
```javascript
function funky(o) {
	o = null;
}

var x = [];
funky(x);

log(x);
```
A: `[]`
First, we have the global variable x that points at the array. We pass the contents of x to o, then we replace o with null.

#### Quiz 2
```javascript
function swap(a, b) {
	var temp = a;
	a = b;
	b = temp;
}

var x = 1, y = 2;
swap(x, y);
log(x);
```
A: 1
**We pass the contents of the variable, not the variable.**


#### Function 2
```javascript
// Write three binary functions, add, sub, and mul, that take two numbers and return their sum, difference, and product.
function add(a, b) {
	return a + b;
}

function sub(a, b) {
	return a - b;
}

function mul(a, b) {
	return a * b;
}
```

#### Function 3
```javascript
// Write a function identityf that takes an argument and returns a function that returns that argument.
function identityf(x) {
	return function() {
		return x;
	};
}
```

#### Function 4
```javascript
// Write a function addf that addf from two invocations.
// addf(3)(4) -> 7
function addf(a) {
	return function(b) {
		return a + b;
	};
}
```

#### Function 5: Higher Order Function
```javascript
// Write a function liftf that takes a binary function, and makes it callable with two invocations.
// var addf = liftf(add)
// addf(3)(4)
// liftf(mul)(5)(6)
function liftf(fn) {
	return function(a) {
		return function(b) {
			return fn(a, b);
		};
	};
}
```
Higher order function are functions that receive other functions as parameters and return other functions as results.

#### Function 6: Curry
```javascript
// Write a function curry that takes a binary function and an argument, and returns a function that can take a second argument.
// var add3 = curry(add, 3);
// add3(4) -> 7
function curry(fn, a) {
	return function(b) {
		return fn(a, b);
	};
}

// Use old function
function curry(fn, a) {
	return liftf(fn)(a);
}

// Use ES6
function curry(fn, ...a) {
	return function(...b) {
		return fn(...a, ...b);
	};
}
```
Taking a function with multiple arguments and turning it into multiple functions that take a single argument is called currying.

#### Function 7: Functional Programming
```javascript
// Without writing any new functions, show three ways to create the inc function.
// var inc = _ _ _ ;
// inc(5) -> 6
// inc(inc(5)) -> 7
// A1
inc = curry(add, 1);
// A2
inc = liftf(add)(1);
// A3
inc = addf(1);
``` 
**Functional Programming Rule 1**: Let the function do the work. If you've already written a function that does what you need, you don't need to write another one.

#### Function 7: Twice
```javascript
// Write a function twice that takes a binary function and returns a unary function that passes its argument to the binary function twice.
function twice(fn) {
	return function(x) {
		fn(x, x)
	} 
}
var doubl = twice(add)
var square = twice(mul)
```


#### Function 8: Reverse
```javascript
// Write reverse, a function that reverses the arguments of a binary function.
// var bus = reverse(sub);
// bus(3, 2) -> -1
function reverse(fn) {
	return function(a, b) {
		fn(b, a);
	};
}

function reverse(fn) {
	return function(...args) {
		return func(...args.reverse());
	};
}
```

#### Function 9: Composeu
```javascript
// Write a function composeu that takes two unary funtions and returns a unary function that calls them both.
// composeu(doubl, square)(5) // 100
function composeu(fn1, fn2) {
	return function(x) {
		return fn2(fn1(x))
	}
}
```

#### Function 10
```javascript
// Write a function composeb that takes two binary functions and returns a function that calls them both.
// composeb(add, mul)(2, 3, 7) -> 35
function composeb(fn1, fn2) {
	return function(x, y, z) {
		return fn2(fn1(x,y), z);
	};
}
```

#### Function 11
```javascript
// Write a limit function that allows a binary function to be called a limited number of times.
// var add_ltd = limit(add, 1);
// add_ltd(3, 4) -> 7
// add_ltd(3, 5) -> undefined
function limit(fn, times) {
	return function(a, b) {
		if(times > 0) {
			times--;
			return fn(a, b);
		}
		return undefined;	
	};
}
```