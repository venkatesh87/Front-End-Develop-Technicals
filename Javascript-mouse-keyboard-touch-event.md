### I. Javascript Mouse, Keyboard, Touch event.
---
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

>**```onmouseover```/```onmouseout``` - When the mouse passes over an element**:
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

>**```mouseover```/```mouseout``` - When pressing/releasing a mouse button**:
- ```mouseover```: Sự kiện di chuột xảy ra khi con trỏ chuột nằm trên phần tử được chọn.
- ```mouseout```: Sự kiện onmouseout xảy ra khi con trỏ chuột được di chuyển ra khỏi phần tử.

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

<script>
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
</script>
```

>**```onmousedown```/```onmouseup``` - When pressing/releasing a mouse button**:
- ```onmousedown```: Sự kiện onmousedown xảy ra khi người dùng nhấn một nút chuột trên một phần tử.
- ```onmouseup```:  Sự kiện onmouseup xảy ra khi người dùng thả một nút chuột lên một phần tử.
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

>```**mousedown``` - When mouse is clicked: Alert which element, ```mouseup``` - When mouse is clicked: Alert which button**:
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

>**```onmousemove```/```onmouseout``` - When moving the mouse pointer over/out of an image**:
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

**2. Click Events**

>**```onclick``` - When button is clicked**:
```javascript

```
>```ondblclick``` - When a text is double-clicked:
```javascript

```

**3. Load Events**

>**```onload``` - When the page has been loaded**:
```javascript

```
>**```onerror``` - When an error occurs when loading an image**:
```javascript

```

>**```onunload``` - When the browser closes the document**:
```javascript

```

>**```onresize``` - When the browser window is resized**:
```javascript

```

**4. Input Events**

>**```onblur``` - When a user leaves an input field**:
```javascript

```

>**```onchange``` - When a user changes the content of an input field**:
```javascript

```

>**```onchange``` - When a user selects a dropdown value**:
```javascript

```

>**```onfocus``` - When an input field gets focus**:
```javascript

```

>**```onselect``` - When input text is selected**:
```javascript

```

>**```onsubmit``` - When a user clicks the submit button**:
```javascript

```

>**```onreset``` - When a user clicks the reset button**:
```javascript

```

>**```onkeydown``` - When a user is pressing/holding down a key**:
```javascript

```

>**```onkeypress``` - When a user is pressing/holding down a key**:
```javascript

```

>**```onkeyup``` - When the user releases a key**:
```javascript

```

>**```onkeyup``` - When the user releases a key**:
```javascript

```

>**```onkeydown``` vs ```onkeyup``` - Both**:
```javascript

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

