# ES6 Template Literals

Template literals are very handy for strings that use variables, or need to 
make use of a quick javascript expression. Template literals are enclosed with 
the back-tick  (\` \`). Template literals can also have `placeholders`, 
these are declared with a dollar sign and curly braces `${placeholder}`.
```js
// es6
let number = 42;
let str = `Here's my favourite number: ${number}.`;
console.log(str) // Here's my favourite number: 42.

let count = 0;
let displayCount = `${count + 1}`;
console.log(displayCount); // 1 
```

Template literals can be `tagged` with a function identifier before the 
back-ticks. The function allows you to parse the tempate literal, the first 
argument is an array of string values, the rest of the arguments relate to 
the placeholders in the template literal.

```js
let name = 'Theodor Logan';
let age = 21;

function showNameAndAge(strings, nameHolder, ageHolder) {
	let piece1 = strings[0]; // is
	let piece2 = string[1]; // years of age.
	let ageNotice = '';
	if(ageHolder < 25) {
		ageNotice = 'What a babyface. ';
	} else {
		ageNotice = 'What an oldtimer. ';
	}
	return = `${ageNotice}${nameHolder}${piece1}${ageHolder}${piece2}`;
}

showNameAndAge`${name} is ${age} years of age.` // What a babyface. Theodor Loagn is 21 years of age.
```

Tagged templates literals do not need to return a string.
