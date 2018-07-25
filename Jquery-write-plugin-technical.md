#### Advanced Plugin Concepts
---
>**$.fn**
- Ví dụ ```show()``` và ```hide()``` là 2 hàm nằm trong ```jQuery.fn```
```$``` là viết tắt của jQuery

```fn``` là viết tắt của prototype

>**Nếu viết đầy đủ ra sẽ thế này**

```javascript
window.jQuery.prototype.highlight_link = function(){};
```

>**Để sử dụng plugin trên ta gọi như sau:**

```javascript
$('#1st_link').highlight_link();
```

>**Version added: 1.0** jQuery.extend( target, [ object1 ], [ objectN ])
  + **target** Một đối tượng sẽ nhận các thuộc tính mới nếu các đối tượng bổ sung được truyền vào hoặc sẽ mở rộng vùng tên jQuery nếu nó là đối số duy nhất.
  + **object1**: An đối tượng chứa các thuộc tính bổ sung để hợp nhất.
  + **object n**: Các đối tượng bổ sung có chứa các thuộc tính để hợp nhất.
>**version added: 1.1.4** jQuery.extend( [ deep ], target, object1, [ objectN ] )
  + **deep:** Nếu đúng, quá trình hợp nhất sẽ trở thành đệ quy. 
  + **target** Các đối tượng để mở rộng. Nó sẽ nhận được các thuộc tính mới. 
  + **object1**: An đối tượng chứa các thuộc tính bổ sung để hợp nhất.
  + **object n**: Các đối tượng bổ sung có chứa các thuộc tính để hợp nhất.
>**Hợp nhất hai đối tượng ```modifying the first```**
```javascript
var object1 = {
  apple: 0,
  banana: {weight: 52, price: 100},
  cherry: 97
};
var object2 = {
  banana: {price: 200},
  durian: 100
};
$.extend(object1, object2);
```
**Result:** ```object1 === {apple: 0, banana: {price: 200}, cherry: 97, durian: 100}```

>**Hợp nhất hai đối tượng Merge two objects ```recursively```, ```modifying the first```**

```javascript
var object1 = {
  apple: 0,
  banana: {weight: 52, price: 100},
  cherry: 97
};
var object2 = {
  banana: {price: 200},
  durian: 100
};

$.extend(true, object1, object2);
```
**Result:** ```object1 === {apple: 0, banana: {weight: 52, price: 200}, cherry: 97, durian: 100}```
>**Hợp nhất settings and options, modifying settings**

```javascript
var settings = { validate: false, limit: 5, name: "foo" };
var options = { validate: true, name: "bar" };
jQuery.extend(settings, options);
```
**Result:** ```settings == { validate: true, limit: 5, name: "bar" }```
```javascript
settings == { validate: true, limit: 5, name: "bar" }
empty == { validate: true, limit: 5, name: "bar" }
```
>**Hợp nhất các giá trị mặc định và tùy chọn mà không sửa đổi các giá trị mặc định. Đây là một mẫu phát triển plugin phổ biến**
```javascript
var empty = {}
var defaults = { validate: false, limit: 5, name: "foo" };
var options = { validate: true, name: "bar" };
var settings = $.extend(empty, defaults, options);
```
**Result:** ```settings == { validate: true, limit: 5, name: "bar" }```

##### 1. Cung cấp quyền truy cập công khai vào Setting Plugin Default:

- Phương thức ```$.extend()``` bây giờ sẽ recurse thông qua tất cả các đối tượng lồng nhau để cung cấp cho chúng ta một phiên bản hợp nhất của cả các giá trị defaults và các options được truyền, cho các options được ưu tiên vượt qua.
>Javascript Code:
```javascript
// Plugin definition.
$.fn.hilight = function( options ) {
    // Extend our default options with those provided.
    // Note that the first argument to extend is an empty(Lưu ý rằng đối số đầu tiên extend là rỗng)
    // object – this is to keep from overriding our "defaults" object.(object - điều này là để tránh ghi đè đối tượng "defaults" của chúng)
    var opts = $.extend( {}, $.fn.hilight.defaults, options );
    // Our plugin implementation code goes here.(Mã triển khai plugin của chúng tôi xuất hiện ở đây)
};
 
// Plugin defaults – added as a property on our plugin function.(Plugin defaults: được thêm dưới dạng thuộc tính trên chức năng plugin của chúng)
$.fn.hilight.defaults = {
    foreground: "red",
    background: "yellow"
};
```

