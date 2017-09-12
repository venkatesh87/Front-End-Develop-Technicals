### Functions for accessing elements by class, id and other selectors.

#### I. Select DOM elements by CSS selector

- ```querySelectorAll``` - a CSS selector method like the one provided by jQuery.
- ```querySelectorAll()``` returns a list of DOM elements that match a given CSS selector. If you have ever used jQuery to select an element, you know how to make use of this method:

```javascript
var matches = document.querySelectorAll('div.foo');
for (i=0; i<matches.length; i++)
  console.log(matches[i].innerHTML);
```

- In the example, a NodeList of all ```<div>``` tags that have the class "foo" assigned is fetched. If no element matches the given selector, n empty NodeList is returned. The method works with basically any CSS selector, just like jQuery's $(...) method. Cross browser support is great; IE 8 is limited to CSS 2.1 selectors and it has issues with some unrecognized HTML5 tags. Other examples:

```javascript
// select all div tags + link tags with the class "info"
var matches = document.querySelectorAll("div, a.info");

// select all text input fields
var matches = document.querySelectorAll("input[type='text']");
```

- As you can see, it's exactly what jQuery's selector engine does for you - only faster and no extra library required. In addition, there's an even faster method available for fetching only the first matching element:

```javascript
var match = document.querySelector('div.foo');

// equals for the matched element
var match = document.querySelectorAll('div.foo')[0];
```

#### II. Select elements by class name

- ```getElementsByClassName``` - a fast way of selecting DOM elements by class name in modern browsers. Does not work in IE 8 and below.

-The ```getElementsByClassName()``` method returns a collection of elements with the given class name as a NodeList. It is supported in modern browsers. Internet Explorer has support for this method as of version 9. Example:

```javascript
var list = document.getElementsByClassName('foo');

// get the number of selected elements
console.log(list.length);

// iterate over elements and output their HTML content
for (var i = 0; i < list.length; i++)
  console.log(list[i].innerHTML);
```

- As with ```getElementById()```, it's also possible to select elements by class name within another container:

```javascript
var container = document.getElementById('header');
var list = container.getElementsByClassName('foo');
```

#### III. Select elements by tag name

- ```getElementsByTagName``` - a fast and cross browser safe way for selecting DOM elements by tag name, e.g. "div", "a", "span", etc.

```javascript
var list = document.getElementsByTagName('a');

// get the number of selected elements
console.log(list.length);

// iterate over elements and output href attribute values
for (var i = 0; i < list.length; i++)
  console.log(list[i].href);
```

- As with getElementById(), it's possible to select elements by tag name within another container:

```javascript
var container = document.getElementById('header');
var list = container.getElementByTagName('a');
```

#### IV. Select an element by ID

- ```getElementById``` - a fast and cross browser safe way for selecting DOM elements.
- The method ```getElementById()``` is supported in all major browsers and returns the first element with the specified ID. It is the fastest way for accessing DOM tree elements. Example:

```javascript
var el = document.getElementById('foo');
el.innerHTML = 'Hello World!';
```

