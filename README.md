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

<h2 name="Arrow-Functions">Arrow Functions</h2>

`(x, y) => {}` is a shorter form for `function (x, y) {}`. But the big difference is that the `this` in the function body is what you most likely expect it to be: that of the outer scope.

So for example, this won’t log the name:

```js
this.name = 'Jack';
…
setTimeout(function(){
  console.log(this.name);
}, 100);
```

But with the usage of the ES.next arrows, this will work:

```js
this.name = 'Jack';
…
setTimeout(() => {
  console.log(this.name);
}, 200);
```


A single expression, however, requires no braces:

```js
setTimeout(() => console.log(this.name), 300);
```

Single parameter case needs no parentheses around parameter list.

```js
let yell = x => x.toUpperCase();
yell("Avast"); // AVAST
```

### Short forms

The following functions all do the same.

```js
function(x)    { return x * x; };  // old school
        (x) => { return x * x; };  // ES6 arrow function
         x  => { return x * x; };  // skip parentheses for single args
         x  =>          x * x;     // skip {return …} for simple calls
```

### Examples

```js

var numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

var index = numbers.map((v, i) => i);  // [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
var odds = numbers.filter(v => v % 2); // [1, 3, 5, 7, 9]
var evens = odds.map(v => v + 1);      // [2, 4, 6, 8, 10]
```

Statement body needs braces, must use `return` explicitly if not void:

```js
// Statement bodies
var squares = numbers.filter(v => {
  var root = Math.sqrt(v);
  return root == Math.floor(root);
});
```

Parenthesize the body to return an object literal expression:

```js
var pairs = numbers.map((v, i) => ({value: v, index: i}));
```

