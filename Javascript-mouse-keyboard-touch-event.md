### I. Javascript Mouse, Keyboard, Touch event.
---
- Phương thức ```addEventListener()``` không được hỗ trợ trong Internet Explorer 8 và các phiên bản trước đó.
>**Nếu trình duyệt hỗ trợ sự kiện con trỏ**
```javascript
pointerdown: Con trỏ được nhấn
pointerup: Phát hành con trỏ
pointerleave: Con trỏ ra ngoài khu vực
pointermove: Con trỏ đang di chuyển
```

>**Thêm tất cả sự kiện của trình nghe chuột fallback của người nghe**
```javascript
mousedown: Nhấn chuột
mouseup: Nhả chuột
mouseleave: Chuột ra khỏi khu vực
mousemove: Chuột đang di chuyển
```

>**Thêm tất cả sự kiện chạm vào người nghe lại dự phòng**
```javascript
touchstart: ngón tay chạm vào màn hình
touchend: Ngón tay không còn chạm vào màn hình nữa
touchmove: ngón tay đang di chuyển
```

**1. Mouse Events**

>**```onmouseover```/```onmouseout```**:
- ```mouseover```: Sự kiện di chuột xảy ra khi con trỏ chuột nằm trên phần tử được chọn.
- ```mouseout```: Sự kiện onmouseout xảy ra khi con trỏ chuột được di chuyển ra khỏi phần tử.
```javascript
<img onmouseover="bigImg(this)" onmouseout="normalImg(this)" border="0" src="smiley.gif" alt="Smiley" width="32" height="32">
```

```javascript
function bigImg(x) {
    x.style.height = "64px";
    x.style.width = "64px";
}
function normalImg(x) {
    x.style.height = "32px";
    x.style.width = "32px";
}
```

```javascript
document.getElementById("demo").onmouseover = function() {mouseOver()};
document.getElementById("demo").onmouseout = function() {mouseOut()};
function mouseOver() {
  document.getElementById("demo").style.color = "red";
}
function mouseOut() {
  document.getElementById("demo").style.color = "black";
}
```

```javascript
document.getElementById("demo").addEventListener("mouseover", mouseOver);
document.getElementById("demo").addEventListener("mouseout", mouseOut);
function mouseOver() {
  document.getElementById("demo").style.color = "red";
}
function mouseOut() {
  document.getElementById("demo").style.color = "black";
}
```

```
<ul id="test">
  <li>item 1</li>
  <li>item 2</li>
  <li>item 3</li>
</ul>
```
```javascript
var test = document.getElementById("test");

// this handler will be executed only once when the cursor moves over the unordered list
test.addEventListener("mouseenter", function( event ) {   
// highlight the mouseenter target
event.target.style.color = "purple";

// reset the color after a short delay
setTimeout(function() {
  event.target.style.color = "";
}, 500);
}, false);

// this handler will be executed every time the cursor is moved over a different list item
test.addEventListener("mouseover", function( event ) {   
// highlight the mouseover target
event.target.style.color = "orange";

// reset the color after a short delay
setTimeout(function() {
  event.target.style.color = "";
}, 500);
}, false);
```

>**```onmousedown```/```onmouseup``` - When pressing/releasing a mouse button**:
- ```onmousedown```: Sự kiện onmousedown xảy ra khi người dùng nhấn một nút chuột trên một phần tử.
- ```onmouseup```:  Sự kiện onmouseup xảy ra khi người dùng thả một nút chuột lên một phần tử.

```javascript
<p id="demo" onmousedown="mouseDown()" onmouseup="mouseUp()">Click me.</p>
function mouseDown() {
  document.getElementById("demo").innerHTML = "The mouse button is held down.";
}
function mouseUp() {
  document.getElementById("demo").innerHTML = "You released the mouse button.";
}
```

