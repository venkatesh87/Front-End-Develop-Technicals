# I. Memorize the company project GDIT

**1. 20180328_I_DESIGN**
- Switch screen with smartphone.

>JavaScript Code:
```javascript
function myResizeFunction() {
  if($(window).width() <= 1100){
    // do something
  }
}
$(myResizeFunction); // Do on DOM ready
$(window).on("load resize", myResizeFunction); 
```

>JavaScript Code hiệu quả:
```javascript
// Bind to the resize event of the window object
$(window).on("resize", function () {
  // Set .right's width to the window width minus 480 pixels
  $(".content .right").width( $(this).width() - 480 );
// Invoke the resize event immediately
}).resize();
```

>JavaScript Code hiệu quả:
```javascript
$('.nav-icons').click(function(e) {
  if($(window).width()<=1000){
    $(this).toggleClass('open');
  }
});
```

>JavaScript Code EventListener sẽ không hiểu:
```javascript
if($(window).width()<=1000){
  $('.nav-icons').click(function(e) {
    $(this).toggleClass('open');
  });
}
```

**ForEach**:
>JavaScript Code:
var Navigation = {
  selector: {
    nav_item: document.querySelectorAll('.navigation ul li')  
  },
  init: function(){
    Navigation.nav_reset();
  },
  nav_reset: function(){
    if ($(window).width() > 1000) {
      Navigation.selector.nav_item.forEach(function(userItem) {
        userItem.style.WebkitOpacity = "1";
        userItem.style.msOpacity = "1";
        userItem.style.opacity = "1";
        userItem.style.WebkitTransform = "translate3d(0, 0, 0)";
        userItem.style.msTransform = "translate3d(0, 0, 0)";
        userItem.style.transform = "translate3d(0, 0, 0)";
      });
    } else if ($(window).width() <= 1000) {
      Navigation.selector.nav_item.forEach(function(userItem) {
        userItem.style.WebkitOpacity = "0";
        userItem.style.msOpacity = "0";
        userItem.style.opacity = "0";
        userItem.style.WebkitTransform = "translate3d(0, 40px, 0)";
        userItem.style.msTransform = "translate3d(0, 40px, 0)";
        userItem.style.transform = "translate3d(0, 40px, 0)";
      });
    }
  }
}
```

**TweenMax:** Thuộc tính ```autoAlpha: 0``` tương đương với ```opacity: 0```.

**2. **
- Text.

>JavaScript Code:
```javascript

```

**3. **
- Text.

>JavaScript Code:
```javascript

```

**4. **
- Text.

>JavaScript Code:
```javascript

```

**5. **
- Text.

>JavaScript Code:
```javascript

```

**6. **
- Text.

>JavaScript Code:
```javascript

```

**7. **
- Text.

>JavaScript Code:
```javascript

```

**8. **
- Text.

>JavaScript Code:
```javascript

```

**9. **
- Text.

>JavaScript Code:
```javascript

```

**10. **
- Text.

>JavaScript Code:
```javascript

```

**11. **
- Text.

>JavaScript Code:
```javascript

```

**12. **
- Text.

>JavaScript Code:
```javascript

```

**13. **
- Text.

>JavaScript Code:
```javascript

```

**14. **
- Text.

>JavaScript Code:
```javascript

```

**15. **
- Text.

>JavaScript Code:
```javascript

```

**16. **
- Text.

>JavaScript Code:
```javascript

```

**17. **
- Text.

>JavaScript Code:
```javascript

```
