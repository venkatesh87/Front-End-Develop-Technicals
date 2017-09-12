## I. AJAX:

### 1. JSON:

> **jQuery:**

```javascript
$.getJSON('/my/url', function(data) {

});
```

> **IE9+:**

```javascript
var request = new XMLHttpRequest();
request.open('GET', '/my/url', true);

request.onload = function() {
  if (request.status >= 200 && request.status < 400) {
    // Success!
    var data = JSON.parse(request.responseText);
  } else {
    // We reached our target server, but it returned an error

  }
};

request.onerror = function() {
  // There was a connection error of some sort
};

request.send();
```

### 2. Post:

> **jQuery:**

```javascript
$.ajax({
  type: 'POST',
  url: '/my/url',
  data: data
});
```

> **IE8+:**

```javascript
var request = new XMLHttpRequest();
request.open('POST', '/my/url', true);
request.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded; charset=UTF-8');
request.send(data);
```

### 3. Request:

> **jQuery:**

```javascript
$.ajax({
  type: 'GET',
  url: '/my/url',
  success: function(resp) {

  },
  error: function() {

  }
});
```

> **IE9+:**

```javascript
var request = new XMLHttpRequest();
request.open('GET', '/my/url', true);

request.onload = function() {
  if (request.status >= 200 && request.status < 400) {
    // Success!
    var resp = request.responseText;
  } else {
    // We reached our target server, but it returned an error

  }
};

request.onerror = function() {
  // There was a connection error of some sort
};

request.send();
```

## II. EFFECTS

### 1. Fade In:

> **jQuery:**

```javascript
$(el).fadeIn();
```

> **IE9+:**

```javascript
function fadeIn(el) {
  el.style.opacity = 0;

  var last = +new Date();
  var tick = function() {
    el.style.opacity = +el.style.opacity + (new Date() - last) / 400;
    last = +new Date();

    if (+el.style.opacity < 1) {
      (window.requestAnimationFrame && requestAnimationFrame(tick)) || setTimeout(tick, 16);
    }
  };

  tick();
}

fadeIn(el);
```

### 2. Hide:

> **jQuery:**

```javascript
$(el).hide();
```

> **IE8+:**

```javascript
el.style.display = 'none';
```

### 3. Show:

> **jQuery:**

```javascript
$(el).show();
```

> **IE8+:**

```javascript
el.style.display = '';
```

## III. ELEMENTS

### 1. Add Class:

> **jQuery:**

```javascript
$(el).addClass(className);
```

> **IE8+:**

```javascript
if (el.classList)
  el.classList.add(className);
else
  el.className += ' ' + className;
```

### 2. After:

> **jQuery:**

```javascript
$(el).after(htmlString);
```

> **IE8+:**

```javascript
el.insertAdjacentHTML('afterend', htmlString);
```

### 3. Append:

> **jQuery:**

```javascript
$(parent).append(el);
```

> **IE8+:**

```javascript
parent.appendChild(el);
```

### 4. Before:

> **jQuery:**

```javascript
$(el).before(htmlString);
```

> **IE8+:**

```javascript
el.insertAdjacentHTML('beforebegin', htmlString);
```

### 5. Children:

> **jQuery:**

```javascript
$(el).children();
```

> **IE8+:**

```javascript
el.cloneNode(true);
```

### 6. Contains:

> **jQuery:**

```javascript
$.contains(el, child);
```

> **IE8+:**

```javascript
el !== child && el.contains(child);
```

### 7. Contains Selector:

> **jQuery:**

```javascript
$(el).find(selector).length;
```

> **IE8+:**

```javascript
el.querySelector(selector) !== null
```

### 8. Each:

> **jQuery:**

```javascript
$(selector).each(function(i, el){

});
```

> **IE9+:**

```javascript
var elements = document.querySelectorAll(selector);
Array.prototype.forEach.call(elements, function(el, i){

});
```

### 9. Empty:

> **jQuery:**

```javascript
$(el).empty();
```

> **IE9+:**

```javascript
el.innerHTML = '';
```

### 10. Filter:

> **jQuery:**

```javascript
$(selector).filter(filterFn);
```

> **IE9+:**

```javascript
Array.prototype.filter.call(document.querySelectorAll(selector), filterFn);
```

### 11. Find Children:

> **jQuery:**

```javascript
$(el).find(selector);
```

> **IE8+:**

```javascript
el.querySelectorAll(selector);
```

### 12. Find Elements:

> **jQuery:**

```javascript
$('.my #awesome selector');
```

> **IE8+:**

```javascript
document.querySelectorAll('.my #awesome selector');
```

### 13. Get Attributes:

> **jQuery:**

```javascript
$(el).attr('tabindex');
```

> **IE8+:**

```javascript
el.getAttribute('tabindex');
```

### 14. Get Html:

> **jQuery:**

```javascript
$(el).html();
```

> **IE8+:**

```javascript
el.innerHTML
```

### 15. Get Outer Html:

> **jQuery:**

```javascript
$('<div>').append($(el).clone()).html();
```

> **IE8+:**