>**Bây giờ người dùng có thể bao gồm một dòng như thế này trong kịch bản của họ:**
```javascript
// This needs only be called once(một lần) and does not
// have to be called from within a "ready" block
$.fn.hilight.defaults.foreground = "blue";
```

>And now we can call the plugin method like this and it will use a blue foreground col:
```javascript
$( "#myDiv" ).hilight();
```
- As you can see, we've allowed the user to write a single line of code to alter the default foreground color of the plugin. And users can still selectively override this new default value when they want(Như bạn có thể thấy, chúng tôi đã cho phép người dùng viết một dòng mã để thay đổi màu nền trước mặc định của plugin. Và người dùng vẫn có thể ghi đè có chọn lọc giá trị mặc định mới này khi họ muốn):
```javascript
// Override plugin default foreground color.
$.fn.hilight.defaults.foreground = "blue";
// ...
// Invoke plugin using new defaults.
$( ".hilightDiv" ).hilight();
// ...
// Override default by passing options to plugin method.
$( "#green" ).hilight({
    foreground: "green"
});
```
##### 2. Provide Public Access to Secondary Functions as Applicable(Cung cấp quyền truy cập công khai vào các hàm phụ như có thể áp dụng):

>Javascript Code:
```javascript
// Plugin definition.
$.fn.hilight = function( options ) {
    // Iterate and reformat each matched element.
    return this.each(function() {
        var elem = $( this );
        // ...
        var markup = elem.html();
        // Call our format function.
        markup = $.fn.hilight.format( markup );
        elem.html( markup );
    });
 
};
 
// Define our format function.
$.fn.hilight.format = function( txt ) {
    return "<strong>" + txt + "</strong>";
};
```
##### 3. Bob and Sue:

>Javascript Code:
```javascript
jQuery.fn.superGallery = function( options ) {
    // Bob's default settings:
    var defaults = {
        textColor: "#000",
        backgroundColor: "#fff",
        fontSize: "1em",
        delay: "quite long",
        getTextFromTitle: true,
        getTextFromRel: false,
        getTextFromAlt: false,
        animateWidth: true,
        animateOpacity: true,
        animateHeight: true,
        animationDuration: 500,
        clickImgToGoToNext: true,
        clickImgToGoToLast: false,
        nextButtonText: "next",
        previousButtonText: "previous",
        nextButtonTextColor: "red",
        previousButtonTextColor: "red"
    };
 
    var settings = $.extend( {}, defaults, options );
 
    return this.each(function() {
        // Plugin code would go here...
    });
 
};
```

>Javascript Code:
```javascript
var defaults = {
    wrapperAttrs : {
        class: "gallery-wrapper"
    },
    // ... rest of settings ...
};
 
// We can use the extend method to merge options/settings as usual:
// But with the added first parameter of TRUE to signify a DEEP COPY:
var settings = $.extend( true, {}, defaults, options );
```
##### 4. Provide Callback Capabilities:
- Callback là gì? - Một Callback về cơ bản là một hàm được gọi sau, thường được kích hoạt(```triggered```) bởi một event. Nó được chuyển như một đối số(argument), thường là lời gọi khởi tạo của một thành phần, trong trường hợp này là một plugin jQuery.
>Javascript Code:
```javascript
var defaults = {
    // We define an empty anonymous function so that
    // we don't need to check its existence before calling it.
    onImageShow : function() {},
    // ... rest of settings ...
};
// Later on in the plugin:
nextButton.on( "click", showNextImage );
 
function showNextImage() {
 
    // Returns reference to the next image node
    var image = getNextImage();
 
    // Stuff to show the image here...
 
    // Here's the callback:
    settings.onImageShow.call( image );
}
```

>**Cú pháp cơ bản để tạo một jQuery Plugin**:
```javascript
$.fn.your_function_name = function() {
  //your code write here
}
```

```javascript
$('#1st_link').mouseover(function(){
	$(this).css('color', 'red');
	$(this).css('font-size', '30px');
});
$('#1st_link').mouseout(function(){
	$(this).css('color', 'white');
	$(this).css('font-size', '15px');
});
```

