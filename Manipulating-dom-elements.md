### Adding, removing, copying DOM elements and related manipulations.

#### I. Create a DOM element

- How to create a new element and attach it to the DOM tree.

- Use the ```createElement()``` method for creating a DOM element:

```javascript
var el = document.createElement('div');
```

- Fill the new element with any HTML content:

```javascript
el.innerHTML = '<p>Hello World!</p>';
```

- Alternatively, use DOM methods for creating content nodes and append them to the new element. This approach requires more code, and is in general slower or equally fast as working with innerHTML:

```javascript
var textnode = document.createTextNode('Hello World!');
el.appendChild(textnode);
```

- "el" can now be inserted into the DOM tree:

```javascript
document.body.appendChild(el);
```

#### II. Remove an element from the DOM tree and insert a new one in its place.

- Replacing one element with another by use of the cross-browser safe DOM method replaceChild():

```javascript
  // select the element that will be replaced
var el = document.querySelector('div');

// <a href="/javascript/manipulation/creating-a-dom-element-51/">create a new element</a> that will take the place of "el"
var newEl = document.createElement('p');
newEl.innerHTML = '<b>Hello World!</b>';

// replace el with newEL
el.parentNode.replaceChild(newEl, el);
```

#### III. Unwrap a DOM element

- Remove the parents of an element from the DOM, leaving the element's content in place.

- How to unwrap an element with cross browser safe DOM methods:


```javascript
// select element to unwrap
var el = document.querySelector('div');

// get the element's parent node
var parent = el.parentNode;

// move all children out of the element
while (el.firstChild) parent.insertBefore(el.firstChild, el);

// remove the empty element
parent.removeChild(el);
```

- The code is straight forward and much faster than the corresponding jQuery's method ```$.unwrap()```.

#### IV. Empty an element's content

- Remove all child nodes of an element from the DOM.

- Use the innerHTML property of an element for removing all child elements, and thus clearing its content:

```javascript
var el = document.querySelector('div');
el.innerHTML = '';
```

- Event handlers bound to any part of the element's content are destroyed in the process.

#### V. Removing an element

- Remove an element from the DOM tree.

- Cross browser safe removal of an element from the DOM tree:

```javascript
var el = document.querySelector('div'); // select the first returned <div> element 
el.parentNode.removeChild(el);
```

- So, first select the element to remove. Then walk up the tree to its parent and remove the child element from there.

#### VI. Insert an element after or before another

- Insert an HTML structure after or before a given DOM tree element.

- The following helper function ```insertAfter()``` lets you insert a new element after an existing one in the DOM tree:

```javascript
function insertAfter(el, referenceNode) {
  referenceNode.parentNode.insertBefore(el, referenceNode.nextSibling);
}

// example
var newEl = document.createElement('div');
newEl.innerHTML = '<p>Hello World!</p>';

var ref = document.querySelector('div.before');

insertAfter(newEl, ref);
```

- To insert an element before another one, we can use a very similar helper function: ```insertBefore()```

```javascript
function insertBefore(el, referenceNode) {
    referenceNode.parentNode.insertBefore(el, referenceNode);
}

// example
var newEl = document.createElement('div');
newEl.innerHTML = '<p>Hello World!</p>';

var ref = document.querySelector('div.before');

insertBefore(newEl, ref);
```

- These DOM methods are supported by all major browsers, including IE 8 and below.

- If you intend to insert a new structure in form of an HTML text string, you should make use of ```insertAdjacentHTML()```. This method parses the specified text as HTML and inserts the resulting elements into the DOM tree at a specified position. It does not reparse the element it is being used on and thus it does not corrupt the existing elements inside the element.

#### VII. Get the text content of an element

- Get the combined text contents of an element, including its descendants, or set the text content of the element.

- Use the element property textContent (IE 8: innerText) for getting the content of an element and its descendants, stripped of all HTML tags:

```javascript
var el = document.querySelector('div');
text = el.textContent || el.innerText;
console.log(text);
```

#### VIII. Get and set the HTML content of an element

- Read or write the HTML content of an element.

