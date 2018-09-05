# ES6 Destructuring Assignment

Destructuring assignment lets you unpack values from an array or object.

```js
const [x, y] = [1, 2, 3, 4, 5];
console.log(x); // 1
console.log(y); // 2;

const person = { name: 'Bill', age: 42, email: 'bill@example.ca', url: 'http://example.ca' };
const {name, age} = person;
console.log(name, age); // Bill, 42
```

Sometimes you want to keep all the other stuff. That is where the spread 
operator [`...`][Spread Operator] comes in handy.

```js
const [x, y, ...allTheRest] = [1, 2, 3, 4, 5];
console.log(x, y, allTheRest); // 1, 2, [3, 4, 5]

const person = { name: 'Bill', age: 42, email: 'bill@example.ca', url: 'http://example.ca' };
const {name, age, ...details} = person;
console.log(name, age, details); // Bill, 42, {email: 'bill@example.ca', url: 'http://example.ca'}
```

You can also destructure to build new variables!

```js
const otherObj = {};
const person = { name: 'Bill', age: 42, email: 'bill@example.ca', url: 'http://example.ca' };
const obj = {...otherObj, person};
console.log(obj); // { person: {[...]} }
```

`obj` now has our `person` property with our person `Bill`. If the person 
property was already set in `otherObj` then we would override that property. 
Let's look at unpacking the length property from a string with destructuring.


```js
const arr = ['hammer', 'nails', 'pizza', 'test'];
// without destructuring
console.log(arr.map(value => value.length)); // [6, 5, 5, 4]
// with destructuring
console.log(arr.map(({ length }) => length)); // [6, 5, 5, 4]
```

Let's breakdown the line we just added. `console.log(arr.map(` is pretty 
standard. `({ length })` is the parameter for our arrow function, we are passing 
in a string and destructuring the length property from the string and passing 
that as a variable called `length`. The function parameter is the string 
length. `=> length));` the rest of our arrow function. The property is also 
the variable identifier and we only return the `length`. If you need a default 
with destructuring, you can do that too!

```js 
const { name = 'Bill', age = 30 } = { name: 'Ted' };
console.log(name, age)// Ted, 30

const [x = 5, y = 10] = [20];
console.log(x, y) // 20, 10
```

[Spread Operator]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax
