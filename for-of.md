# ES6 for/of

The `for/of` loop uses the [iterable protocol][Iterable Protocol] to create a 
loop. Strings, Arrays, TypedArray, Map, Set, NodeList, and custom iterable 
function hooks can all be used with `for/of`.

```js
const arr = [1, 2, 3];
for(let number of arr) {
	console.log(number) // 1 2 3
}
```

To iterate over an object you can use the protocol `Object.entries()`.
This will give arrays of `['key', 'value']` pairs. Unlike `for/in` this will
not iterate through the object prototype

```js
const obj = { a:1, b:2, c:3 };
for (let prop of Object.entries(obj)) {
	console.log(prop); // ['a', 1] ['b', 2] ['c', 3]
}
```

[Iterable Protocol]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols#The_iterable_protocol
