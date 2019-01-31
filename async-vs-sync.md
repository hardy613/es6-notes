# Asynchronous vs Synchronous Programming

> Time is an illusion. Lunchtime doubly so.
- Douglas Adams, The Hitchhiker's Guide to the Galaxy

## Introduction

In programming synchronous operations block instructions until the task is 
completed while asynchronous operations can execute without blocking other 
operations. Asynchronous operations generally complete by firing an event or by 
calling a provided `callback` function, sometimes refered to as a `future` or 
`promise`.

## Breaking Down JavaScript

Javascript has:
- A Callstack
- WebAPI
- Event Loop
- Callback Queue

The Callstack is the imediate work you program will do. 

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
completes it puts the callback on the event loop. The Event Loop waits for the 
stack to complete the loaded work. Once the Event Loop notices the stack is 
clear it will add any work to the stack from the Callback Queue.

Consider `window.setTimeout` with a timer of `0` with a callback function that 
uses a variable before it is declared.

```js
window.setTimeout(() => console.log(i), 0)
let i = 0 
i += 1
```

Instead of an error, we get the correct answer `1`, this is because the function 
that `console.log`'s is a parameter to the first WebAPI instruction 
`window.setTimeout`. The callback funtion is moved to the callback queue. Once 
the stack clears declaring the variable and adding one to the variable our 
function is called and it is safe to use the variable.

## Starting with `callbacks`
L


A `NodeJs` example:

```js
const fs = require('fs')
const content = 'Logging to a file'
fs.writeFile('test.txt', content, (err) => {
	if(err) {
		throw err
	}
	console.log('logs completed')
})
console.log('end script')
```
In this example what is the order of the `console.log`'s ?

<details>
<summary>Answer</summary>

- `end script`
- `logs completed`

The callback is called once the `writeFile` API has completed:

- opening or creating the file
- writing to the file
- closing the file at the location speicfied

`fs.writeFile` is asynchronous so `console.log('end script')` is called before 
the work `writeFile` has to do. Doing this action synchronouly sould require a 
try catch and the synchronous version of `writeFile` - `writeFileSync`. If `err` 
is set it would be thrown causing `console.log` not be called.

```js
const fs = require('fs')
const content = 'Logging to a file'
try {
	fs.writeFileSync('test.txt', content)
	console.log('logs completed')
} catch (err) {
	throw err
}
```
</details>

## Synchronous Operations




```js
Array
	.from({ length: 5000 }, (v, i) => i + 1)
	.forEach(value => console.log(value))
```


## Asynchronous Operations