```javascript
document.getElementById("demo").onmousedown = function() {mouseDown()};
document.getElementById("demo").onmouseup = function() {mouseUp()};
function mouseDown() {
  document.getElementById("demo").innerHTML = "The mouse button is held down.";
}
function mouseUp() {
  document.getElementById("demo").innerHTML = "You released the mouse button.";
}
```

```javascript
document.getElementById("demo").addEventListener("mousedown", mouseDown);
document.getElementById("demo").addEventListener("mouseup", mouseUp);
function mouseDown() {
  document.getElementById("demo").innerHTML = "The mouse button is held down.";
}
function mouseUp() {
  document.getElementById("demo").innerHTML = "You released the mouse button.";
}
```

>**```onmousemove```**:
- ```onmousemove```: Sự kiện onmousemove xảy ra khi con trỏ đang di chuyển trong khi nó ở trên một phần tử.
```
<div onmousemove="myFunction(event)" onmouseout="clearCoor()"></div>
```

```javascript
function myFunction(e) {
  var x = e.clientX;
  var y = e.clientY;
  var coor = "Coordinates: (" + x + "," + y + ")";
  document.getElementById("demo").innerHTML = coor;
}
function clearCoor() {
  document.getElementById("demo").innerHTML = "";
}
```

```javascript
document.getElementById("myDIV").onmousemove = function(event) {myFunction(event)};
function myFunction(e) {
  var x = e.clientX;
  var y = e.clientY;
  var coor = "Coordinates: (" + x + "," + y + ")";
  document.getElementById("demo").innerHTML = coor;
}
```

```javascript
document.getElementById("myDIV").addEventListener("mousemove", function(event) {
    myFunction(event);
});
function myFunction(e) {
  var x = e.clientX;
  var y = e.clientY;
  var coor = "Coordinates: (" + x + "," + y + ")";
  document.getElementById("demo").innerHTML = coor;
}
```

>**```onmouseenter```/```onmouseleave```**:
- Sự kiện ```onmouseenter``` xảy ra khi con trỏ chuột được di chuyển vào một phần tử.
- Sự kiện này thường được sử dụng cùng với sự kiện ```onmouseleave``` xảy ra khi con trỏ chuột được di chuyển ra khỏi một phần tử.
- Sự kiện onmouseenter tương tự như sự kiện ```onmouseover```. Sự khác biệt duy nhất là sự kiện ```onmouseenter``` không bong bóng (không phổ biến lên hệ thống phân cấp tài liệu)

```javascript
<h1 id="demo" onmouseenter="mouseEnter()" onmouseleave="mouseLeave()">Mouse over me</h1>
function mouseEnter() {
  document.getElementById("demo").style.color = "red";
}
function mouseLeave() {
  document.getElementById("demo").style.color = "black";
}
```

```javascript
document.getElementById("demo").onmouseenter = function() {mouseEnter()};
document.getElementById("demo").onmouseleave = function() {mouseLeave()};
function mouseEnter() {
  document.getElementById("demo").style.color = "red";
}
function mouseLeave() {
  document.getElementById("demo").style.color = "black";
}
```

```javascript
document.getElementById("demo").addEventListener("mouseenter", mouseEnter);
document.getElementById("demo").addEventListener("mouseleave", mouseLeave);
function mouseEnter() {
  document.getElementById("demo").style.color = "red";
}
function mouseLeave() {
  document.getElementById("demo").style.color = "black";
}
```

**2. Click Events**

>**```onclick``` - When button is clicked**:
```
<p id="demo" onclick="myFunction()">Click me.</p>
function myFunction() {
  document.getElementById("demo").innerHTML = "YOU CLICKED ME!";
}
```

```javascript
document.getElementById("demo").onclick = function() {myFunction()};
function myFunction() {
  document.getElementById("demo").innerHTML = "YOU CLICKED ME!";
}
```

```javascript
document.getElementById("demo").addEventListener("click", myFunction);
function myFunction() {
  document.getElementById("demo").innerHTML = "YOU CLICKED ME!";
}
```

