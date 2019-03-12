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
**2. JavaScript Window Screen**

- The window.screen object can be written without the window prefix.(Đối tượng window.screen có thể được viết mà không có tiền tố ```window```.)

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

**3. What is the difference, between ```window```, ```screen```, and ```document``` in Javascript?**

- **window:** 

  + Là gốc đối tượng JavaScript chính.
  + Là đối tượng chung trong trình duyệt.
  + Bạn có thể truy cập nó dưới dạng ```window``` trong hầu hết các trường hợp (trong trình duyệt).
  + ```window.screen``` là một đối tượng thông tin nhỏ về kích thước màn hình vật lý.
  + Là global object thực sự.
  + ```window.screen``` là một đối tượng thông tin nhỏ về kích thước màn hình vật lý.

  + ```$(window).width()```: chiều rộng của cửa sổ trình duyệt, nó có thể thay đổi với trình duyệt.
  + ```window.screen.width ```: nó phụ thuộc vào chiều rộng màn hình của bạn, nó là một giá trị cố định.
  + https://www.w3schools.com/jsref/obj_window.asp
  
- **screen:** 

  + screen là màn hình, nó chứa các thuộc tính về màn hình của người dùng.
  
- **document:** 
  + Là DOM
  + ```window.document``` hoặc chỉ tài liệu là đối tượng chính của mô hình đối tượng tài liệu có thể nhìn thấy (hoặc tốt hơn: rendered) / DOM.
  
**4. ```jQuery Dimensions```**

![jQuery Dimensions](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/img_jquerydim.gif)
- **width():** phương thức thiết lập hoặc trả về chiều rộng của một phần tử (không bao gồm padding, border và margin).
- **height():** phương thức thiết lập hoặc trả về chiều cao của một phần tử (không bao gồm padding, border và margin).
- **innerWidth():** phương thức trả về chiều rộng của một phần tử (bao gồm padding).
- **innerHeight():** phương thức trả về chiều cao của một phần tử (bao gồm padding).
- **outerWidth():** phương thức trả về chiều rộng của một phần tử (bao gồm phần padding và border).
- **outerHeight():** phương thức trả về chiều cao của một phần tử (bao gồm phần padding và border).

**5. ```addEventListener```**

```javascript
element.addEventListener("mouseover", myFunction);
element.addEventListener("click", mySecondFunction);
element.addEventListener("mouseout", myThirdFunction);
element.addEventListener("resize", myThirdFunction);
element.addEventListener("mousemove", myThirdFunction);
```

**6. offsetHeight , offsetLeft, offsetParent, offsetTop, offsetWidth**
```javascript

```

**7. ```scrollX```, ```scrollY```**

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

**8. clientWidth, clientHeight**
- Lấy chiều rộng và chiều cao của họp bao gồm phần ```padding```, không bao gồm ```border```.

```javascript
function myFunction() {
  var elmnt = document.getElementById("myDIV");
  var txt = "Height including padding: " + elmnt.clientHeight + "px<br>";
  txt += "Width including padding: " + elmnt.clientWidth + "px";
  document.getElementById("demo").innerHTML = txt;
}
```

**9. MouseEvent ```screen```, ```screenX```, ```screenY``` Property**

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

**10. MouseEvent ```clientX```, ```clientY```**

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

**11. ```pageXOffset```, ```pageYOffset```**
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

**12. ```scrollTop```**
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

**13. ```scrollLeft```**
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

**14. ```scrollBy```**
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

**15. ```getBoundingClientRect()```**

- top – Tọa độ Y cho cạnh phần tử trên cùng.

- left – Tọa độ X cho cạnh phần tử bên trái.

- right – Tọa độ X cho cạnh phần tử bên phải.

- bottom – Tọa độ Y cho cạnh phần tử đáy.

- ![coords](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/coords.png)

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

**Move html-element to click-position**
```
var theThing = document.querySelector("#thing");
var container = document.querySelector("#contentContainer");

container.addEventListener("click", function(event) {
 var xPosition = event.clientX - container.getBoundingClientRect().left - (theThing.clientWidth / 2);
 var yPosition = event.clientY - container.getBoundingClientRect().top - (theThing.clientHeight / 2);
 // in case of a wide border, the boarder-width needs to be considered in the formula above
 theThing.style.left = xPosition + "px";
  theThing.style.top = yPosition + "px";
});
```

