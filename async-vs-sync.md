# Asynchronous vs Synchronous Programming

> Time is an illusion. Lunchtime doubly so.
- Douglas Adams, The Hitchhiker's Guide to the Galaxy

## Introduction

In programming synchronous operations block instructions until the task is 
completed while asynchronous operations can execute without blocking other 
operations. Asynchronous operations generally complete by firing an event or by 
calling a provided `callback` function.

## Breaking Down JavaScript

Javascript has:
- A Callstack
- WebAPI
- Event Loop
- Callback Queue

The Callstack is the imediate work your program will do. 

```js
let i = 0 // declare a mutable variable
i += 1 // add one to the variable
console.log(i) // log the variable
```
In the above example declaring a variable, adding one to the variable and 
log the variable are all three separate instructions that get added to the 
stack.

WebApi's are methods available from environments where JavaScript is run. In 
browsers the `window` and it's methods are apart of the WebAPI. When the WebAPI 
completes it puts the callback on the callback queue. The Event Loop waits for 
the stack to complete the loaded work. Once the Event Loop notices the stack is 
clear it will add work to the stack from the Callback Queue.

Consider `window.setTimeout` with a timer of `0` and a callback function that 
uses a variable before it is declared.

```js
window.setTimeout(() => console.log(i), 0)
let i = 0 
i += 1
```
Instead of an error, we get the correct answer `1`, this is because the function 
that uses `console.log` is a parameter to the first WebAPI instruction 
`window.setTimeout`. The callback function is moved to the callback queue when 
the timer completes. Once the stack clears declaring and adding one 
to the variable our function is called and it is safe to use the variable.

## Starting with `callbacks`

A callback executes once it is added to the Callstack. In the previous example 
this relied on a timer so complete, however other API's will have other 
condiditons. A `NodeJs` example:

```js
const fs = require('fs')
const content = 'Logging to a file'
fs.writeFile('test.txt', content, (err) => {
	if(err) {
		throw err
		process.exit(1)
	}
	console.log('logs completed')
	process.exit(0)
})
console.log('end script')
```
The callback is called once the `writeFile` API has completed:

- opening or creating the file
- writing to the file
- closing the file at the location speicfied

`fs.writeFile` is asynchronous so `console.log('end script')` is called before 
the work `writeFile` completes.  

What changes are needed to do this action synchronously?

<details>
<summary>Answer</summary>

```js
const fs = require('fs')
const content = 'Logging to a file'
try {
	fs.writeFileSync('test.txt', content)
	console.log('logs completed')
	process.exit(0)
} catch (err) {
	throw err
	process.exit(1)
}
```
If `err` is thrown the `console.log` is not called.
</details>

## Synchronous Operations

Synchronous Operations that run block the next operation until it completes.
Blocking operations may not always seem like an issue because computers are 
fast, for example: creating an array and logging the values in an array.

```js
Array
	.from({ length: 5 }, (v, i) => i + 1)
	.forEach(value => console.log(value))
```
However if the length was 5000 it would take longer before the array was logged.
The difference in timing is a result of the thread being locked for a longer 
time.

## Asynchronous Operations

Asynchronous Operations happen independantly from the main program flow. A 
common use for aynchronous code is querying a database and using the 
result. Passing a callback to provide a way to interact with the response or 
error.

```js
const database = require('thecoolestnewestdbframework')
database('table')
	.select('*')
	.asCallback((err, res) => {
		if (err) {
			throw err
		}
		// do something with result
	})
```

While the database load and responds to the request the rest of the page or 
other resources can load.

### Promises and Asynchornous code 

Promises are another way to interact with asynchronous code. In the above example
if the `const` database returned a Promise then we could write:

```js
const database = require('thecoolestnewestdbframework')
database('table')
	.select('*')
	.then(res => {
		// do something with result
	})
	.catch(err => throw err)
```
A Promise represents the work that is happening asynchronously, when the Promise 
resolves the result can be caught as an error, or use in a `then` method. `then` 
returns a promise, this means `then` is chainable returning another Promise to 
the next `then`.

```js
const database = require('thecoolestnewestdbframework')
database('table')
	.select('*')
	.then(res => {
		// do something with result
		return somethingDifferent
	})
	.then(res => {
		// do something else with new result
	})
	.catch(err => throw err)
```


