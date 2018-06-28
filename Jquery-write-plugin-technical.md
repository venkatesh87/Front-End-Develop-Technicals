#### Advanced Plugin Concepts
---
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
**Hợp nhất các giá trị mặc định và tùy chọn mà không sửa đổi các giá trị mặc định. Đây là một mẫu phát triển plugin phổ biến**
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

>Bây giờ người dùng có thể bao gồm một dòng như thế này trong kịch bản của họ:
```javascript
// This needs only be called once(một lần) and does not
// have to be called from within a "ready" block
$.fn.hilight.defaults.foreground = "blue";
```

>And now we can call the plugin method like this and it will use a blue foreground col:
```javascript
$( "#myDiv" ).hilight();
```

>As you can see, we've allowed the user to write a single line of code to alter the default foreground color of the plugin. And users can still selectively override this new default value when they want(Như bạn có thể thấy, chúng tôi đã cho phép người dùng viết một dòng mã để thay đổi màu nền trước mặc định của plugin. Và người dùng vẫn có thể ghi đè có chọn lọc giá trị mặc định mới này khi họ muốn):
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

>Javascript Code:
```javascript

```

>Javascript Code:
```javascript

```

>Javascript Code:
```javascript

```