**elementFromPoint(x, y)**
- Cuộc gọi đến ```document.elementFromPoint(x, y)``` trả về phần tử lồng nhau nhất ở tọa độ cửa sổ (x, y).
- Cú pháp là: ```let elem = document.elementFromPoint(x, y);```
- mã bên dưới làm nổi bật và xuất ra thẻ của phần tử hiện đang ở giữa cửa sổ:

```javascript
let centerX = document.documentElement.clientWidth / 2;
let centerY = document.documentElement.clientHeight / 2;

let elem = document.elementFromPoint(centerX, centerY);

elem.style.background = "red";
alert(elem.tagName);
```

**Document coordinates**
- Các toạ độ tương đối tài liệu bắt đầu từ góc trên bên trái của tài liệu, không phải là cửa sổ.

- Trong CSS, các tọa độ cửa sổ tương ứng với ```position:fixed```, trong khi tọa độ tài liệu tương tự như ```position:absolute``` ở trên cùng.

- Chúng ta có thể sử dụng ```position:absolute``` và ```top/left``` để đặt một cái gì đó tại một vị trí nhất định của tài liệu, để nó vẫn còn đó trong một cuộn trang. Nhưng trước tiên chúng ta cần tọa độ đúng.

- Để rõ ràng, chúng tôi sẽ gọi các tọa độ **window** ```(clientX, clientY)``` và tọa độ **document** ```(pageX, pageY)```

**Khi trang không được **scroll**, thì tọa độ **window ** và tọa độ **document** thực sự giống nhau. Điểm số của chúng không khớp với nhau:**

- ![coordinates zero](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/document-window-coordinates-zero.png)

**Và nếu chúng ta scroll nó, sau đó (clientX, clientY) thay đổi, bởi vì chúng liên quan đến cửa sổ, nhưng (pageX, pageY) vẫn giữ nguyên.**
- Đây là cùng một trang sau cuộn dọc:

- ![coordinates scroll](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/document-window-coordinates-scroll.png)

- ```clientY``` của tiêu đề "Từ bài viết nổi bật hôm nay" đã trở thành 0, bởi vì phần tử hiện ở trên đầu cửa sổ.
- ```clientX``` không thay đổi, vì chúng ta không cuộn theo chiều ngang.
- các tọa độ ```pageX``` và ```pageY``` của phần tử vẫn như cũ, vì chúng liên quan đến tài liệu.

**Nhận tọa độ tài liệu**
- Không có phương pháp chuẩn nào để lấy tọa độ tài liệu của một phần tử. Nhưng thật dễ dàng để viết nó.
- Hai hệ tọa độ được kết nối theo công thức:
- ```pageY = clientY + chiều cao của phần dọc được cuộn ra của tài liệu.```
- ```pageX = clientX + chiều rộng của phần ngang được cuộn ra của tài liệu.```
- Hàm ```getCoords(elem)``` sẽ lấy các tọa độ cửa sổ từ ```elem.getBoundingClientRect()``` và thêm cuộn hiện tại vào chúng:

```
// get document coordinates of the element
function getCoords(elem) {
  let box = elem.getBoundingClientRect();

  return {
    top: box.top + pageYOffset,
    left: box.left + pageXOffset
  };
}
```

**16. indexOf():** 

>**indexOf() String**: Phương thức ```indexOf()``` trả về vị trí của lần xuất hiện đầu tiên của một giá trị được chỉ định trong một chuỗi.
```javascript
function myFunction() {
    var str = "Hello world welcome to the universe.";
    var n = str.indexOf("welcome");
    document.getElementById("demo").innerHTML = n;
}
```
**==> Result:** 12

>**indexOf() Array**: Phương thức ```indexOf()``` tìm kiếm mảng cho mục được chỉ định và trả về vị trí(position) của nó.
```javascript
function myFunction() {
  var fruits = ["Banana", "Orange", "Apple", "Mango"];
  var a = fruits.indexOf("Apple");
  document.getElementById("demo").innerHTML = a;
}
```
**==> Result:** 2

**17. splice():** The splice() method adds/removes items to/from an array, and returns the removed item(s).

```javascript
array.splice(index, howmany, item1, ....., itemX)
```

>**Case 1**
```javascript
var fruits = ["Banana", "Orange", "Apple", "Mango"];
fruits.splice(2, 1, "Lemon", "Kiwi");
```

>**Result 1**

- At position 2, remove 2 items:

```javascript
Banana,Orange,Lemon,Kiwi,Mango
```

