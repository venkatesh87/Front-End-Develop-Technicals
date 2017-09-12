### A collection of frequently used animations and effects for DOM elements.

#### I. Animate an element property

- How to do animations, such as fading, sliding, or just toggling visibility with JS and CSS3.

- Animations in JavaScript aren't difficult to accomplish. As an example, two functions that behave similar to jQuery's ```$.fadeIn()``` and ```$.fadeOut()```:

```javascript
// fade an element from the current state to full opacity in "duration" ms
function fadeOut(el, duration) {
  var s = el.style,
    step = 25 / (duration || 300);
  s.opacity = s.opacity || 1;
  (function fade() {
    (s.opacity -= step) < 0 ? s.display = "none" : setTimeout(fade, 25); })();
}

// fade out an element from the current state to full transparency in "duration" ms
// display is the display style the element is assigned after the animation is done
function fadeIn(el, duration, display) {
  var s = el.style,
    step = 25 / (duration || 300);
  s.opacity = s.opacity || 0;
  s.display = display || "block";
  (function fade() {
    (s.opacity = parseFloat(s.opacity) + step) > 1 ? s.opacity = 1 : setTimeout(fade, 25); })();
}
```

- However, using JavaScript for rather simple animations without special effects, is probably not the best choice. For things like fading, sliding, positioning, or simply hiding, it's often easier (and faster) to create classes with CSS3 transitions and add/remove those classes to elements as needed.

- Here's a working demo for slide toggling an element with the help of CSS3 transitions:

> **HTML**

```javascript
<p>
  <input type="button" value="Toggle" onclick="toggle(document.querySelector('.toggle'));">
</p>
<div class="toggle">Hello World!</div>
```

> **CSS**

```javascript
.toggle {
  overflow: hidden;
  transition: height .4s, padding .4s;
}

.toggle.is_hidden {
  height: 0 !important;
  padding-top: 0 !important;
  padding-bottom: 0 !important;
}

div {
  background: #1663d6;
  color: #fff;
  font: bold 20px sans-serif;
  width: 300px;
  text-align: center;
  padding: 50px;
  border-radius: 5px;
}
```

> **JS**

```javascript
function hasClass(el, className) {
  return el.classList ? el.classList.contains(className) : new RegExp('\\b' + className + '\\b').test(el.className);
}

function addClass(el, className) {
  if (el.classList) el.classList.add(className);
  else if (!hasClass(el, className)) el.className += ' ' + className;
}

function removeClass(el, className) {
  if (el.classList) el.classList.remove(className);
  else el.className = el.className.replace(new RegExp('\\b' + className + '\\b', 'g'), '');
}

function toggle(el) {
  hasClass(el, 'is_hidden') ? removeClass(el, 'is_hidden') : addClass(el, 'is_hidden');
}
```

- In this example, we make use of our plainJS class helpers ```hasClass()```, ```addClass()```, and ```removeClass()```. The essential JavaScript for accomplishing the task comprises just a tiny code snippet:

```javascript
function toggle(el) {
  hasClass(el, 'is_hidden') ? removeClass(el, 'is_hidden') : addClass(el, 'is_hidden');
}
```
#### II. Hide or show an element

- Toggle an element's display property for rendering it visible or invisible.

- Showing and hiding an element can be achieved by toggling its display style:

```javascript
var el = document.querySelect('div');

// hide
el.style.display = 'none';

// show
el.style.display = '';
// or if the div element is hidden by default via CSS stylesheet
el.style.display = 'block';
```

- However, creating a function, such as ```$.show()``` and ```$.hide()``` in jQuery, requires a bit more than that. Hiding an element is always done by setting its display style to ```'none'```. Showing an element is more difficult, because this functionality must take into account stylesheet rules, as well as the default display style of an element. E.g. a ```span``` has ```inline``` as its default display value. Setting it to block is wrong.

- The following helpers are quite convenient, but in order to keep things simple, the ```show()``` function requires an additional argument; the target display value of the element (block, inline-block, inline, etc.):

```javascript
function hide(el) {
  el.style.display = 'none';
}

function show(el, value) {
  el.style.display = value;
}

function toggle(el, value) {
  var display = (window.getComputedStyle ? getComputedStyle(el, null) : el.currentStyle).display;
  if (display == 'none') el.style.display = value;
  else el.style.display = 'none';
}
```

- ```toogle()``` can be used to switch between visible and invisible. If you don't want to or cannot pass in the target display value manually, it gets more complicated. The following helpers are basically vanilla JavaScript clones of jQuery's ```$.show()``` and ```$.hide()```. For these functions to work, it's required to store the initial/default display style of an element. For this, the data attribute "olddisplay" is used:

```javascript
// get the default display style of an element
function defaultDisplay(tag) {
  var iframe = document.createElement('iframe');
  iframe.setAttribute('frameborder', 0);
  iframe.setAttribute('width', 0);
  iframe.setAttribute('height', 0);
  document.documentElement.appendChild(iframe);

  var doc = (iframe.contentWindow || iframe.contentDocument).document;

  // IE support
  doc.write();
  doc.close();

  var testEl = doc.createElement(tag);
  doc.documentElement.appendChild(testEl);
  var display = (window.getComputedStyle ? getComputedStyle(testEl, null) : testEl.currentStyle).display
  iframe.parentNode.removeChild(iframe);
  return display;
}

// actual show/hide function used by show() and hide() below
function showHide(el, show) {
  var value = el.getAttribute('data-olddisplay'),
    display = el.style.display,
    computedDisplay = (window.getComputedStyle ? getComputedStyle(el, null) : el.currentStyle).display;

  if (show) {
    if (!value && display === 'none') el.style.display = '';
    if (el.style.display === '' && (computedDisplay === 'none')) value = value || defaultDisplay(el.nodeName);
  } else {
    if (display && display !== 'none' || !(computedDisplay == 'none'))
      el.setAttribute('data-olddisplay', (computedDisplay == 'none') ? display : computedDisplay);
  }
  if (!show || el.style.display === 'none' || el.style.display === '')
    el.style.display = show ? value || '' : 'none';
}

// helper functions
function show(el) { showHide(el, true); }

function hide(el) { showHide(el); }
```

- It's a convenient and useful function, but it does involve a rather large chunk of code. So, you might be better off setting the display style of an element manually as shown above.
