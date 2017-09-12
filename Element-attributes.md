### Functions for getting and setting DOM attributes of elements.

#### I. Set, get, and remove properties of DOM elements

- Get the value of an input field or the href of an anchor. Learn how to work with element properties.

- While jQuery provides an extra method for setting and getting element property values, there's no such thing in plain JavaScript. Element properties, such as ```href```, ```title```, ```alt```, and ```value```, are directly accessible as JavaScript object properties:

- Here are some examples:

```javascript
  var el = document.querySelector('a');
console.log(el.href);
if (el.title != 'foo') el.title = 'foo';

var inp = document.querySelector('input[type="text"]');
console.log(inp.value);
inp.value = 'Hello World!';
```

- HTML attributes, such as class or href are directly bound to their element's properties. Meaning if you change the property, the attribute gets changes, as well - and vice versa.

- It's also allowed to create custom properties:

```javascript
var el = document.querySelector('div');
el.foo = { bar: true };
console.log(el.foo);
```

- To remove such a property at a later time, use the ```delete``` statement:

```javascript
delete el.foo;
```

#### II. Adding, removing, and testing for classes

- ```addClass```, ```removeClass```, ```hasClass``` - three important functions for working with DOM element classes.

- There are convenient methods for manipulating an element's class attribute: ```classList.add()```, ```classList.remove()``` and ```classList.contains()```. Unfortunately, browser support is not sufficient at the time of this writing. Therefore, we need to make use of short helper function that correspond to the jQuery methods ```$.addClass()```, ```$.removeClass()``` and ```$.hasClass()```:

```javascript
  function hasClass(el, className) {
    return el.classList ? el.classList.contains(className) : new RegExp('\\b'+ className+'\\b').test(el.className);
}

function addClass(el, className) {
    if (el.classList) el.classList.add(className);
    else if (!hasClass(el, className)) el.className += ' ' + className;
}

function removeClass(el, className) {
    if (el.classList) el.classList.remove(className);
    else el.className = el.className.replace(new RegExp('\\b'+ className+'\\b', 'g'), '');
}
```

- How to use these helper functions:

```javascript
var el = document.querySelector('div');
if (!hasClass(el, 'foo')) addClass(el, 'foo');
```

- If you intend to make thousands and thousands of class manipulations, you could take a slightly different and better performing approach that involves a bit more code:

```javascript
var hasClass, addClass, removeClass;

if ('classList' in document.documentElement) {
  hasClass = function(el, className) { return el.classList.contains(className); };
  addClass = function(el, className) { el.classList.add(className); };
  removeClass = function(el, className) { el.classList.remove(className); };
} else {
  hasClass = function(el, className) {
    return new RegExp('\\b' + className + '\\b').test(el.className);
  };
  addClass = function(el, className) {
    if (!hasClass(el, className)) { el.className += ' ' + className; }
  };
  removeClass = function(el, className) {
    el.className = el.className.replace(new RegExp('\\b' + className + '\\b', 'g'), '');
  };
}
```

#### III. Setting, getting, and removing data attributes

- Read, write, or remove data values of an element.

- In vanilla JavaScript setting a data attribute of an element is done with the generic ```setAttribute()``` method. This is the equivalent of jQuery's ```$.data()``` method. Here's an example for setting and retrieving the attribute ```"data-foo"```:

```javascript
// setting data-foo
var el = document.querySelector('div');
el.setAttribute('data-foo', 'Hello World!');
```

- ```getAttribute()``` is used for reading the data attribute of an element:

```javascript
// getting data-foo
var el = document.querySelector('img');
console.log(el.getAttribute('data-foo'));
```

- Make use of the removeAttribute() method to delete the given data attribute:

```javascript
el.removeAttribute('data-foo');
```

#### IV. Getting, setting, and removing attributes

- ```getAttribute```, ```setAttribute```, ```removeAttribute``` - modify attributes, such as id, alt, title and more.

- In vanilla JavaScript an attribute's value can be read with the ```getAttribute()``` method:

```javascript
// read the title of an element
var el = document.querySelector('img');
console.log(el.getAttribute('title'));
```

- Setting an attribute or modifying it's current value is done via the element's ```setAttribute()``` method:

```javascript
// set the alt attribute of an element
var el = document.querySelector('img');
el.setAttribute('alt', 'Hello World!');
```

- Make use of the ```removeAttribute()``` method to erase an attribute from the element:

```javascript
el.removeAttribute('alt');
```
