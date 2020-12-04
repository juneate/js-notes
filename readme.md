




## Objects

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

## Document

### Selecting elements

The `document` can search for an element within its branches and will return a *reference* to the location of the element, or `null` if no match was found.

```js
// Location of the first element who matches the CSS selector
document.querySelector(`.btn`)

// Location of the first element who matches the CSS selector
document.getElementById(`#rollAgain`)
```

**TIP**: Store the reference in a variable so you can return to the element again when changes need to be made (like a map to a treasure chest).

### Element content

If you had an existing document element built with these instructions:

```html
<p class="output">Hello, <em hidden>world!</em></p>
```

For the Element defined above, here are three of its properties which all hold a different representation of its content

```js
// Locate an element, store its reference
let eleOutput = document.querySelector(`.output`)

// ACCESSING THE CURRENT CONTENT

eleOutput.textContent   // Hello, world

eleOutput.innerHTML     // Hello, <em hidden>world!</em>

eleOutput.innerText     // Hello, 

// ASSIGNING NEW CONTENT

eleOutput.textContent = 
```

**NOTE**: Using `innerText` is generally discouraged when practical, as it has a number of inconsistencies with its use, and is heavier than the other methods in terms of processing resources.
