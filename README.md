# ES6
An introduction to ES6 features to get you up to speed with what the future will look like — things have changed and the `ES6` spec has added syntax that devs will love. It's **wise to adopt today** what **we'll see tomorrow**.

## Table of Contents
* [ECMA Brief History](#history)
* [Introduction](#es6-introduction)
* [Tools](#tools)
* [Block Scoping](#block-scoping)
* [Let and Const](let-and-const)
* [Destructuring](#destructuring)
* [String & Template Literals](#string-and-template-literals)
* [Math & Number](#numbers-and-strings)
* [Arrays](#arrays)
* [Rest Parameter & Spread Operator](#spread-and-rest)
* [Modules](#modules)
* [Classes](#classes)
* [Symbols](#symbols)
* [Generators](#generators)
* [Arrow Functions](#arrow-functions)
* [Map & WeakMap](#map-and-weakmap)
* [Set & WeakSet](#set-and-weakset)
* [Promises](#promises)

## History
* ECMAScript is now 17 years old with it's birth in 1997 
  * ECMAScript is the standard. `JavaScript`, `ActionScript` and `JScript` are implementations of it.
  * JavaScript has drastically changed from just `validation` and `on change` handlers to projects with a huge code base
  * The language was invented by Brendan Eich at Netscape in just under two weeks.
  * It first appeared in Navigator 2.0 browser and has appeared in all subsequent browsers from Netscape and in all browsers from Microsoft starting with Internet Explorer 3.0. 

_A brief snapshot of it's history:_

| Edition  | Year          | Notes                                                                                    |
| -------- |:-------------:|------------------------------------------------------------------------------------------|
| 1        | 1997          |      Oracle (prev. Sun) had trademark to Java, therefore JavaScript                      |
| 2        | 1998          |      ECMA International creates the ECMA-262 standard                                    |
| 3        | 1999          |      Introduced many features inherint in the language today                             |
| *3.1     | 2008          |      Eventually standardized as the 5th of ECMA-262, also described as ECMAScript 5      |
| *4       | abandoned     |      Abandoned due to political reasons                                                  |
| 5        | 2009          |      Added 'use strict' ( aligns with 3+ )                                               |
| 5.1      | 2011          |      Maintenance revision (alings with 3+ )                                              |
| 6        | 2015          |      Significant features added, that's why you're here                                  |
| 6        | unreleased    |      Early stages of development                                                         |

&#8593; [Back to TOC](#table-of-contents)

## ES6 Introduction
`ES6` is the newest addition to the language and adds **significant** new syntax for writing complex JavaScript applications.
 * There is 5 years between `ES5` and `ES6`.  
 * 'ES6' is the first **ECMAScript Harmony** specification and is also known as `ES Harmony`, `ES2015`, `ES.next` but commonly referred to as `ES6`.
* The specification was finalized in `June 2015`as it reached `feature complete` status
  * Subsequent versions will be released on a 12 month cadence, and will be dubbed `ES7`, `ES2016` respectively.

[&#8593; Back to TOC](#table-of-contents)  

## Tools
You should want to experiment and play around with code — it's easy to get up and running. There are several techniques and the premise all these tools are built upon is called `transpiling`, or **JavaScript to JavaScript** transpiling which compiles the latest version into older versions.
* Transpilation is the future for future ECMAScript such as `ES2015` and `ES2016`
* The most popular JavaScript transpilers are `Babel` and was previously known as `6to5` and `traceur`
* Transpilation is possible to incorporate into your build process using [Broccoli](), [Gulp](), [Browserify](), [RequireJS](), [Webpack]() et al and friends.

_The easiest way to get up and running in the `web browser`:_

* In the web browser you can use the online `Babel REPL` — this compiles `ES6` to `ES5` and you don't have to install anything.
* Another web based tool is `Scratch JS` and comes in the form of a chrome extension. This interactive playground let's you transpile your code in the all familiar `dev tools` environment.

_If you prefer the `command line`:_
a
* Use Node,js v4.x.x or `>`, they support is in-built for Babel
* Run `npm install -g babel' and `babel node`

_Using an `IDE`:_

* You can easily use `Babel` to transpile your code in **Webstorm**, the setup won't take more than a couple of moments.

_Node has decent built in support for `ES6` thanks for the `V8` engine:_

* Node suports `ES6` features split into three groups
 * Shipping: which do not require a **runtime flag**
 * Staged: almost-complete features that are not considered stable
 * In progress: features can be individually activated by their respective harmony flag `--harmony_destrucuting`

&#8593; [Back to TOC](#table-of-contents)
 
## Block Scoping
ES6 introduces block scoping:
* anything between `{` ... `}` introduces it's own scope
* this works like an `IIFE`
* functions are **block scoped** in ES6 
 * this is more mainstream than **function scoping** which makes it easier when coming from or moving to other languages  

``` javascript
{
    let quux = "Hello World from ES6";
    console.log(quux); // => Hello World from ES6
}

{
    let foo = "This has a different scope";
    console.log(foo); // => This has a different scope
}

console.log(quux); // Reference Error: quux is not defined
```

> In ES5 you would use the `function` as the **fundamental construct** for all your variable scoping.

``` javascript
var x = 7;

(function iife() {
  var x = 10;
  console.log( x ); // => 10;
})();

console.log( x ); // 7  
```

&#8593; [Back to TOC](#table-of-contents)
    
## Let and Const

`let` and `const` are two new identifiers for storing values in `ES6` which you can additionally use to declare variables
'let' and 'const' throw more exceptions as they behave more strictly than 'var'
* `let` is block scoped and is **hoisted** to the top of it's block, **unlike** `var` which is hoisted to the top of it's **function** or **script**
* `const` is also block scoped and is also **hoisted** to the top of it's block
    * it's worth noting that in ES6 functions are **block scoped** instead of lexically scoped
'var`
* `let` does not create a property on the global object
* `const` creates **immutable** variables, whilst `let` create **mutable** ones
* a duplicate declaration of `let` will throw a **Reference Error** within a block or function
 * this is also known as `TDZ` or temporal dead zone
* _Basic rules to follow_: 
 * don't use `var`, or leave it as a signal in untouched legacy code.
 * use `let` when you want to rebind.
 * prefer `const` for variables that never change.
 * don't blindly refactor legacy code when replacing `var` with `let` and `const`.
 
> how `let` works: 
 
 ``` javascript
 function myfunc() {
   if ( true ) {
     let x = 54321;
   }
   console.log( x ); // => ReferenceError: x is not defined  
 }
``` 

``` javascript
// legacy ES5
 function myfunc() {
   if ( true ) {
     var x = 54321;
   }
   console.log( x ); // => 54321 
 }
``` 
> using block scoped `let`:

``` javascript
let outer = "outer";
{
  let inner = "inner";
    { 
      let nested = "nested"
    }
  console.log( inner ); // => you can access `inner`
  console.log( nested ) // => throws error  
} 
// you can access `outer` here
// you cannot access `inner` and `nested` here 
```

> more scoping rules for variables declared by `let`. you can clearly see that when refac:

``` javascript
function letBlocks {
  let a = 23;
  if ( true ) {
    let a = 56;
    console.log( a ); // => 56
  }  
  console.log( a ); // => 23
}  
```

> How `const` works. Variables declared with `const` are immutable, but note that the values aren't just the declarations:

``` javascript
const foo = '123';
foo = '321';
console.log( foo ); // TypeError

// changing const values
const myarr = [1,2,3,4];
myarr.push(5);
console.log( myarr ); // => 1, 2, 3, 4, 5

const obj = {};
obj.prop = 123;
console.log( obj ); // => { Object: prop: 123 }
```

&#8593; [Back to TOC](#table-of-contents)

## Destructuring

Just like an object literal is a convenient way to construct an object, ES6 destructing allows you to extract values from data stored in objects or arrays.
* You can assign to more than just **variables**
* Destructuring can be used in **assignments**, **variable declarations** and **parameters**
* `spread` and `rest` operators work with destructuring
* You can destructure a `for-of` loop

> Objects:

``` javascript
const myObj = { firstname: 'Ahad', lastname: 'Bokhari' };
const { firstName: fname, lastName: lname }; = myObj
console.log( fname, lname ); // => Ahad Bokhari

let a, b;
({ a, b } = {a: 1, b: 2});
console.log(a, b);

// deeper objects
const {
  prop1: z,
  prop2: {
    prop2: {
      nested: [ , , c]
    }
  }
} = { prop1: "Hello", prop2: { prop2: { nested: ["a", "b", "c"] }}};
console.log(z, c);
```

> Arrays:

``` javascript
const myArr = [ 'y', 'z'];
const [ a, b ] = myArr;
console.log( a, b ); // => y, z

let [ a, , b ] = [ 'x', 'y', 'z' ];
console.log( a, b );

// deeper arrays
const [ a, [b, [c, d]]] = [1, [2, [[[3, 4], 5], 6 ]]];
console.log("a:", a, "b:", b, "c:", c, "d:", d); // => a: 1 b: 2 c: [ [ 3, 4 ], 5 ] d: 6
```

&#8593; [Back to TOC](#table-of-contents)

## String and Template Literals
We all know that JavaScript `strings` are limited and lacking in capabality, especially if you're coming from **Ruby** or **Python**. Template literals are a feature that developers will love and are basically just `string literals` allowing `embedded expressions`.
* `ES6` introduces `string interpolation`, `string formatting`, `multiline strings` and `embedded expressions` with template literals
* Template strings use (``) rather than single or double quotes used with regular strings
* Placeholders using the `${ }` syntax are used from string substition and works fine with any kind of **expression**
 * expressions in between the placeholders (${expression}) and text b/w them get passed to a function
  
> Familiarize yourself with the `syntax`:

``` javascript
const a = `this is a template literal`;
console.log( typeof a ); // => string

const b = `You can use template literals in multiline
statements without using \\n`;
console.log( b ); // => yup, it works!

const c = `Some string text ${expression}`;
```

> Use the following syntax to `embed` expressions within template literals

``` javascript
const a = 100,
      b = 100;
console.log(`The sum of ${a} * ${b} is ${a * b}`); 
// => The sum of 100 * 100 is 1000

const user = { name: `Ahad Bokhari` };
console.log(`You are now logged in, ${ user.name.toUpperCase() }. `);
// => You are now logged in AHAD BOKHARI
```

&#8593; [Back to TOC](#table-of-contents)

## Math and Number 

* Additions to `integer literals` have been added included `octal` and `binary` literals
* Methods that have been added to `Number` apart from the usual four suspects are, `Number.EPSILON`, `Number.isInteger`, `Number.isNaN`, `Number.isFinite`, `number.isSafeInteger`
* `Number.MAX_SAFE_INTEGER`, `Number.MIN_SAFE_INTEGER` are the largest and smalled integer that are represented in JavaScript
* The math object has also received some useful methods in `ES6`, `Math.sign`, `Math.trunc`, `Math.cbrt`

&#8593; [Back to TOC](#table-of-contents)

## Arrays

`ES6` brings an abundance of new Array methods

* Array: `from`, `of`
* Array.prototype: `findIndex()`, `fill()`, `find()`, `copyWithin()`, `keys()`, `values()`, `entries()`

> Using `Array.from` we create a new array instance from an `array-like` or `iterable object` 

```javascript
var doc = document.querySelectorAll('*');
Array.from(doc).forEach(function(nodes) {
  console.log(nodes);
});
```

> Using `Array.of` we create an array of variable arguments passed to the function

``` javascript
var arr = Array.of(true, null, undefined, `some message`, 50);
console.log( arr ); //[ true, null, undefined, "some message", 50]
```

> Examples of additional `array` methods:

``` javascript
// copyWithin()
[1, 2, 3, 4, 5].copyWithin(0, 3); // => [4, 5, 3, 4, 5]

let letters = ["A", "B", "C", "D", "E", "F", "G", "H", "I", "J"];
letters.copyWithin(4, 0); // => there is an optional parameter copyWithin(4, 0, 2)
console.log(letters); // ["A", "B", "C", "D", "A", "B", "C", "D", "E", "F"]

// find()
let cities = ["Beirut", "Karachi", "Islamabad", "Athens", "Kabul", "Tapei", "Bucharest"];

let t = cities.find(char => char.endsWith("t"));
console.log( t ); 

// keys()
let people = ["Ahad", "Moe", "Zoey", "Snaey"];

for( let entry of fruits.entries() ) {
  console.log(entry[0]);
  // 0
  // 1
  // 2
  // 3
  
  console.log(entry[1]);
  // Ahad
  // Moe
  // Zoey
  // Snaey
}
```

&#8593; [Back to TOC](#table-of-contents)

## Rest Paramater and Spread Operator

## Modules

At the core of modularity developers need a module system — a way to spread their work across numerous files and directories with access to each other. Without support for modules natively in ECMAScript there has been a community created effort to implement work-arounds — CommonJS and AMD being the most prevelant as
they both have communities that rally around them, but are incompatible with each other. The good news is ES6, ( TC39 group ) has finalized a module syntax which developers can greatly benefit from using the best from both worlds.
* The goal of modules in `ES6` is to keep **both** `CommonJS` and `AMD` user happy with a single format and borrows the best from both worlds
 * `ES6` modules will have a compact syntax with a preference for a single exports ( such as CommonJS )
 * direct support for asynchronous and configurable module loading is supported
* There are two types of exports, `named` exports and `default` exports
 * **named exports** can be used to export multiple things using the keyword `export`
 * **default exports** used to export a default single value
* To import functions, objects and primitives that have been exported from an external module use the `import` statement
 * you may `import` an entire modules contents, a single member or multiple members in a module

> A convenient way to specify `named` exports as below:
 
``` javascript
// lib.js
// -------
export const quux = Math.sqrt( 2 ); // => exports a constant
export function multiply( x, y ) {
  return x * y;
} // => exports a function

export function addContact( id, callback ) {
  callback();
} // => exports a function

export function refreshContact() {
  alert( `Hello ES6 Modules` );
} // => exports a function
```
> And of course `import` them into another file:

``` javascript
// main.js
// -------
import quux from 'lib';
import { multiply, addContact, refreshContact } from 'lib';

console.log( quux ); // => 1.4142135623730951
console.log( multiply(10, 10); // => 1000
console.log(addContact(1, refreshContact)); // => alerts `Hello ES6 Modules`
// app.js
// ------
// import the whole module
import * as lib from 'lib'

console.log( lib.quux ); // => 1.4142135623730951
console.log( lib.refreshContact() ); // => alerts `Hello ES6 Modules`
```
> Another technique in a module, we could use the following:

``` javascript
const quatro = 10 * 10 * 10 * 10;
export { quatro }; 
```

> `default` exports is simple one module that you want to export as the default ( like CommonJS ) and it turns out you can use `default` exports and `named` exports both in your module. There is alot more on `modules` in `ES6` including `script` tags, using `promises` and `module loading` which is an API that allows you to programmatically work with modules and configure module loading. 

&#8593; [Back to TOC](#table-of-contents)

## Classes

## Generators

## Arrow Functions

Arrow functions are one of the more popular features of `ES6` saving developer time and simplifying function scope. 
* The arrow `(=>)` or `fat arrow` provides a shorthand for the function keyword with lexical `this` binding
 * Arrow functions change the way `this` binds in functions
 * They work much like `lambdas` in languages like `C#` or `Python`
   * `lambda` expressions are are often passed as arguments to **higher order functions**
 * we avoid the `function` keyword, `return` keyword and `curly brackets` when using arrow functions
* Arrow functions allow developers to remove boilerplate, however you shouldn't remain ignorant of how 'lexical` scoping `this` works 
* Be careful when using `arrow functions` as they aren't applicable everywhere, **use cases** will depend from situation to situation

> For the sake of simplicity, we could do the following:

``` javascript
const msg = () => alert("Hello Arrow Function");
console.log(msg());
```

``` javascript
let square = ( a, b ) => a * b; 
console.log(square(5, 5)); // 25
```

``` javascript
let x = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
let z = x.map(x => x); 
console.log(z); // [ 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 ]
```

> Every new function defines it's own `this` value, yet `arrow` functions **close** over the `this` value

``` javascript
// in ES5
function Tree() {
  that = this;
  that.age = 0;
  
  setInterval(function growOld() {
    that.age++;
  }, 1000);  
}

var t = new Tree();

// in ES6
function Tree() {
  this.age = 0;
  
  setInterval(() => {
    this.age++;
     5000);
  }
}
     
var t = new Tree();
```

&#8593; [Back to TOC](#table-of-contents)

## Map and WeakMap

## Set and WeakSet

## Promises
