# ES6 Classes

ES6 `class` is new syntax for the traditional classes introduced in ES2015. 
ES6 Classes are not introducing anything to JavaScript rather _just another way 
to write a JavaScript class_. Class bodys are subject to JavaScript's
`strict mode`, the class body has new keywords and some words are 
reserved as keywords for future use.

As with functions, there are two ways to declare a class, `expression` or 
`declaration`. 

```js
// expression
const Instrument = class {}; // or class Instrument {}
const instrument = new Instrument();

// declaration
class Instrument {}
const instrument = new Instrument();
```

Unlike a function, a class must be declared or expressed before it can used.

## Constructors

`constructor` is a reserved keyword for classes and represent a function that
is called during a constructor initialization.

```js
class Instrument {
	constructor(props) {
		this._make = props.make;
		this._type = props.type;
	}

	get type() {
		return this._type;
	}
}

const noiseMaker = new Instrument({ make: 'Crafter', type: 'Guitar' });
console.log(noiseMaker.type); // Guitar
```
## Getters and Setters

`getters` and `setters` allow read and write access to class properties without 
having to define methods. Getters and setters are accessible by inherited 
classes.

```js
class Instrument {
	constructor(props) {
		this._make = props.make;
		this._type = props.type;
	}

	set make(make) {
		this._make = make;
	}

	get make() {
		return this._make;
	}

	set type(type) {
	 this._type = type;
	}

	get type() {
		return this._type;
	}

}

const noiseMaker = new Instrument({ make: 'Crafter', type: 'Guitar' });
noiseMaker.type = 'Drums';
noiseMaker.make = 'Yamaha';
console.log(noiseMaker.type); // Drums
```

## Inheriting

Classes can inherit a parent class. Keeping with Instruments, let's make a 
guitar class. The `super` keyword refers to the class being inherited.

```js
class Guitar extends Instrument {
	constructor(make) {
		super({make, type: 'Guitar'});
	}

	get make() {
		return `The make of the guitar is: ${super.make}`;
	}
}

const myGuitar = new Guitar('Fender');
console.log(myGuitar.make); // The make of the guitar is: Fender
myGuitar.make = 'Crafter';
console.log(myGuitar.make); // The make of the guitar is: Crafter
console.log(myGuitar.type); // Guitar
```

## Methods

Class methods are functions with the `function` keyword dropped.

```js
class Guitar extends Instrument {
	constructor(make) {
		super({make, type: 'Guitar'});
	}

	get make() {
		return `The make of the guitar is: ${super.make}`;
	}

	log() {
		console.log(this.make, this.type);
	}
}

const fender = new Guitar('Fender');
fender.log(); // The make of this guitar is: Fender, Guitar
```

## Object Definitions

Currently our object `.toString()` definition would return `[object Object]`.
We can change the definition with a method property.

```js
class Guitar extends Instrument {
	constructor(make) {
		super({make, type: 'Guitar'});
	}

	get make() {
		return `The make of the guitar is: ${super.make}`;
	}

	toString() {
		return `[${super.name} ${this.type}]`;
	}
}

const fender = new Guitar('Fender');
console.log(fender.toString()); // [Instrument Guitar]
```

## `super` and `this`

Before you can use `this.property` in a constructor of an inherited class, you 
must call `super()` first.

```js
class Guitar extends Instrument {
	constructor(make, stringCount) {
		super({make, type: 'Guitar'});
		this._stringCount = stringCount || 6;
	}

	get make() {
		return `The make of the guitar is: ${super.make}`;
	}

	get stringCount() {
		return this._stringCount;
	}

	set stringCount(stringCount) {
		this._stringCount = stringCount;
	}
}

const guitar = new Guitar('Fender', 12);
console.log(guitar.stringCount); // 12
```
