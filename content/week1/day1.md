---
title: "Day 1: Introduction"
weight: 1
---

<date>Monday, May 14, 2018</date>

## Lecture Videos

Morning:

* [Playlist](https://www.youtube.com/watch?v=vGMMHQfp8Vk&list=PLuT2TqJuwaY_Hj168ujFhP0w5HzmaDLfG) | [Day 1, part 1](https://www.youtube.com/watch?v=vGMMHQfp8Vk&t=16s)

Afternoon:

* [Playlist] | [Day 1, part 1]

## Topics

* History of JavaScript and the Web
* Getting the most out of a coding bootcamp
* Starting a project with git
* Anatomy of an HTML element ([tags](https://developer.mozilla.org/en-US/docs/Web/HTML/Element), [attributes](https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes), [text content](https://developer.mozilla.org/en-US/docs/Web/API/Node/textContent))
* Basic CSS selector syntax
  * Element name (`div`, `h1`, `p`, etc.)
  * Element ID (`#theID`, `div#theID`, etc.)
  * Class name (`.theClass`, `p.theClass`, etc.)
* Basic DOM manipulation
  * `document.querySelector`/`document.querySelectorAll`
  * `.textContent`
  * `.innerHTML`
* Developer console
  * `console.log`
  * `debugger`
* Basic [event](https://www.w3schools.com/js/js_events.asp) handling
  * [Events in JavaScript](https://www.kirupa.com/html5/javascript_events.htm) - blog post with more detail than we discussed in class
  * `.addEventListener()` - [MDN docs](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener)
  * `.preventDefault()`
  * `.target`

## Examples

### Git

#### Starting a new project with a git repository

First make a new directory and then navigate into the new directory.  Then start a new repository with `git init`.

{{< term >}}
mkdir my_new_project
cd my_new_project
git init
{{< /term >}}

To be able to make our first commit, we need to first add something to our empty project folder.  A common first choice is a `README.md` file, which is a document written in [markdown](https://guides.github.com/features/mastering-markdown/) that provides information about the project.

{{< term >}}
echo "# My New Project" >> README.md
git add .
git commit -m "Initial commit"
{{< /term >}}

Once we have our first commit, we can add a 'remote' for our repository, like [github](https://github.com) or [bitbucket](https://bitbucket.org/).  For github, log in to github.com, then hit the '+' button in the top right of the screen to add a new repository.  Then, it will give you the following commands to run from the command line.

{{< term >}}
git remote add origin git@github.com:myusername/my_new_project.git
git push -u origin master
{{< /term >}}

This adds the github remote as 'origin' and sets it as the default for when you push your changes.  From this point forward, just type `git push` to push your changes to the remote.

### DOM Manipulation
{{< code html >}}
&lt;div class=&quot;person&quot;&gt;
  &lt;h2 id=&quot;firstName&quot;>Han&lt;/h2&gt;
  &lt;h2 id=&quot;lastName&quot;>Solo&lt;/h2&gt;
  &lt;p>Made the Kessel Run in less than 12 parsecs&lt;/p&gt;
  &lt;button>Click here to hire me!&lt;/button&gt;
&lt;/div&gt;
{{< /code >}}

{{< code js >}}
// Get all h2 elements with querySelectorAll. Returns a NodeList
const headings = document.querySelectorAll('.person h2')
console.log(headings)     // [h2#firstName, h2#lastName]

// Get a single element with querySelector
const heading = document.querySelector('.person h2')
console.log(heading)      // h2#firstName

// Do something when a click event occurs
const button = document.querySelector('button')
button.addEventListener('click', (ev) => {
  alert('clicked!')
  console.log(ev.target)  // button
})
{{< /code >}}

## Presentations
* <a target="_blank" href="/history-of-the-web.pdf">JavaScript History</a>
* <a target="_blank" href="/bootcamp-tips-expectations.pdf">Bootcamp Expectations and Tips for Success</a>

## Links
* [Mozilla Developer Network (MDN)](https://developer.mozilla.org/en-US/) - An excellent documentation and learning resource for all your HTML/CSS/JS needs

## Projects

### First JS
[CodePen](https://codepen.io/dstrus/pen/wjxWWB)

### User Directory
[Morning](https://github.com/xtbc18s1/user-directory) | [Afternoon](https://github.com/xtbc18s1/user-directory/tree/afternoon)

## Homework

* Make the button change the text of the heading (the `<h1>`).

### Bonus Credit

* Add multiple headings to the page, and make the button change the _second_ one.

### Super Mega Bonus Credit

* Add a form to the page
* Add a text input to the form.
* When the form is submitted, update the heading with the text that you type in the text input.
