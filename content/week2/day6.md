---
title: "Day 6: React"
weight: 2
---

<date>Tuesday, May 22, 2018</date>

## Recap

* Reactrobats (take two): [Morning](https://codepen.io/dstrus/professor/gzEZKd/)

## Lecture Videos

Morning:

* [Playlist](https://www.youtube.com/watch?v=vGMMHQfp8Vk&list=PLuT2TqJuwaY_Hj168ujFhP0w5HzmaDLfG) | [Day 6, Part 1](https://www.youtube.com/watch?v=iwe0wOMVfwc&index=64&list=PLuT2TqJuwaY_Hj168ujFhP0w5HzmaDLfG)

Afternoon:

* [Playlist](https://www.youtube.com/watch?v=uX8_DUKyTx0&list=PLuT2TqJuwaY_XxGei4xUXZn9HuTU3jBRk) | [Day 6, Part 1](https://www.youtube.com/watch?v=p_CZgN4DWSE&list=PLuT2TqJuwaY_XxGei4xUXZn9HuTU3jBRk&index=66)

## Topics

### Scope
* Variable Scope (`var`, `const`, `let`)

### React

* Using `map` with components
* Stateless Functional Components
  * [Functional Stateless Components in React](http://javascriptplayground.com/blog/2017/03/functional-stateless-components-react/)
  * [Functional Components vs. Stateless Functional Components vs. Stateless Components](https://tylermcginnis.com/functional-components-vs-stateless-functional-components-vs-stateless-components/)
  * [Nine Wins You Might Have Overlooked](https://hackernoon.com/react-stateless-functional-components-nine-wins-you-might-have-overlooked-997b0d933dbc)
* [CSS in JS](https://hackernoon.com/all-you-need-to-know-about-css-in-js-984a72d48ebc)

## Examples

### Variable Scope
The biggest difference between `var` and `let` is that `var` variables are scoped to the _function_ in which they are declared, while `let` variables are scoped to the _block_ in which they are declared.  One of the easiest examples to see this behavior is in a simple `for` loop.

{{< code js >}}
function loopStuff() {
  for (var i = 0; i < 5; i++) {
    // do stuff in the loop
  }
  console.log(i)
}

loopStuff() // => 5

function loopMoreStuff() {
  for (let i = 0; i < 5; i++) {
    // do stuff in the loop
  }
  console.log(i)
}

loopMoreStuff() // => Uncaught ReferenceError: i is not defined
{{< /code >}}

In the function `loopStuff`, `var i` is still available outside the `for` loop so it can be logged to the console.  It is scoped to the function itself.

In the function `loopMoreStuff`, `let i` is not available outside the block it is scoped to (the `for` loop).

The main difference between `const` and `var`/`let` is that `const` cannot be reassigned.
{{< code js >}}
let variableOne = 4
variableOne = 5

var variableTwo = 4
variableTwo = 5

const variableThree = 4
variableThree = 5 // => Uncaught TypeError: Assignment to constant variable
{{< /code >}}

{{% aside tip "Default to using const" %}}
Always use `const` as your default way to declare variables, unless you know specifically that you will need to reassign it, in which case use `let`.  You should rarely, if ever, use `var`.  For further reading, check out [this article](https://medium.com/javascript-scene/javascript-es6-var-let-or-const-ba58b8dcde75).
{{% /aside %}}

### [React](https://facebook.github.io/react/)

#### Using `map` with Components

**Person.js**

{{< code jsx >}}
class Person extends React.Component {
  render() {
    return (
      &lt;li&gt;Hello, {this.props.person.name}!&lt;/li&gt;
    )
  }
}

export default Person
{{< /code >}}

**PersonList.js**

{{< code jsx >}}
import Person from './Person'

class PersonList extends React.Component {
  render() {
    const people = [
      { name: 'Dana', hair: 'blonde' },
      { name: 'Nichole', hair: 'long' },
      { name: 'Davey', hair: 'long gone' }
    ]
    return (
      &lt;div&gt;
        &lt;h2&gt;People&lt;/h2&gt;
        {
          people.map((person => &lt;Person person={person} /&gt;))
        }
      &lt;/div&gt;
    )
  }
}

export default PersonList
{{< /code >}}

#### Stateless Functional Components

Not every React Component needs to have state.  Many simply render a bit of `props` and UI.  For such components, we don't need to instantiate a whole class that inherits from `React.Component`, we can simply write a function that accepts `props` as an argument and returns the markup we need.

For instance, in the previous example, the `Person` component can easily be re-written as a Stateless Functional Component.

{{< code jsx >}}
function Person (props) {
  return (
    &lt;li&gt;Hello, {props.person.name}!&lt;/li&gt;
  )
}

// Or...

const Person = (props) => &lt;li&gt;Hello, {props.person.name}!&lt;/li&gt;
{{< /code >}}

### JavaScript (ES6+)

#### Named and default exports and imports

Prior to ES6, there were many competing ways to export and import JavaScript modules.  The most common were [CommonJS](https://webpack.github.io/docs/commonjs.html) and [AMD](http://requirejs.org/docs/whyamd.html).  Luckily ES6 defined a specification for standardizing module export and import.

There are two types of exports from any JS file - *named* and *default*.  The important thing to remember is that there can only be *one* default export per module, but there can be as many named exports as you want.

**myModule.js**
{{< code js >}}
export const myNumber = 8

export function sayHi () {
  console.log('hello')
}

export default class MyClass {
  add (a, b) {
    return a + b
  }
}
{{< /code >}}

The main difference is how they are imported.  Default exports get the most concise syntax:

{{< code js >}}
import MyClass from 'myModule'

const classInstance = new MyClass()
classInstance.add(1, 2) // => 3
{{< /code >}}

{{% aside info "Default import naming" %}}
Since there can be only one default export per module, the name by which you import the default export is not important - you can name it whatever you want.  For instance, instead of importing as `MyClass`, we could have said `import LuftBallons from 'myModule'`, and it would have worked just fine.  To read more about default and named exports, click [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/export).
{{% /aside %}}

Named exports get a slightly more verbose syntax for importing, and the names _are_ important (otherwise it can't determine what you want to import).

{{< code js >}}
import { myNumber, sayHi } from 'myModule'

console.log(myNumber) // => 8

sayHi() // => 'hello'
{{< /code >}}

If you need to import a named export under a different name&mdash;if, for example, you have another import or local variable with the same name&mdash;you can specifiy a different name using _as_.

{{< code js >}}
import { myNumber as num, sayHi as yo } from 'myModule'

console.log(num) // => 8

yo() // => 'hello'
{{< /code >}}

You can also combine default and named imports in the same line.

{{< code js >}}
import MyClass, { myNumber, sayHi } from 'myModule'
{{< /code >}}

## Projects

* [Static Noteherder] (https://github.com/xtbc18s1/static-noteherder)
* Noteherder: [Morning](https://github.com/xtbc18s1/noteherder) | [Afternoon](https://github.com/xtbc18s1/noteherder/tree/afternoon)

## Homework

* Finish styling `Sidebar`.
* Add JSX and style to `NoteList` and `NoteForm`.

### Bonus Credit

* Store a list of hard-coded notes in `state`.
* Use `map` to list these notes in `NoteList`.

### Super Mega Bonus Credit

Load a note into `NoteForm` when you click it in `NoteList`.