>**Case 2**
```javascript
var fruits = ["Banana", "Orange", "Apple", "Mango", "Kiwi"];
fruits.splice(2, 2);
```

>**Result 2**
```javascript
Banana,Orange,Kiwi
```
**18. document.getElementsByClassName():** Get all elements with the specified class name

>**HTML**
```javascript
<div class="example">First div element with class="example".</div>
<div class="example">Second div element with class="example".</div>
<button onclick="myFunction()">Try it</button>
```

>**JS**
```javascript
function myFunction() {
  var x = document.getElementsByClassName("example");
  x[0].innerHTML = "Hello World!";
}
```

**19. document.getElementsByTagName():** Get all elements in the document with the specified tag name.

>**HTML**
```javascript
<p>An unordered list:</p>
<ul>
  <li>Coffee</li>
  <li>Tea</li>
  <li>Milk</li>
</ul>
<p>Click the button to display the innerHTML of the second li element (index 1).</p>
<button onclick="myFunction()">Try it</button>
<p id="demo"></p>
```

>**JS**
```javascript
function myFunction() {
  var x = document.getElementsByTagName("LI");
  document.getElementById("demo").innerHTML = x[1].innerHTML;
}
```

**20. document.querySelectorAll():** Get all elements in the document with class="elements"

>**HTML**
```javascript
var elements = document.querySelectorAll('.elements');
document.querySelectorAll('[data-foo]')
```

>**JS**
```javascript
function myFunction() {
  var x = document.getElementsByClassName("example");
  x[0].innerHTML = "Hello World!";
}
```

**21. document.createElement():** Create a <button> element

>**JS**
```javascript
var element= document.createElement("div");
document.body.appendChild(element);
```

**22. getAttribute():** Get the value of the class attribute of an ```<h1>``` element

>**HTML**
```javascript
<h1 class="democlass">Hello World</h1>
<p>Click the button to display the value of the class attribute of the h1 element.</p>
<button onclick="myFunction()">Try it</button>
<p id="demo"></p>
```

>**JS**
```javascript
function myFunction() {
  var x = document.getElementsByTagName("H1")[0].getAttribute("class");
  document.getElementById("demo").innerHTML = x;
}
```

**23. setAttribute():** Add the class attribute with the value of "democlass" to a ```<h1>``` element

>**HTML**
```javascript
<h1>Hello World</h1>
<p>Click the button to add a class attribute with the value of "democlass" to the h1 element.</p>
<button onclick="myFunction()">Try it</button>
```

>**JS**
```javascript
function myFunction() {
  document.getElementsByTagName("H1")[0].setAttribute("class", "democlass");
}
```

**24. getBoundingClientRect():** 
- rect is a DOMRect object with eight properties: left, top, right, bottom, x, y, width, height
- Kết quả là hình chữ nhật nhỏ nhất chứa toàn bộ phần tử, với các thuộc tính chỉ đọc, ```left, top, right, bottom, x, y, width, height``` mô tả toàn bộ hộp viền theo pixel. Các thuộc tính khác với ```width``` và ```height``` có liên quan đến phía trên cùng bên trái của chế độ xem.
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
**25. requestAnimationFrame():** 

- **sectionSyntax**: ```window.requestAnimationFrame(callback);```
- ```window.requestAnimationFrame()``` cho trình duyệt biết rằng bạn muốn thực hiện một animation và yêu cầu trình duyệt gọi một hàm được chỉ định để cập nhật một animation trước khi vẽ lại lần tiếp theo. Phương thức nhận một cuộc gọi lại như một đối số được gọi trước khi repaint.

- **callback**: Một tham số chỉ định một hàm để gọi khi đó là thời gian để cập nhật hoạt ảnh của bạn cho lần lặp lại tiếp theo. Gọi lại có một đối số duy nhất, một ```DOMHighResTimeStamp```, cho biết thời gian hiện tại (thời gian được trả về từ ```performance.now ()```) khi ```requestAnimationFrame()``` bắt đầu kích hoạt các cuộc gọi lại.

- **Return value**: Giá trị số nguyên dài, id yêu cầu, xác định duy nhất mục nhập trong danh sách gọi lại. Đây là giá trị khác 0, nhưng bạn không thể đưa ra bất kỳ giả định nào khác về giá trị của nó. Bạn có thể chuyển giá trị này tới ```window.cancelAnimationFrame()``` để hủy yêu cầu gọi lại làm mới.

