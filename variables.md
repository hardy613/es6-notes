# ES6 Variables


## `var` vs `let`
A variable in javascript is a named space in memory. Triditionally the keyword
`var` initializes the `indentifier` with a `value`:

```js
var	my_variable	=	'value';
//1	//2			//3 

//1 the var keyword
//2 the identifier
//3 the value
```
There are rules for naming the variable identifier, they are:
- identifiers cannot be keywords
- can be alphanumeric, although cannot start with a number
- `$` and `_` are also allowed characters for an indentifier

Variables decalred by `var` have the scope of the entire function.

```js
function myFunc() {
	if(true) {
		var my_var = 'test';
	}
	console.log(my_var); // test
}
```

## The `let` keyword

`let` is preferred over `var`. Variables decalred by `let` have their scope
within the `block` they are defined.

```js
function myFunc() {
	if(true) {
		let my_var = 'test';
	}
	console.log(my_var); // TypeError
}
```

Block scoping allows for variable [`shadowing`][Shadowing].

```js
function myFunc() {
	let my_var = 'test';
	if(true) {
		let my_var = 'new test';
		console.log(my_var); // new test
	}
	console.log(my_var); // test
}
```

## The `const` keyword

ES6 also introduced a new variable keyword: `const`. Variables declared with 
the `const` keyword are block scoped just like `let` however they cannot 
change by reassignment and they cannot be redeclared, they are immutable.

```js
const version = '0.0.1';
version = '0.0.2'; // TypeError: invalid assignment to const

const name = 'bill';
const name = 'ted'; // SyntaxError: Identifier 'name' has already been declared
```
Variables decalred by `const` (constants) cannot be changed, however; with a 
for loop the scope is redeclared at the start of each loop, where a new 
`const` can be initalized.

```js 

function myFunc(...args) {
	for(let [index, el] of args.entries()) {
		const message = `${el} found at index: ${index}`;
		console.log(message);
	} 
}

myFunc('test', 100, 200);
```

[Shadowing]: https://en.wikipedia.org/wiki/Variable_shadowing