>**```ondblclick``` - When a text is double-clicked**:
- Sự kiện ondblclick xảy ra khi người dùng nhấp đúp vào một phần tử.

```javascript
<p id="demo" ondblclick="myFunction()">Double-click me.</p>
function myFunction() {
  document.getElementById("demo").innerHTML = "I was double-clicked!";
}
```

```javascript
document.getElementById("demo").ondblclick = function() {myFunction()};
function myFunction() {
  document.getElementById("demo").innerHTML = "I was double-clicked!";
}
```

```javascript
document.getElementById("demo").addEventListener("dblclick", myFunction);
function myFunction() {
  document.getElementById("demo").innerHTML = "I was double-clicked!";
}
```

**3. Load Events**

>**```onload``` - When the page has been loaded**:
- Sự kiện ```onload``` xảy ra khi một đối tượng đã được nạp.
- ```onload``` thường được sử dụng trong phần tử ```<body>``` để thực thi một tập lệnh khi một trang web đã tải xong toàn bộ nội dung (bao gồm cả hình ảnh, tệp kịch bản, các tệp CSS, v.v ...).

```javascript
<iframe onload="myFunction()" src="/default.asp"></iframe>
function myFunction() {
    document.getElementById("demo").innerHTML = "Iframe is loaded.";
}
```

```javascript
document.getElementById("myFrame").onload = function() {myFunction()};
function myFunction() {
  document.getElementById("demo").innerHTML = "Iframe is loaded.";
}
```

```javascript
document.getElementById("myFrame").addEventListener("load", myFunction);
function myFunction() {
  document.getElementById("demo").innerHTML = "Iframe is loaded.";
}
```

>**```onerror``` - When an error occurs when loading an image**:
- Sự kiện ```onerror``` được kích hoạt nếu xảy ra lỗi khi tải tệp tin bên ngoài 
```javascript
<img src="image.gif" onerror="myFunction()">
<p id="demo"></p>
function myFunction() {
  document.getElementById("demo").innerHTML = "The image could not be loaded.";
}
```

```javascript
document.getElementById("myImg").onerror = function() {myFunction()};
function myFunction() {
  document.getElementById("demo").innerHTML = "The image could not be loaded.";
}
```

```javascript
document.getElementById("myImg").addEventListener("error", myFunction);
function myFunction() {
  document.getElementById("demo").innerHTML = "The image could not be loaded.";
}
```

>**```onunload``` - When the browser closes the document**:
- Thuộc tính ```onunload``` sẽ kích hoạt khi trang đã được dỡ xuống (hoặc cửa sổ trình duyệt đã bị đóng).
- ```onunload``` xảy ra khi người dùng điều hướng khỏi trang (bằng cách nhấp vào liên kết, gửi biểu mẫu, đóng cửa sổ trình duyệt ...)
- Nếu bạn tải lại trang, bạn cũng sẽ kích hoạt sự kiện onunload (và sự kiện tải lên).

```javascript
<body onunload="myFunction()">
function myFunction() {
  alert("Thank you for visiting W3Schools!");
}
```

>**```onresize``` - When the browser window is resized**:
- Sự kiện onresize xảy ra khi cửa sổ trình duyệt đã được thay đổi kích cỡ.

```javascript
<body onresize="myFunction()">
function myFunction() {
  var w = window.outerWidth;
  var h = window.outerHeight;
  var txt = "Window size: width=" + w + ", height=" + h;
  document.getElementById("demo").innerHTML = txt;
}
</script>
```

```javascript
document.getElementsByTagName("BODY")[0].onresize = function() {myFunction()};
var x = 0;
function myFunction() {
  var txt = x += 1;
  document.getElementById("demo").innerHTML = txt;
}
```

```javascript
window.addEventListener("resize", myFunction);
var x = 0;
function myFunction() {
  var txt = x += 1;
  document.getElementById("demo").innerHTML = txt;
}
```

