---
title: "Day 4: Cloning Elements and Data Attributes"
weight: 4
---

<date>Thursday, May 17, 2018</date>

## Lecture Videos

Morning:

* [Playlist](https://www.youtube.com/watch?v=vGMMHQfp8Vk&list=PLuT2TqJuwaY_Hj168ujFhP0w5HzmaDLfG) | [Day 4, Part 1](https://www.youtube.com/watch?v=l49C0WKrjMM&index=39&list=PLuT2TqJuwaY_Hj168ujFhP0w5HzmaDLfG)

Afternoon:

* [Playlist](https://www.youtube.com/watch?v=kBU2t3htGNI&t=2s&list=PLuT2TqJuwaY_XxGei4xUXZn9HuTU3jBRk&index=42) | [Day 4, Part 1](https://www.youtube.com/watch?v=kBU2t3htGNI&t=2s&list=PLuT2TqJuwaY_XxGei4xUXZn9HuTU3jBRk&index=42)

## Topics

### Markdown

* [Markdown Cheatsheet](http://assemble.io/docs/Cheatsheet-Markdown.html)
* [Mastering Markdown](https://guides.github.com/features/mastering-markdown/)

### DOM Manipulation
* [data attributes](https://developer.mozilla.org/en-US/docs/Learn/HTML/Howto/Use_data_attributes)
* [parentElement](https://developer.mozilla.org/en-US/docs/Web/API/Node/parentElement)
* [childNodes](https://developer.mozilla.org/en-US/docs/Web/API/Node/childNodes)
* [firstChild](https://developer.mozilla.org/en-US/docs/Web/API/Node/firstChild)
* [firstElementChild](https://developer.mozilla.org/en-US/docs/Web/API/ParentNode/firstElementChild)
* [insertBefore](https://developer.mozilla.org/en-US/docs/Web/API/Node/insertBefore)
* [closest](https://developer.mozilla.org/en-US/docs/Web/API/Element/closest) (experimental)

### Array methods
* [`Array.prototype` documentation on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/prototype?v=control)
* [`unshift()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/unshift?v=control)
* [`reverse()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reverse?v=control)

### Foundation

Foundation is a CSS (and JS) framework that makes it easy to create stylish, responsive web pages.  The foundation (get it?) of it is the [grid system](http://foundation.zurb.com/grid.html).  The grid splits the page into 12 equally-sized columns, making it easy to set the alignment of elements on the page by specifying how many columns they span.

In addition, you can add sizes of 'small', 'medium', 'large', etc, to specify different behavior at different screen sizes.  In the following example, the two child divs will be full screen width at small screen sizes (stacked on top of each other), and half of the screen width at medium and larger screen sizes (appearing next to each other).

{{< code html >}}
&lt;div class=&quot;row&quot;&gt;
  &lt;div class=&quot;small-12 medium-6 columns&quot;&gt;
  &lt;/div&gt;
  &lt;div class=&quot;small-12 medium-6 columns&quot;&gt;
  &lt;/div&gt;
&lt;/div&gt;
{{< /code >}}

* [Foundation CSS Framework](http://foundation.zurb.com)
* [Button](http://foundation.zurb.com/sites/docs/button.html)
* [Button Group](http://foundation.zurb.com/sites/docs/button-group.html)
* [Un-bulleted List](http://foundation.zurb.com/sites/docs/typography-helpers.html#un-bulleted-list)

## Examples

### Data Attributes

HTML5 gave us a way to save extra information on a standard HTML Element via the `data-*` attributes. Basically, you can add any arbitrary information you want, prefixing the name of the attribute with `data-`.  This data is then accessible through JavaScript via the `someElement.dataset` object, or through CSS via `attr(data-*)`.

{{< code html >}}
&lt;div
  id="my-div"
  data-name="Awesome div"
  data-id="div-1234"
  data-color="blue"
  data-marshmallows="yummy"&gt;
&lt;/div&gt;
{{< /code >}}

{{< code js >}}
const myDiv = document.querySelector('#my-div')

myDiv.dataset.name            // "Awesome div"
myDiv.dataset.data-id         // "div-1234"
myDiv.dataset.color           // "blue"
myDiv.dataset.marshmallows    // "yummy"
{{< /code >}}

{{< code css >}}
#my-div {
  background-color: attr(data-color);
}

div[data-id='div-1234'] {
  height: 400px;
  width: 400px;
}
{{< /code >}}

### `.cloneNode`
Sometimes it may be easier to clone an existing node rather than build an entirely new one, especially if the markup is complex.  In our 'Tatum Tots' project, we kept a hidden `li` in the DOM that we cloned every time we needed to render a new list item.

{{< code html >}}
&lt;li class="flick grid-x align-middle template"&gt;
  &lt;span class="flick-name cell auto"&gt;sdfkjhgds&lt;/span&gt;
  &lt;span class="actions button-group cell shrink"&gt;
    &lt;button class="fav button warning"&gt;fav&lt;/button&gt;
    &lt;button class="remove button alert"&gt;del&lt;/button&gt;
  &lt;/span&gt;
&lt;/li&gt;
{{< /code >}}

{{< code css >}}
/* hides any 'li' with a 'template' class */
li.template {
  display: none;
}
{{< /code >}}

{{< code js >}}
const list = document.querySelector('ul')
const templateItem = document.querySelector('li.template')

// Make a copy of the templateItem
// Pass 'true' as an argument to clone all children as well
const newItem = templateItem.cloneNode(true)

// remove 'template' class so it is no longer hidden
newItem.classList.remove('template')

list.appendChild(newItem)
{{< /code >}}

### Array methods

{{< code js >}}
const ary = [1, 2, 3, 4, 5]

ary.unshift(0)

console.log(ary)    // [0, 1, 2, 3, 4, 5]

ary.shift()         // 0

console.log(ary)    // [1, 2, 3, 4, 5]

ary.reverse()

console.log(ary)    // [5, 4, 3, 2, 1]
{{< /code >}}

## Projects

Tatum Tots
* [Morning](https://github.com/xtbc18s1/tatum-tots)
* [Afternoon](https://github.com/xtbc18s1/tatum-tots/tree/afternoon)

## Homework

* Make the _delete_ button **work**, if you haven't already.
* Make the _fav_ button change the style of the list item in some way.

### Bonus Credit

* Make the _fav_ button also change the object in the array. For example:

{{< code js >}}{
  id: 1,
  name: 'GI Joe',
  fav: true,
}
{{< /code >}}

### Super Mega Bonus Credit

* Add buttons to move the flick up and down the list.
* Make the buttons also change their place in the array.

### Super Mega Bonus Credit Hyper Fighting

* Allow users to edit the names of the flicks in the list after they're added.

(Would it be nice if we could make that span's **content editable**?)
