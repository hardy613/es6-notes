# Asynchronous vs Synchronous Programming

## Introduction

In programming synchronous operations block instructions until the task is 
completed while asynchronous operations can execute without blocking other 
operations. Asynchronous operations generally complete by firing an event or by 
calling a provided `callback` function.

Javascript has the callstack, webAPI, event loop and callback queue. Operations 
happen in that order, however The stack must be cleared for the evenloop to 
push callbacks from the on the queue to the stack. NodeJs or browsers act as 
the WebAPI. 

## breaking down `callbacks`

A lot of developers starting with asynchronous code are familiar 
with `callbacks`. A `callback` function pushed is onto the callback queue once
the webAPI has completed it's task. When the stack clears the event loop pushes 
the callback function onto the stack.

Using `setTimeout` you can mock asynchronous behaviour. In a modern 
browser try:

```js
const time = window.setTimeout(() => {
	console.log('one')
}, 0)
console.log('two');
```
The results are: 

- `two`
- `one`

This is becuase `setTimeout` pushes the `callback` onto the callback queue after 
the set amount of time, in this case `0`. Once `two` is logged the event loop 
pushes the callback onto the stack can `one` is logged.

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
is set it would be thrown and the `console.log`'s would not be called.

```js
const fs = require('fs')
const content = 'Logging to a file'
try {
	fs.writeFileSync('test.txt', content)
} catch (err) {
	throw err
}
console.log('logs completed')
console.log('end script')
```
</details>

## Starting with  Synchronous Operations

```js
const arr = [1, 2, 3, 4, 5, 6]
arr.forEach(value => {
	const element = document.createElement('li')
	element.textContent = `https://example.com/page/${value}`
	const ul = document.querySelector('#page-list')
	ul.appendChild(element)
	const link = document.createElement('a')
	link.href = element.textContent
	element.appendChild(link)
	element.addEventListener('click', () => {
		console.log(`clicked ${element.textContent}`) // don't track me bro
	})
})
console.log('all done')
```
In the above example operations are executed one after another. `all done` will 
only be logged once all the `li` and `a` tags have been added to the document. 
While the `forEach` happens over the array other operations are blocked until 
the `forEach` completes. The same goes for the operations inside the `forEach`, 
one must complete before the next instruction can happen.

## Asynchronous 