**4. Input Events**

>**```onblur``` - When a user leaves an input field**:
- Sự kiện ```onblur``` xảy ra khi một đối tượng mất ```focus```.
- Sự kiện ```onblur``` thường được sử dụng với mã form validation (ví dụ: khi người dùng bỏ một form field).
- Sự kiện ```onblur``` là sự phản đối của sự kiện ```onfocus```.
- Sự kiện ```onblur``` tương tự như sự kiện onfocusout. Sự khác biệt chính là sự kiện onblur không bong bóng. Do đó, nếu bạn muốn tìm hiểu xem một phần tử hoặc con của nó có mất tập trung, bạn có thể sử dụng sự kiện ```onfocusout```. Tuy nhiên, bạn có thể đạt được điều này bằng cách sử dụng tham số optionalCapture tùy chọn của phương thức ```addEventListener()``` cho sự kiện onblur.

```javascript
<input type="text" onblur="myFunction()">
function myFunction() {
  alert("Input field lost focus.");
}
```

```javascript
document.getElementById("fname").onblur = function() {myFunction()};
function myFunction() {
  alert("Input field lost focus.");
}
```

```javascript
document.getElementById("fname").addEventListener("blur", myFunction);
function myFunction() {
  alert("Input field lost focus.");
}
```

>**```onchange``` - When a user changes the content of an input field**:
- Sự kiện ```onchange``` xảy ra khi giá trị của một phần tử đã được thay đổi.
- Đối với các nút ```radio``` và hộp kiểm, sự kiện ```onchange``` xảy ra khi trạng thái đã kiểm tra đã được thay đổi.
- Sự kiện này tương tự như sự kiện ```oninput```. Sự khác biệt là sự kiện ```oninput``` xảy ra ngay sau khi giá trị của một phần tử đã thay đổi, trong khi onchange xảy ra khi phần tử mất tiêu điểm, sau khi nội dung đã được thay đổi. Sự khác biệt khác là sự kiện ```onchange``` cũng hoạt động trên các phần tử ```<select>```.

```javascript
<input type="text" id="fname" onchange="myFunction()">
function myFunction() {
  var x = document.getElementById("fname");
  x.value = x.value.toUpperCase();
}
```

```javascript
document.getElementById("fname").onchange = function() {myFunction()};
function myFunction() {
 var x = document.getElementById("fname");
 x.value = x.value.toUpperCase();
}
```

```javascript
document.getElementById("fname").addEventListener("change", myFunction);
function myFunction() {
  var x = document.getElementById("fname");
  x.value = x.value.toUpperCase();
}
```

>**```onchange``` - When a user selects a dropdown value**:
- Thực thi JavaScript khi người dùng thay đổi tùy chọn đã chọn của phần tử ```<select>```
```javascript
<select id="mySelect" onchange="myFunction()">
  <option value="Audi">Audi
  <option value="BMW">BMW
  <option value="Mercedes">Mercedes
  <option value="Volvo">Volvo
</select>
function myFunction() {
    var x = document.getElementById("mySelect").value;
    document.getElementById("demo").innerHTML = "You selected: " + x;
}
```

>**```onfocus``` - When an input field gets focus**:
- Sự kiện ```onfocus``` xảy ra khi một phần tử được focus.
- Sự kiện ```onfocus``` thường được sử dụng với ```<input>```, ```<select>``` và ```<a>```.
- Sự kiện ```onfocus``` là sự đối ngược với sự kiện ```onblur```.
- Sự kiện ```onfocus``` tương tự như sự kiện ```onfocusin```. Sự khác biệt chính là sự kiện ```onfocus``` không bong bóng. Vì vậy, nếu bạn muốn tìm hiểu xem một phần tử hoặc con của nó có được tiêu điểm, bạn có thể sử dụng sự kiện ```onfocusin```. Tuy nhiên, bạn có thể đạt được điều này bằng cách sử dụng tham số ```optionalCapture``` tùy chọn của phương thức ```addEventListener()``` cho sự kiện ```onfocus```.