```javascript
var start = null;
var element = document.getElementById('SomeElementYouWantToAnimate');
element.style.position = 'absolute';

function step(timestamp) {
  if (!start) start = timestamp;
  var progress = timestamp - start;
  element.style.left = Math.min(progress / 10, 200) + 'px';
  if (progress < 2000) {
    window.requestAnimationFrame(step);
  }
}

window.requestAnimationFrame(step);
```

**26. cancelAnimationFrame():**

- **Syntax**: ```window.cancelAnimationFrame(requestID);```

- **Parameters**: requestID: Giá trị ID được trả về bởi lệnh gọi đến window.requestAnimationFrame () đã yêu cầu gọi lại.

```javascript
var requestAnimationFrame = window.requestAnimationFrame || window.mozRequestAnimationFrame ||
  window.webkitRequestAnimationFrame || window.msRequestAnimationFrame;

var cancelAnimationFrame = window.cancelAnimationFrame || window.mozCancelAnimationFrame;

var start = window.mozAnimationStartTime; // Only supported in FF. Other browsers can use something like Date.now().

var myReq;

function step(timestamp) {
  var progress = timestamp - start;
  d.style.left = Math.min(progress / 10, 200) + 'px';
  if (progress < 2000) {
    myReq = requestAnimationFrame(step);
  }
}
myReq = requestAnimationFrame(step);

cancelAnimationFrame(myReq);
```

**27. Làm thế nào để nắm bắt các sự kiện CSS3 Animation trong JavaScript**
- CSS3 Animation được thực hiện trơn tru và nhanh chóng nhưng không giống như JavaScript, bạn không có kiểm soát theo từng khung hình. May mắn thay, bạn có thể áp dụng các trình xử lý sự kiện cho bất kỳ phần tử nào để xác định trạng thái hoạt ảnh. Điều này cho phép kiểm soát chi tiết như chơi các hình động khác nhau theo thứ tự.
```javascript
#anim.enable {
  -webkit -animation: flash 1 s ease 3;
  -moz-animation: flash 1 s ease 3;
  -ms-animation: flash 1 s ease 3;
  -o-animation: flash 1 s ease 3;
  animation: flash 1 s ease 3;
}

/* animation */
@ - webkit - keyframes flash {
  50 % { opacity: 0; }
}

@ - moz - keyframes flash {
  50 % { opacity: 0; }
}

@ - ms - keyframes flash {
  50 % { opacity: 0; }
}

@ - o - keyframes flash {
  50 % { opacity: 0; }
}

@keyframes flash {
  50 % { opacity: 0; }
}
```
- Khi lớp **enable** được **applied ** cho phần tử với ID **anim**, Animation  có tên ```flash``` được chạy ba lần. Mỗi lần lặp lại kéo dài một giây trong đó phần tử mất dần sau đó.

**28. animationstart**

- Sự kiện ```animationstart``` được kích hoạt khi animation bắt đầu lần đầu tiên.

```javascript
var anim = document.getElementById("anim");
anim.addEventListener("animationstart", AnimationListener, false);
```

**29. animationiteration**: Lặp lại

- Sự kiện animation được kích hoạt ở đầu mỗi lần lặp lại hoạt ảnh mới, tức là mỗi lần lặp lại trừ lần lặp đầu tiên.

```javascript
anim.addEventListener("animationiteration", AnimationListener, false);
```

**30. AnimationEnd**

- Sự kiện Animation được kích hoạt khi hoạt ảnh kết thúc.

```javascript
anim.addEventListener("animationend", AnimationListener, false);
```
>**HTML**
```javascript
<pre id="log">Event information log
=====================
</pre>
```

>**javascript**
```javascript
var
  anim = document.getElementById("anim"),
  log = document.getElementById("log"),
  pfx = ["webkit", "moz", "MS", "o", ""];

// button click event
anim.addEventListener("click", ToggleAnimation, false);

// animation listener events
PrefixedEvent(anim, "AnimationStart", AnimationListener);
PrefixedEvent(anim, "AnimationIteration", AnimationListener);
PrefixedEvent(anim, "AnimationEnd", AnimationListener);


// apply prefixed event handlers
function PrefixedEvent(element, type, callback) {
  for (var p = 0; p < pfx.length; p++) {
    if (!pfx[p]) type = type.toLowerCase();
    element.addEventListener(pfx[p]+type, callback, false);
  }
}

// handle animation events
function AnimationListener(e) {
  LogEvent("Animation '"+e.animationName+"' type '"+e.type+"' at "+e.elapsedTime.toFixed(2)+" seconds");
  if (e.type.toLowerCase().indexOf("animationend") >= 0) {
    LogEvent("Stopping animation...");
    ToggleAnimation();
  }
}

// start/stop animation
function ToggleAnimation(e) {
  var on = (anim.className != "");
  LogEvent("Animation is " +(on ? "disabled.\n" : "enabled."));
  anim.textContent = "Click to "+(on ? "start" : "stop")+" animation";
  anim.className = (on ? "" : "enable");
  if (e) e.preventDefault();
};

// log event in the console
function LogEvent(msg) {
  log.textContent += msg + "\n";
  var ot = log.scrollHeight - log.clientHeight;
  if (ot > 0) log.scrollTop = ot;
}

```

