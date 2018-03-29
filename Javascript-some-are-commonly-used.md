#### I. JavaScript array - Exercises, Practice, Solution
---

**1. JavaScript Window**

>**window, width, height**
- Global variables are properties of the window object.
- Global functions are methods of the window object.
- The browser window (the browser viewport) is NOT including toolbars and scrollbars.(Cửa sổ trình duyệt (khung nhìn trình duyệt) KHÔNG bao gồm thanh công cụ và thanh cuộn.)
```javascript
window.addEventListener("scroll", function(e) {
  m = window.pageYOffset || document.documentElement.scrollTop;
})
```

```javascript
var w = window.innerWidth
|| document.documentElement.clientWidth
|| document.body.clientWidth;

var h = window.innerHeight
|| document.documentElement.clientHeight
|| document.body.clientHeight;

var x = document.getElementById("demo");
x.innerHTML = "Browser inner window width: " + w + ", height: " + h + ".";
```
**2. JavaScript Window Screen**

- The window.screen object can be written without the window prefix.(Đối tượng window.screen có thể được viết mà không có tiền tố cửa sổ.)

```javascript
screen.width
screen.height
screen.availWidth
screen.availHeight
screen.colorDepth
screen.pixelDepth
```

```javascript
document.getElementById("demo").innerHTML = "Screen Width: " + screen.width;
```

```javascript
document.getElementById("demo").innerHTML = "Screen Height: " + screen.height;
```

**2. addEventListener**

```javascript
element.addEventListener("mouseover", myFunction);
element.addEventListener("click", mySecondFunction);
element.addEventListener("mouseout", myThirdFunction);
element.addEventListener("resize", myThirdFunction);
element.addEventListener("mousemove", myThirdFunction);
```

**3. offsetHeight , offsetLeft, offsetParent, offsetTop, offsetWidth**
```javascript

```

**4. scrollX, scrollY**

>**scrollX**
```javascript
if (window.scrollX > 400) {
  window.scroll(0,0);
}
```
- The ```pageXOffset``` property is an alias for the ```scrollX``` property(Thuộc tính ```pageXOffset``` là một bí danh cho thuộc tính ```scrollX```): 
```javascript
window.pageXOffset == window.scrollX; // always true
```

>**scrollY**
```javascript
// make sure and go down to the second page 
if (window.scrollY) {
  window.scroll(0, 0);  // reset the scroll position to the top left of the document.
}
window.scrollByPages(1);
```

**5. screen, screenX, screenY**

>**screen**
- Returns a reference to the screen object associated with the window. The screen object, implementing the Screen interface, is a special object for inspecting properties of the screen on which the current window is being rendered.
- Trả về một tham chiếu đến đối tượng màn hình liên kết với cửa sổ. Đối tượng màn hình, thực hiện giao diện Screen, là một đối tượng đặc biệt để kiểm tra các thuộc tính của màn hình mà trên đó cửa sổ đang được hiển thị.

```javascript
screenObj = window.screen;
```

>**screenX**
- The ```Window.screenX``` read-only property returns the horizontal distance, in CSS pixels, of the left border of the user's browser from the left side of the screen.
- Thuộc tính chỉ đọc ```Window.screenX``` trả về khoảng cách ngang, trong pixel CSS, của đường biên bên trái của trình duyệt của người dùng từ phía bên trái của màn hình.

```javascript
lLoc = window.screenX 
```

>**screenY**
- The ```Window.screenY``` read-only property returns the vertical distance, in CSS pixels of the top border of the user's browser from the top edge of the screen.
- Thuộc tính chỉ đọc ```Window.screenY``` trả về khoảng cách theo chiều dọc, trong pixel CSS của đường viền trên của trình duyệt của người dùng từ cạnh trên của màn hình.

```javascript
lLoc = window.screenY
```

**6. pageXOffset, pageYOffset**

>**pageXOffset**

- Đây là bí danh cho scrollX

```javascript
xOffset = window.pageXOffset;
```

>**pageYOffset**

- Trang thuộc tính chỉ đọc WindowYOffset là một bí danh cho scrollY;như vậy, nó trả về số pixel mà tài liệu hiện đang cuộn dọc theo trục thẳng đứng (nghĩa là, lên hoặc xuống).với một giá trị 0,0 chỉ ra rằng cạnh trên cùng của tài liệu hiện đang được căn chỉnh với cạnh trên cùng của khu vực nội dung của cửa sổ.

```javascript
window.pageYOffset;
yOffset = window.pageYOffset;
```
**7. onresize, onscroll**
```javascript

```

*8. **
```javascript

```

**9. **
```javascript

```

**10. **
```javascript

```

**11. **
```javascript

```