```javascript
Enter your name: <input type="text" id="fname" onfocus="myFunction()">
function myFunction() {
  document.getElementById("fname").style.backgroundColor = "red";
}
```

```javascript
Enter your name: <input type="text" id="fname">
document.getElementById("fname").onfocus = function() {myFunction()};
function myFunction() {
  document.getElementById("fname").style.backgroundColor = "red";
}
```

```javascript
Enter your name: <input type="text" id="fname">
document.getElementById("fname").addEventListener("focus", myFunction);
function myFunction() {
  document.getElementById("fname").style.backgroundColor = "red";
}
```

```javascript
Enter your name: <input type="text" id="myInput" onfocus="focusFunction()" onblur="blurFunction()">
function focusFunction() {
  // Focus = Changes the background color of input to yellow
  document.getElementById("myInput").style.background = "yellow";
}

function blurFunction() {
  // No focus = Changes the background color of input to red
  document.getElementById("myInput").style.background = "red";
}
```

```javascript
<input type="text" onfocus="this.value=''" value="Blabla">
```

```javascript
var x = document.getElementById("myForm");
x.addEventListener("focus", myFocusFunction, true);
x.addEventListener("blur", myBlurFunction, true);

function myFocusFunction() {
  document.getElementById("myInput").style.backgroundColor = "yellow";  
}

function myBlurFunction() {
  document.getElementById("myInput").style.backgroundColor = "";  
}
```

```javascript
var x = document.getElementById("myForm");
x.addEventListener("focusin", myFocusFunction);
x.addEventListener("focusout", myBlurFunction);

function myFocusFunction() {
  document.getElementById("myInput").style.backgroundColor = "yellow";
}

function myBlurFunction() {
  document.getElementById("myInput").style.backgroundColor = "";  
}
```
>**```onselect``` - When input text is selected**:
- Sự kiện ```onselect``` xảy ra sau khi một số văn bản đã được chọn trong một phần tử.
- Sự kiện ```onselect``` chủ yếu được sử dụng trên các phần tử ```<input type = "text">``` hoặc ```<textarea>```.

```javascript
Select some text: <input type="text" value="Hello world!" onselect="myFunction()">
function myFunction() {
  document.getElementById("demo").innerHTML = "You selected some text!";
}
```

```javascript
Select some text: <input type="text" value="Hello world!" id="myText">
document.getElementById("myText").onselect = function() {myFunction()};
function myFunction() {
  document.getElementById("demo").innerHTML = "You selected some text!";
}
```

```javascript
document.getElementById("myText").addEventListener("select", myFunction);

function myFunction() {
  document.getElementById("demo").innerHTML = "You selected some text!";
}
```

>**```onsubmit``` - When a user clicks the submit button**:
- Thuộc tính ```onsubmit``` được kích hoạt khi một biểu mẫu được gửi.
```javascript
<form action="/action_page.php" onsubmit="myFunction()">
  Enter name: <input type="text" name="fname">
  <input type="submit" value="Submit">
</form>
function myFunction() {
  alert("The form was submitted");
}
```

```javascript
<form id="myForm" action="/action_page.php">
  Enter name: <input type="text" name="fname">
  <input type="submit" value="Submit">
</form>
document.getElementById("myForm").onsubmit = function() {myFunction()};
function myFunction() {
  alert("The form was submitted");
}
```

```javascript
document.getElementById("myForm").addEventListener("submit", myFunction);
function myFunction() {
  alert("The form was submitted");
}
```

>**```onreset``` - When a user clicks the reset button**:
- The onreset event occurs when a form is reset.
```javascript
<form onreset="myFunction()">
  Enter name: <input type="text">
  <input type="reset">
</form>
function myFunction() {
  document.getElementById("demo").innerHTML = "The form was reset";
}
```

