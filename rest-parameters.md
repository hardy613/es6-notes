# ES6 Rest parameters

Functions can take a rest parameter that act as a placeholder for a non-finite number of arguments.

```javascript
function score(user, ...marks) {
  const marks_count = marks.length;
  let total = 0;

  // sum all the marks together
  for (let mark of marks) {
    total += mark;
  }

  const score = Math.round(total / marks_count);

  return `John has a score of ${score}`;
}

console.log(score("John", 12, 8, 8, 12, 15));

// "John has a score of 11"
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
