#### I. Javascript Some Are Commonly Used
---

**1. JavaScript Window**

>**```window```, ```width```, ```height```**
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
>**2. JavaScript Window Screen**

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

>**3. ```addEventListener```**

```javascript
element.addEventListener("mouseover", myFunction);
element.addEventListener("click", mySecondFunction);
element.addEventListener("mouseout", myThirdFunction);
element.addEventListener("resize", myThirdFunction);
element.addEventListener("mousemove", myThirdFunction);
```

**4. offsetHeight , offsetLeft, offsetParent, offsetTop, offsetWidth**
```javascript

```

**5. ```scrollX```, ```scrollY```**

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

**6. MouseEvent ```screen```, ```screenX```, ```screenY``` Property**

>**screen**
- Returns a reference to the screen object associated with the window. The screen object, implementing the Screen interface, is a special object for inspecting properties of the screen on which the current window is being rendered.
- Trả về một tham chiếu đến đối tượng màn hình liên kết với cửa sổ. Đối tượng màn hình, thực hiện giao diện Screen, là một đối tượng đặc biệt để kiểm tra các thuộc tính của màn hình mà trên đó cửa sổ đang được hiển thị.

```javascript
screenObj = window.screen;
```

>**MouseEvent ```screenX``` Property**
- Thuộc tính ```screenX``` trả về tọa độ ngang (theo màn hình máy tính người dùng) của con trỏ chuột khi một sự kiện được kích hoạt.

```javascript
lLoc = window.screenX 
```

>**MouseEvent ```screenY``` Property**
- Thuộc tính ```screenY``` trả về tọa độ dọc (theo màn hình máy tính người dùng) của con trỏ chuột khi một sự kiện được kích hoạt.

```javascript
lLoc = window.screenY
```

>**6. MouseEvent ```clientX```, ```clientY```**

>**MouseEvent clientX**
- The ```clientX``` property returns the horizontal coordinate (according to the client area) of the mouse pointer when a mouse event was triggered.
- Thuộc tính clientX trả về tọa độ theo chiều ngang (theo client area) của con trỏ chuột khi một sự kiện chuột được kích hoạt.
- The client area is the current window.
- client area là cửa sổ hiện tại.
- To get the vertical coordinate (according to the client area) of the mouse pointer, use the clientY property.
- Để có được tọa độ theo chiều dọc (theo client area) của con trỏ chuột, sử dụng tài sản ```clientY```.
- Xuất ra tọa độ của con trỏ chuột khi nhấp chuột vào một phần tử:
```javascript
function showCoords(event) {
  var x = event.clientX;
  var y = event.clientY;
  var coords = "X coords: " + x + ", Y coords: " + y;
  document.getElementById("demo").innerHTML = coords;
}
```

>**MouseEvent ```clientY```**
- The clientY property returns the vertical coordinate (according to the client area) of the mouse pointer when a mouse event was triggered.
- Thuộc tính clientY trả về tọa độ theo chiều dọc (theo khu vực khách hàng) của con trỏ chuột khi một sự kiện chuột được kích hoạt.
- To get the horizontal coordinate (according to the client area) of the mouse pointer, use the clientX property.
- Để có được tọa độ ngang (theo khu vực khách hàng) của con trỏ chuột, hãy sử dụng thuộc tính clientX.
- Xuất ra các tọa độ của con trỏ chuột trong khi con trỏ chuột di chuyển qua một phần tử:
```javascript
function showCoords(event) {
  var x = event.clientX;
  var y = event.clientY;
  var coords = "X coords: " + x + ", Y coords: " + y;
  document.getElementById("demo").innerHTML = coords;
}
```
>**Phân biệt sự khác biệt giữa ```clientX``` và ```clientY``` và ```screenX``` và màn hình**

```javascript
<div onclick="showCoords(event)"><p id="demo"></p></div>
function showCoords(event) {
    var cX = event.clientX;
    var sX = event.screenX;
    var cY = event.clientY;
    var sY = event.screenY;
    var coords1 = "client - X: " + cX + ", Y coords: " + cY;
    var coords2 = "screen - X: " + sX + ", Y coords: " + sY;
    document.getElementById("demo").innerHTML = coords1 + "<br>" + coords2;
}
```

>**7. ```pageXOffset```, ```pageYOffset```**
- Các thuộc tính ```pageXOffset``` và ```pageYOffset``` trả về các pixel mà document hiện tại đã được ```cuộn``` ```từ góc trên``` ```bên trái``` của ```cửa sổ```, ```theo chiều ngang``` và ```theo chiều dọc```.
- Thuộc tính pageXOffset và pageYOffset bằng với thuộc tính scrollX và scrollY.
- ```window.pageXOffset```, ```window.pageYOffset```

```javascript
window.addEventListener("scroll", function(e) { 
  r = window.pageYOffset || document.documentElement.scrollTop 
});
```

>**```pageXOffset```**

- Đây là bí danh cho ```scrollX```

