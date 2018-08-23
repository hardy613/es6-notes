# ES6 Rest Parameters

The `rest parameter` is an Array instance of unnamed arguments in the function
definition. 

```js
function oneTwoAndTheRest(one, two, ...andTheRest) {
	console.log(one, two, andTheRest);
}

oneTwoAndTheRest(1, 2, 3, 4, 5); // 1, 2, [3, 4, 5]
oneTwoAndTheRest(1, 2); // 1, 2, []
```

The rest parameter is an array instance. Array methods like `push`, 
`pop`, `sort` are available, including `for/of`.

```js
function sortArgs(...agrs) {
	return args.sort();
}

sortArgs(5,3,1,4,2); // 1, 2, 3, 4, 5

// thanks to @khalyomede on github for the suggestion
function avg(...points) {
	return Math.round(points.reduce((acc, curr) => acc + curr, 0) / points.length);
}

avg(5, 10, 15, 20, 25, 30) // 18
```

The rest parameter does not have `callee`.
