* Definition:
	* A function defined inside of another function, the inner function has access to the variables and scope of the outer function.
	* Allow for private variables and **state maintenance**
	* Used frequently in JS frameworks: React, Vue, Angular.
	* Reference: https://www.youtube.com/watch?v=beZfCfiuIkA

* Example 1: Private variables
```javascript
function outer(){ 
	const message = "Hello"; 
	
	function inner(){ 
		console.log(message); 
	} 
	
	inner(); 
} 

message = "Goodbye"; 
outer();

```

* Example 2: State maintenance
```javascript
function createCounter() { 
	let count = 0; 
	
	function increment() { 
		count++; 
		console.log(`Count increased to ${count}`); 
	} 
		
	function getCount() { 
		return count; 
	} 
		
	return {increment, getCount}; 
} 
	
const counter = createCounter(); 
counter.increment(); 
counter.increment(); 
counter.increment(); 

console.log(`Current count: ${counter.getCount()}`);
		
```

* Example 3: State maintenance
```javascript
function createGame(){ 
	let score = 0; 
	
	function increaseScore(points){ 
		score += points; 
		console.log(`+${points}pts`); 
	} 
	
	function decreaseScore(points){ 
		score -= points; 
		console.log(`-${points}pts`); 
	} 
	
	function getScore(){ 
		return score; 
	} 
	
	return {increaseScore, decreaseScore, getScore}; 
} 

const game = createGame(); 
game.increaseScore(5); 
game.increaseScore(6); 
game.decreaseScore(3); 

console.log(`The final score is ${game.getScore()}pts`);

```

Original Version:
```javascript
var names = [
	'zero', 'one', 'two', 'three',
	'four', 'five', 'six', 'seven',
	'eight', 'nine'
]

var digit_name = function(n) {
	return names[n]
}

alert(digit_names(3)); // 'three'
```

[[Closure]] Version: 
```javascript
var digit_name = (function () {
	var names = [
		'zero', 'one', 'two', 'three',
		'four', 'five', 'six', 'seven',
		'eight', 'nine'
	]
	
	return function (n) {
		return names[n]
	}
}())

alert(digit_names(3)); // 'three'
``` 