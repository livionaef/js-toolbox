# JS-Toolbox

## 1. Intro & Functions

> You only understand what you can build by yourself => use no dependencies

### Canvas

```javascript
const canvas = document.getElementById("canvas");
const context = canvas.getContext("2d");

context.fillStyle = "black";
context.fillRect(0, 0, canvas.width, canvas.height);
```

### Key events

```javascript
const rightArrow = 39;
const leftArrow = 37;
window.onkeydown = evt => {
	(evt.keyCode === rightArrow) ? … : … ;
};
```

### Game loop

```javascript
setInterval( () => {
	nextBoard();
	display(context);
}, 1000 / 5);
```

### Fundamentals of Lambda Calculus & Functional Programming in JavaScript - YouTube Video

[Video-Link](https://www.youtube.com/watch?v=3VQ382QG-y4)

### Example

A function `plus` that returns the sum of its arguments:

```javascript
const plus = x => y => x + y;
```



## 2. Lambda

### JavaScript Variables

Only use `let` and `const`:

```javascript
let x = ...; 	// mutable,   local scope
const x = ...; 	// immutable, local scope
```

### IIFE

> immediately invoked function expression

```javascript
function foo() {..}; foo()
( function foo() {..} ) ()
( function() {..} ) ()
( () => {..} ) ()
```

### Alpha Translation

```javascript
const id = x => x
const id = y => y
```

### Beta Reduktion

```javascript
( f => x => f(x) ) (id) (1)
(	   x => id(x))		(1)
(			id(1))
(x => x) (1)
1
```

### Eta Reduktion

```javascript
x => y => plus (x) (y)
x => 	  plus (x)
		  plus
```

### Examples

`F3` is a proper eta reduction of `F2`

```javascript
const id = x => x;
const konst = x => y => x;

const F1 = x => y => konst (id) (x) (y);
const F2 = x =>      konst (id) (x);
const F3 = 	         konst (id);
```

`a1` is a proper beta expansion of `a2`

```javascript
const id = x => x;

const a1 = y => id(y);
const a2 = y => y;
```

`a2` is a proper beta reduction of `a1`

```javascript
const id = x => x;

const a1 = y => id(y);
const a2 = y => y;
```

`id1` and `id2` are alpha-equivalent

```javascript
const id1 = x => x;
const id2 = y => y;
```



## 3. Algebraic Data Types

> "I recommend that you write programs as though JavaScript had been designed correctly." - Douglas Crockford, How JavaScript works, p. 6.2

### Atomic Lamda Terms

```javascript
// atoms
const id = x => x;
const konst = x => y => x;

// derived true, false, and, or, equals, …
const F = …;
const T = …;
```

### Pair, Product Type

```javascript
const pair = x => y => f => f(x)(y);
const fst = p => p(T);
const snd = p => p(F);
```

### Pair encoding

```javascript
const person =
				firstname =>
				lastname =>
				age =>
				pair (pair(firstname)(lastname)) (age);

const firstn = p => fst(fst(p));
const lastn  = p => snd(fst(p));
const age    = p => snd(p);
```

### Either, Co-Product, Sum

```javascript
// dual of the product
const pair = x => y => f => f(x)(y); 	// one ctor
const fst  = p => p(T); 			 	// accessor 1
const snd  = p => p(F);      		 	// accessor 2

// here we have now the basic sum type
const Left   = x => f => g => f(x); 	// ctor 1
const Right  = x => f => g => g(x); 	// ctor 2
const either = e => f => g => e(f)(g); 	// accessor
```

### Special Case: Maybe

```javascript
// go around null / undefined
const Nothing = Left ();
const Just 	  = Right;
const maybe   = either;

maybe (expressionThatMightGoWrong)
	  (handleBad)
	  (handleGood);
```

### Example

```javascript
// error handling with either
const eShow = result => result (msg => msg) (val => "Result is:" + val);
```



## 4. Map, Filter, Reduce

> "Developers seem to love those languages most, in which they understood the value of higher-order functions." -@ProfDKoenig

### Map

```javascript
const times = a => b => a * b;

const twoTimes = times(2);

[1, 2, 3].map(x => times(2)(x));
[1, 2, 3].map(times(2));
[1, 2, 3].map(twoTimes);
```

### Filter

```javascript
const odd = x => x % 2 === 1;

[1, 2, 3].filter(x => x % 2 === 1);
[1, 2, 3].filter(x => odd(x));
[1, 2, 3].filter(odd);
```

### Reduce

```javascript
const plus = (accu, cur) => accu + cur;

[1, 2, 3].reduce((accu, cur) => accu + cur);
[1, 2, 3].reduce(plus);

// variant with initial accu value as 2nd argument
// then cur starts at first element
[1, 2, 3].reduce(plus, 0);
```

### Examples

```javascript
// function that checks which numbers in an array are divideable 
// by the given argument
const divides = x => y => y % x === 0;
```

```javascript
// function that joins values of an array together with given argument
const join = (a) => (b, c) => b + a + c;
```



## 5. Scripting, PWA, Plotter, Excel eval()

## 6. Objects

## 7. Classes

## 8. Moves, User Interfaces

## 9. UI Engineering

## 10. Async Programming

## 11. Data Flow, Excel improved

## 12. Modules

## 13. Transpilers, TS, PS, Elm

## 14. Crazy JavaScript