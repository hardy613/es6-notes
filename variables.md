
# ES6 Variables


## `var` vs `let`
A variable in javascript is a named space in memory. Traditionally the keyword
`var` initializes the `identifier` with a `value`:
 

{% runkit %}
 
var	my_variable	=	'value';
//1	//2			//3 

//1 the var keyword
//2 the identifier
//3 the value


{% endrunkit %} 



There are rules for naming the variable identifier. These are:
- identifiers cannot be keywords
- can be alphanumeric, although cannot start with a number
- `$` and `_` are also allowed characters for an identifier

Variables declared by `var` have the scope of the entire function.

{% runkit %}
function myFunc() {
	if(true) {
		var my_var = 'test';
	}
	console.log(my_var); // test
}

myFunc();

{% endrunkit %} 

## The `let` keyword

`let` is preferred over `var`. Variables declared by `let` have their scope
within the `block` they are defined.

{% runkit %}
function myFunc() {
	if(true) {
		let my_var = 'test';
	}
	console.log(my_var); // TypeError
}

myFunc();
{% endrunkit %} 

Block scoping allows for variable [`shadowing`][Shadowing].

{% runkit %}
function myFunc() {
	let my_var = 'test';
	if(true) {
		let my_var = 'new test';
		console.log(my_var); // new test
	}
	console.log(my_var); // test
}

myFunc();
{% endrunkit %}

## The `const` keyword

ES6 also introduced a new variable keyword: `const`. Variables declared with 
the `const` keyword are block scoped just like `let` however they cannot 
change by reassignment and they cannot be re-declared; they are immutable.

{% runkit %}
const version = '0.0.1';
version = '0.0.2'; // TypeError: invalid assignment to const

const name = 'bill';
const name = 'ted'; // SyntaxError: Identifier 'name' has already been declared
{% endrunkit %}
Variables declared by `const` (constants) cannot be changed. However, with a 
for loop the scope is redeclared at the start of each loop, where a new 
`const` can be initalized.

{% runkit %}

function myFunc(items) {
	for(let i = 0; i < items.length; i++) {
		const message = items[i] + ' found at index: ' + i;
		console.log(message);
	} 
}

myFunc(['test', 100, 200]);

{% endrunkit %}

[Shadowing]: https://en.wikipedia.org/wiki/Variable_shadowing