```javascript
el.outerHTML
```

### 16. Get Style:

> **jQuery:**

```javascript
$(el).css(ruleName);
```

> **IE9+:**

```javascript
getComputedStyle(el)[ruleName];
```

### 17. Get Text:

> **jQuery:**

```javascript
$(el).text();
```

> **IE9+:**

```javascript
el.textContent
```

### 18. Has Class:

> **jQuery:**

```javascript
$(el).hasClass(className);
```

> **IE8+:**

```javascript
if (el.classList)
  el.classList.contains(className);
else
  new RegExp('(^| )' + className + '( |$)', 'gi').test(el.className);
```

### 1. Matches:

> **jQuery:**

```javascript
$(el).is($(otherEl));
```

> **IE9+:**

```javascript
var matches = function(el, selector) {
  return (el.matches || el.matchesSelector || el.msMatchesSelector || el.mozMatchesSelector || el.webkitMatchesSelector || el.oMatchesSelector).call(el, selector);
};

matches(el, '.my-class');
```

### 1. Next:

> **jQuery:**

```javascript
$(el).next();
```

> **IE9+:**

```javascript
el.nextElementSibling
```

### 1. Offset:

> **jQuery:**

```javascript
$(el).offset();
```

> **IE8+:**

```javascript
var rect = el.getBoundingClientRect();
{
  top: rect.top + document.body.scrollTop,
  left: rect.left + document.body.scrollLeft
} 
```

### 1. Offset Parent:

> **jQuery:**

```javascript
$(el).offsetParent();
```

> **IE8+:**

```javascript
el.offsetParent || el
```

### 1. Outer Height:

> **jQuery:**

```javascript
$(el).outerHeight();
```

> **IE8+:**

```javascript
el.offsetHeight
```

### 1. Outer Height With Margin:

> **jQuery:**

```javascript
$(el).outerHeight(true);
```

> **IE9+:**

```javascript
function outerHeight(el) {
  var height = el.offsetHeight;
  var style = getComputedStyle(el);

  height += parseInt(style.marginTop) + parseInt(style.marginBottom);
  return height;
}

outerHeight(el);
```

### 1. Outer Width:

> **jQuery:**

```javascript
$(el).outerWidth();
```

> **IE8+:**

```javascript
el.offsetWidth
```

### 1. Outer Width With Margin:

> **jQuery:**

```javascript
$(el).outerWidth(true);
```

> **IE9+:**

```javascript
function outerWidth(el) {
  var width = el.offsetWidth;
  var style = getComputedStyle(el);

  width += parseInt(style.marginLeft) + parseInt(style.marginRight);
  return width;
}

outerWidth(el);
```

### 1. Parent:

> **jQuery:**

```javascript
$(el).parent();
```

> **IE8+:**

```javascript
el.parentNode
```

### 1. Position:

> **jQuery:**

```javascript
$(el).position();
```

> **IE8+:**

```javascript
{left: el.offsetLeft, top: el.offsetTop}
```

### 1. Position Relative To Viewport:

> **jQuery:**

```javascript
var offset = el.offset();

{
  top: offset.top - document.body.scrollTop,
  left: offset.left - document.body.scrollLeft
}
```

> **IE8+:**

```javascript
el.getBoundingClientRect()
```

### 1. Prepend:

> **jQuery:**

```javascript
$(parent).prepend(el);
```

> **IE8+:**

```javascript
parent.insertBefore(el, parent.firstChild);
```

### 1. Prev:

> **jQuery:**

```javascript
$(el).prev();
```

> **IE9+:**

```javascript
el.previousElementSibling
```

### 1. Remove:

> **jQuery:**

```javascript
$(el).remove();
```

> **IE8+:**

```javascript
el.parentNode.removeChild(el);
```

### 1. Remove Class:

> **jQuery:**

```javascript
$(el).removeClass(className);
```

> **IE8+:**

```javascript
if (el.classList)
  el.classList.remove(className);
else
  el.className = el.className.replace(new RegExp('(^|\\b)' + className.split(' ').join('|') + '(\\b|$)', 'gi'), ' ');
```

### 1. Replace From Html:

> **jQuery:**

```javascript
$(el).replaceWith(string);
```

> **IE8+:**

```javascript
el.outerHTML = string;
```

### 1. Set Attributes:

> **jQuery:**

```javascript
$(el).attr('tabindex', 3);
```

> **IE8+:**

```javascript
el.setAttribute('tabindex', 3);
```

### 1. Set Html:

> **jQuery:**

```javascript
$(el).html(string);
```

> **IE8+:**

```javascript
el.innerHTML = string;
```

### 1. Set Style:

> **jQuery:**

```javascript
$(el).css('border-width', '20px');
```

> **IE8+:**

```javascript
// Use a class if possible
el.style.borderWidth = '20px';
```

### 1. Set Text:

> **jQuery:**

```javascript
$(el).text(string);
```

> **IE9+:**

```javascript
el.textContent = string;
```

### 1. Siblings:

> **jQuery:**

```javascript
$(el).siblings();
```