```javascript
$.fn.highlight_link = function() {
	this.mouseover(function(){
		$(this).css('color', 'red');
		$(this).css('font-size', '30px');
	});
	this.mouseout(function(){
		$(this).css('color', 'white');
		$(this).css('font-size', '15px');
	});
}
```
**```$``` là viết tắt của jQuery**
**```fn``` là viết tắt của prototype**: Nếu viết đầy đủ ra sẽ thế này
```javascript
window.jQuery.prototype.highlight_link = function(){};
```
- Để sử dụng plugin trên ta gọi như sau:
```javascript
$('#1st_link').highlight_link();
```

**>Để phương thức plugin trên có thể kết nối chúng ta thêm dòng mã trả về đối tượng jQuery gốc như sau**

```javascript
$.fn.highlight_link = function() {
	this.mouseover(function(){
		...
	});
	this.mouseout(function(){
		...
	});
    return this;
}
```
**>Đầu tiên ta thêm vào các tham số mặc định như sau:**
```javascript
(function ( $ ) {
    $.fn.highlight_link = function() {
    	var defaults = {
        	mouseover_color: 'red',
            mouseover_size: '30px',
            mouseout_color: 'white',
            mouseout_size: '15px'
        };
        var settings = defaults;
        this.mouseover(function(){
            $(this).css('color', settings.mouseover_color);
            $(this).css('font-size', settings.mouseover_size);
        });
        this.mouseout(function(){
            $(this).css('color', settings.mouseout_color);
            $(this).css('font-size', settings.mouseout_size);
        });
        return this;
    }
}( jQuery ));
```

**>Chấp nhận các tham số người dùng truyền vào.**

```javascript
(function ( $ ) {
    $.fn.highlight_link = function(options) {
    	var defaults = {
        	mouseover_color: 'red',
            mouseover_size: '30px',
            mouseout_color: 'white',
            mouseout_size: '15px'
        };
        var settings = $.extend(defaults, options);
        this.mouseover(function(){
            $(this).css('color', settings.mouseover_color);
            $(this).css('font-size', settings.mouseover_size);
        });
        this.mouseout(function(){
            $(this).css('color', settings.mouseout_color);
            $(this).css('font-size', settings.mouseout_size);
        });
        return this;
    }
}( jQuery ));
```

```javascript
$('#1st_link').highlight_link({
	  mouseover_color: '#FFFF00',
    mouseover_size: '50px',
    mouseout_color: '#333333',
    mouseout_size: '15px'
});
```

**Viết một plugin đơn giản**

```javascript
(function( $ ) {
  $.myFunction = function() {
    // viết code vào đây
  };
  $.fn.myPlugin = function() {
    // viết phần code của plugin vào đây
  };
})( jQuery ); 
```

```javascript
(function( $ ) {
  $.say = function(x) {
    alert(x);
  };

  $.fn.makeBlue = function() {
    return this.css("color", "blue");
  };
})( jQuery ); 

$.say("Hello the world!");
$(".abc").makeBlue().show();
```

**Duy trì đặc tính gọi dạng chuỗi của jQuery**

**Truyền tham số**

- Khi viết hàm với jQuery, ta thường định nghĩa tham số default và cho phép người dùng plugin có thể truyền tham số vào hàm, nếu user không truyền vào hay truyền thiếu thì các tham số có giá trị mặc định. Trong trường hợp này ta sử dụng hàm có sẵn $.extend mà jQuery cung cấp:

- ```$.extend``` nhận 2 hoặc nhiềm tham số, nó có nhiệm vụ thêm các method và các biến của tham số từ thứ 2 trở đi vào tham số thứ 1. Phương thức này có tác dụng trộn các đối tượng với nhau và gán kết quả vào đối tượng đầu tiên truyền vào tham số. Các thuộc tính bị trùng của đối tượng đầu tiên sẽ bị ghi đè bởi các đối tượng phía sau.
```javascript
defaults = { size: 3 };
options = { height: 6 };
var opts = $.extend(defaults, options)
// opts == defaults == { size: 3, height: 6 }
// options == { height: 6 };
```

