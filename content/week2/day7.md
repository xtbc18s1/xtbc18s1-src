---
title: "Day 7: Props and Restructuring"
weight: 3
---

<date>Wednesday, May 23, 2018</date>

## Lecture Videos

Morning:

* [Playlist](https://www.youtube.com/watch?v=vGMMHQfp8Vk&list=PLuT2TqJuwaY_Hj168ujFhP0w5HzmaDLfG) | [Day 7, Part 1](https://www.youtube.com/watch?v=emiWhMcrhkc&list=PLuT2TqJuwaY_Hj168ujFhP0w5HzmaDLfG&index=77)

Afternoon:

* [Playlist](https://www.youtube.com/watch?v=uX8_DUKyTx0&list=PLuT2TqJuwaY_XxGei4xUXZn9HuTU3jBRk) | [Day 7, Part 1](https://www.youtube.com/watch?v=KLCIn7x5_3Y&index=79&list=PLuT2TqJuwaY_XxGei4xUXZn9HuTU3jBRk)

## Topics

### CSS-in-JS

* [Aphrodite](https://github.com/Khan/aphrodite): Support for colocating your styles with your JavaScript component.

### React

* Methods as props
* [Controlled](https://facebook.github.io/react/docs/forms.html) vs [Uncontrolled](https://facebook.github.io/react/docs/uncontrolled-components.html) Forms
* [Controlled and uncontrolled form inputs in React don't have to be complicated](https://goshakkk.name/controlled-vs-uncontrolled-inputs-react/)

### JavaScript

* [Destructuring assignment](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)
* [Spread operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)
* Property initializers (and arrow functions)

## Examples

### [React](https://facebook.github.io/react/)

#### Methods as props

Sometimes one component needs to update another component's state. It can't do that directly, but it can call a method from that other component if it's available via a prop.

{{< code lang="jsx" line="5,23" class="line-numbers" >}}
import React from 'react'
import ReactDOM from 'react-dom'

const PartyButton = ({ celebrate, celebrations }) =&gt; {
  return &lt;button onClick={celebrate}&gt;Party! {celebrations}&lt;/button&gt;
}

class App extends React.Component {
  constructor() {
    super()
    this.state = {
      celebrations: 0,
    }
    this.celebrate = this.celebrate.bind(this)
  }

  celebrate() {
    const celebrations = this.state.celebrations + 1
    this.setState({ celebrations })
  }

  render() {
    return &lt;PartyButton celebrate={this.celebrate} celebrations={this.state.celebrations} /&gt;
  }
}

ReactDOM.render(&lt;App /&gt;, document.querySelector('main'))
{{< /code >}}

### JavaScript (ES6+)

#### Destructuring assignment

[Destructuring assignment](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment) syntax is a JavaScript expression that makes it possible to unpack values from arrays, or properties from objects, into distinct variables.

{{< code js >}}
const myObj = {
  a: true,
  b: 'Destructuring!'
}

let { a, b } = myObj

console.log(a) // => true
console.log(b) // => 'Destructuring!'
{{< /code >}}

#### Property initializers

{{% aside info "Subject to minor changes" %}}
[Property initializers](https://github.com/tc39/proposal-class-public-fields) are a [Stage 3 proposal](https://tc39.github.io/process-document/) for ECMAScript, meaning that they're a candidate, but requires further refinement and feedback from implementations and users before it becomes part of the standard. Facebook itself is already using these techniques in production, however.
{{% /aside %}}

From the proposal:

> "Class instance fields" describe properties intended to exist on instances of a class (and may optionally include initializer expressions for said properties).

We can take advantage of this in React.

[**Read more: Using ES7 property initializers in React**](https://babeljs.io/blog/2015/06/07/react-on-es6-plus)

We can use a property initializer to set the initial value of state without writing a constructor:

{{< code jsx >}}
class Song extends React.Component {
  state = {
    versesRemaining: 5,
  }
}
{{< /code >}}

We can even set default props and use those in the initial state:

{{< code jsx >}}
class Song extends React.Component {
  static defaultProps = {
    autoPlay: false,
    verseCount: 10,
  }
  state = {
    versesRemaining: this.props.verseCount,
  }
}
{{< /code >}}

#### Property initializers + arrow functions

Combining property initializers and arrow functions gives us a convenient way to auto-bind `this`, since arrow functions inherit `this` from the scope in which they are declared (lexical scoping):

{{< code jsx >}}
class Something extends React.Component {
  handleButtonClick = (ev) => {
    // `this` is bound correctly!
    this.setState({ buttonWasClicked: true });
  }
}
{{< /code >}}


## Projects

* Noteherder [Morning](https://github.com/xtbc18s1/noteherder) | [Afternoon](https://github.com/xtbc18s1/noteherder/tree/afternoon)

## Homework

## Day 7 Homework

* Make the delete button work.

### Bonus Credit

* Persist the list of notes across page refreshes, using `localStorage`.

### Super Mega Bonus Credit

* Sign up for [Firebase](https://firebase.google.com/).
* Add the [Re-base library](https://github.com/tylermcginnis/re-base) to your project.
* Sync your notes with Firebase.
* Profit.
