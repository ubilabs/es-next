# es-next

ES.next examples for better understanding.

- [Arrow Functions](#Arrow-Functions)
- [Classes](#Classes)
- [Enhanced Object Literals](#Enhanced-Object-Literals)
- [Template Strings](#Template-Strings)
- [Destructuring](#Destructuring)
- [Default](#Default)
- [Rest](#Rest)
- [Spread](#Spread)
- [Let + Const](#Let-Const)
- [Iterators + For..Of](#Iterators-For-Of)
- [Generators](#Generators)
- [Comprehensions](#Comprehensions)
- [Unicode](#Unicode)
- [Modules](#Modules)
- [Module Loaders](#Module-Loaders)
- [Map + Set + WeakMap + WeakSet](#Map-Set-WeakMap-WeakSet)
- [Proxies](#Proxies)
- [Symbols](#Symbols)
- [Subclassable Built-ins](#Subclassable-Built-ins)
- [Math + Number + String + Object APIs](#Math-Number-String-Object-APIs)
- [Binary and Octal Literals](#Binary-and-Octal-Literals)
- [Promises](#Promises)
- [Reflect API](#Reflect-API)
- [Tail Calls](#Tail-Calls)

## <a name="Arrow-Functions">Arrow Functions</a>

`(x, y) => {}` is a shorter form for `function (x, y) {}`. But the big difference is that the `this` in the function body is what you most likely expect it to be: that of the outer scope.

So for example, this won’t log the name:

```js
this.name = 'Peter';
…
setTimeout(function(){
  console.log(this.name);
}, 1000);
```

But with the usage of the ES.next arrows, this will work:

```js
this.name = 'Peter';
…
setTimeout(() => {
  console.log(this.name);
}, 1000);
```

### Examples

```js
var odds = evens.map(v => v + 1);
var nums = evens.map((v, i) => v + i);
```

```js
// Statement bodies
nums.forEach(v => {
  if (v % 5 === 0) {
    fives.push(v);
  }
});
```

## <a name="Classes">Classes</a>

The new `class` in ES.Next offers nice syntax sugar to get started with classes way easier:

```js
class First {
  constructor(){
    age = 42;
  }
  isItTheAnswer(){
    return this.age === '42';
  }
}
```

Classes can `extend` other classes and call their `super` functions. Also, there are getters and setters:

```js
class Second extends First {
  constructor(){
    super();
  }
  get age() {
    return this.age;
  }
  set age(value) {
    if (value < 0) {
      throw new Error('Age must be non-negative.')
    }
    this.age = value
  }
}
```

Classes can have static members. Like other languages with static class members, the static keyword will create a method associated with the class, and not with an instance of the class. In other words, you can only reach a static method using the name of the class. Static methods have no access to the fields, properties, and methods defined on an instance of the class using this.

### Examples

## <a name="Enhanced-Object-Literals">Enhanced Object Literals</a>

### Examples

## <a name="Template-Strings">Template Strings</a>

As there is no *sprintf* or something similar, composing strings in ES5 is a bit painful:

```js
var name = 'Peter Griffin',
  greeting = 'Hello ' + name + '! We welcome you to ' +
    'the next season.';
```

In ES6, template strings got introduced which allow the usage of variables available in the scope and support strings on multiple lines:

```js
var name = 'Peter Griffin',
  greeting = `
    Hello ${name}!
    We welcome you to the next season.
  `;
```

### Examples

```js
// Basic literal string creation
`In JavaScript "\n" is a line-feed.`
```

```js
// Multiline strings
`In JavaScript this is
 not legal.`
```

```js
// Interpolate variable bindings
var name = "Bob", time = "today";
`Hello ${name}, how are you ${time}?`
```

```js
// Construct an HTTP request prefix is used to interpret the replacements and construction
GET`http://foo.org/bar?a=${a}&b=${b}
    Content-Type: application/json
    X-Credentials: ${credentials}
    { "foo": ${foo},
      "bar": ${bar}}`(myOnReadyStateChangeHandler);
```

## <a name="Default">Default</a>

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

## <a name="Destructuring">Destructuring</a>

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

## <a name="Rest">Rest</a>

### Examples

## <a name="Spread">Spread</a>

### Examples

## <a name="Let-Const">Let + Const</a>

### Examples

## <a name="Iterators-For-Of">Iterators + For..Of</a>

### Examples

## <a name="Generators">Generators</a>

### Examples

## <a name="Comprehensions">Comprehensions</a>

### Examples

## <a name="Unicode">Unicode</a>

### Examples

## <a name="Modules">Modules</a>

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

## <a name="Module-Loaders">Module Loaders</a>

### Examples

## <a name="Map-Set-WeakMap-WeakSet">Map + Set + WeakMap + WeakSet</a>

### Examples

## <a name="Proxies">Proxies</a>

### Examples

## <a name="Symbols">Symbols</a>

### Examples

## <a name="Subclassable-Built-ins">Subclassable Built-ins</a>

### Examples

## <a name="Math-Number-String-Object-APIs">Math + Number + String + Object APIs</a>

### Examples

## <a name="Binary-and-Octal-Literals">Binary and Octal Literals</a>

### Examples

## <a name="Promises">Promises</a>

### Examples

## <a name="Reflect API">Reflect-API</a>

### Examples

## <a name="Tail Calls">Tail-Calls</a>

### Examples
