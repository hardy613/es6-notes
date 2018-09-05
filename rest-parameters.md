# ES6 Rest parameters

Functions can take a rest parameter that act as a placeholder for a non-finite number of arguments.

```javascript
function logArgsLength(...args) {
  console.log(args.length);
}

logArgsLength(1, 2); // 2
logArgsLength(1, 'a', 'b', 'c', 2, 3) // 6
```

Rest parameters give an array instance. `pop`, `push`, `join` and other array methods are available.

```javascript
function sentence(...words) {
  return words.join(" ");
}

console.log(sentence("You", "are", "awesome")); // "You are awesome"
console.log(sentence(["You", "are", "awesome"])); // "You,are,awesome"
```

`for...of ` loops can also be used with a rest operator.

```javascript
function avg(...numbers) {
  let total = 0;
  
  for(let number of numbers) {
  	total += number;
  }

  return Math.round(total / numbers.length);  
}

avg(1, 2, 3); // 2
avg(1, 2, 3, 4, 5, 6); // 4
```

The rest parameter is the remaining unnamed arguments from the function declaration and must be the last parameter.

```javascript
function debug(...items, something_else) {
  console.log('items', items);
  console.log(something_else);
}

debug(1, 2, 3, 'last'); // SyntaxError: Unexpected token
```