```javascript
xOffset = window.pageXOffset;
```

>**```pageYOffset```**

- Trang thuộc tính chỉ đọc WindowYOffset là một bí danh cho ```scrollY```;như vậy, nó trả về số pixel mà tài liệu hiện đang cuộn dọc theo trục thẳng đứng (nghĩa là, lên hoặc xuống).với một giá trị 0,0 chỉ ra rằng cạnh trên cùng của tài liệu hiện đang được căn chỉnh với cạnh trên cùng của khu vực nội dung của cửa sổ.

```javascript
window.pageYOffset;
yOffset = window.pageYOffset;
```

>**sticky header**

```javascript
var navbar = document.getElementById("navbar");
var sticky = navbar.offsetTop;
function myFunction() {
  if (window.pageYOffset >= sticky) {
    navbar.classList.add("sticky")
  } else {
    navbar.classList.remove("sticky");
  }
}
```

>**9. ```scrollTop```**
- Thuộc tính ```scrollTop``` đặt hoặc trả về số lượng pixel mà nội dung của phần tử được cuộn theo chiều dọc.

```javascript
<div id="myDIV" onscroll="myFunction()">
  <div id="content">Scroll inside me!</div>
</div>
<p id="demo"></p>
function myFunction() {
    var elmnt = document.getElementById("myDIV");
    var x = elmnt.scrollLeft;
    var y = elmnt.scrollTop;
    document.getElementById ("demo").innerHTML = "Horizontally: " + x + "px<br>Vertically: " + y + "px";
}
```

```
<button onclick="myFunction()">Scroll contents of body</button><br><br>
function myFunction() {
  var body = document.body; // For Safari
  var html = document.documentElement; // Chrome, Firefox, IE and Opera places the overflow at the html level, unless else is specified. Therefore, we use the documentElement property for these browsers
  body.scrollLeft += 30;
  body.scrollTop += 10;
  html.scrollLeft += 30;
  html.scrollTop += 10;
}
```

>**12. ```scrollLeft```**
- Sử dụng thuộc tính ```scrollLeft``` để đặt hoặc trả lại số pixel mà nội dung của phần tử được cuộn theo chiều ngang.
```javascript
<div id="myDIV" onscroll="myFunction()">
  <div id="content">Scroll inside me!</div>
</div>
<p id="demo"></p>
function myFunction() {
    var elmnt = document.getElementById("myDIV");
    var x = elmnt.scrollLeft;
    var y = elmnt.scrollTop;
    document.getElementById ("demo").innerHTML = "Horizontally: " + x + "px<br>Vertically: " + y + "px";
}
```

>**13. ```scrollBy```**
- Phương thức ```scrollBy()``` cuộn ```document``` theo số pixel được chỉ định.
- window.scrollBy(xnum, ynum)

```javascript
<button onclick="scrollWin(0, 50)">Scroll down</button>
<button onclick="scrollWin(0, -50)">Scroll up</button>
<button onclick="scrollWin(100, 0)">Scroll right</button>
<button onclick="scrollWin(-100, 0)">Scroll left</button>
function scrollWin() {
    window.scrollBy(0, 100);
}
```

**14. ```getBoundingClientRect()```**
- rect is a DOMRect object with eight properties: ```left```, ```top```, ```right```, ```bottom```, ```x```, ```y```, ```width```, ```height```.
```javascript
var rect = obj.getBoundingClientRect();
```
- Kết quả là hình chữ nhật nhỏ nhất chứa toàn bộ phần tử, với các thuộc tính chỉ đọc, ```left```, ```top```, ```right```, ```bottom```, ```x```, ```y```, ```width```, ```height``` mô tả toàn bộ hộp viền theo pixel. Các thuộc tính khác với ```width``` và ```height``` có liên quan đến phía trên cùng bên trái của chế độ xem.
- The ```Element.getBoundingClientRect()``` method returns the size of an element and its position relative to the viewport.
- Các hộp viền trống sẽ bị bỏ qua hoàn toàn. Nếu tất cả các hộp biên của phần tử trống, thì hình chữ nhật được trả về với chiều rộng và chiều cao bằng không và ở trên cùng và bên trái là phía trên cùng bên trái của hộp viền cho hộp CSS đầu tiên (theo thứ tự nội dung) cho thành phần.
- Các tập lệnh yêu cầu khả năng tương thích trình duyệt chéo cao có thể sử dụng ```window.pageXOffset``` và ```window.pageYOffset``` thay vì ```window.scrollX``` và ```window.scrollY```. Các tập lệnh không có quyền truy cập vào các thuộc tính này có thể sử dụng mã như sau:

```javascript
// For scrollX
(((t = document.documentElement) || (t = document.body.parentNode))
  && typeof t.scrollLeft == 'number' ? t : document.body).scrollLeft
// For scrollY
(((t = document.documentElement) || (t = document.body.parentNode))
  && typeof t.scrollTop == 'number' ? t : document.body).scrollTop
```

