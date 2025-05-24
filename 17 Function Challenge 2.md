#### Function 1
```javascript
// Make a function gensymf that makes a function that generates unique symbols.
var geng = gensymf("G"),
	genh = gensymf("H");
geng() // "G1"
genh() // "H1"
geng() // "G2"
genh() // "H2"

function gensymf(str) {
	var num = 0;
	return function() {
		num += 1;
		return str + num;
	};
}
```

#### Function 2
```javascript
// Write a function gensymff that takes a unary function and a seed and returns a gensymf.
var gensymf = gensymff(inc, 0),
	geng = gensymf("G"),
	genh = gensymf("H");
geng() // "G1"
genh() // "H1"
geng() // "G2"
genh() // "H2"

function gensymff(unary, number) {
	return function(prefix) {
		var num = number;
		return function() {
			num = unary(num);
			return prefix + num;
		};
	}
}
```

#### Function 3
```javascript
// Make a function fibonaccif that returns a generator that will return the next fibonacci number.
var fib = fibonaccif(0, 1);
fib() // 0
fib() // 1
fib() // 1
fib() // 2
fib() // 3
fib() // 5

// solution1: first output return num1, second output return num2, others all return num1 + num2
function fibonaccif(num1, num2) {
	var i = 0
	return function() {
		var next;
		switch(i) {
			case 0: 
				i = 1;
				return num1;
			case 1:
				i = 2;
				return num2;
			default:
				next = num1 + num2;
				num1 = num2;
				num2 = next;
				return next;
		}
	}
}

// solution2: use a variable store the value of num1, use num1 store the value of num2; num2 store the value of num2 + next;
function fibonaccif(num1, num2) {
	return function() {
		var next = num1;
		num1 = num2;
		num2 += next;
		return next;
	}
}
```

#### Function 4
```javascript
// Write a counter function that returns an object containing two functions that implement an up/down counter, hiding the counter.
var object = counter(10),
	up = object.up,
	down = object.down;
up() // 11
down() // 10
down() // 9
up() // 10

function counter(num) {
	return {
		up: function() {
			num += 1;
			return num;
		},
		down: function() {
			num -= 1;
			return num;
		}
	};
}
```

#### Function 5
```javascript
// Make a revocable function that takes a binary function, and returns an object containing an invoke functioin that can invoke the binary function, and a revoke function that disables the invoke function.
var rev = revocable(add),
	add_rev = rev.invoke;
add_rev(3, 4); // 7
rev.revoke();
add_rev(5, 7); // undefined

function revocable(fn) {
	return {
		invoke: function(first, second) {
			if(binary !== undefined) {
				return fn(first, second);
			}
		}
		revoke: function() {
			fn = undefined;
		}
	}
}
```

#### Function 6
```javascript
// Write a function m that takes a value and an optional source string and returns them in an object.
JSON.stringfy(m(1)) // {"value": 1, "source": "1"}
JSON.stringfy(m(Math.PI, "pi")) // {"value": 3.14159..., "source": "pi"}

function m(value, source) {
	return {
		value,
		source: (typeof source === 'string') ? source : String(value),
	}
}

```

#### Function 7
```javascript
// Write a function addm that takes two m objects and returns an m object.
JSON.stringfy(addm(m(3), m(4))) // {"value": 7, "source": "(3+4)"}
JSON.stringfy(addm(m(1), m(Math.PI, "pi"))) // {"value": 4.14159..., "source": "(1+pi)"}

function addm(m1, m2) {
	return {
		value: m1.value + m2.value,
		source: `${m1.source}+${m2.source}`
	}
}

// LET THE OBJECTS DO THE WORK!!!
function addm(m1, m2) {
	return m(
		m1.value + m2.value,
		`${m1.source}+${m2.source}`
	)
}
```

#### Function 8: Monad
```javascript
// Write a function liftm that takes a binary function and a string and returns a function that acts on m objects.
var addm = liftm(add, "+");
JSON.stringfy(addm(m(3), m(4))) // {"value": 7, "source": "(3+4)"}
JSON.stringfy(liftm(mul, "*")(m(3), m(4))) // {"value": 12, "source": "(3*4)"}

function liftm(fn, operator) {
	return function(m1, m2) {
		return m(
			fn(m1.value, m2.value),
			`${m1.source}${operator}${m2.source}`
		)
	}
}
```
A **monad** is a thing where you can take functions and lift them up to a higher level where they can have or acquire some new capability.

#### Function 9
```javascript
// Modify function liftm so that the functions it produces can accept arguments that are either number or m objects.
var addm = liftm(add, "+");
JSON.stringfy(addm(3, 4)) // {"value":7, "source": "(3+4)"}

function liftm(fn, operator) {
	return function(m1, m2) {
		if(typeof m1 === 'number') {
			m1 = m(m1)
		}
		if(typeof m2 === 'number') {
			m2 = m(m2)
		}
		return m(
			fn(m1.value, m2.value),
			`${m1.source}${operator}${m2.source}`
		)
	}
}
```

#### Function 10
```javascript
// Write a function exp that evaluates simple array expressions.
var sae = [mul, 5, 11];
exp(sae) // 55
exp(42) // 42

function exp(x) {
	if(typeof x === 'array') {
		return x[0](x[1], x[2])
	}
	return x
}
```

#### Function 11
```javascript
// Modify exp to evaluate nested array expressions.
var nae = [
	Math.sqrt,
	[
		add,
		[square, 3],
		[square, 4]
	]
];
exp(nae) // 5

function exp(value) {
	if(typeof value === 'array') {
		return value[0](exp(value[1]), exp(value[2]));
	}
	return value;
}
```
Anytime you're dealing with nested data structures, recursion is usually the ideal way to deal with it.

#### Function 12
```javascript
// Write a function addg that adds from many invocations, until it sees an empty invocation.
addg() // undefined
addg(2)() // 2
addg(2)(7)() // 9
addg(3)(0)(4)() // 7
addg(1)(2)(4)(8)() // 15

function addg(first) {

	function more(next) {
		if(next === undefined) {
			return first;
		}
		first += next;
		return more;
	}
	if(first !== undefined) {
		return more;
	}
}

```

#### Function 13
```javascript
// Write a function liftg that will take a binary function and apply it to many invocations.
liftg(mul)() // undefined
liftg(mul)(3)() // 3
liftg(mul)(3)(0)(4)() // 0
liftg(mul)(1)(2)(4)(8)() // 64

function liftg(fn) {
	return function(first) {
		if(first === undefined) {
			return first;
		}
		return function more(next) {
			if(next === undefined) {
				return first;
			}
			first = fn(first, next);
			return more;
		};
	};
}
```

#### Function 14
```javascript
// Write a function arrayg that will build an array from many invocations.
arrayg() // []
arrayg(3)() // [3]
arrayg(3)(4)(5)() // [3, 4, 5]

function arrayg(first){
	let array = [];
	function more(value) {
		if(value === undefined) {
			return array;
		} 
		array.push(value);
		return more;
	};
	return more(first);
}

function arrayg(first) {
	if(first === undefined) {
		return [];
	}
	return liftg(
		function(array, value) {
			array.push(value);
			return array;
		}
	)([first]);
}
```

#### Function 15
```javascript
// Make a function continuize that takes a unary function, and returns a function that takes a callback and an argument.
sqrtc = continuize(Math.sqrt);
sqrtc(alert, 81) // 9

function continuize(unary) {
	return function(callback, arg) {
		return callback(unary(arg));
	};
}

function continuize(any) {
	return function(callback, ...arg) {
		return callback(any(...arg));
	}
}
```
