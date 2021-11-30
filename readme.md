# Introductory JavaScript Notes

## Miscellaneous

### Comments
- Single-line comments: `// comment!`
- Multi-line comments: `/* comment! */`
- Browser "console" testing messages: ``console.log(`hello world`)``

### Casing
- Kebob casing: `naming-things-is-tricky`  (preferred by CSS and the file system)
- Snake casing: `naming_things_is_tricky`
- Camel casing: `namingThingsIsTricky` (preferred by JavaScript)

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

// (BEDMAS/PEDMAS!)
5 + 2 * 3    // 11
(5 + 2) * 3  // 21
```

---

## Variables

Variables hold a single value. Use `var`, `let` or `const` (constant: value can not be changed) to declare a variable the first time. Use `=` ("assignment operator") to assign a value to a variable.

```javascript
let name
name = `Ada Lovelace`
```

---

## Template strings

Wrapping a string with backtick quotes allows for an evaluation (interpolator) symbol `${}` to include variables or calculations in place within the string.

```js
let item = `The Big JS Book`
let qty = 3
let cost = 4.32

`Total cost for ${name}: $${qty * cost}.`
// Total cost for The Big JS Book: $12.96.
```

---

## Functions

Named blocks of code that can be called upon to run at any time through the life of the application. Each invocation of a function has its own variable scope that is flushed from memory when the invocation is complete. 

Functions can receive instructions ("arguments") in the form of values or variables when invoked, storing them in the function scope as variables ("parameters"). Functions can `return` a resulting value back to where it was called (acting in a way that makes it similar to a variable, holding a dynamic value).

```js
let multiply = function(a, b) {
  return a * b
}

// Invoke the function
multiply(3, 5)  // 15
multiply(2, 6)  // 12
```

Two other ways to write the function above (still invoking the same way, both still creating a variable with the function name within the current scope):

```js
function multiply(a, b) {
  return a * b
}
```

```js
let multiply = (a, b) => {
  return a * b
}
```

Note: The latter form can also be written as `(a, b) => a * b` (omitting `return` and the `{` `}`) when it only returns a single value. Note, if the function only receives a single argument, it may optionally omit the `(` `)` around the parameter list.

---

## Objects

Objects literals allow multiple named values ("properties") for a single entity, to be stored in a `{}` wrapped structure. An object's properties can hold any datatype a variable can store, including functions, and other objects.

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
The variable or property that an Object is assigned to is actually holding a _reference_ to the Object, not the Object itself.

---

## Array

Arrays allow multiple values of the same structure or type to be stored in a single structure, wrapped with `[]`. Array values are stored at numerical indices, counting up from index `0`. The number of values in an Array is stored in its `length` property.

```js
// Array of Strings
let names = [
  `Tim Berners-Lee`, `Ada Lovelace`, `Grace Hopper`
]
console.log(names.length)  // 3
console.log(names[0])      // Tim Berners-Lee
```

```js
// Array of Objects, behaves like a table
let students = [
  {name: `Tim Berners-Lee`, grade: 80},
  {name: `Ada Lovelace`, grade: 83},
  {name: `Grace Hopper`, grade: 72},
]
console.table(students) // Logs a table of 2 columns, 3 rows
```

Like Object literals, assigning an Array to a variable or Object property stores its reference, not a copy of the Array.

An Array has many useful built-in methods to use or manipulate its values. Generally speaking, accessing Array values individually is discouraged (use an Object for that purpose). Arrays are usually iterated over, either in part or in full.

```js
// Add or remove values

names.push(`Alan Turing`) // Add to the end
names.pop() // Remove from the end, returns: Alan Turing
names.unshift(`Alan Turing`) // Add to the start
names.shift() // Removes from the start, returns: Alan Turing
```

```js
// Iterate over each value

let printName = function(name) {
  console.log(`I 💗 ${name}.`)
}

// For each value, call a function, passing the value to its first parameter
names.forEach(printName)

// Result:
// I 💗 Tim Berners-Lee
// I 💗 Ada Lovelace
// I 💗 Grace Hopper
```

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

Other condition evaluation techniques: ternary, case/switch statements

### Comparison operators

*Comparison operators* are binary operators that compare their *left* and *right* value (or variable), resulting in a `Booleans` (`true` or `false`): 
- `<` (less than), `>` (greater than), `<=` (less than or equal to), `>=` (greater than or equal to)
- Equivalency (values mean the same thing): `==` (equal), `!=` (not equal), 
- Identical (both value _and_ type): `===` (identical), `!==` (not identical)

---

## Math library

A few useful `Math` methods to assist with transforming numbers:

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

#### CSS Properties

```js
// Modify a single CSS property, like "color" and "text-align"
ele.style.color = `tomato`     // color: tomato
ele.style.textAlign = `right`  // text-align: right

// The same can be done to maintain CSS property formatting
ele.style.setProperty(`color`, `tomato`)
ele.style.setProperty(`text-align`, `right`)
```

These properties are all applied to the element's `style` object, which represents styling applied by the HTML `style=""` attribute, thus taking top priority in the cascade. The `style` object only holds values applied this way (or via the HTML `style` attribute), therefor CSS property values cannot be determined using this format (see the the [MDN definition for `window.getComputedStyle()`](https://developer.mozilla.org/en-US/docs/Web/API/Window/getComputedStyle) to learn more).

#### CSS Classes

```js
// Assign classes to an element (will overwrite existing classes)
ele.className = `item shown`   // class="item shown"

// Affect the classes applied to an element
ele.classList.add(`highlight`)
ele.classList.remove(`highlight`)
ele.classList.toggle(`highlight`)
```

### Attributes

```js
// Set and get attribute values
ele.setAttribute(`title`, `Hello world`)  // title="Hello world"
ele.getAttribute(`title`)                 // Hello world
```

### Event listeners

Three pieces of information are required to listen for an Event:
- The element waiting for an Event (`ele`)
- The type of event expected (`` `click` ``)
- The function that handles it (`handleClick`)

```javascript
// Handler function
let handleClick = function(event) { 
   // An object holding information about the event
   console.log(event)
}

// When `ele` is clicked, call the handleClick function
ele.addEventListener(`click`, handleClick)
```

Note the `addEventListener` method is passed a reference to the function, but does not invoke the function using `()`. Consider you are _training_ the element to perform the action **only** when the Event occurs, but not invoking the function at this point.

MDN has published a list of [common Event types](https://developer.mozilla.org/en-US/docs/Web/Events).
