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

## Destructuring

### Examples

## Default

### Examples

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