- The element property innerHTML is used for getting and setting the HTML content of en element in vanilla JavaScript:

```javascript
var el = document.querySelector('div');

// get HTML content
console.log(el.innerHTML);

// set HTML content
el.innerHTML = '<p>Hello World!</p>'
```

- Simple as that. jQuery's $.html() method does exactly that in the background.

#### IX. Append or prepend to an element

- Insert a new element or an HTML structure to the end or the beginning of another element's content.

- Using the property innerHTML of an element to get or modify its content:

```javascript
var el = document.querySelector('div');

// get element content as string
console.log(el.innerHTML)

// append to the element's content
el.innerHTML += '<p>Hello World!</p>';

// prepend to the element's content
el.innerHTML = '<p>Hello World!</p>' + el.innerHTML;
```

- ```innerHTML``` is essentially the element's content as a string. Be warned, though: Modifying innerHTML will destroy and rebuild all descendant elements of the container. Event handlers bound to any of the destroyed elements are lost in the process and need to be reattached if required.

- Alternatively, it's possible to use DOM methods for creating, inserting, and moving elements:

```javascript
var el = document.querySelector('div');

// create a p element for inserting in el
var newEl = document.createElement('p');
// use the innerHTML property for inserting HTML content
// or append a textNode to the p element
newEl.appendChild(document.createTextNode('Hello World!'));

// append p as a new child to el
el.appendChild(newEl);

// same result with insertBefore()
el.insertBefore(newEl, null);

// use as second argument the child node you want to insert the new node before
// example: prepend newEl as first child to el
el.insertBefore(newEl, el.childNodes[0]);
```

- This approach requires more code, and is in general slower or equally fast as working with innerHTML. However, using DOM methods ensures event handlers bound to the element's content remain intact.

#### XI. Wrap an HTML structure around an element

- How to use a given container as wrapper for another DOM element.

- Wrap a given element in a new container element using plain JavaScript:

```javascript
// element that will be wrapped
var el = document.querySelector('div.wrap_me');

// create wrapper container
var wrapper = document.createElement('div');

// insert wrapper before el in the DOM tree
el.parentNode.insertBefore(wrapper, el);

// move el into wrapper
wrapper.appendChild(el);
```

- The same procedure in form of a helper function:

```javascript
function wrap(el, wrapper) {
    el.parentNode.insertBefore(wrapper, el);
    wrapper.appendChild(el);
}

// example: wrapping an anchor with class "wrap_me" into a new div element
wrap(document.querySelector('a.wrap_me'), document.createElement('div'));
```

#### XII. Clone an element

- Create a deep copy of a DOM element.

```javascript
var el = document.querySelector('div');

var foo = el.cloneNode(true);
```

- ```cloneNode(true)``` creates a deep copy of the selected DOM element including attributes and child elements. To clone only the node and its attributes, pass false as argument to ```cloneNode()```.

#### XIII. Iterating over a list of selected elements

- How to loop through a NodeList and do something with each element.

- There are several ways of iterating through a list of selected elements. First, learn about the ```for()``` loop:

```javascript
var divs = document.querySelectorAll('div'), len = divs.length;

for (var i=0; i<len; i++) {
  divs[i].style.color = "green";
}
```

- As you can see, the NodeList's length is determined before the loop. This approach is faster than using divs.length inside the for statement, because the length would otherwise be read repeatedly for each iteration.

- A reverse ```while()``` loop is an alternative, even more efficient approach and it also involves less code:

```javascript
var divs = document.querySelectorAll('div'), i = divs.length;
while (i--) {
  divs[i].style.color = "green";
}
```

- Finally, you can use this little trick, that is similar to jQuery's ```$.each()``` method:

```javascript
var divs = document.querySelectorAll('div');

[].forEach.call(divs, function(item) {
  item.style.color = "green";
});
```

- Naturally, you can create a helper function with any of these loops inside. Or if you don't mind dropping support for IE8 and other old browsers, you can simply do:

```javascript
var divs = document.querySelectorAll('div');

divs.forEach(function(item) {
  item.style.color = "green";
});
```
