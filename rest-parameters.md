# ES6 Rest parameters

Functions can take a rest parameter that act as a placeholder for a non-finite number of arguments.

```javascript
function logArgsLength(...args) {
  console.log(args.length);
}

logArgsLength(1, 2); // 2
logArgsLength(1, 'a', 'b', 'c', 2, 3) // 6
```

Rest parameters automatically build an array, so given this function:

```javascript
function sentence(...words) {
  return words.join(" ");
}
```

The following code will work as expected:

```javascript
console.log(sentence("You", "are", "awesome"));

// "You are awesome"
```

While this code will convert the array into its string representation:

```javascript
console.log(sentence(["You", "are", "awesome"]));

// "You,are,awesome"
```

Rest parameters build an array with the parameters **left**, so if you put a rest parameters in first argument followed by another one:

```javascript
function debug(...items, something_else) {
  console.log('items', items);
  console.log(something_else);
}

debug(1, 2, 3, 'last');
```

This will produce the following error:

```
SyntaxError: Unexpected token, expected ) (1:23)
```
