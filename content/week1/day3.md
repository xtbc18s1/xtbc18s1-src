---
title: "Day 3: Arrays and Objects"
weight: 3
---

<date>Wednesday, May 16, 2018</date>

## Lecture Videos

Morning:

* [Playlist](https://www.youtube.com/watch?v=vGMMHQfp8Vk&list=PLuT2TqJuwaY_Hj168ujFhP0w5HzmaDLfG) | [Day 3, Part 1](https://www.youtube.com/watch?v=mOC3SwLgYTo&index=25&list=PLuT2TqJuwaY_Hj168ujFhP0w5HzmaDLfG)

Afternoon:

* [Playlist](https://www.youtube.com/watch?v=uX8_DUKyTx0&list=PLuT2TqJuwaY_XxGei4xUXZn9HuTU3jBRk) | [Day 3, Part 1](https://www.youtube.com/watch?v=Y1uDUTL9BJU&list=PLuT2TqJuwaY_XxGei4xUXZn9HuTU3jBRk&index=27)
 
## Topics

### Arrays
* `Array.map` - [Docs on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map?v=control)
* [Understanding JavaScript's `map()`](https://www.discovermeteor.com/blog/understanding-javascript-map/) blog post

### Objects
* Object literals
* Property Naming
* Retrieving property values
* Setting property values

[Arrays and Objects CodePen Example](https://codepen.io/dstrus/pen/aGRLBo?editors=0012)

### Handling exceptions

* `try`
* `catch`
* `finally`

### Styling

#### Flexbox
* [A Complete Guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
* [Flexbox.io](https://flexbox.io/)

#### Fonts
* [Google Fonts](https://fonts.google.com/)

#### Tips and Tricks on CSS
* [CSS Tricks](https://css-tricks.com/)

## Examples

### Arrays
Arrays are extremely useful data structures in JavaScript, as they can be easily iterated and transformed through methods like `map`, `filter`, and `reduce`.  Sometimes, you may have an 'array-like' collection (like a `NodeList` or function arguments) that you would need to convert to an actual Array before you could use these methods.  This can be done using `Array.from`

{{< code js >}}
let paragraphs = document.querySelectorAll('p')
paragraphs.map((p) => {
  p.textContent = "This won't work because paragraphs is a NodeList, not Array!"
})
// => Uncaught TypeError: paragraphs.map is not a function

let actualArrayOfParagraphs = Array.from(paragraphs)
actualArrayOfParagraphs.map((p) => {
  p.textContent = "This totally does work because we created an Array from our NodeList!"
})
{{< /code >}}

{{% aside info "Requirements for 'Array.from'" %}}
What objects can you convert to an Array using 'Array.from'?  

* Any array-like object with a 'length' property and indexed elements
* Iterable objects (like Map or Set)

For more info, check out [this article](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/from?v=control) on MDN.
{{% /aside %}}

### Objects
Almost everything in JavaScript is an Object.  The easiest way to create new Objects is with the [object initializer](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Object_initializer), more commonly known as 'object literal' syntax.  Basically, use curly braces to make an object `{}` and fill in the properties that you want.

Objects contain `key`/`value` pairs that allow you to set and retrieve values from them.

{{< code js >}}
// create a new object and assign some properties
const myObject = {
  prop1: 'Hello there',
  prop2: 42
}

// access the values in several ways, usually 'dot' or 'square bracket' notation
myObject.prop1 // => 'Hello there'
myObject['prop1'] //=> 'Hello there'

// new key/value pairs can also be assigned with these notations
myObject.prop3 = 'New Value!'
myObject['prop4'] = 'Newest Value!'

console.log(myObject)
// { 
//   prop1: 'Hello there',
//   prop2: 42,
//   prop3: 'New Value!',
//   prop4: 'Newest Value!'
// }
{{< /code >}}

We know that we can iterate through an Array using `map` or `forEach`.  Can we do something similar with objects?  There are a few ways to do it, but one of the newest and easiest is the `Object.keys` method.  It iterates through the enumerable properties of an object, returning an array of the property keys. Once we have an array of keys, we can `map` over _that_ and access each of the object properties individually.

{{< code js >}}
const myObj = {
  a: 'hi',
  b: 42,
  c: [1, 2, 3]
}

const myObjKeys = Object.keys(myObj)    // ['a', 'b', 'c']

myObjKeys.map(key => myObj[key])        // ['hi', 42, [1, 2, 3]]
{{< /code >}}

### Handling exceptions
In JavaScript (as in many languages), there is a way to 'try' a block of code that may produce an exception, and if it _does_ produce an exception, 'catch' it and execute a different block of code.  The catch block receives the exception as an argument.  There is also an optional 'finally' block, which will _always_ run, regardless of whether there was an exception.

{{< code js >}}
try {
  // try running this code first
  somethingThatMightBlowUp()
} catch (e) {
  // executes if the 'try' block produced an exception
  logMyErrors(e)
} finally {
  // always executes after the previous blocks have run
  console.log("Done!  Maybe there was an exception, maybe there wasn't.")
}
{{< /code >}}

For more info, read [this MDN article](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/try...catch).

## Projects

### User Directory
[Final Version](https://github.com/xtbc18s1/user-directory)

## Homework

Create a brand-new app to create a list of something. For example: Tatum Tots, our favorite Channing Tatum movies.

You should be able to type an item into a form and have it added to a list (a `ul`).

### Bonus Credit

In addition to building a list item and adding it to the DOM, also store each item in an array.

### Super Mega Bonus Credit

Add a _delete_ button to each list item that removes it from the list.

### Super Mega Bonus Credit Hyper Fighting

Remove the item from the array as well.
