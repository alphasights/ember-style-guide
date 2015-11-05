# JavaScript Style Guide

This guide applies only to JavaScript files. It assumes use of Babel to compile ES\* features.

## Table Of Contents

+ [Variables](#variables)
+ [Objects](#objects)
+ [Array](#arrays)
+ [Strings](#strings)
+ [Variables](#variables)
+ [Whitespace](#whitespace)
+ [Commas](#commas)
+ [Semicolons](#semicolons)
+ [Block Statements](#block-statements)
+ [Conditional Statements](#conditional-statements)
+ [Properties](#properties)
+ [Functions](#functions)
+ [Arrow Functions](#arrow-functions)
+ [Function Arguments](#function-arguments)
+ [Rest Parameters](#rest-parameters)
+ [Destructuring](#destructuring)
+ [Comments](#comments)

## Variables

+ Use `let` instead of `var`.
+ Use `const` for variables which aren't going to change.

## Objects

+ Use literal form for object creation.

```javascript
let foo = {};
```

+ Pad single-line objects with one space.

```javascript
let bar = { color: 'orange' };
```

## Arrays

+ Use literal form for array creation (unless you know the exact length).

```javascript
let foo = [];
```

+ If you know the exact length and know that array is not going to grow, use `Array`.

```javascript
let foo = new Array(16);
```

+ Use `push` to add an item to an array.

```javascript
let foo = [];
foo.push('bar');
```

+ Follow commas with spaces, but don't pad single-line arrays.

```javascript
let foo = [1, 2, 3];
```

## Strings

+ Use `'single quotes'`.
+ Use ``backticks with ${variables}`` for string interpolation.


## Variables

+ Put all non-assigning declarations on one line.

```javascript
let a, b;
```

+ Use a single `let` declaration for each assignment.

```javascript
let a = 1;
let b = 2;
```

## Whitespace

+ Use soft tabs set to 2 spaces.

```javascript
function() {
∙∙var name;
}
```

+ Place 1 space before the leading brace.

```javascript
obj.set('foo', {
  foo: 'bar'
});

test('foo-bar', function() {
});
```

+ No spaces before semicolons.

```javascript
let foo = {};
```

+ Keep parenthesis adjacent to the function name when declared or called.

```javascript
function foo() {
}

foo();
```

+ Spaces are required around binary operators.

```javascript
// assignments
let foo = bar + 'a';

// conditionals
if (foo === 'bara') {
}

// parameters
function(test, foo) {
}
```

## Commas

+ Skip trailing commas.

```javascript
let foo = [1, 2, 3];
let bar = { a: 'a' };
```

+ Skip leading commas.

```javascript
var foo = [
  1,
  2,
  3
];
```

## Semicolons

+ Use semicolons.

## Block Statements

+ Use spaces.

```javascript
// conditional
if (notFound) {
  return 0;
} else {
  return 1;
}

switch (condition) {
  case 'yes':
    // code
    break;
}

try {
  // code that throws an error
} catch(e) {
  // code that handles an error
}
```

+ Opening curly brace should be on the same line as the beginning of a statement or declaration.

```javascript
function foo() {
  let obj = {
    val: 'test'
  };

  return {
    data: obj
  };
}

if (foo === 1) {
  foo();
}
```

+ Keep `else` and its accompanying braces on the same line.

```javascript
if (foo === 1) {
  bar = 2;
} else {
  bar = '2';
}

if (foo === 1) {
  bar = 2;
} else if (foo === 2) {
  bar = 1;
} else {
  bar = 3;
}
```

## Conditional Statements

+ Use `===` and `!==`.
+ Use curly braces.

```javascript
if (notFound) {
  return;
}
```

+ Use explicit conditions.

```javascript
if (arr.length > 0) {
  // code
}

if (foo !== '') {
  // code
}
```

## Properties

+ Use dot-notation when accessing properties.

```javascript
let foo = {
  bar: 'bar'
};

foo.bar;
```

+ Use `[]` when accessing properties with a variable.

```javascript
let propertyName = 'bar';
let foo = {
  bar: 'bar'
};

foo[propertyName];
```

## Functions

+ Make sure to name functions when you define them.

```javascript
function fooBar() {
}
```
## Arrow Functions

+ Make sure arrow functions are done on multiple lines.

```javascript
var foo = [1, 2, 3, 4].map((item) => {
  return item * 2;
});
```

## Function Arguments

`arguments` object must not be passed or leaked anywhere.
See the [reference](https://github.com/petkaantonov/bluebird/wiki/Optimization-killers#3-managing-arguments).

+ Use a `for` loop with `arguments` (instead of `slice`).

```javascript
function fooBar() {
  let args = new Array(arguments.length);

  for (let i = 0; i < args.length; ++i) {
    args[i] = arguments[i];
  }

  return args;
}
```

+ Don't re-assign the arguments.

```javascript
function fooBar() {
  arguments = 3;
}

function fooBar(opt) {
  opt = 3;
}
```

+ Use a new variable if you need to re-assign an argument.

```javascript
function fooBar(opt) {
  let options = opt;

  options = 3;
}
```

## Rest Parameters

Since [Babel implements](https://babeljs.io/repl/#?experimental=true&playground=true&evaluate=true&loose=false&spec=false&code=function%20foo\(...args\)%20%7B%0A%20%20%0A%7D) Rest parameters in a non-leaking matter you should use them whenever applicable.

```javascript
function foo(...args) {
  args.forEach((item) => {
    console.log(item);
  });
}
```

## Destructuring

When decomposing simple arrays or objects, prefer [destructuring](http://babeljs.io/docs/learn-es6/#destructuring).

```javascript
// array destructuring
let fullName = 'component:foo-bar';
let [
  first,
  last
] = fullName.split(':');
```

```javascript
// object destructuring
let person = {
  firstName: 'Stefan',
  lastName: 'Penner'
};

let {
  firstName,
  lastName
} = person;
```

## Comments

+ Use `//` for single line comments.

```javascript
function foo() {
  let bar = 5;

  // multiplies `bar` by 2.
  fooBar(bar);

  console.log(bar);
}
```
