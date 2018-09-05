# ES6 Arrow Functions

Arrow functions are a shorthand syntax for functions that do not contain its 
own `this`, `arguments`, `super`, or `new.target` and cannot be used as 
constructors.

```js
const arr = ['hammer', 'nails', 'pizza', 'test'];
console.log(arr.map(value => value.length)); // [6, 5, 5, 4]
```

Arrow functions are useful for anonymous functions,
however their power is with the lexical scoping of `this`.

```js
function es6LexicalScope() {
	this.timeSpentSeconds = 0;
	setInterval(() => {
		console.log(this.timeSpentSeconds++); // 1 2 3 ...
	}, 1000);
}
es6LexicalScope();
```

Arrow functions do not have a `prototype`.

```js
const func = () => {};
console.log(func.prototype); // undefined
```

To return an object as an implicit return, you can wrap the object in 
the [`grouping operator`][Grouping Operator] (parentheses).

```js
const returnObj = () => { test: 'value' };
console.log(returnObj); // undefined

const returnObj = () => ({test: 'value'});
console.log(returnObj); // { test: 'value' }
```

If you noticed, there is a small difference between the usage of arrow 
functions in the provided exmaples. The usage of `()`:
- Arrow functions with no parameters require `()`
- Arrow functions with one parmeter `()` are optional
- Arrow functions with two or more parameters require `()`
- Arrow functions that only return, do not need `{}`, `return`, or `;`

```js
const fn1 = () => {[Native Code]};
const fn2 = param => {[Native Code]};
const fn2a = (param) => {[Native Code]};
const fn3 = (param1, param2) => {[Native Code]};
const fn4 = param => param;
```

[Grouping Operator]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Grouping
