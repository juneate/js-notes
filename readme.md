# JavaScript Notes (Term 1)

## Miscellaneous
- Single-line comments: `// comment!`
- Multi-line comments: `/* comment! */`
- Browser "console" testing messages: ``console.log(`hello world`)``

---

## Data types
In Javascript there are *eight* data types (seven "primitive" data types, plus `Object` - more on that later). The three primitive types that are most recognizable to beginners are: `Number`, `String` and `Boolean`:

```javascript
12345.67       // Number (integer, decimal, positive or negative)
`Hello world`  // String ('', "", or ``)
true           // Boolean (true or false)
```

---

## Arithmetic operators
Will perform some mathematical operation with numbers
```javascript
5 + 2        // 7
5 - 2        // 3
5 * 2        // 10
5 / 2        // 2.5
5 ** 2       // 25 (exponent)
5 % 2        // 1 (remainder, aka "modulus")
5 + 2 * 3    // 11
(5 + 2) * 3  // 21 (BEDMAS/PEDMAS!)
```

---

## Variables
Variables hold a single value. Use `var`, `let` or `const` (constant: value can not be changed) to declare a variable the first time. Use `=` ("assignment operator") to assign a value to a variable.

```javascript
let name
name = 'Ada Lovelace'
```

---

## Template strings
Wrapping a string with backtick quotes allows for an evaluation symbol `${}` to include variables or calculations in place within the string.

```js
let item = `The Big JS Book`
let qty = 3
let cost = 4.32

`Total cost for ${name}: $${qty * cost}.`
// Total cost for The Big JS Book: $12.96.
```

---

## Objects

Objects literals allow multiple values ("properties") to be stored in a single structure, wrapped in `{}`. Properties can hold any datatype (like a variable), including other objects.

```js
let person = {
  name: `Tim Berners-Lee`,
  weight: 87,
  born: {
    day: 8,
    month: `June`,
    year: 1955
  }
}

// Access property values
console.log(`${person.name} weighs ${person.weight}kg.`)

// Access properties within embedded objects
console.log(`He was born in the year ${person.born.year}.`)

// Replace property values
person.weight = 88

// Add new properties
person.career = `Inventor`
```
The variable an Object is assigned to is actually holding a _reference_ to the Object, not the Object itself.

---

## Conditions

A condition can be checked using an `if` statement. If the "condition" is `true`, the block will run, if `false` (or "falsy") it will evaluate the next condition (if one exists).

```javascript
if ( condition ) {
  // the initial condition
} else if ( condition ) {
  // (optional) condition(s) can be added after the initial "if"
} else {
  // (optional) "default" condition
}
```
### Comparison operators

*Comparison operators* are binary operators that compare their *left* and *right* value (or variable), resulting in a `Booleans` (`true` or `false`): 
- `==` (equal value), `!=` (not equal to), `<` (less than), `>` (greater than), `<=` (less than or equal to), `>=` (greater than or equal to)
- Identical (both value _and_ type): `===` (identical), `!==` (not identical)

Other condition evaluation techniques: ternary, case/switch statements

---

## Math library

A few useful `Math` methods:

```javascript
Math.random()    // a random number between 0 and 0.999 (a percentage)
Math.round(5.5)  // 6, because of standard rounding rules
Math.ceil(5.5)   // 6, ceil (ceiling) always rounds up
Math.floor(5.5)  // 5, floor always rounds down
```

---

## Document elements

Given an existing document element built with these instructions:

```html
<p id="output">Hello, <em hidden>world!</em></p>
```

### Selecting

Store the reference in a variable so you can return to the element again when changes need to be made (like a map to a treasure chest). All these methods return a reference to the first matching Element found, or `null` if a match is not found:

```js
let ele

ele = document.querySelector(`#output`) // css selector
ele = document.getElementById(`output`) // any element id
```

### Content

For the Element defined above, here are three of its properties which all hold a different representation of its content:

```js
ele.textContent   // Hello, world
ele.innerHTML     // Hello, <em hidden>world!</em>
ele.innerText     // Hello, 
```

Assigning new content to an element:

```js
ele.textContent = `Goodbye, world`
// does not convert the HTML tags to an element, will display as assigned
ele.textContent = `<em>Goodbye</em>, world` 

// will convert the HTML tags to an emphesis element
ele.innerHTML = `<em>Goodbye</em>, world`
```

**NOTE**: Using `innerText` is generally discouraged when practical, as it has a number of inconsistencies with its use, and is heavier than the other methods in terms of processing resources.

### Styling

```js
// Modify a single CSS property, like "color" and "text-align"
ele.style.color = `tomato`     // color: tomato
ele.style.textAlign = `right`  // text-align: right

// The same can be done to maintain CSS property formatting
ele.style.setProperty(`color`, `tomato`)
ele.style.setProperty(`text-align`, `right`)

// Assign classes to an element (will overwrite existing classes)
ele.className = `item shown`   // class="item shown"

// Affect the classes applied to an element
ele.classList.add(`highlight`)
ele.classList.remove(`highlight`)
ele.classList.toggle(`highlight`)
```

### Attributes

```js
ele.setAttribute(`title`, `Hello world`)  // title="Hello world"
ele.getAttribute(`title`)                 // Hello world
```

### Event listeners

```javascript
let handleClick = function(event) { 
   // An object holding information about the event
   console.log(event)
}

ele.addEventListener('click', handleClick)
```

Three pieces of information is required:
- The element waiting for an Event (`ele`)
- The type of event expected (`` `click` ``)
- The function that handles it (`handleClick`)

A list of [some comment Event types can be found here](https://developer.mozilla.org/en-US/docs/Web/Events).
