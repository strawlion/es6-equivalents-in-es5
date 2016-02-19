# <img src="http://i.imgur.com/yy1sACZ.png" width="100px"> ECMAScript 6 equivalents in ES5

*Please note this document is very much a work in progress. Contributions are welcome.*

**Table of contents:**

1. [Arrow Functions](#arrow-functions)
1. [Block Scoping Functions](#block-scoping-functions)
1. [Template Literals](#template-literals)
1. [Computed Property Names](#computed-property-names)
1. [Destructuring Assignment](#destructuring-assignment)
1. [Default Parameters](#default-parameters)
1. [Iterators and For-Of](#iterators-and-for-of)
1. [Classes](#classes)
1. [Modules](#modules)
1. [Numeric Literals](#numeric-literals)
1. [Property Method Assignment](#property-method-assignment)
1. [Object Initializer Shorthand](#object-initializer-shorthand)
1. [Rest Parameters](#rest-parameters)
1. [Spread Operator](#spread-operator)
1. [Proxying a function object](#proxying-a-function-object)
1. [About](#about)
1. [License](#license)

## Arrow Functions

An arrow function expression (also known as fat arrow function) has a shorter syntax compared to function expressions and lexically binds the this value. Arrow functions are always anonymous.


ES6:

```js
[1, 2, 3].map(n => n * 2);
// -> [ 2, 4, 6 ]
```

ES5 equivalent:

```js
[1, 2, 3].map(function(n) { return n * 2; }, this);
// -> [ 2, 4, 6 ]
```

## Block Scoping Functions

Block scoped bindings provide scopes other than the function and top level scope. This ensures your variables don't leak out of the scope they're defined:

ES6:

```js
// let declares a block scope local variable,
// optionally initializing it to a value in ES6

var a = 5;
var b = 10;

if (a === 5) {
  let a = 4; // The scope is inside the if-block
  var b = 1; // The scope is inside the function

  console.log(a);  // 4
  console.log(b);  // 1
}

console.log(a); // 5
console.log(b); // 1
```

ES6:

```js
// const creates a read-only named constant in ES6.
const myFavoriteNumber = 7;

try {
  myFavoriteNumber = 15;
} catch (err) {
  console.log('my favorite number is still: ' + myFavoriteNumber);
  // will still print 7
}
```

## Template Literals

ES6 Template Literals are strings that can include <strong>embedded expressions</strong>. This is sometimes referred to as string interpolation.

ES6:

```js
// Basic usage with an expression placeholder
var name = 'Adam';
console.log(`My name is ${name}!`);

// Expressions work just as well with object literals
var person = { name: 'Adam' };
console.log(`My name is still ${person.name}!`);

// Expression interpolation. One use is readable inline math.
var a = 50;
var b = 100;
console.log(`The number of JS frameworks is ${a + b} and not ${2 * a + b}.`);

// Multi-line strings without needing \n\
console.log(`string text line 1
string text line 2`);

// Functions inside expressions
function getResult() { return 'result'; }
console.log(`foo ${ getResult() } bar`);
```

## Computed Property Names

Computed property names allow you to specify properties in object literals based on expressions:

ES6:

```js
var prefix = 'foo';
var myObject = {
  [prefix + 'bar']: 'hello',
  [prefix + 'baz']: 'world'
};

console.log(myObject['foobar']);
// -> hello
console.log(myObject['foobaz']);
// -> world
```

## Destructuring Assignment

The destructuring assignment syntax is a JavaScript expression that makes it possible to extract data from arrays or objects using a syntax that mirrors the construction of array and object literals.

ES6:

```js
var { foo, bar } = { foo: 'lorem', bar: 'ipsum' };
console.log(foo); // -> lorem
console.log(bar); // -> ipsum
```

ES6:

```js
var [a, , b] = [1, 2, 3];
console.log(a) // -> 1
console.log(b) // -> 3
```

## Default Parameters

Default parameters allow your functions to have optional arguments without needing to check arguments.length or check for undefined.

ES6:

```js
function greet(message='hello', name='world') {
  console.log(message, name);
}

greet();
// -> hello world
greet('hey');
// -> hey world
```

## Classes

This implements class syntax and semantics as described in the ES6 draft spec. Classes are a great way to reuse code.
Several JS libraries provide classes and inheritance, but they aren't mutually compatible.

ES6:

```js
class Hello {
  constructor(name) {
    this.name = name;
  }

  sayHello() {
    return 'Hello ' + this.name + '!';
  }

  static sayHelloAll() {
    return 'Hello everyone!';
  }
}

class HelloWorld extends Hello {
  constructor() {
    super('World');
  }
}

var helloWorld = new HelloWorld();
console.log(helloWorld.sayHello()) // -> Hello World!
console.log(Hello.sayHelloAll()); // -> Hello everyone!
```

## Modules

Modules try to solve many issues in dependencies and deployment, allowing users to create modules with explicit exports, import specific exported names from those modules, and keep these names separate.

*Assumes an environment using CommonJS*


app.js - ES6

```js
import * as math from 'lib/math';
console.log('2π = ' + math.sum(math.pi, math.pi));
```

lib/math.js - ES6

```js
export {
  sum,
  pi: 3.141593
};

function sum(x, y) {
  return x + y;
}
```


## Property Method Assignment

Method syntax is supported in object initializers, for example see toString():

ES6:

```js
var object = {
  value: 42,
  toString() {
    return this.value;
  }
};

console.log(object.toString() === 42); // -> true
```

## Object Initializer Shorthand

This allows you to skip repeating yourself when the property name and property value are the same in an object literal.

ES6:

```js
var x = 1;
var y = 10;

var point = { x, y };
console.log(point.x) // -> 1
console.log(point.y) // -> 10
```

## Rest Parameters

Rest parameters allows your functions to have variable number of arguments without using the arguments object.
The rest parameter is an instance of Array so all the array methods just work.

ES6:

```js
function sum(...values) {
  return values.reduce((sum, value) => sum + value, 0);
}

console.log(sum(1, 2, 3)); // -> 6
```

## Spread Operator

The spread operator is like the reverse of rest parameters. It allows you to expand an array into multiple formal parameters.

ES6:

```js
function add(a, b) {
  return a + b;
}

let values = [1, 2];

console.log(add(...values)); // -> 3
```

## About

Inspired by:

* [ES6 Feature Proposals](http://tc39wiki.calculist.org/es6/)
* [ES6 Features](https://github.com/lukehoban/es6features)
* [ECMAScript 6 support in Mozilla](https://developer.mozilla.org/en-US/docs/Web/JavaScript/New_in_JavaScript/ECMAScript_6_support_in_Mozilla)
* [Babel](https://babeljs.io)
* [JS Rocks](http://jsrocks.org/)


## License

This work is licensed under a [Creative Commons Attribution 4.0 International](http://creativecommons.org/licenses/by/4.0/) License.