> **IE9+:**

```javascript
Array.prototype.filter.call(el.parentNode.children, function(child){
  return child !== el;
});
```

### 1. Toggle Class:

> **jQuery:**

```javascript
$(el).toggleClass(className);
```

> **IE9+:**

```javascript
if (el.classList) {
  el.classList.toggle(className);
} else {
  var classes = el.className.split(' ');
  var existingIndex = classes.indexOf(className);

  if (existingIndex >= 0)
    classes.splice(existingIndex, 1);
  else
    classes.push(className);

  el.className = classes.join(' ');
}
```

## III. EVENTS

### 1. Off:

> **jQuery:**

```javascript
$(el).off(eventName, eventHandler);
```

> **IE9+:**

```javascript
el.removeEventListener(eventName, eventHandler);
```

### 1. On:

> **jQuery:**

```javascript
$(el).on(eventName, eventHandler);
```

> **IE9+:**

```javascript
el.addEventListener(eventName, eventHandler);
```

### 1. Ready:

> **jQuery:**

```javascript
$(document).ready(function(){

});
```

> **IE9+:**

```javascript
function ready(fn) {
  if (document.attachEvent ? document.readyState === "complete" : document.readyState !== "loading"){
    fn();
  } else {
    document.addEventListener('DOMContentLoaded', fn);
  }
}
```

### 1. Trigger Custom:

> **jQuery:**

```javascript
$(el).trigger('my-event', {some: 'data'});
```

> **IE9+:**

```javascript
if (window.CustomEvent) {
  var event = new CustomEvent('my-event', {detail: {some: 'data'}});
} else {
  var event = document.createEvent('CustomEvent');
  event.initCustomEvent('my-event', true, true, {some: 'data'});
}

el.dispatchEvent(event);
```

### 1. Trigger Native:

> **jQuery:**

```javascript
$(el).trigger('change');
```

> **IE9+:**

```javascript
// For a full list of event types: https://developer.mozilla.org/en-US/docs/Web/API/document.createEvent
var event = document.createEvent('HTMLEvents');
event.initEvent('change', true, false);
el.dispatchEvent(event);
```
## IV. UTILS

### 1. Bind:

> **jQuery:**

```javascript
$.proxy(fn, context);
```

> **IE9+:**

```javascript
fn.bind(context);
```

### 1. Array Each:

> **jQuery:**

```javascript
$.each(array, function(i, item){

});
```

> **IE9+:**

```javascript
array.forEach(function(item, i){

});
```

### 1. Deep Extend:

> **jQuery:**

```javascript
$.extend(true, {}, objA, objB);
```

> **IE8+:**

```javascript
var deepExtend = function(out) {
  out = out || {};

  for (var i = 1; i < arguments.length; i++) {
    var obj = arguments[i];

    if (!obj)
      continue;

    for (var key in obj) {
      if (obj.hasOwnProperty(key)) {
        if (typeof obj[key] === 'object')
          out[key] = deepExtend(out[key], obj[key]);
        else
          out[key] = obj[key];
      }
    }
  }

  return out;
};

deepExtend({}, objA, objB);
```

### 1. Extend:

> **jQuery:**

```javascript
$.extend({}, objA, objB);
```

> **IE8+:**

```javascript
var extend = function(out) {
  out = out || {};

  for (var i = 1; i < arguments.length; i++) {
    if (!arguments[i])
      continue;

    for (var key in arguments[i]) {
      if (arguments[i].hasOwnProperty(key))
        out[key] = arguments[i][key];
    }
  }

  return out;
};

extend({}, objA, objB);
```

### 1. Index Of:

> **jQuery:**

```javascript
$.inArray(item, array);
```

> **IE9+:**

```javascript
array.indexOf(item);
```

### 1. Is Array:

> **jQuery:**

```javascript
$.isArray(arr);
```

> **IE9+:**

```javascript
Array.isArray(arr);
```

### 1. Map:

> **jQuery:**

```javascript
$.map(array, function(value, index){

});
```

> **IE9+:**

```javascript
array.map(function(value, index){

});
```

### 1. Now:

> **jQuery:**

```javascript
$.now();
```

> **IE9+:**

```javascript
Date.now();
```

### 1. Parse Html:

> **jQuery:**

```javascript
$.parseHTML(htmlString);
```

> **IE9+:**

```javascript
var parseHTML = function(str) {
  var tmp = document.implementation.createHTMLDocument();
  tmp.body.innerHTML = str;
  return tmp.body.children;
};

parseHTML(htmlString);
```

### 1. Parse Json:

> **jQuery:**

```javascript
$.parseJSON(string);
```

> **IE8+:**

```javascript
JSON.parse(string);
```

### 1. Trim:

> **jQuery:**

```javascript
$.trim(string);
```

> **IE9+:**

```javascript
string.trim();
```

### 1. Type:

> **jQuery:**

```javascript
$.type(obj);
```

> **IE9+:**

```javascript
Object.prototype.toString.call(obj).replace(/^\[object (.+)\]$/, '$1').toLowerCase();
```
