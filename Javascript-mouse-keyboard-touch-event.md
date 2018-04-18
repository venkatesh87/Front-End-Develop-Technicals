### I. Javascript Mouse, Keyboard, Touch event.
---

**1. Mouse Events**

>```onmouseover```/```onmouseout``` - When the mouse passes over an element:
```javascript

```
>```onmousedown```/```onmouseup``` - When pressing/releasing a mouse button:
```javascript

```

>```onmousedown``` - When mouse is clicked: Alert which element:
```javascript

```

>```onmousedown``` - When mouse is clicked: Alert which button:
```javascript

```

>```onmousemove```/```onmouseout``` - When moving the mouse pointer over/out of an image:
```javascript

```

>```onmouseover```/```onmouseout``` - When moving the mouse over/out of an image:
```javascript

```

>```onmouseover``` an image map:
```javascript

```

**2. Click Events**

>```onclick``` - When button is clicked:
```javascript

```
>```ondblclick``` - When a text is double-clicked:
```javascript

```

**3. Load Events**

>```onload``` - When the page has been loaded:
```javascript

```
>```onerror``` - When an error occurs when loading an image:
```javascript

```

>```onunload``` - When the browser closes the document:
```javascript

```

>```onresize``` - When the browser window is resized:
```javascript

```

**4. Input Events**

>```onblur``` - When a user leaves an input field:
```javascript

```

>```onchange``` - When a user changes the content of an input field:
```javascript

```

>```onchange``` - When a user selects a dropdown value:
```javascript

```

>```onfocus``` - When an input field gets focus:
```javascript

```

>```onselect``` - When input text is selected:
```javascript

```

>```onsubmit``` - When a user clicks the submit button:
```javascript

```

>```onreset``` - When a user clicks the reset button:
```javascript

```

>```onkeydown``` - When a user is pressing/holding down a key:
```javascript

```

>```onkeypress``` - When a user is pressing/holding down a key:
```javascript

```

>```onkeyup``` - When the user releases a key:
```javascript

```

>```onkeyup``` - When the user releases a key:
```javascript

```

>```onkeydown``` vs ```onkeyup``` - Both:
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


>Nếu trình duyệt hỗ trợ sự kiện con trỏ
```javascript
pointerdown: Con trỏ được nhấn
pointerup: Phát hành con trỏ
pointerleave: Con trỏ ra ngoài khu vực
pointermove: Con trỏ đang di chuyển

>Thêm tất cả sự kiện của trình nghe chuột fallback của người nghe
```javascript
mousedown: Nhấn chuột
mouseup: Nhả chuột
mouseleave: Chuột ra khỏi khu vực
mousemove: Chuột đang di chuyển
```

>Thêm tất cả sự kiện chạm vào người nghe lại dự phòng
```javascript
touchstart: ngón tay chạm vào màn hình
touchend: Ngón tay không còn chạm vào màn hình nữa
touchmove: ngón tay đang di chuyển
```
