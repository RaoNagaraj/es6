# ES6
A list of ES6 / Harmony / ES2015 features, tips, tools and resources — standardization and implementation might take a while to reach the point where ECMAScript6 is widely adopted by developers, but it's **wise to adopt today what we'll see tomorrow**.

## Table of Contents
* [ECMA History](#history)
* [Introduction](#es6-introduction)
* [Tools](#tools)
* [Block Scoping](#block-scoping)
* [Let and Const](let-and-const)
* [Parameter Handling](#parameter-handling)
* [Destructuring Assignment](#destructuring-assignment)
* [Classes](#classes)
* [Modules](#modules)
* [Template Literals](#template-literals)
* [Generators](#generators)
* [Arrow Functions](#arrow-functions)
* [Map](#map)
* [Promises](#promises)

## History
* ECMAScript is now 17 years old with it's birth in 1997 
  * ECMAScript is the standard. `JavaScript`, `ActionScript` and `JScript` are implementations of it.
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

## ES6 Introduction
`ES6` is the newest addition to the language and adds **significant** new syntax for writing complex JavaScript applications.
 * There is 5 years between `ES5` and `ES6`.  
 * 'ES6' is the first **ECMAScript Harmony** specification and is also known as `ES Harmony`, `ES2015`, `ES.next` but commonly referred to as `ES6`.
* The specification was finalized in `June 2015`as it reached `feature complete` status
  * Subsequent versions will be released on a 12 month cadence, and will be dubbed `ES7`, `ES2016` respectively.

## Tools
You should want to experiment and play around with code — it's easy to get up and running. There are several techniques and the premise all these tools are built upon is called `transpiling`, or **JavaScript to JavaScript** transpiling which compiles the latest version into older versions.
* Transpilation is the future for future ECMAScript such as `ES2015` and `ES2016`
* The most popular JavaScript transpilers are `Babel` and was previously known as `6to5`
* Transpilation is possible to incorporate into your build process using [Broccoli](), [Gulp](), [Browserify](), [RequireJS](), [Webpack]() et al and friends.

_The easiest way to get up and running in the web browser:_

* In the web browser you can use the online `Babel REPL` — this compiles `ES6` to `ES5` and you don't have to install anything.
* Another web based tool is `Scratch JS` and comes in the form of a chrome extension. This interactive playground let's you transpile your code in the all familiar `dev tools` environment.

_If you prefer the command line:_
a
* Use Node,js v4.x.x or `>`, they support is in-built for Babel
* Run `npm install -g babel' and `babel node`

_Using an IDE_

* You can easily use `Babel` to transpile your code in **Webstorm**, the setup won't take more than a couple of moments.

_Node has decent built in support for `ES6` thanks for the `V8` engine:_

* Node suports `ES6` features split into three groups
 * Shipping: which do not require a **runtime flag**
 * Staged: almost-complete features that are not considered stable
 * In progress: features can be individually activated by their respective harmony flag `--harmony_destrucuting`
 
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

> How `let` works: 
 
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
> Using block scoped `let`:

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

> More scoping rules for variables declared by `let` — you can clearly see that when refactoring legacy code you have to be careful:

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

> Unlike `let` variables **declared** with `const` are immutable.

``` javascript
// simply just creates an immutable binding
const foo = '123';
foo = '321';
console.log( foo ); // TypeError
```

> Take into consideration that `const` creates an **immutable binding**, you can still change it's value. If you truly want the value to be **immutable** use `object.freeze`.

``` Javascript
const myarr = [1,2,3,4];
myarr.push(5);
console.log( myarr ); // => 1, 2, 3, 4, 5

const obj = {};
obj.prop = 123;
console.log( obj ); // => { Object: prop: 123 }
obj = {}; // => TypeError

// using object freeze to create `immutable value`
const bar = Object.freeze({
  'baz': 27
});
bar.baz = 42; // TypeError
console.log(foo.bar); // => 27
```

_Basic rules to follow_: 
 * don't use `var`, or leave it as a signal in untouched legacy code.
 * use `let` when you want to rebind.
 * prefer `const` for variables that never change.
 * don't blindly refactor legacy code when replacing `var` with `let` and `const`.

## Parameter Handling

## Destructuring Assignment

## Classes

## Modules

## Template Literals

## Generators

## Arrow Functions

## Map

## Promises
