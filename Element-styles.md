### Get the computed style properties or set CSS properties for an element.

#### I. Set and get CSS styles of elements

- The ```getComputedStyle()``` method (```IE < 9```: ```currentStyle property```) corresponds to the rendered on-page style of an element after all stylesheets were applied. It can be accessed as follows:

```javascript
var el = document.querySelector('div');

// getComputedStyle for modern browsers, currentStyle for IE
var style = window.getComputedStyle ? getComputedStyle(el, null) : el.currentStyle;

// reading properties
console.log(style.backgroundColor);

// reading properties containing hyphens
console.log(style['-webkit-text-size-adjust']);
```

- Setting style properties is done directly via the ```style``` property of an element:

```javascript
var el = document.querySelector('div');

el.style.backgroundColor = 'green';
el.style.display = 'none';
el.style['border-radius'] = '5px';
```

- Multiple styles can be set at once by use of the cssText property:

```javascript
  el.style.cssText += 'background: green, display: none;';
```

#### II. Get and set scroll position of an element

- Get or set the horizontal and vertical scroll position of an element or the document.

- Use the properties scrollTop and scrollLeft to get or set the scroll position of an element:

```javascript
var el = document.querySelector('div');

// get scroll position in px
console.log(el.scrollLeft, el.scrollTop);

// set scroll position in px
el.scrollLeft = 500;
el.scrollTop = 1000;
```

- Getting the **scroll position of the document** in px.

```javascript
var scrollLeft = window.pageXOffset || document.documentElement.scrollLeft,
    scrollTop = window.pageYOffset || document.documentElement.scrollTop;
```

- Setting the document scroll position of the document in px:

```javascript
document.documentElement.scrollTop = document.body.scrollTop = 1000;
document.documentElement.scrollLeft = document.body.scrollLeft = 500;
```

#### III. Get the offset position of an element relative to its parent

- Get the top/left coordinates of an element relative to the offset parent.

- Use ```offsetLeft``` and ```offsetTop``` for finding an element's position in px with respect to its ```offsetParent``` container:

```javascript
var el = document.querySelector('div');
console.log(el.offsetLeft, el.offsetTop);
```

#### IV. Get the position of an element relative to the document

- Get the current top/left coordinates(Tọa độ) of an element relative to the document.

- To get the top and left position of an element relative to the document, we first determine the X/Y coordinates of an element on the screen via ```getBoundingClientRect()```. We then add scroll top/left position to these coordinates. Helper function:

```javascript
function offset(el) {
  var rect = el.getBoundingClientRect(),
    scrollLeft = window.pageXOffset || document.documentElement.scrollLeft,
    scrollTop = window.pageYOffset || document.documentElement.scrollTop;
  return { top: rect.top + scrollTop, left: rect.left + scrollLeft }
}

// example use
var div = document.querySelector('div');
var divOffset = offset(div);
console.log(divOffset.left, divOffset.top);
```

- The result of this helpers is equal to jQuery's $.offset(). getBoundingClientRect() is a very useful, cross browser safe method that returns top, right bottom, and left position of any element relative to the viewport.

#### V. Getting width and height of an element

- Get the current computed dimension of an element, with or without borders and margins

- Use the following methods to get width and height of each of those boxes:

```javascript
var box = document.querySelector('div');

// width and height in pixels, including padding and border
// Corresponds to jQuery outerWidth(), outerHeight()
var width = box.offsetWidth;
var height = box.offsetHeight;

// width and height in pixels, including padding, but without border
// Corresponds to jQuery innerWidth(), innerHeight()
var width = box.clientWidth;
var height = box.clientHeight;
```

- The margin of an element is calculated from its computed style:

```javascript
var style = window.getComputedStyle ? getComputedStyle(el, null) : el.currentStyle;

var marginLeft = parseInt(style.marginLeft) || 0;
var marginRight = parseInt(style.marginRight) || 0;
var marginTop = parseInt(style.marginTop) || 0;
var marginBottom = parseInt(style.marginBottom) || 0;
```

- The computed style may be used to read other properties, too. For example border width:

```javascript
var borderLeft = parseInt(style.borderLeftWidth) || 0;
```

- Getting the window width and height is done differently. Just like in jQuery, the above presented methods do not work on the window or document object. Use this instead:

```javascript
var w = window.innerWidth || document.documentElement.clientWidth || document.body.clientWidth;
var h = window.innerHeight || document.documentElement.clientHeight || document.body.clientHeight;
```

