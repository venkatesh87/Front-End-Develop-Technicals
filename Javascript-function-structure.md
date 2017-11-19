### 1. Window onload

```javascript
$( window ).load(function() {
	// code here
});
```

### 2. Document ready

```javascript
$(document).ready(function(){
	// code here
});
```

### 3. function($)

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

### 4. App function

```
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

### 5. Function Expression