**31. Browser Compatibility**

```javascript
var pfx = ["webkit", "moz", "MS", "o", ""];
function PrefixedEvent(element, type, callback) {
  for (var p = 0; p < pfx.length; p++) {
    if (!pfx[p]) type = type.toLowerCase();
    element.addEventListener(pfx[p]+type, callback, false);
  }
}
```

```javascript
// animation listener events
PrefixedEvent(anim, "AnimationStart", AnimationListener);
PrefixedEvent(anim, "AnimationIteration", AnimationListener);
PrefixedEvent(anim, "AnimationEnd", AnimationListener);
```

**32. Sự kiện hoạt ảnh CSS3 trong JavaScript**
- Có 3 sự kiện hoạt ảnh CSS3 mà bạn có thể liên kết trong JavaScript:
- ```animationstart```: kích hoạt khi Animation bắt đầu.
- ```animationiteration```: kích hoạt khi vòng lặp Animation bắt đầu lại.
- ```animationend```: kích hoạt khi một Animation kết thúc (chú ý, không bao giờ kích hoạt các Animation vô hạn)
**Prefixing**
- Họ sẽ lưu phiên bản tiền tố chính xác trong các biến animationStart, animationIteration và animationEnd toàn cục, mà sau đó bạn có thể sử dụng để ràng buộc sự kiện.

```javascript
// Initialise needed variables
var prefixes = ["webkit", "moz", "MS", "o"];
var elem = document.createElement('div');

// Animation Start
window.animationStart = "animationstart";
for (var i = 0; i < prefixes.length; i++) {
  if (elem.style[prefixes[i] + "AnimationStart"] !== undefined) {
    window.animationStart = prefixes[i] + "AnimationStart";
    break;
  }
}

// Animation Iteration
window.animationIteration = "animationiteration";
for (var i = 0; i < prefixes.length; i++) {
  if (elem.style[prefixes[i] + "AnimationIteration"] !== undefined) {
    window.animationIteration = prefixes[i] + "AnimationIteration";
    break;
  }
}

// Animation End
window.animationEnd = "animationend";
for (var i = 0; i < prefixes.length; i++) {
  if (elem.style[prefixes[i] + "AnimationEnd"] !== undefined) {
    window.animationEnd = prefixes[i] + "AnimationEnd";
    break;
  }
}
```
- Bây giờ chúng ta chỉ cần ràng buộc sự kiện, gọi hàm doSomething khi nó kích hoạt:

```javascript
element.addEventListener(animationStart, doSomething, false);
element.addEventListener(animationIteration, doSomething, false);
element.addEventListener(animationEnd, doSomething, false);
```

**33. Detect the End of CSS Animations and Transitions with JavaScript**
- CSS cho phép bạn tạo các hiệu ứng động với các hiệu ứng chuyển tiếp và các khung hình chính mà chỉ có thể thực hiện được với JavaScript hoặc Flash. Thật không may, với CSS không có cách nào để thực hiện gọi lại khi hoạt ảnh hoàn tất. Với JavaScript, bạn có thể phát hiện phần cuối của quá trình chuyển đổi CSS hoặc hoạt ảnh và sau đó kích hoạt một chức năng.
**Phát hiện và thực hiện khi chuyển tiếp kết thúc bằng jQuery**
- Sử dụng JavaScript, chúng tôi có thể phát hiện sự kiện chuyển đổi; tuy nhiên đối với trình duyệt chéo, hỗ trợ chúng tôi cần bao gồm các tiền tố của trình duyệt khác.
- Sau đó gắn kết sự kiện với một hàm của jQuery, đảm bảo rằng nó chỉ chạy một lần (nó không thể xử lý sự kiện sau khi nó chạy một lần). (Đọc thêm về một chức năng)

