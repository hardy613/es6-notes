# Symbols

The symbols descriptor is used to specify the specials symbols used in newer syntax of the ECMAScript standard. A symbol can be a string, image, or identifier.

Some behavior linked to these symbols are already built-in the language, like the rest parameters :

```javascript
const count = (...items) => items.length

console.log(count('first', 'second', 'third')) // 3
```

Sometimes, extending the behavior to special types, like userland classes can be useful. Let's imagine we have a Garage class:

```javascript
class Garage {

  constructor(...motorcycles) {
    this.motorcycles = motorcycles
  }
}

const myGarage = new Garage('Street Triple S', 'MT07', 'Z900')
```

And let's imagine we want to have a shorthand to get all our motorcycles:

```javascript
console.log([...myGarage]) // TypeError: myGarage is not iterable
```

In order to add this behavior to our garage implementation in JavaScript, we need to add a special function to our class:

```javascript
class Garage {

  constructor(...motorcycles) {
    this.motorcycles = motorcycles
  }

  *[Symbol.iterator]() {
    for (const motorcycle of this.motorcycles) {
      yield motorcycle
    }
  }

}
```

It will allow us to iterator over each one of our motorcycle from our garage:

```javascript
console.log(...myGarage) // Array(3) [ "Street Triple S", "MT07", "Z900" ]
```

In fact, it uses a generator function, because the Iterator interface needs us to implement a generator function in order to use that little trick. It is like if we had written something like this:

```javascript
*...() {
  // ...
}
```

Except we can't really write it that way, because it is a reserved keyword. Using the `Symbol.iterator` let's us access this special keyword. The brackets are here to define a dynamic name to our function, which will be understand as the `...` keyword at runtime.

Another cool example is making our own range function, just like in Python, but cooler:

```javascript
Number.prototype[Symbol.iterator] = function *() {
  for (let index = 0; index < this; index++) {
    yield index
  }
}

console.log([...10]) // Array(10) [ 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 ]
```

Notice that I also used a generator function for the same reasons we said before.
