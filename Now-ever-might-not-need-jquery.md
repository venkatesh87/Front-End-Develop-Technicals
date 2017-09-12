### 1. Remove an element from the page:

    - Remember the maddeningly roundabout way you had to remove an element from the page with vanilla DOM? 
    ```el.parentNode.removeChild(el);``` ? Here's a comparison of the jQuery way and the new improved vanilla way.

> **jQuery:**

```javascript
var $elem = $(".someClass") //select the element 
$elem.remove(); //remove the element
```

> **Without jQuery:**

```javascript
var elem = document.querySelector(".someClass"); //select the element
elem.remove() //remove the element
```

### 2. Prepend an element:

> **jQuery:**

```javascript
$elem.prepend($someOtherElem);
```

> **Without jQuery:**

```javascript
elem.prepend(someOtherElem);
```

### 3. Insert an element before another element:

> **jQuery:**

```javascript
$elem.before($someOtherElem);
```

> **Without jQuery:**

```javascript
elem.before(someOtherElem);
```

### 4. Replace an element with another element:

> **jQuery:**

```javascript
$elem.replaceWith($someOtherElem);
```

> **Without jQuery:**

```javascript
elem.replaceWith(someOtherElem);
```

### 5. Find the closest ancestor that matches a given selector:

> **jQuery:**

```javascript
$elem.closest("div");
```

> **Without jQuery:**

```javascript
elem.closest("div");
```

### 6. Browser Support of DOM manipulation methods:

> **Desktop:** 

| Chrome      | Opera       | Firefox     | IE          | Edge        | Safari      |
| ----------- |:-----------:|:-----------:|:-----------:|:-----------:|:-----------:|
| 54          | 41          | 49          | No          | 54          | 54          |

> **Mobile / Tablet:**

| iOS Safari  | Opera Mobile | Opera Mini  | Android     | Android Chrome | Android Firefox |
| 10.0-10.2   | No           | No          | 56          | 59             | 54              |

### 7. Fade in an Element:

> **jQuery:**

```javascript
$elem.fadeIn();
```

> **CSS:**

```
.thingy {
  display: none;
  opacity: 0;
  transition: 200;
}
```

> **Without jQuery:**

```javascript
elem.style.display = "block";
requestAnimationFrame(() => elem.style.opacity = 1);
```

### 8. Call an event handler callback only once:

> **jQuery:**

```javascript
$elem.one("click", someFunc);
```
   - In the past when writing plain JavaScript, we had to call removeEventListener inside of the callback function.

> **JS:**

```javascript
function dostuff() {
  alert("some stuff happened");
  this.removeEventListener("click", dostuff);
}
var button = document.querySelector("button");
button.addEventListener("click", dostuff);
```
   - Now things are a lot cleaner. You might have seen the third optional parameter sometimes passed into addEventListener. It's a boolean to decide between event capturing or event bubbling. Nowadays, however, the third argument can alternatively be a configuration object.

> **JS:**

```javascript
elem.addEventListener('click', someFunc, { once: true, });
```
   - If you still want to use event capturing as well as have the callback called only once, then you can specify that in the configuration object as well:

> **JS:**

```javascript
elem.addEventListener('click', myClickHandler, {
  once: true,
  capture: true
});
```

### 9. Animation

   - jQuery's .animate() method is pretty limited.

> **jQuerys :**

```javascript
$elem.animate({
  width: "70%",
  opacity: 0.4,
  marginLeft: "0.6in",
  fontSize: "3em",
  borderWidth: "10px"
}, 1500);
```
   - The docs say "All animated properties should be animated to a single numeric value, except as noted below; most properties that are non-numeric cannot be animated using basic jQuery functionality." This rules out transforms, and you need a plugin just to animate colors. You'd be far better off with the new Web Animations API.

> **JS:**

```javascript
var elem = document.querySelector('.animate-me');
elem.animate([
  { 
    transform: 'translateY(-1000px) scaleY(2.5) scaleX(.2)', 
    transformOrigin: '50% 0', 
    filter: 'blur(40px)', 
    opacity: 0 
  },
  { 
    transform: 'translateY(0) scaleY(1) scaleX(1)',
    transformOrigin: '50% 50%',
    filter: 'blur(0)',
    opacity: 1 
  }
], 1000);
```

### 10. Ajax:

    - Another key selling point of jQuery in the past has been Ajax. jQuery abstracted away the ugliness of ```XMLHttpRequest```:

> **jQuery:**

```javascript
$.ajax('https://some.url', {
  success: (data) => { /* do stuff with the data */ }
});
```
    - The new fetch API is a superior replacement for XMLHttpRequest and is now supported by all modern browsers.

> **JS:**

```javascript
fetch('https://some.url')
  .then(response => response.json())
  .then(data => {
    // do stuff with the data
  });
```

    - Admittedly fetch can be a bit more complicated than this small code sample. For example, the Promise returned from 
      fetch() won't reject on HTTP error status. It is, however, far more versatile than anything built on top of 
      XMLHttpRequest.

    - If we want ease of use though, there is a simpler option that has gained popularity - but it's not native to the 
      browser, which brings me onto...

### 11. Iterating a NodeList in 2017:

    - Another key selling point of jQuery in the past has been Ajax. jQuery abstracted away the ugliness of ```XMLHttpRequest```:

> **jQuery:**

```javascript
var myArrayFromNodeList = [].slice.call(document.querySelectorAll('li'));
```

Or:

```javascript
[].forEach.call(myNodeList, function (item) {...}
```

```javascript
Array.from(querySelectorAll('li')).forEach((li) => /* do something with li */);
```

```javascript
document.querySelectorAll('li').forEach((li) => /* do some stuff */);
```