### Functions for accessing elements by class, id and other selectors.

#### I. Match element selector

- Check the current elements against a CSS selector.
- To check whether a given element matches a CSS selector, modern browsers support the ```matches()``` or ```matchesSelector()``` DOM method. Here's a polyfill for other browsers:

``` javascript
// matches polyfill
this.Element && function(ElementPrototype) {
  ElementPrototype.matches = ElementPrototype.matches ||
    ElementPrototype.matchesSelector ||
    ElementPrototype.webkitMatchesSelector ||
    ElementPrototype.msMatchesSelector ||
    function(selector) {
      var node = this,
        nodes = (node.parentNode || node.document).querySelectorAll(selector),
        i = -1;
      while (nodes[++i] && nodes[i] != node);
      return !!nodes[i];
    }
}(Element.prototype);
```

- Browsers supporting DOM4 make use of the optimized internal method, which is much faster. This is generally recommended when extending native objects. Now you can call matches() on any DOM element:

``` javascript
var el = document.querySelector('span');
console.log(el.matches('.foo'));
```

#### II. Get parent element node

- Getting the parent DOM node of an element.

- Selecting the parent node of an element via cross-browser safe DOM method:

``` javascript
var el = document.querySelector('div');
var parent = el.parentNode;
```

#### III. Get siblings of an element

- Get the next, previous or all siblings of an element or retrieve siblings that match a given selector.

- A helper function for fetching all siblings for a given DOM element -  or a filtered set of them:

``` javascript
function getSiblings(el, filter) {
  var siblings = [];
  el = el.parentNode.firstChild;
  do { if (!filter || filter(el)) siblings.push(el); } while (el = el.nextSibling);
  return siblings;
}

// example filter function
function exampleFilter(el) {
  return elem.nodeName.toLowerCase() == 'a';
}

// usage
el = document.querySelector('div');
// get all siblings of el
var sibs = getSiblings(el);
// get only anchor element siblings of el
var sibs_a = getSiblings(el, exampleFilter);
```

- There are faster DOM methods for only getting the previous or next sibling of an element:

``` javascript
var previous = el.previousSibling;
var next = el.nextSibling;
```

- Get all following siblings of an element, optionally filtered:

``` javascript
// this helper accepts a filter function as shown above: "exampleFilter()"
function getNextSiblings(el, filter) {
  var siblings = [];
  while (el = el.nextSibling) { if (!filter || filter(el)) siblings.push(el); }
  return siblings;
}
```

- Get all preceding siblings of an element, optionally filtered:

``` javascript
// this helper accepts a filter function as shown above: "exampleFilter()"
function getPreviousSiblings(el, filter) {
  var siblings = [];
  while (el = el.previousSibling) { if (!filter || filter(el)) siblings.push(el); }
  return siblings;
}
```

#### IV. Get closest element by selector

- Get the first element that matches the selector by testing the element itself and traversing up through its ancestors in the DOM tree.

- ```closest()```, the analog to jQuery's ```$.closest()```, is an element method introduced in DOM4 and supported by modern browsers, such as Firefox and Chrome. Here's a polyfill for Internet Explorer and other browsers without native support:

``` javascript
// matches polyfill
this.Element && function(ElementPrototype) {
  ElementPrototype.matches = ElementPrototype.matches ||
    ElementPrototype.matchesSelector ||
    ElementPrototype.webkitMatchesSelector ||
    ElementPrototype.msMatchesSelector ||
    function(selector) {
      var node = this,
        nodes = (node.parentNode || node.document).querySelectorAll(selector),
        i = -1;
      while (nodes[++i] && nodes[i] != node);
      return !!nodes[i];
    }
}(Element.prototype);

// closest polyfill
this.Element && function(ElementPrototype) {
  ElementPrototype.closest = ElementPrototype.closest ||
    function(selector) {
      var el = this;
      while (el.matches && !el.matches(selector)) el = el.parentNode;
      return el.matches ? el : null;
    }
}(Element.prototype);
```

- Browsers supporting DOM4 make use of the optimized internal method, which is much faster. This is generally recommended when extending native objects. Now you can call ```closest()``` on any DOM element, just like in jQuery:

``` javascript
var el = document.querySelector('span');
console.log(el.closest('div'));
```

#### V. Select the children of an element

- Getting the children of a DOM element.

- Selecting the children of an element with DOM methods:

``` javascript
var el = document.querySelector('div');

var children = el.childNodes,
  number_of_children = children.length;

for (var i = 0; i < number_of_children; i++)
  console.log(children[i].innerHTML);
```

- There are faster methods for only fetching the first or last child of an element:

``` javascript
var firstChild = el.firstChild;
var lastChild = el.lastChild;
```
