---
title: "Day 2: Functions and The DOM"
weight: 2
---

<date>Tuesday, May 15, 2018</date>

## Lecture Videos

Morning:

* [Playlist](https://www.youtube.com/watch?v=vGMMHQfp8Vk&list=PLuT2TqJuwaY_Hj168ujFhP0w5HzmaDLfG) | [Day 2, part 1](https://www.youtube.com/watch?v=KGsggCwZA0Y&index=6&list=PLuT2TqJuwaY_Hj168ujFhP0w5HzmaDLfG)

Afternoon:

* [Playlist](https://www.youtube.com/watch?v=uX8_DUKyTx0&list=PLuT2TqJuwaY_XxGei4xUXZn9HuTU3jBRk) | [Day 2, part 1]()

## Topics

### Functions
* Function Expressions
* Function Declarations
* Function Hoisting ([MDN](https://developer.mozilla.org/en-US/docs/Glossary/Hoisting))

### Git

* [Git Guide](http://rogerdudler.github.io/git-guide/)
* [Git Basics](https://git-scm.com/book/en/v2/Getting-Started-Git-Basics)
* [Understanding Git (part 1): Explain It Like I'm Five] (https://hackernoon.com/understanding-git-fcffd87c15a3)

<div class="img github-flow"></div>

### DOM
* Adding HTML content to an existing element with `someElement.innerHTML`
* Creating elements with `document.createElement`
* Setting style properties with `someElement.style.stylePropertyName`
* Appending child elements with `someElement.appendChild`
* [REM vs EM - The Great Debate](https://zellwk.com/blog/rem-vs-em/)

## Examples

### Functions
{{< code js >}}
  // function declaration - use 'function' keyword
  function aMostExcellentFunction() {
    console.log('This function is great!')
  }

  aMostExcellentFunction() // => 'This function is great!'

  // function expression - defines a function as part of a larger expression syntax
  // (usually assignment to a variable)
  const anotherExcellentFunction = () => {
    console.log('This function is also great!')
  }

  anotherExcellentFunction() // => 'This function is also great!'
{{< /code >}}


### DOM
If we start with the following markup:
{{< code html >}}
&lt;div id=&quot;my-div&quot;&gt;&lt;/div&gt;
{{< /code >}}
We can add additional markup to it programmatically using JavaScript.  One way is to create new HTMl elements using `document.createElement`, and adding them by using `appendChild`.  Styling of the element can even be changed by manipulating the element's `style` property.

{{< code js >}}
// create an h1 and modify text content and color
const heading = document.createElement('h1')
heading.textContent = "This is the best heading I've ever seen"
heading.style.color = "red"

// get a reference to the existing div and add the heading as a child element
const div = document.querySelector('#my-div')
div.appendChild(heading)
{{< /code >}}

This will produce the following markup:
{{< code html >}}
&lt;div id=&quot;my-div&quot;&gt;
  &lt;h1 style=&quot;color: red;&quot;&gt;This is the best heading I've ever seen&lt;/h1&gt;
&lt;/div&gt;
{{< /code >}}

## Presentations

* <a target="_blank" href="/day02.pdf">Review: HTML and the DOM</a>

## Projects

### User Directory

[Morning](https://github.com/xtbc18s1/user-directory/tree/master) | [Afternoon](https://github.com/xtbc18s1/user-directory/tree/afternoon)

## Homework

* Create a new function called `renderColor` that returns a `div` element.
* Call that function when adding that `div` to `colorItem`.

### Bonus Credit

* Create a new function called `renderListItem`.
* Use it to create list items for each stat.

### Super Mega Bonus Credit

* Create a new function called `renderList`.
* Use it to create the list for each person's stats.
* Call `renderListItem` from `renderList`, not directly from `handleSubmit`.

### Super Mega Bonus Credit Hyper Fighting

* Be Strong!  Do not resort to the use of `innerHTML`.  Keep using `document.createElement`.