- Ta thường đặt tham số thứ nhất là ```{}``` để không bị ảnh hưởng tới tham số gốc.

```javascript
defaults = { size: 3 };
options = { height: 6 };
var opts = $.extend( {}, defaults, options)
// opts == { size: 3, height: 6 }
// defaults == { size: 3 };
// options == { height: 6 };
```

- Ví dụ đơn giản sử dụng ```$.extend```:

```javascript
(function($) {

  $.fn.textHover = function(options) {

    var defaultVal = {
      Text: 'Your mouse is over',
      ForeColor: 'red',
      BackColor: 'gray'
    };

    var obj = $.extend(defaultVal, options);

    return this.each(function() {

      var selObject = $(this);

      var oldText = selObject.text();
      var oldBgColor = selObject.css("background-color");
      var oldColor = selObject.css("color");

      selObject.hover(function() {
          selObject.text(obj.Text);
          selObject.css("background-color", obj.BackColor);
          selObject.css("color", obj.ForeColor);
        },
        function() {
          selObject.text(oldText);
          selObject.css("background-color", oldBgColor);
          selObject.css("color", oldColor);
        }
      );
    });
  }
})(jQuery);
```

**Nếu sử dụng hiệu ứng chuyển động không cần plugin, mã javascript sẽ như sau:**

```javascript
$(document).ready(function() {
    $('ul#menu li a').mouseover(function() {
        $(this).animate( { paddingLeft:"20px" }, 300);
    }).mouseout(function() {
        $(this).animate( { paddingLeft:"0" }, 300);
    });
});   
```

**Cấu trúc cơ bản của plugin như sau:**

```javascript
//Bạn cần đặt function quanh $ để tránh trường hợp bị trùng lặp
(function($) {
  // Thông báo phương thức tới jQuery
  $.fn.extend({

    //Đây là phần bạn viết tên plugin
    neoanimatemenu: function() {

      // Kiểm tra từng element và xử lý
      return this.each(function() {

        //Thêm mã xử lý ở đây

      });
    }
  });
})(jQuery);
```
- Nhưng nếu viết plugin, chúng ta sẽ chỉ cần gọi:

```javascript
$(document).ready(function() {
  $('#menu').neoAnimateMenu({
    padding: 20
  })
});
```

**Thêm các lựa chọn mặc định cho plugin:**

```javascript
(function($) {
  $.fn.extend({

    // truyền biến options vào hàm
    neoAnimateMenu: function(options) {

      // Đặt các giá trị mặc định, sử dụng dấu phẩy để chia từng giá trị
      var defaults = {
        padding: 20,
        mouseOverColor: '#000000',
        mouseOutColor: '#ffffff'
      }

      var options = $.extend(defaults, options);

      return this.each(function() {
        var opts = options;

        //Thêm mã xử lý ở đây
        alert(opts.padding);

      });
    }
  });

})(jQuery);
```

**Từ cấu trúc trên, chúng ta sẽ sửa thành plugin neoAnimateMenu như sau:**

```javascript
(function($) {
  $.fn.extend({

    neoAnimateMenu: function(options) {

      // Đặt các giá trị mặc định
      var defaults = {
        animatePadding: 60
      };

      var options = $.extend(defaults, options);

      return this.each(function() {
        var opts = options;

        // Đặt tên biến cho element (ul)
        var obj = $(this);

        // Lấy tất cả thẻ li trong ul
        var items = $("li a", obj);

        // Thêm sự kiện mouseover và mouseout vào thẻ a
        items.mouseover(function() {
          // lúc này this chính là thẻ a
          $(this).animate({ paddingLeft: opts.animatePadding }, 500);
        }).mouseout(function() {
          $(this).animate({ paddingLeft: '0' }, 500);
        });
      });
    }
  });
})(jQuery);
```

```javascript
(function($) {
  $.fn.extend({

    fnexample: function(options) {
      var defaults = {
        paddingLeft: 20,
        mouseOverColor: '#000000',
        mouseOutColor: '#ffffff'
      }

      var options = $.extend(defaults, options);

      return this.each(function() {
        var opts = options;
        $(this).click(function() {
          alert(opts.paddingLeft);
        }).css('padding-left', opts.paddingLeft);
      });
    }
  });

})(jQuery);
```
