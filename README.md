# es-next

ES.next examples for better understanding.

## Arrow functions

### Examples

## Classes

### Examples

## Enhanced Object Literals

### Examples

## Template Strings

### Examples

## Default

Often a parameter in a function has to be defined. To catch not defined parameters, a check is the first thing that happens in a function: 

```js
function ajax(url) {
  url = url || 'http://duckduckgo.com';
}
ajax();
```

In ES.next, it is possible, to define defaults for parameters, so that check is unnecessary:

```js
function ajax(url = 'http://duckduckgo.com') {
  console.log(url); // logs: 'http://duckduckgo.com'
}
ajax();
```

### Examples

```js
function add(x, y = 12) {
  return x + y;
}
console.log(add(3)); // logs: 15
```

## Destructuring

When passing a lot of data to a function it is often done via an `options` object:

```js
ajax(‘/todo’, {
  method: ‘POST’,
  body: 'Some content')
});
```
Then, to acces these params in ES5, one would assign them manually:

```js
function ajax(url, options) {
  options = options || {};

  var body = options.body || '',
    method = options.method || 'GET';
}
```
In ES.next, we can define these directly:

```js
function ajax(url, {body='', method='GET'}) {
  console.log(method);
}
```

This can also be used in assignments:

```js
var [a, , b] = [1,2,3];
console.log(a, b); // logs: 1, 3
```

### Examples

```js
function getData() {
  return {
    name: 'Peter',
    age: 34,
    location: {
      city: 'Hamburg',
      country: 'Germany'
    }
  }
}
var {age, name, location: { city }} = getData();
console.log(age, name, city); // logs: 34, 'Peter', 'Hamburg'
```

```js
var [a] = [];
console.log(a); // logs: undefined;

// Using a default:
var [a = 1] = [];
console.log(a); // logs: 1
```

## Rest

### Examples

## Spread

### Examples

## Let + Const

### Examples

## Iterators + For..Of

### Examples

## Generators

### Examples

## Comprehensions

### Examples

## Unicode

### Examples

## Modules

ES.next introduces module support to prevent filling up the global scope. The syntax is a bit different than the NPM module syntax.

When exporting a `default`, it can be imported via giving some name on import:

```js
// header.js
export default function header(){}

// app.js
import header from ‘header’;
```

But when importing named exports, they have to defined via `{ }`:

```js
// header.js
export function header(){}

// app.js
import { header } from ‘header’;
```

### Examples

```js
// lib/math.js
export var pi = 3.141593;

// lib/mathplusplus.js
export * from "lib/math";
export var e = 2.71828182846;
export default function(x) {
    return Math.exp(x);
}

// app.js
import exp, {pi, e} from "lib/mathplusplus";
alert("2π = " + exp(pi, e));
```

## Module Loaders

### Examples

## Map + Set + WeakMap + WeakSet

### Examples

## Proxies

### Examples

## Symbols

### Examples

## Subclassable Built-ins

### Examples

## Math + Number + String + Object APIs

### Examples

## Binary and Octal Literals

### Examples

## Promises

### Examples

## Reflect API

### Examples

## Tail Calls

### Examples
