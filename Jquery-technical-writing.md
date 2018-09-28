#### JQuery Technical Writing
---

## 1. Code JavaScript Flag :

**- Case 1:**
```javascript
  window.DEBUG = true;

  function log(a, b, c, d) {
       if(DEBUG) {
           console.log(a, b, c, d);
       }
  } 

  if(DEBUG) {
      // Do dev stuff
  } else {
     // Do produection stuff
  }

  log("foobar") // Does not need to be wrapper, as log() itself is functional only in debug mode    
```

**- Case 2:** 

```javascript
var is_playing = true;
if (is_playing) {
  player.pauseVideo();
  playButton.className += " disable";
} else {
  player.playVideo();
  playButton.className = playButton.className.replace('disable', '');
}
```

**- Case 3:** 

```javascript
stopBodyScrolling(true);

stopBodyScrolling(false);

function stopBodyScrolling (bool) {
    if (bool === true) {
        document.body.addEventListener("touchmove", freezeVp, false);
    } else {
        document.body.removeEventListener("touchmove", freezeVp, false);
    }
}

var freezeVp = function(e) {
    e.preventDefault();
};
```

**- Case 4:**

```
#container {width: 400px;height: 400px;position: relative;background: yellow;}
#animate {width: 50px;height: 50px;position: absolute; background-color: red;}
<button onclick="myMove()">Click Me</button>
<div id ="container">
<div id ="animate"></div>

function myMove() {
  var elem = document.getElementById("animate");   
  var pos = 0;
  var id = setInterval(frame, 5);
  function frame() {
    if (pos == 350) {
      clearInterval(id);
    } else {
      pos++; 
      elem.style.top = pos + 'px'; 
      elem.style.left = pos + 'px'; 
    }
  }
}
```
**- Case 5:**

```
function checkCookies() {
    var text = "";
    if (navigator.cookieEnabled == true) {
      text = "Cookies are enabled.";
    } else {
      text = "Cookies are not enabled.";
    }
    document.getElementById("demo").innerHTML = text;
}
```

**- Case 6:** Khi gọi một function trong function thì hãy bỏ cặp dấu ngoặc này () đi, ```displayDate```, ```frame```.

```
document.getElementById("myBtn").addEventListener("click", displayDate);
function displayDate(){
	 document.getElementById('demo').innerHTML = Date();
}
```

**2. Funtion parameters**

>JavaScript Code:
```javascript
/**
 * Show selected text value dropdown
 
 * @param string selectItem Selected item selector
 * @param string showTo   Show selected text to element selector
 * 
 * @return void
 **/
function showSelected(selectItem, showTo) {
  $(document).on('click', selectItem, function() {
    $(showTo).text($(this).text());
  });
};
showSelected('.dropdown-catagory li a', '.dropdown-toggle .value-catagory');
```

**2. Funtion map function**

>JavaScript Code:
```javascript

```

**3. **

>JavaScript Code:
```javascript

```

**4. **

>JavaScript Code:
```javascript

```

**5. **

>JavaScript Code:
```javascript

```

**6. **

>JavaScript Code:
```javascript

```

**7. **

>JavaScript Code:
```javascript

```

**8. **

>JavaScript Code:
```javascript

```

**9. **

>JavaScript Code:
```javascript

```

**10. **

>JavaScript Code:
```javascript

```

**11. **

>JavaScript Code:
```javascript

```

**12. **

>JavaScript Code:
```javascript

```

**13. **

>JavaScript Code:
```javascript

```

**14. **

>JavaScript Code:
```javascript

```

**15. **

>JavaScript Code:
```javascript

```

**16. **

>JavaScript Code:
```javascript

```

**17. **

>JavaScript Code:
```javascript

```

**18. **

>JavaScript Code:
```javascript

```

**19. **

>JavaScript Code:
```javascript

```

**20. **

>JavaScript Code:
```javascript

```

**21. **

>JavaScript Code:
```javascript

```

**22. **

>JavaScript Code:
```javascript

```

**23. **

>JavaScript Code:
```javascript

```

**24. **

>JavaScript Code:
```javascript

```

**25. **

>JavaScript Code:
```javascript

```

**26. **

>JavaScript Code:
```javascript

```

**27. **

>JavaScript Code:
```javascript

```

**28. **

>JavaScript Code:
```javascript

```

**29. **

>JavaScript Code:
```javascript

```

**30. **

>JavaScript Code:
```javascript

```

**31. **

>JavaScript Code:
```javascript

```
**32. **

>JavaScript Code:
```javascript

```

**33. **

>JavaScript Code:
```javascript

```

**34. **

>JavaScript Code:
```javascript

```

**35. **

>JavaScript Code:
```javascript

```

