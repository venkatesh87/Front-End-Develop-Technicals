#### 1. Window onload
---
```javascript
$( window ).load(function() {
	// code here
});
```

#### 2. Document ready
---
```javascript
$(document).ready(function(){
	// code here
});
```

#### 3. function($)
---
```javascript
(function($) {
  $(function() {
    // Function
    var handleFunction = function() {
      
    };
    // Call function
    handleFunction();

  });
})(jQuery);
```

#### 4. App function
---
```javascript
var App = function() {
  function handleFunction() {
		// code here   
  }
  return {
    init: function() {
      handleFunction();
    }
  };
}();
$(document).ready(function() {
  App.init();
});
```

#### 5. App function
---
- Kiểm tra xem thử ```window``` có hàm ```tt_sticky``` hay chưa. Nếu chưa có thì gán ```function``` cho nó.

```javascript
var jc = jQuery;
jc.noConflict();
'use strict';
jc(document).ready(function() {
  tt_sticky();
});

if ('function' !== typeof(window['tt_sticky'])) {
  window.tt_sticky = function() {
    var isMobile = jc('body').hasClass('touch') ? true : false;
    if (jc('.tt_sticky').length) {
      var menuposition;
      var menu_content_offset = jc('#header_container').outerHeight() - jc('.tt_sticky').outerHeight();
      jc('#header_container').css('min-height', jc('#header_container').outerHeight());
      if (jc('.admin-bar').length && !window.matchMedia('(max-width: 600px)').matches) {
        menuposition = jc('#header_container').offset().top - jc('#wpadminbar').outerHeight() + menu_content_offset;
      } else {
        menuposition = jc('#header_container').offset().top + menu_content_offset;
      }
      jc(window).resize(function() {
        setTimeout(function() {
          jc('#header_container').css('min-height', jc('.tt_sticky').outerHeight());
        }, 500);
        if (jc('.admin-bar').length && !window.matchMedia('(max-width: 600px)').matches) {
          menuposition = jc('#header_container').offset().top - jc('#wpadminbar').outerHeight() + menu_content_offset;
        } else {
          menuposition = jc('#header_container').offset().top + menu_content_offset;
        }
      })
      jc(window).scroll(function(event) {
        if (jc(window).scrollTop() > menuposition) {
          jc('.tt_sticky').addClass('tt_stuck');
        } else {
          jc('.tt_sticky').removeClass('tt_stuck');
        }
      });
    }
    if (jc('.tt_header_hiding').length && isMobile == false) {
      var didScroll;
      var delta = 5;
      var navbarHeight = jc('#header_container').outerHeight() + jc('.tt_header_hiding').outerHeight();
      var lastScrollTop = jc('#header_container').offset().top + jc('.tt_header_hiding').outerHeight();
      var firstTop = jc('#header_container').offset().top + jc('.tt_sticky').outerHeight();
      jc(window).scroll(function(event) {
        if (jc(window).scrollTop() > menuposition) {
          didScroll = true;
          hasScrolled();
        }
      });

      function hasScrolled() {
        var st = jc(window).scrollTop();
        if (Math.abs(lastScrollTop - st) <= delta) { return; }
        if (st > lastScrollTop && st > navbarHeight) {
          jc('.tt_header_hiding').css('margin-top', -jc('.tt_header_hiding').outerHeight());
          jc('.tt_header_hiding').addClass('.tt_header_hidden');
        } else {
          if (st + jc(window).height() < jc(document).height()) {
            jc('.tt_header_hiding').removeClass('.tt_header_hidden');
            jc('.tt_header_hiding').css('margin-top', '0');
          }
        }
        if (st > firstTop) {
          lastScrollTop = st;
        } else {
          lastScrollTop = firstTop;
        }
      }
    }
  };
}
```
#### 6. function for jQuery**
---
```javascript
//function to fix height of iframe!
  var calcHeight = function() {
    var headerDimensions = $('#mainlivedemo').height();
    var selector = ($('.stretched').length > 0) ? '#iframelive' : '#iframelive iframe';
    $(selector).height($(window).height() - headerDimensions);
  }
  $(document).ready(function() {
    calcHeight();
  });
  $(window).resize(function() {
    calcHeight();
  }).load(function() {
    calcHeight();
  });
  ```
  
### 7. Function Declarations
---
```javascript
function functionName(parameters) {
  code to be executed
}
```

### 8. Function Expression
---
```javascript
var x = function (a, b) {
  return a * b
};
document.getElementById("demo").innerHTML = x(4,5);
```
