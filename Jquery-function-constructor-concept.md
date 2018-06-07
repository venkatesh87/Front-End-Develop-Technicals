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

#### 5. function for jQuery**
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
  
### 6. Function Declarations
---
```javascript
function functionName(parameters) {
  code to be executed
}
```

### 7. Function Expression
---
```javascript
var x = function (a, b) {
  return a * b
};
document.getElementById("demo").innerHTML = x(4,5);
```
