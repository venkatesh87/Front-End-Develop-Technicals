**1. indexOf():** 

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

**2. splice():** The splice() method adds/removes items to/from an array, and returns the removed item(s).

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
**3. document.getElementsByClassName():** Get all elements with the specified class name

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

**4. document.getElementsByTagName():** Get all elements in the document with the specified tag name.

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

**5. document.querySelectorAll():** Get all elements in the document with class="elements"

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

**6. document.createElement():** Create a <button> element

>**JS**
```javascript
var element= document.createElement("div");
document.body.appendChild(element);
```

**7. getAttribute():** Get the value of the class attribute of an ```<h1>``` element

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

**8. setAttribute():** Add the class attribute with the value of "democlass" to a ```<h1>``` element

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

**9. getBoundingClientRect():** 
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
**10. requestAnimationFrame():** 

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


**11. cancelAnimationFrame():**

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

**AnimationEnd**

https://www.sitepoint.com/css3-animation-javascript-event-handlers/
http://blogs.sitepointstatic.com/examples/tech/animation-api/index.html
https://jonsuh.com/blog/detect-the-end-of-css-animations-and-transitions-with-javascript/
http://blog.teamtreehouse.com/using-jquery-to-detect-when-css3-animations-and-transitions-end
https://mxstbr.blog/2015/06/animation-events/
https://developer.mozilla.org/en-US/docs/Web/Events/animationend
