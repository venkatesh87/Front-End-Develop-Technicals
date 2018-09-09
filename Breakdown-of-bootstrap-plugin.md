Most of the Bootstrap javascript plugins like Modal, Dropdown and others, share the same basic template. I wanted to extract that template out from their js plugin and explain each part individually. Here is the basic template extracted from modal.js.

```javascript
+function ($) {
  'use strict';

  // MODAL CLASS DEFINITION

  // ======================


  var Modal = function (element, options) {
    this.options        = options
    this.$body          = $(document.body)
    ...
  }

  Modal.VERSION  = '3.2.0'

  Modal.DEFAULTS = {
    backdrop: true,
    keyboard: true,
    show: true
  }

   Modal.prototype.show = function (_relatedTarget) {
     ....
   }

  // MODAL PLUGIN DEFINITION

  // =======================


  function Plugin(option, _relatedTarget) {
    return this.each(function () {
      var $this   = $(this)
      var data    = $this.data('bs.modal')
      var options = $.extend({}, Modal.DEFAULTS, $this.data(), typeof option == 'object' &amp;&amp; option)

      if (!data) $this.data('bs.modal', (data = new Modal(this, options)))
      if (typeof option == 'string') data[option](_relatedTarget)
      else if (options.show) data.show(_relatedTarget)
    })
  }

  var old = $.fn.modal

  $.fn.modal             = Plugin
  $.fn.modal.Constructor = Modal


  // MODAL NO CONFLICT

  // =================


  $.fn.modal.noConflict = function () {
    $.fn.modal = old
    return this
  }

  ....

}(jQuery);
```

Let's break this template further and look at each of the parts separately:

####  1. Self Invoking Function:


```javascript
+function ($) {
 ...
}(jQuery)
```

Self-invoking functions are the functions which get invoked as soon as it gets defined. They create a scope for all the variables and functions defined within the function so they don't leak to global scope.

Another interesting thing about this function is that it is starting with the plus sign '+'.  The reason for this is to make parser think that it is the function expression instead of the function statement. Whenever javascript parser sees 'function' at the start of the line, it considers that as a function statement. A function statement requires that the function should have a name and it also cannot end the statement with parenthesis like '(jquery)'.

A function expression on the other-hand, can be anonymous, and you can invoke them right away by putting parenthesis at the end. Putting any operator, like +, -, ! etc., in front of the function will make the parser think that it's a function expression.

Lastly, you may have noticed that we actually pass 'jQuery' to the function and make '$' the parameter name. This way we can reference jQuery within function with '$'. Outside the scope of the function, you can continue to use '$' for other libraries. This avoids any conflict between jQuery and other libraries which share '$'.

#### 2. Strict Mode

```javascript
"use strict";
```

By switching on the strict mode of javascript, you opt into a better, more secure and a restricter version of javascript. In this mode, for example, you cannot use undeclared variables.  This way you cannot add variables to global scope by mistake, for example:

```javascript
function test() {
  "use strict";
  x = 10; /* throws syntax error - Uncaught ReferenceError: x ... */
}
```

#### 3. Constructor Function & Prototype

```javascript
var Modal = function (element, options) {
    this.options        = options
    this.$body          = $(document.body)
    ...
  }

Modal.VERSION  = '3.2.0'

Modal.DEFAULTS = {
  backdrop: true,
  keyboard: true,
  show: true
}

Modal.prototype.show = function (_relatedTarget) {
  ....
}
```

Modal is a constructor function which gets executed when 'new Modal()' is called. The important thing to note is that 'this' in modal function can change references based on how it is called.

If it's executed with the new operator like, 'new Modal()", then 'this' is bound to a newly created object and all the properties like 'options' are set on that object and everything works as expected.

However, if this function is called without the 'new' operator like 'Modal();' then 'this' is bound to the global object and it can clobber the global namespace. In this case, 'this.options' will be same as calling 'window.options'. Take a look at the example below which shows how the references of 'this' changes:

```javascript
var Tester = function() {
  console.log(this);
}

Tester();     /* outputs: Window    */
new Tester(); /* outputs: Tester {} */
```

#### 4. Main Plugin Function

```javascript
// MODAL PLUGIN DEFINITION

  // =======================

  function Plugin(option, _relatedTarget) {
    return this.each(function () {
      var $this   = $(this)
      var data    = $this.data('bs.modal')
      var options = $.extend({}, Modal.DEFAULTS, $this.data(), typeof option == 'object' &amp;&amp; option)

      if (!data) $this.data('bs.modal', (data = new Modal(this, options)))
      if (typeof option == 'string') data[option](_relatedTarget)
      else if (options.show) data.show(_relatedTarget)
    })
  }
```

This plugin function is the method which gets exposed to jQuery's prototype ($.fn). This is the method which gets called when you call '$('.my_modal').modal();'.

Interesting part about this method is how it puts the Modal object in the data params.

```javascript
var data    = $this.data('bs.modal')
...
if (!data) $this.data('bs.modal', (data = new Modal(this, options)))
```

This enables the re-use of the same Modal object, if you show or hide the same modal multiple times on the page. Its an interesting technique to memorize object by using  data attribute.

Another thing to note is that you can also pass string to call specific methods eg. $('.my_modal).modal('show'). This is done by using this line.

```javascript
if (typeof option == 'string') data[option](_relatedTarget)
```

#### 5. Constructor Property

```javascript
var old = $.fn.modal

$.fn.modal             = Plugin
$.fn.modal.Constructor = Modal
```

Finally, the Constructor property which exposes the main Modal function object. This is useful for extending Modal or for changing the default settings e.g '$.fn.modal.Constructor.DEFAULTS.show = false;'. This will change the default settings for all the instances of the Modal.
## Note:

```javascript
return this.each(function () {}
```

Cái này có tác dụng gọi plugin ở những selector khác nhau mà ko ảnh hưởng gì.

```javascript
$('.my_modal').modal();'
```

```javascript
$('.my_modal').modal();'
```

```javascript
$('.my_modal').modal();'
```

## Tổng hợp link Bootstrap Menu:

1. https://mobirise.com/bootstrap-menu/bootstrap-dropdown-menu-hover.html

## Refer:

1. http://sortedarray.com/breakdown-of-bootstrap-plugin/

2. https://octobercms.com/docs/ui/foundation

3. http://jbeurel.github.io/bootstrap-annotated-source/docs/modal.html

