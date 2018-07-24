#### jQuery Plugin Patterns
---

/*
A (very) WIP collection of optimized/recommended jQuery plugin patterns
from @addyosmani, @cowboy, @ajpiano and others.

Disclaimer:
-----------------------
Whilst the end-goal of this gist is to provide a list of recommended patterns, this
is still very much a work-in-progress. I am not advocating the use of anything here 
until we've had sufficient time to tweak and weed out what the most useful patterns
are (and what needs to straight-out be avoided). Please keep in mind if re-sharing.

But..why do you/we care about this again?:
-----------------------
Shiz like this https://github.com/zenorocha/jquery-boilerplate
(related comments from adam and ralph here:  
https://github.com/zenorocha/jquery-boilerplate/issues/11).

Notes from me:
-----------------------
I'm working on a collection of (proven) jQuery plugin patterns that we can 
recommend to others. I understand that ideally developers shouldn't 
*need* boilerplate code nor patterns for this type of thing given we have 
an excellent guide already, however, because there is enough variation in 
how plugins are implemented to warrant work put into this, I'm happy to 
explore the idea for now.
Please feel free to suggest patterns and alternatives. If you've been mentioned 
below and would like to improve (or even suggest removal) of a pattern, go for 
it. I just want us to push something concrete that can be used at the end of the 
day.

Credits:
----------------------
All those listed

Dude..wasting time with this:
----------------------
If you think this is an uber waste of time..feel free to say. I currently think
it would offer something useful to developers looking for direction, but that's
not to say I'm right at all.
*/

```javascript
/*
**********************************************************
Plugin boilerplate from @ajpiano with a minor adjustment.
**********************************************************
*/

;(function ($, undefined) {

    // Create the defaults, only once!
    var defaults = {
        propertyName: "value"
    };

    // The actual plugin constructor
    function Plugin(element, options) {
        this.element = element;
        this.options = $.extend({}, defaults, this.options);
        this.init();
    }

    Plugin.prototype.init = function () {
        // Place initialization logic here
        // You already have access to the DOM element and the options via the instance, 
        // e.g., this.element and this.options
    };

    // A really lightweight plugin wrapper around the constructor, 
    // preventing against multiple instantiations
    $.fn.plugin = function (options) {
        return this.each(function () {
            if (!$.data(this, "plugin")) {
                $.data(this, "plugin", new Plugin(this, options));
            }
        });
    }

})(jQuery);
```

```javascript
/*
**********************************************************
A distilled template based on @cowboys jQuery pluginization
'best options' tip where options can be overridden both globally 
and per-call. Thanks to @mathias for reminding me about the 
pattern.
**********************************************************
*/

(function ($, undefined) {
    $.fn.pluginName = function (options) {
        // Override defaults with specified options.
        options = $.extend({}, $.fn.pluginName.options, options);
        return this.each(function () {
            var elem = $(this);
        });
    };
    // Some sensible defaults.
    $.fn.pluginName.options = {
        key: "value",
        myMethod: function (elem, param) {}
    };
})(jQuery);
```

```javascript
/*
*******************************************************
jQueryUI 1.8/9 Widget boilerplate from @addyosmani 
with input from @peolanha
*******************************************************
*/

(function ($, window, document, undefined) {

    $.widget("demo.myComponent", {

        //Options to be used as defaults
        options: {
            someValue: null
        },

        //Setup widget (eg. element creation, apply theming, bind events etc.)
        _create: function () {
            //this.element.addStuff();
        },

        //Destroy an instantiated plugin and clean-up modifications the widget has made to the DOM
        destroy: function () {
            //this.element.removeStuff();
            // For UI 1.8, destroy must be invoked from the base widget
            $.Widget.prototype.destroy.call(this);
            // For UI 1.9, define _destroy instead and don't worry about calling the base widget
        },

        methodB: function (event) {
            //_trigger dispatches callbacks the plugin user can subscribe to
            //signature: _trigger(type, event, objectOfKeyValuePairsToPassToCallback)
            this._trigger('methodA', event, {
                key: value
            });
        },

        methodA: function (event) {
            this._trigger('dataChanged', event, {
                key: value
            });
        },

        //Respond to any changes the user makes to the option method
        _setOption: function (key, value) {
            switch (key) {
            case "someValue":
                //this.options.someValue = doSomethingWith( value );
                break;
            default:
                //this.options[ key ] = value;
                break;
            }

            // For UI 1.8, _setOption must be manually invoked from the base widget
            $.Widget.prototype._setOption.apply(this, arguments);
            // For UI 1.9 the _super method can be used instead
            //this._super( "_setOption", key, value );
        }
    });

})(jQuery, window, document);
```

```javascript
/*
****************************************************************
jQuery plugin skeleton using extend pattern 
by @oscargodson with input from @timmywil
note: needs comments
****************************************************************
*/

;(function($){
    $.fn.extend({
        pluginname: function(options) {
            this.defaultOptions = {};
            var settings = $.extend({}, this.defaultOptions, options);
            return this.each(function() {
                var $this = $(this);
            });
        }
    });
})(jQuery);
```

