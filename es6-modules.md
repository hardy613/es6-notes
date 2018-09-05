# ES6 Modules

ES6 modules use the `import` and `export` keywords and are intended to be used
with the browser or with a server environment like `NodeJs`

```js
// utils.js
export function add(left = 0, right = 0) {
	return left + right;	
};

export function times(left = 0, right = 0) {
	return left * right;
}
```

Now we can import our utils files. There are a few ways we can import.

```js
// index.js
import * as utils from './utils.js'
// utils.add(), utils.times()

import { add, times } from './utils.js'
// add(), times()
```

You can also export variables or objects. 

```js
// my-module.js

const myVariable = 100;

const person = {
	name: 'Bill',
	age: 42
};

function trim(string = '') {
	return typeof string === 'string' && string.trim();
};

export { myVariable, person, trim };

// index.js
import { myVariable as maxAge, person, trim } from './my-module.js';

console.log(maxAge, person.age); // 100, 42

trim(' test '); // 'test'
```

There are two different types of export, `named` and `default`. You can have 
multiple `named` exports in a module but only one `default` export. The above 
examples are all from the `named` export, let's take a look at the `default` 
export syntax.

```js
// a default funtion
export default function() {[...]}
export default function myFunc() {[...]}

// a default class
export default class MyClass {[...]}
```

You can also have a variable as a default export

```js 
// other-module.js
const mySuperLongNamedVariable = 100;
export default mySuperLongNamedVariable;
```

When importing defaults, you can name them without the ` * as ` keyword.

```js
// index.js
import theVariable from './other-module.js'
console.log(theVariable); // 100
```