([Run examples above](http://jsbin.com/povipu/edit?js,console));

<h2 name="Classes">Classes</h2>

The new `class` in ES.Next offers nice syntax sugar to get started with classes way easier.

```js
class Pirate {
  constructor(name){
    this.name = name;
    this.grogs = 0;
  }
  drink(){
    this.grogs++;
  }
  isDrunk(){
    return this.grogs > 10;
  }
}

var bill = new Pirate('Bill');
bill.isDrunk(); // returns false
```

([Run code above](http://jsbin.com/lutalabalu/edit?js,console))

### Extend classes

Classes can `extend` other classes and call their `super` functions.

```js
class Pirate {
  constructor(name){
    this.name = name;
    this.grogs = 0;
  }
  drink(){
    this.grogs++;
  }
  isDrunk(){
    return this.grogs > 10;
  }
}

class Captain extends Pirate {
  constructor(name){
    super(name);
  }
  isDrunk(){
    return this.grogs > 50;
  }
}

var bill = new Pirate('Bill'),
  jack = new Captain('Jack'),
  rounds = 20;

while (rounds--) {
  bill.drink();
  jack.drink();
}

bill.isDrunk(); // returns true
jack.isDrunk(); // returns false
```

([Run code above](http://jsbin.com/xerefo/edit?js,console))

### Getter and Setters

Also, there are getters and setters:

```js
class Treasure {
  constructor(){
    this.coins = 0;
  }
  get weight() {
    return this.coins * 50;
  }
  set weight(value) {
    if (value <= 0) {
      throw new Error('Avast: weight must be greater than 0!!')
    }
    this.coins = value / 50;
  }
}

var booty = new Treasure();
console.log(booty.coins, booty.weight); // 0, 0

booty.coins = 10;
console.log(booty.weight); // 500 gramm

booty.coins++;
console.log(booty.weight); // 550 gramm

booty.weight = 2000;
console.log(booty.coins); // 40 coins

booty.weight = -77; // throws an error
```

([Run code above](http://jsbin.com/qusafi/edit?js,console))

Classes can have static members. Like other languages with static class members, the static keyword will create a method associated with the class, and not with an instance of the class. In other words, you can only reach a static method using the name of the class. Static methods have no access to the fields, properties, and methods defined on an instance of the class using this.

### Examples

<h2 name="Enhanced-Object-Literals">Enhanced Object Literals</h2>

### Examples

<h2 name="Template-Strings">Template Strings</h2>

As there is no *sprintf* or something similar, composing strings in ES5 is a bit painful:

```js
var name = 'Jack',
  greeting = 'Ahoy ' + name + ', welcome on board';
```

In ES6, template strings got introduced which allow the usage of template variables (`${variable}`) available in the scope and support strings on multiple lines:

```js
var name = 'Jack',
  greeting = `Ahoy ${name},
    welcome on board!
  `;
```

### Examples

```js
// Basic literal string creation
`In JavaScript "\n" is a line-feed.`
```

```js
// Multiline strings
`In old school JavaScript (ES5) this
was not valid but works in ES6.
Make sure to use backticks
instead of single or double quotes.

Yarr!`
```

```js
// Interpolate variable bindings
var name = "Jack",
 drink = "grog",
 message = `${name} wants another ${drink}!`
```

```js
class Pirate {
  constructor(name){
    this.name = name;
  }
  yell(){
    console.log(`I am ${this.name}!`);
  }
}

var jack = new Pirate('Bill');
jack.yell();

```

([Run examples above](http://jsbin.com/faqeci/edit?js,console))

<h2 name="Default">Default</h2>

Often a parameter in a function has to be defined. To catch not defined parameters, a check is the first thing that happens in a function:

```js
function yell(message) {
  message = message || 'Arrr';
  console.log(message.toUpperCase() + '!');
}
yell();
```

In ES.next, it is possible, to define defaults for parameters, so that check is unnecessary:

```js
function yell(message = 'Arrr') {
  console.log(message.toUpperCase() + '!');
}

yell(); // "ARRR!"
yell('Avast'); // AVAST!
```

([Run example above](http://jsbin.com/wuvoso/edit?js,console))

<h2 name="Destructuring">Destructuring</h2>

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
var [a, , b] = [1, 2, 3];
console.log(a, b); // logs: 1, 3
```

### Examples

```js
function getData() {
  return {
    name: 'Jack',
    age: 33,
    location: {
      region: 'Bermuda',
      island: 'Isle of Devils'
    }
  }
}
var {age, name, location: { region }} = getData();
console.log(age, name, region); // logs: 33, 'Jack', 'Bermuda'
```

```js
var [a] = [];
console.log(a); // logs: undefined;

// Using a default:
var [a = 1] = [];
console.log(a); // logs: 1
```

<h2 name="Rest">Rest</h2>

### Examples

<h2 name="Spread">Spread</h2>

### Examples

<h2 name="Let-Const">Let + Const</h2>

### Examples

<h2 name="Iterators-For-Of">Iterators + For..Of</h2>

### Examples

<h2 name="Generators">Generators</h2>

### Examples

<h2 name="Comprehensions">Comprehensions</h2>

### Examples

<h2 name="Unicode">Unicode</h2>

### Examples

<h2 name="Modules">Modules</h2>

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

To just import a module, but not naming it can be done, too:

```js
import 'picturefill';
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

<h2 name="Module-Loaders">Module Loaders</h2>

### Examples

<h2 name="Map-Set-WeakMap-WeakSet">Map + Set + WeakMap + WeakSet</h2>

### Examples

<h2 name="Proxies">Proxies</h2>

### Examples

<h2 name="Symbols">Symbols</h2>

### Examples

<h2 name="Subclassable-Built-ins">Subclassable Built-ins</h2>

### Examples

<h2 name="Math-Number-String-Object-APIs">Math + Number + String + Object APIs</h2>

### Examples

<h2 name="Binary-and-Octal-Literals">Binary and Octal Literals</h2>

### Examples

<h2 name="Promises">Promises</h2>

### Examples

<h2 name="Reflect API">Reflect-API</h2>

### Examples

<h2 name="Tail Calls">Tail-Calls</h2>

### Examples