```javascript
/*
**************************************************************
jQueryUI 1.8 widget pattern demonstrating custom event pub/sub 
fore more info read: http://bit.ly/cKAmDa
Use jQuery’s custom events to enable publish/speak and subscribe/
listen into widgets. Each widget would publish certain events and 
subscribe to others. This approach effectively decouples the widgets 
and allows them to function independently.
note from addy: if you would prefer to use pub/sub here instead
you can either implement something lightweight based on ben alman's
pub/sub or use a mediator to publish/subscribe instead.
**************************************************************
*/

(function(){
    $.widget("ui.ajaxStatus", {
        options: {

        },
        _create : function() {
            var self = this;

            self.element.addClass("dpui-widget")
            self.element.bind("dpui:ajaxStart", function(e) {
                console.log("ajax start");
            });

            self.element.bind("dpui:ajaxEnd", function(e) {
                console.log("ajax end");
            });
        },
        destroy: function(){
            $.Widget.prototype.destroy.apply(this, arguments);
        },
    });
});

//usage: $(".dpui-widget").trigger("dpui:ajaxStart");
```

```javascript
/*
***********************************************
Namespaced Starter Template from @dougneiner
***********************************************
*/

(function ($) {
    if (!$.myNamespace) {
        $.myNamespace = new Object();
    };

    $.myNamespace.myPluginName = function (el, myFunctionParam, options) {
        // To avoid scope issues, use 'base' instead of 'this'
        // to reference this class from internal events and functions.
        var base = this;

        // Access to jQuery and DOM versions of element
        base.$el = $(el);
        base.el = el;

        // Add a reverse reference to the DOM object
        base.$el.data("myNamespace.myPluginName", base);

        base.init = function () {
            base.myFunctionParam = myFunctionParam;

            base.options = $.extend({}, $.myNamespace.myPluginName.defaultOptions, options);

            // Put your initialization code here
        };

        // Sample Function, Uncomment to use
        // base.functionName = function(paramaters){
        // 
        // };
        // Run initializer
        base.init();
    };

    $.myNamespace.myPluginName.defaultOptions = {
        myDefaultValue: ""
    };

    $.fn.mynamespace_myPluginName = function (myFunctionParam, options) {
        return this.each(function () {
            (new $.myNamespace.myPluginName(this, myFunctionParam, options));
        });
    };

})(jQuery);
```

```javascript
/*
***************************************************************
A lite (non jQueryUI) widget pattern for plugins from @cowboy
***************************************************************
*/

/*!
 * jQuery simpleWidget - v0.1pre - 10/28/2010
 * http://benalman.com/
 * 
 * Copyright (c) 2010 "Cowboy" Ben Alman
 * Dual licensed under the MIT and GPL licenses.
 * http://benalman.com/about/license/
 */

(function($,undefined){
  '$:nomunge'; // Used by YUI compressor.
  
  $.simpleWidget = function( widget_name, widget ) {
    
    // Create selector.
    $.expr[':'][ widget_name ] = function( elem ) {
      return !!$.data( elem, widget_name );
    };
    
    // Create plugin method.
    $.fn[ widget_name ] = function( options ) {
      var args,
        args_to_slice = 0,
        method_name = '_create',
        result;
      
      // Was a method name passed as the first argument?
      if ( typeof options === 'string' && $.isFunction( widget[ options ] ) ) {
        method_name = options;
        args_to_slice = 1;
      }
      
      // Parse the passed arguments.
      args = Array.prototype.slice.call( arguments, args_to_slice );
      
      // Call the appropriate method in the context of each passed element's
      // instance.
      this.each(function(){
        var elem = $(this),
          data = elem.data( widget_name ),
          created = data,
          method;
        
        // If widget has no data, initialize instance data.
        data || elem.data( widget_name, data = $.extend( {}, widget, {
          element: elem,
          options: options
        }));
        
        // Only execute method when appropriate.
        if ( created ? method_name !== '_create' : method_name !== 'destroy' ) {
          method = data[ method_name ];
          result = $.isFunction( method ) && method.apply( data, args );
        }
        
        if ( method_name === 'destroy' ) {
          // If destroying a widget, remove instance data.
          elem.removeData( widget_name );
          
        } else if ( result !== undefined ) {
          // If method returned a non-undefined value, break out of the each.
          return false;
        }
      });
      
      // If method returned a non-undefined value, return that value (this will
      // break the chain).
      return result !== undefined ? result : this;
    };
  };
  
})(jQuery);
```

```javascript
/*
***********************************************
Light plugin with public/private methods from @cowboy
***********************************************
*/

(function($){
  
  var private_var;
  
  $.myNS = {
    public_method1: function(){
      private_method();
    },
    public_method2: function(){
      return private_var;
    }
  };
  
  function private_method() {
    $.myNS.public_method2();
  }
  
})(jQuery);
```
