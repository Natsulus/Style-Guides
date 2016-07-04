# Natsulus' JavaScript Style Guide

*A simplified collective of other style guides and my preferences using Airbnb's format. This is a style guide that I made for myself to follow in my personal projects and is not a "recommended" style guide like the other style guides below.*

WIP, only 5% complete.

Other Style Guides
- [Standard](https://github.com/feross/standard/blob/master/RULES.md)
- [Crockford](http://javascript.crockford.com/code.html)
- [Idiomatic.js](https://github.com/rwaldron/idiomatic.js)
- [Node.js](https://github.com/felixge/node-style-guide)
- [JS Winning Style](https://github.com/Seravo/js-winning-style)
- [Google](https://google.github.io/styleguide/javascriptguide.xml)
- [Airbnb](https://github.com/airbnb/javascript)

## Table of Contents
1. [Variables](#variables)
2. [Objects](#objects)
3. [Arrays](#arrays)
4. [Strings](#strings)
5. [Functions](#functions)
6. [Arrow Functions](#arrow-functions)
7. [Classes](#classes)
8. [Modules](#modules)
9. [Properties](#properties)
10. [Conditional](#conditional)
11. [Blocks](#blocks)
12. [Comments](#comments)
13. [Whitespace](#whitespace)
14. [Commas](#commas)
15. [Semicolons](#commas)
16. [Type Casting](#type-casting)
17. [Naming](#naming)
18. [Accessors](#accessors)
19. [Events](#events)

## Variables

  <a name="1.1"></a>
  - [1.1](#1.1) Use `const` for all references.

    *[`prefer-const`](http://eslint.org/docs/rules/prefer-const.html), [`no-const-assign`](http://eslint.org/docs/rules/no-const-assign.html)*
    ```js
    // ✗
    var a = 1;
   
    // ✓
    const a = 1;
    ```

  <a name="1.2"></a>
  - [1.2](#1.2) If a reference must be reassigned, use `let`.
    
    *[`no-var`](http://eslint.org/docs/rules/no-var.html)*
    ```js
    // ✗
    var a = 1;
    a = 5;
  
    // ✓
    let a = 1;
    a = 5;
    ```

  <a name="1.3"></a>
  - [1.3](#1.3) `let` and `const` are block-scoped.
    
    ```js
    if (true) {
    	let a = 1;
        const b = 5;
    }
    console.log(a); // ReferenceError
    console.log(b); // ReferenceError
    ```

  <a name="1.4"></a>
  - [1.4](#1.4) Use one `const` or `let` per variable.
    
    *[`one-var`](http://eslint.org/docs/rules/one-var.html)*
    ```js
    // ✗
    const five = 5,
    	fruit = 'Apple',
        ayy = 'lmao';
        
    // ✓
    const five = 5;
    const ayy = 'lmao';
    const fruit = 'Apple';
    ```

  <a name="1.5"></a>
  - [1.5](#1.5) Group all `const` then `let` with those unassigned first.
    
    ```js
    // ✗
    let no = 1;
    const five = 5;
    let fruit;
    const ayy = 'lmao';
    let time = 'tick';
        
    // ✓
    const five = 5;
    const ayy = 'lmao';
    let fruit;
    let no = 1;
    let time = 'is ticking';
    ```

  <a name="1.6"></a>
  - [1.6](#1.6) Assign variables where you need them, but place them in a reasonable place.
    
    ```js
    // ✗
    function checkName(hasName) {
    	const name = getName();
        
        if (hasName === 'test') {
        	return false;
        }
        
        if (name === 'test') {
        	this.setName('');
            return false;
        }
        
        return name;
    }
        
    // ✓
    function checkName(hasName) {
        if (hasName === 'test') {
        	return false;
        }
        
    	const name = getName();
        
        if (name === 'test') {
        	this.setName('');
            return false;
        }
        
        return name;
    }
    ```
    
## Objects

  <a name="2.1"></a>
  - [2.1](#2.1) Use the literal syntax for object creation.
    
    *[`no-new-object`](http://eslint.org/docs/rules/no-new-object.html)*
    ```js
    // ✗
    const item = new Object();
  
    // ✓
    const item = {};
    ```

  <a name="2.2"></a>
  - [2.2](#2.2) Don't use reserved words as keys.
    
    ```js
    // ✗
    const item = {
    	default: 'food',
        cost: 5
    };
  
    // ✓
    const item = {
        cost: 5,
    	defaults: 'food'
    };
    ```

  <a name="2.3"></a>
  - [2.3](#2.3) Use readable synonyms in place of reserved words.
    
    ```js
    // ✗
    const item = {
    	class: 'food'
    };
    
    // ✗
    const item = {
    	klass: 'food'
    };
  
    // ✓
    const item = {
    	type: 'food'
    };
    ```

  <a name="2.4"></a>
  - [2.4](#2.4) Use computed property names when creating objects with dynamic property names.
    
    ```js
    function getKey(k) {
    	return `the key ${k}`;
	}
    
    // ✗
    const item = {
    	type: 'food'
    };
    item[getKey('foo')] = true;
  
    // ✓
    const item = {
    	type: 'food',
        [getKey('foo')]: true
    };
    ```

  <a name="2.5"></a>
  - [2.5](#2.5) Use shorthand object methods.
    
    *[`object-shorthand`](http://eslint.org/docs/rules/object-shorthand.html)*    
    ```js
    // ✗
    const item = {
    	amount: 1,
        
        addAmount: function(value) {
        	return this.amount + value;
        }
    };
  
    // ✓
    const item = {
    	amount: 1,
        
        addAmount(value) {
        	return this.amount + value;
        }
    };
    ```

  <a name="2.6"></a>
  - [2.6](#2.6) Use shorthand property values.
    
    *[`object-shorthand`](http://eslint.org/docs/rules/object-shorthand.html)*   
    ```js
    const type = 'food';
    
    // ✗
    const item = {
    	type: type
    };
  
    // ✓
    const item = {
    	type
    };
    ```

  <a name="2.7"></a>
  - [2.7](#2.7) Group shorthand property values at the beginning of object declaration.
    
    ```js
    const type = 'food';
    const cost = 5;
    
    // ✗
    const item = {
    	amount: 10,
    	type,
        name: 'Pie',
        discount: 0.2,
        day: 'Saturday',
        cost
    };
  
    // ✓
    const item = {
    	cost,
    	type,
    	amount: 10,
        discount: 0.2,
        day: 'Saturday',
        name: 'Pie'
    };
    ```

  <a name="2.8"></a>
  - [2.8](#2.8) Only quote invalid identifiers for properties.
    
    *[`quote-props`](http://eslint.org/docs/rules/quote-props.html)*
    ```js
    // ✗
    const item = {
    	'type': 'food',
        'friday-amount': 20,
        'amount': 10
    };
  
    // ✓
    const item = {
    	amount: 10,
        'friday-amount': 20,
        type: 'food'
    };
    ```

  <a name="2.9"></a>
  - [2.9](#2.9) Do not call `Object.prototype` methods directly. (`hasOwnProperty`, `propertyIsEnumerable`, and `isPrototypeOf`)
    
    ```js
    // ✗
    console.log(object.hasOwnProperty(key));
  
    // ✓
    const has = require('has');
    console.log(has.call(object, key));
    ```
    
## Arrays

  <a name="3.1"></a>
  - [3.1](#3.1) Use the literal syntax for array creation.
    
    *[`no-array-constructor`](http://eslint.org/docs/rules/no-array-constructor.html)*
    ```js
    // ✗
    const item = new Array();
  
    // ✓
    const item = [];
    ```

  <a name="3.2"></a>
  - [3.2](#3.2) Use the literal syntax for array creation.
    
    *[`no-array-constructor`](http://eslint.org/docs/rules/no-array-constructor.html)*
    ```js
    // ✗
    const item = new Array();
  
    // ✓
    const item = [];
    ```

  <a name="3.3"></a>
  - [3.3](#3.3) Use the literal syntax for array creation.
    
    *[`no-array-constructor`](http://eslint.org/docs/rules/no-array-constructor.html)*
    ```js
    // ✗
    const item = new Array();
  
    // ✓
    const item = [];
    ```

  <a name="3.4"></a>
  - [3.4](#3.4) Use the literal syntax for array creation.
    
    *[`no-array-constructor`](http://eslint.org/docs/rules/no-array-constructor.html)*
    ```js
    // ✗
    const item = new Array();
  
    // ✓
    const item = [];
    ```

  <a name="3.5"></a>
  - [3.5](#3.5) Use return statements in array method callbacks, although it can be omitted using an implicit return.
    
    *[`array-callback-return`](http://eslint.org/docs/rules/array-callback-return.html)*
    ```js
    // ✗
    const flat = {};
    [[0, 1], [2, 3], [4, 5]].reduce((memo, item, index) => {
    	const flatten = memo.concat(item);
        flat[index] = flatten;
	});
    
    // ✓
    const flat = {};
    [[0, 1], [2, 3], [4, 5]].reduce((memo, item, index) => {
    	const flatten = memo.concat(item);
        flat[index] = flatten;
        return flatten;
	});
  
    // ✓
    [1, 2, 3].map(x => x + 1);
    ```
    
## Strings

  <a name="4.1"></a>
  - [4.1](#4.1) Use the literal syntax for object creation.
    
    *[`no-new-object`](http://eslint.org/docs/rules/no-new-object.html)*
    ```js
    // ✗
    const item = new Object();
  
    // ✓
    const item = {};
    ```
    
## Functions

  <a name="5.1"></a>
  - [5.1](#5.1) Use the literal syntax for object creation.
    
    *[`no-new-object`](http://eslint.org/docs/rules/no-new-object.html)*
    ```js
    // ✗
    const item = new Object();
  
    // ✓
    const item = {};
    ```
    
## Arrow Functions

  <a name="6.1"></a>
  - [6.1](#6.1) Use the literal syntax for object creation.
    
    *[`no-new-object`](http://eslint.org/docs/rules/no-new-object.html)*
    ```js
    // ✗
    const item = new Object();
  
    // ✓
    const item = {};
    ```
    
## Classes

  <a name="7.1"></a>
  - [7.1](#7.1) Use the literal syntax for object creation.
    
    *[`no-new-object`](http://eslint.org/docs/rules/no-new-object.html)*
    ```js
    // ✗
    const item = new Object();
  
    // ✓
    const item = {};
    ```
    
## Modules

  <a name="8.1"></a>
  - [8.1](#8.1) Use the literal syntax for object creation.
    
    *[`no-new-object`](http://eslint.org/docs/rules/no-new-object.html)*
    ```js
    // ✗
    const item = new Object();
  
    // ✓
    const item = {};
    ```
    
## Properties

  <a name="2.1"></a>
  - [9.1](#9.1) Use the literal syntax for object creation.
    
    *[`no-new-object`](http://eslint.org/docs/rules/no-new-object.html)*
    ```js
    // ✗
    const item = new Object();
  
    // ✓
    const item = {};
    ```
    
## Conditional

  <a name="10.1"></a>
  - [10.1](#10.1) Use the literal syntax for object creation.
    
    *[`no-new-object`](http://eslint.org/docs/rules/no-new-object.html)*
    ```js
    // ✗
    const item = new Object();
  
    // ✓
    const item = {};
    ```
    
## Blocks

  <a name="11.1"></a>
  - [11.1](#11.1) Use the literal syntax for object creation.
    
    *[`no-new-object`](http://eslint.org/docs/rules/no-new-object.html)*
    ```js
    // ✗
    const item = new Object();
  
    // ✓
    const item = {};
    ```
    
## Comments

  <a name="12.1"></a>
  - [12.1](#12.1) Use the literal syntax for object creation.
    
    *[`no-new-object`](http://eslint.org/docs/rules/no-new-object.html)*
    ```js
    // ✗
    const item = new Object();
  
    // ✓
    const item = {};
    ```
    
## Whitespace

  <a name="13.1"></a>
  - [13.1](#13.1) Use the literal syntax for object creation.
    
    *[`no-new-object`](http://eslint.org/docs/rules/no-new-object.html)*
    ```js
    // ✗
    const item = new Object();
  
    // ✓
    const item = {};
    ```
    
## Commas

  <a name="14.1"></a>
  - [14.1](#14.1) Use the literal syntax for object creation.
    
    *[`no-new-object`](http://eslint.org/docs/rules/no-new-object.html)*
    ```js
    // ✗
    const item = new Object();
  
    // ✓
    const item = {};
    ```
    
## Semicolons

  <a name="15.1"></a>
  - [15.1](#15.1) Use the literal syntax for object creation.
    
    *[`no-new-object`](http://eslint.org/docs/rules/no-new-object.html)*
    ```js
    // ✗
    const item = new Object();
  
    // ✓
    const item = {};
    ```
    
## Type Casting

  <a name="16.1"></a>
  - [16.1](#16.1) Use the literal syntax for object creation.
    
    *[`no-new-object`](http://eslint.org/docs/rules/no-new-object.html)*
    ```js
    // ✗
    const item = new Object();
  
    // ✓
    const item = {};
    ```
    
## Naming

  <a name="17.1"></a>
  - [17.1](#17.1) Use the literal syntax for object creation.
    
    *[`no-new-object`](http://eslint.org/docs/rules/no-new-object.html)*
    ```js
    // ✗
    const item = new Object();
  
    // ✓
    const item = {};
    ```
    
## Accessors

  <a name="18.1"></a>
  - [18.1](#18.1) Use the literal syntax for object creation.
    
    *[`no-new-object`](http://eslint.org/docs/rules/no-new-object.html)*
    ```js
    // ✗
    const item = new Object();
  
    // ✓
    const item = {};
    ```
    
## Events

  <a name="19.1"></a>
  - [19.1](#19.1) Use the literal syntax for object creation.
    
    *[`no-new-object`](http://eslint.org/docs/rules/no-new-object.html)*
    ```js
    // ✗
    const item = new Object();
  
    // ✓
    const item = {};
    ```
    
## DT-AS

  **Data Type then Alphabetical Sorting**
  
  *This is how variable names, keys and other assignments should be sorted.*
  
  First sort by
  
  - Undefined/Shorthand Assignment
  - Number
  - Boolean
  - String
  - Array
  - Object
  - Function
  - Dynamic Key
  - Class Types

  then sort each data type in alphabetical order.
    
## TO ADD IN

- Use 2 spaces for indentation
```js
function hello (name) {
  console.log('hi', name)
}
```
- No unused variables
```js
function myFunction () {
  var result = something()   // ✗ avoid
}
```
- Add a space after a keyword
```js
if (condition) {...}   // ✓ ok
if(condition) {...}    // ✗ avoid
```
- No space before function argument
```js
function name(arg) {...}   // ✓ ok
function name (arg) {...}    // ✗ avoid
```
- Always use `===` rather than `==` except where type conversion is necessary
```js
//
```