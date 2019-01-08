# ES6 Promises

> A Promise is an object representing the eventual completion or failure of an 
> asynchronous operation.
> - [MDN][MDN Promise]

## Working with promises

Promises are a convenient way to organize the order of operation for your 
program and provide and alternative to passing callbacks as function parameters.
Say we have a function `callToDb` that makes a database call and returns a 
promise

```js
function success(result) {
	// do something with result
}

function failed(error) {
	// do something with error
}

callToDb('table_name').then(success, failed);
```

`failed` is only called if an `Error` is returned. Both of these arguments are 
optional, however to use the result of the previous promise you need at least 
a success function with one argument

```js

callToDb('table_name')
	.then(response => {
		// do something with response
	})
	.catch(error => {
		// do something with error
	});
```

Like the above `failed` function, `catch` is only called if an `Error` is 
returned. `then` returns a promise meaning we can now create a promise `chain`.

```js

callToDb('table_name')
	.then(response => {
		// do something with response
		let res = response;
		res.changesMade = true;
		return res;
	})
	.then(response => {
		// do more work
	})
	.catch(error => {
		// do something with error
	});
```

Chains can be as long as you need them. `catch` can also be used multiple 
times in a promise chain, the next `catch` in the chain is called on return 
of an `Error` and following `then` blocks will still be called.

```js

callToDb('table_name')
	.then(response => {
		// do something with response
		let res = response;
		res.changesMade = true;
		return res;
	})
	.then(response => {
		// do more work
	})
	.catch(error => {
		// only called for above thens
	})
	.then(response => {
		// do more work
		// will still happen after the catch, even if catch is called
	})
	.catch(error => {
		// do something with error
		// only called for the one above then if an Error is returned
	});
```

## Creating a promise

The promise constructor should only be used to to wrap a function that does not 
support a promise. Most libraries have built-in support for promises which 
enable you to start chaining `then` right out of the box without a promise 
constructor.

The promise constructor takes one `executor` function with two arguments: 
`resolve` and `reject`. Let's create `callToDb`, a wrapping function to a 
function without promise support.

```js

function callToDb(table_name) {
	return new Promise((resolve, reject) => {
		return db_orm(`select * from ${table_name}`, (err, res) => {
			if(err) {
				reject(err);
			} else {
				resolve(res);
			}
		})
	});
}
```
A few things are happening here:

- `db_orm` is our database library without promise support, it takes a callback
- wrapping `db_orm` is our returning `Promise` which has our executor function
with `resolve` and `reject`
- once `db_orm` is in the callback we reject with the error, 
this will trigger a `catch` or
- we `resolve` with our result, this will trigger the next `then`

## Reject

Reject returns a promise that is rejected with a `reason`. To debug with ease 
it is recommended to make the `reason` an `instance of Error`

```js
Promise.reject(new Error('My custom message'))
	.then(result => {
		// not called
	})
	.catch(result => {
		console.log(result); // Error: My custom message
	})
```
To reject a promise inside a `then` chain you can return a `new Error` or 
throw an `Error` to the catch.

## Resolve

Resolve returns a promise that is resolved with a `result`. `result` can also 
be another `promise`, `thenable` or value.

```js
Promise.resolve('Sweet!')
	.then(result => {
		console.log(res); // Sweet!
	})
	.catch(result => {
		// not called
	});
```


[MDN Promise]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises
