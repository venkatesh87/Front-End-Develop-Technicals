### Functions for registering behaviors that take effect when the user interacts with the browser.

#### I. Preventing the default action or bubbling of events

- How to cancel an event or preventing it from bubbling up the DOM tree.

- jQuery offers two useful methods that may be called within events handlers in order to stop the event from happening: ```e.preventDefault()``` and ```e.stopPropagation()```

- In fact, both are plain JavaScript methods that are available on the event object of any handler function:

```javascript
function handler(e) {
  // stop the immediate action of this event
  e.preventDefault();

  // prevent the event fro bubbling up
  e.stopPropagation();
}

// attach handler to the keydown event of the document
if (document.attachEvent) document.attachEvent('onkeydown', handler);
else document.addEventListener('keydown', handler);
```

- Returning ```false``` from an event handler has in most cases the same effect as calling those methods, but there are exceptions, such as form submissions (submit event).

#### II. Getting the keycode from keyboard events

- Binding an event handler to keyboard actions and retrieving the keycode that triggered the event.

- To get the key code, attaching an event handler to any keyboard action is required. The key code is reported on the event object received by the handler function.

```javascript
// event handler function
function handler(e) {
  var key = window.event ? e.keyCode : e.which;
  console.log(key, e.shiftKey, e.altKey, e.ctrlKey);
}

// attach handler to the keydown event of the document
if (document.attachEvent) document.attachEvent('onkeydown', handler);
else document.addEventListener('keydown', handler);
```

- It's possible to use any of the keyboard events (keypress, keydown, keyup) on DOM elements, such as text input fields or textareas.

#### III. Getting the current mouse position

- How to get the current mouse position on mouse move or click.

- To get the current position of the mouse, attaching an event handler to any mouse action is required. The mouse's position is reported on the event object received by the handler function.

```javascript
// event handler function
function handler(e) {
  e = e || window.event;

  var pageX = e.pageX;
  var pageY = e.pageY;

  // IE 8
  if (pageX === undefined) {
    pageX = e.clientX + document.body.scrollLeft + document.documentElement.scrollLeft;
    pageY = e.clientY + document.body.scrollTop + document.documentElement.scrollTop;
  }

  console.log(pageX, pageY);
}

// attach handler to the click event of the document
if (document.attachEvent) document.attachEvent('onclick', handler);
else document.addEventListener('click', handler);
```

- Read Jack Moore's well written article about ```cross-browser mouse positioning``` to learn more details and options about this topic.

#### IV. Running code when the document is ready

- A page can't be manipulated safely until the document is "ready." Here's how to make sure code isn't run prematurely.

- This function is the equivalent of jQuery's ```$(document).ready()``` method:

```javascript
document.addEventListener('DOMContentLoaded', function(){
  // do something
});
```

- However, in contrast to jQuery, this code will only run properly in modern browsers (IE > 8) and it won't in case the document is already rendered at the time this script gets inserted (e.g. via Ajax). Therefore, we need to extend this a little bit:

```javascript
function run() {
    // do something
}

// in case the document is already rendered
if (document.readyState!='loading') run();
// modern browsers
else if (document.addEventListener) document.addEventListener('DOMContentLoaded', run);
// IE <= 8
else document.attachEvent('onreadystatechange', function(){
  if (document.readyState=='complete') run();
});
```

- This covers basically all possibilities and is a viable replacement for the jQuery helper.

#### V. Binding and unbinding of event handlers

- How to attach or detach a handler function to an event, such as click, focus, or submit.

- Modern browsers support ```addEventListener()``` and ```removeEventListener()``` for adding or removing event handlers; IE 8 has its own methods. If you need to support both, use these little helpers as a replacement to jQuery's ```$.on()``` and ```$.off()``` methods:

```javascript
function addEvent(el, type, handler) {
  if (el.attachEvent) el.attachEvent('on'+type, handler); else el.addEventListener(type, handler);
}
function removeEvent(el, type, handler) {
  if (el.detachEvent) el.detachEvent('on'+type, handler); else el.removeEventListener(type, handler);
}
```

**>How to use:**

```javascript
var el = document.querySelector('textarea');

// attach anonymous function to click event
addEvent(el, 'click', function(){ console.log('Clicked!'); })

// attach a named function
var foo = function(){ console.log('Focused!'); };
addEvent(el, 'click', foo);

// remove a previously attached function
removeEvent(el, 'click', foo);
```

- Anonymous functions used as event handler cannot be unbound. A reference to the function used for binding the event must be passed to ```removeEvent()```

- It's not required to unbind event handlers when removing DOM elements. JavaScript's garbage collection will take care of it and free up the reserved memory.

- w3schools offers a useful list of available HTML DOM events. These are HTML attribute names; when binding/unbinding events with the above given helper function, omit the "on" prefix of the name to get the event type. For example, use "mouseup" instead of "onmouseup".

- Alternatively, you can also set the event attribute of an element directly. But it's only possible to assign one handler per element:

```javascript
  var el = document.querySelector('textarea');

// set callback
el.onblur = function(){ console.log('Blurred textarea'); };

// remove callback
delete el.onblur;

// assign handler to window object
window.onload = function(){ alert('Window has loaded.'); };
```

- Use the "on" prefix for setting and removing properties such as ```onblur``` or ```onclick``` of elements.

- Read up on how to live bind events in vanilla JavaScript.

#### VI. Trigger an event

- How to create and dispatch events. Corresponding functions to jQuery's $.trigger(), $.click(), $.blur(), $.keyup(), $.mousedown(), etc.

- There are a few convenient methods for triggering an event on specific elements:

```javascript
var el = document.querySelector('input[type="text"]');

// for any element
el.click();

// for inputs and textareas
el.focus();
el.blur();

// for form elements
var my_form = document.querySelector('form');

my_form.submit();
my_form.reset();
```

- In contrast to jQuery, it is not possible to pass an event handler as argument to any of these methods. Read up on binding event handlers in plain JavaScript.

- If you need to trigger other events, such as ```mousedown``` or ```keyup```, use the following helper function:

```javascript
function triggerEvent(el, type) {
  if ('createEvent' in document) {
    // modern browsers, IE9+
    var e = document.createEvent('HTMLEvents');
    e.initEvent(type, false, true);
    el.dispatchEvent(e);
  } else {
    // IE 8
    var e = document.createEventObject();
    e.eventType = type;
    el.fireEvent('on' + e.eventType, e);
  }
}
```
- Usage example:

```javascript
var el = document.querySelector('input[type="text"]');
triggerEvent(el, 'mousedown');
```


```javascript

```