```javascript
<form id="myForm">
  Enter name: <input type="text">
  <input type="reset">
</form>
document.getElementById("myForm").onreset = function() {myFunction()};
function myFunction() {
  document.getElementById("demo").innerHTML = "The form was reset";
}
```

```javascript
<form id="myForm">
  Enter name: <input type="text">
  <input type="reset">
</form>
document.getElementById("myForm").addEventListener("reset", myFunction);
function myFunction() {
  document.getElementById("demo").innerHTML = "The form was reset";
}
```

>**```onkeydown``` - When a user is pressing/holding down a key**:
- Sự kiện ```onkeydown``` xảy ra khi người dùng nhấn một phím (trên bàn phím).

```javascript
<input type="text" id="demo" onkeydown="myFunction()">
function myFunction() {
  document.getElementById("demo").style.backgroundColor = "red";
}
```

```javascript
document.getElementById("demo").onkeydown = function() {myFunction()};
function myFunction() {
  document.getElementById("demo").style.backgroundColor = "red";
}
```

```javascript
document.getElementById("demo").addEventListener("keydown", myFunction);
function myFunction() {
  document.getElementById("demo").style.backgroundColor = "red";
}
```

>**```onkeypress``` - When a user is pressing/holding down a key**:
- Sự kiện ```onkeypress``` xảy ra khi người dùng nhấn một phím (trên bàn phím).

```javascript
<input type="text" id="demo" onkeypress="myFunction()">
function myFunction() {
  document.getElementById("demo").style.backgroundColor = "red";
}
```

```javascript
document.getElementById("demo").onkeypress = function() {myFunction()};
function myFunction() {
  document.getElementById("demo").style.backgroundColor = "red";
}
```

```javascript
document.getElementById("demo").addEventListener("keypress", myFunction);
function myFunction() {
  document.getElementById("demo").style.backgroundColor = "red";
}
```

>**```onkeyup``` - When the user releases a key**:
- Sự kiện ```onkeyup``` xảy ra khi người dùng giải phóng một phím (trên bàn phím).

```javascript
Enter your name: <input type="text" id="fname" onkeyup="myFunction()">
function myFunction() {
  var x = document.getElementById("fname");
  x.value = x.value.toUpperCase();
}
```

```javascript
Enter your name: <input type="text" id="fname">
document.getElementById("fname").onkeyup = function() {myFunction()};
function myFunction() {
  var x = document.getElementById("fname");
  x.value = x.value.toUpperCase();
}
```

```javascript
Enter your name: <input type="text" id="fname">
document.getElementById("fname").addEventListener("keyup", myFunction);
function myFunction() {
    var x = document.getElementById("fname");
    x.value = x.value.toUpperCase();
}
```

```javascript
var svg = document.querySelector('svg');

// If browser supports pointer events
if (window.PointerEvent) {
  svg.addEventListener('pointerdown', onPointerDown); // Pointer is pressed
  svg.addEventListener('pointerup', onPointerUp); // Releasing the pointer
  svg.addEventListener('pointerleave', onPointerUp); // Pointer gets out of the SVG area
  svg.addEventListener('pointermove', onPointerMove); // Pointer is moving
} else {
  // Add all mouse events listeners fallback
  svg.addEventListener('mousedown', onPointerDown); // Pressing the mouse
  svg.addEventListener('mouseup', onPointerUp); // Releasing the mouse
  svg.addEventListener('mouseleave', onPointerUp); // Mouse gets out of the SVG area
  svg.addEventListener('mousemove', onPointerMove); // Mouse is moving

  // Add all touch events listeners fallback
  svg.addEventListener('touchstart', onPointerDown); // Finger is touching the screen
  svg.addEventListener('touchend', onPointerUp); // Finger is no longer touching the screen
  svg.addEventListener('touchmove', onPointerMove); // Finger is moving
}
```