```javascript
$(".button").click(function() {
  $(this).addClass("animate");
  $(this).one("webkitTransitionEnd otransitionend oTransitionEnd msTransitionEnd transitionend",
    function(event) {
      // Do something when the transition ends
    });
});
```

**Phát hiện tên thuộc tính sự kiện được hỗ trợ**
- Chúng tôi sẽ giới thiệu một hàm, whichTransitionEvent, để phát hiện tên thuộc tính sự kiện được hỗ trợ; gán một biến, trong trường hợp này là transitionEvent, để giữ tên thuộc tính sự kiện; và chuyển biến làm đối số đầu tiên của một hàm.

```javascript
// Function from David Walsh: http://davidwalsh.name/css-animation-callback
function whichTransitionEvent(){
  var t,
      el = document.createElement("fakeelement");

  var transitions = {
    "transition"      : "transitionend",
    "OTransition"     : "oTransitionEnd",
    "MozTransition"   : "transitionend",
    "WebkitTransition": "webkitTransitionEnd"
  }

  for (t in transitions){
    if (el.style[t] !== undefined){
      return transitions[t];
    }
  }
}

var transitionEvent = whichTransitionEvent();

$(".button").click(function(){
  $(this).addClass("animate");
  $(this).one(transitionEvent,
              function(event) {
    // Do something when the transition ends
  });
});
```

**Detect when animations (keyframes) end**

```javascript
function whichAnimationEvent(){
  var t,
      el = document.createElement("fakeelement");

  var animations = {
    "animation"      : "animationend",
    "OAnimation"     : "oAnimationEnd",
    "MozAnimation"   : "animationend",
    "WebkitAnimation": "webkitAnimationEnd"
  }

  for (t in animations){
    if (el.style[t] !== undefined){
      return animations[t];
    }
  }
}

var animationEvent = whichAnimationEvent();

$(".button").click(function(){
  $(this).addClass("animate");
  $(this).one(animationEvent,
              function(event) {
    // Do something when the animation ends
  });
});
```

**Vanilla JavaScript**

```javascript
var button = document.querySelector(".button"),
  transitionEvent = whichTransitionEvent();

button.addEventListener("click", function() {
  if (button.classList) {
    button.classList.add("animate");
  } else {
    button.className += " " + "animate";
  }

  button.addEventListener(transitionEvent, customFunction);
});

function customFunction(event) {
  button.removeEventListener(transitionEvent, customFunction);

  // Do something when the transition ends
}
```
**34. window.location**

```
console.log('window.location: '+window.location);
console.log('window.location.hash xay ra khi click: '+window.location.hash);
console.log('document.location.protocol: '+document.location.protocol);
console.log('window.location.hostname: '+window.location.hostname);
console.log('window.location.pathname: '+window.location.pathname);
console.log('window.location.href: '+window.location.href);
```

**34. localStorage**
- ```localStorage```: Các thuộc tính ```localStorage``` và ```sessionStorage``` cho phép lưu các cặp ```key```/```value``` trong trình duyệt web.
- Đối tượng ```localStorage``` lưu trữ dữ liệu không có ngày hết hạn. Dữ liệu sẽ không bị xóa khi đóng trình duyệt và sẽ có sẵn vào ngày, tuần hoặc năm tiếp theo.
- Thuộc tính localStorage là chỉ đọc.
**Tip**: Cũng xem thuộc tính ```sessionStorage``` lưu trữ dữ liệu cho một phiên (dữ liệu bị mất khi tab trình duyệt bị đóng).

- Syntax for SAVING data to localStorage: 

```javascript
localStorage.setItem("key", "value");
```

- Syntax for READING data from localStorage:

```javascript
var lastname = localStorage.getItem("key");
```

- Syntax for REMOVING data from localStorage:

```javascript
localStorage.removeItem("key");
```
>**Tạo một cặp name/value ```localStorage``` với name = "lastname" và value = "Smith", sau đó lấy giá trị của "Lastname" và chèn nó vào phần tử với id = "result":**

>**Ví dụ sau đây đếm số lần người dùng đã nhấp vào nút:**

```javascript
// Check browser support
if (typeof(Storage) !== "undefined") {
  // Store
  localStorage.setItem("lastname", "Smith");
  // Retrieve
  document.getElementById("result").innerHTML = localStorage.getItem("lastname");
} else {
  document.getElementById("result").innerHTML = "Sorry, your browser does not support Web Storage...";
}
```
