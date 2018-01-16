## I. JavaScript HTML DOM

  - In the DOM, all HTML elements are defined as objects.
  - The programming interface is the properties and methods of each object.
  - A **property** is a value that you can get or set (like changing the content of an HTML element).
  - A **method** is an action you can do (like add or deleting an HTML element).
   
### 1. DOM Methods

```javascript
<p id="demo"></p>
document.getElementById('demo').innerHTML() = "Hello World";
```
- **Method:**  ```javascriptgetElementById()```
- **Property:** ```javascriptinnerHTML()```

### 2. DOM Document

- The document object represents your web page.
- If you want to access any element in an HTML page, you always start with accessing the document object.

**2.1 Finding HTML Elements**
---

- **document.getElementById(id)** -->	Find an element by element id
- **document.getElementsByTagName(name)** -->	Find elements by tag name

    ```
    <ul>
      <li>Coffee</li>
      <li>Tea</li>
      <li>Milk</li>
    </ul>
    <button onclick="myFunction()">Try it</button>
    <p id="demo"></p>
    function myFunction() {
      var x = document.getElementsByTagName("LI");
      document.getElementById("demo").innerHTML = x[1].innerHTML;
    }
    ```
    **Result** ==> Tea
- **document.getElementsByClassName(name)** -->	Find elements by class name

  ```
  <div class="example">First div element with class="example".</div>
  <div class="example">Second div element with class="example".</div>
  <button onclick="myFunction()">Try it</button>
  function myFunction() {
    var x = document.getElementsByClassName("example");
    x[0].innerHTML = "Hello World!";
  }
  ```

**2.2 Changing HTML Elements**
---

- **element.innerHTML =  new html content** -->	Change the inner HTML of an element
- **element.attribute = new value** -->	Change the attribute value of an HTML element
  ```
  <button id="myBtn" onclick="myFunction()">Try it</button>
  <p id="demo"></p>
  function myFunction() {
    var x = document.getElementById("myBtn").attributes[0].name;
    document.getElementById("demo").innerHTML = x;
  }
  ```
  **Result** ==> onclick
  
  ```
  function myFunction() {
    var x = document.getElementById("myBtn").attributes.length;
    document.getElementById("demo").innerHTML = x;
  }
  ```
    **Result** ==> 2
    
- **element.setAttribute(attribute, value)** --> Change the attribute value of an HTML element

  ```
  .democlass { color: red;}
  <h1>Hello World</h1>
  <p>Click the button to add a class attribute with the value of "democlass" to the h1 element.</p>
  <button onclick="myFunction()">Try it</button>
  
  function myFunction() {
    document.getElementsByTagName("H1")[0].setAttribute("class", "democlass"); 
  }
  ```
- **element.style.property = new style** --> Change the style of an HTML element

  ```
  <h1>Hello World!</h1>
  <button type="button" onclick="myFunction()">Set background color</button>
  
  function myFunction() {
    document.body.style.backgroundColor = "red";
  }
  ```

**2.3 Adding and Deleting Elements**
---

- **document.createElement(element)** -->	Create an HTML element

  ```
  <p>Click the button to make a BUTTON element.</p>
  <button onclick="myFunction()">Try it</button>
  
  function myFunction(){
      var btn = document.createElement("BUTTON");
      document.body.appendChild(btn);
  }
  
  function myFunction(){
      var btn = document.createElement("BUTTON");
      var txt = document.createTextNode("Click Me");
      btn.appendChild(txt);
      document.body.appendChild(btn);
  }
  ```
   
- **document.removeChild(element)** -->	Remove an HTML element

  ```
  <ul id="myList">
    <li>Coffee</li>
    <li>Tea</li>
    <li>Milk</li>
  </ul>
  <p>Click the button to remove the first item from the list.</p>
  <button onclick="myFunction()">Try it</button>
  
  function myFunction(){
    var list = document.getElementById('myList');
    list.removeChild(list.childNodes[[0]]);
  }
  ```
  **Result** ==> ```Tea, Milk```
   
- **document.appendChild(element)** -->	Add an HTML element

  ```
  <ul id="myList">
    <li>Coffee</li>
    <li>Tea</li>
  </ul>
  <p>Click the button to append an item to the end of the list.</p>
  <button onclick="myFunction()">Try it</button>
  
  function myFunction(){
    var node = document.createElement('li');
		var textnode = document.createTextNode('Water');
		node.appendChild(textnode);
		document.getElementById('myList').appendChild(node);
  }
  ```
  **Result** ==> ```Tea, Milk, Water```
  
- **document.replaceChild(element)** -->	Replace an HTML element

  ```
  <ul id="myList"><li>Coffee</li><li>Tea</li><li>Milk</li></ul>
  <p>Click the button to append an item to the end of the list.</p>
  <button onclick="myFunction()">Try it</button>
  
  function myFunction(){
    var textnode = document.createTextNode("Water");
    var item = document.getElementById("myList").childNodes[0];
    item.replaceChild(textnode, item.childNodes[0]);
  }
  ```
  **Result** ==> ```Water```
   
   
- **document.write(text)** -->	Write into the HTML output stream

  ```
  document.write("Hello World");
  document.write("<h1>Title</h1>");
  document.write(Date());
  ```
   
**2.4 Adding Events Handlers**
---

- **document.getElementById(id).onclick = function(){code}** --> Adding event handler code to an onclick event

**2.5 Finding HTML Objects**
---

- **document.anchors** -->	Returns all <a> elements that have a name attribute  ==> 1
   ```javascript
   <a name="html">HTML Tutorial</a><br>
   <a name="css">CSS Tutorial</a><br>
   <a name="xml">XML Tutorial</a><br>
   <p>Click the button to display the HTML content of the first anchor in the document.</p>
   <button onclick="myFunction()">Try it</button>
   <p id="demo"></p>
   function myFunction() {
     var x = document.anchors.length;
     document.getElementById("demo").innerHTML = x;
   }
   function myFunction(){
     var x = document.anchors[0].innerHTML;
     document.getElementById('demo') = x;
   }
   ```
   - **Note**: The name attribute of the <a> element is not supported in HTML5.
- **document.applets** -->	Returns all <applet> elements (Deprecated in HTML5)  ==> 1
- **document.baseURI** -->	Returns the absolute base URI of the document  ==> 3
  
  ```
  <button onclick="myFunction()">Try it</button>
  <p id="demo"></p>
  ```
  
  ```
  function myFunction() {
    var x = document.baseURI;
    document.getElementById("demo").innerHTML = x;
  }
  ```
    ==> Result: https://www.w3schools.com/jsref/tryit.asp?filename=tryjsref_doc_baseuri
  
- **document.body** -->	Returns the <body> element	1
  
  ```
  <body>
  <p>Click the button to display the HTML content of the document.</p>
  <button onclick="myFunction()">Try it</button>
  <p id="demo"></p>
  <script>
  function myFunction() {
      var x = document.body.innerHTML;
      document.getElementById("demo").innerHTML = x;
  }
  </script>
  </body>
  ```
  - Return the body property: ```document.body```
  - Set the body property: ```document.body = newContent```

- **document.cookie** -->	Returns the document's cookie  ==> 1
  
   document.cookie = newCookie
   - expires=date: Không bắt buộc. Chỉ định ngày theo định dạng GMT (Xem phương thức Date.toUTCString). Nếu không được chỉ định, cookie sẽ bị xóa khi trình duyệt đóng.
   - path=path: Không bắt buộc. Thông báo cho trình duyệt biết đường dẫn đến thư mục thuộc về cookie, (ví dụ: '/', '/ dir'). Lưu ý: Đường dẫn phải tuyệt đối. Nếu không được chỉ định, cookie thuộc về trang hiện tại
   - domain=domainname: Không bắt buộc. Chỉ định tên miền của trang web của bạn (ví dụ: 'example.com', '.example.com' (bao gồm tất cả các tên miền phụ), 'subdomain.example.com'). Nếu không được chỉ định, tên miền của tài liệu hiện tại sẽ được sử dụng
   - secure: Không bắt buộc. Thông báo cho trình duyệt sử dụng một giao thức an toàn (https) để gửi cookie đến máy chủ
   - An example of creating a cookie:
   
  ```
  document.cookie="username=John Doe; expires=Thu, 18 Dec 2013 12:00:00 UTC; path=/";
  ```
- **document.doctype** -->	Returns the document's doctype	==> 3
- **document.documentElement** -->	Returns the <html> element  ==> 3
- **document.documentMode** -->	Returns the mode used by the browser  ==> 3
- **document.documentURI** -->	Returns the URI of the document  ==> 3
- **document.domain** -->	Returns the domain name of the document server  ==> 1
- **document.domConfig** -->	Obsolete. Returns the DOM configuration  ==> 3
- **document.embeds** -->	Returns all <embed> elements  ==> 3
- **document.forms** -->	Returns all <form> elements  ==> 1
- **document.head** -->	Returns the <head> element  ==> 3
- **document.images** -->	Returns all <img> elements  ==> 1
- **document.implementation** -->	Returns the DOM implementation  ==> 3
- **document.inputEncoding** -->	Returns the document's encoding (character set)  ==> 3
- **document.lastModified** -->	Returns the date and time the document was updated  ==> 3
- **document.links** -->	Returns all <area> and <a> elements that have a href attribute  ==> 1
- **document.readyState** -->	Returns the (loading) status of the document  ==> 3
- **document.referrer** -->	Returns the URI of the referrer (the linking document)  ==> 1
- **document.scripts** -->	Returns all <script> elements  ==> 3
- **document.strictErrorChecking** -->	Returns if error checking is enforced  ==> 3
- **document.title** -->	Returns the <title> element  ==> 1
	
  ```
  <!DOCTYPE html>
  <html>
  <head>
    <title>My title</title>
  </head>
  <body>
  <p>Click the button to display the title of the document.</p>
  <button onclick="myFunction()">Try it</button>
  <p id="demo"></p>
  <script>
  function myFunction() {
      var x = document.title;
      document.getElementById("demo").innerHTML = x;
  }
  </script>

  </body>
  </html>
  ```
  ==> Result: My title
  
- **document.URL** -->	Returns the complete URL of the document  ==> 1
  ```
  <button onclick="myFunction()">Try it</button>
  <p id="demo"></p>
  function myFunction() {
    var x = document.URL;
    document.getElementById("demo").innerHTML = x;
  }
  ```
  ==> Result: https://github.com/daodc/Front-End-Develop-Technicals/edit/master/Javascript-dom.md
### 3. DOM Elements
**Finding HTML Elements**
  **- Finding HTML elements by id**: ```document.getElementById()```
  ```
  var myElement = document.getElementById("intro");
  ```
  **- Finding HTML elements by tag name**: ```document.getELementByTagName('p')```
  ```
  <p>Hello World!</p>
  <p>The DOM is very useful.</p>
  <p>This example demonstrates the <b>getElementsByTagName</b> method</p>
  <p id="demo"></p>
  
  var x = document.getElementsByTagName("p");
  document.getElementById("demo").innerHTML = 'The first paragraph (index 0) is: ' + x[0].innerHTML;
  ```
  
  **- Finding HTML elements by class name**: ```document.getElementsByClassName('intro')```
  ```
  <p>Hello World!</p>
  <p class="intro">The DOM is very useful.</p>
  <p class="intro">This example demonstrates the <b>getElementsByClassName</b> method.</p>
  <p id="demo"></p>
  
  var x = document.getElementsByClassName("intro");
  document.getElementById("demo").innerHTML = 'The first paragraph (index 0) with class="intro": ' + x[0].innerHTML;
  ```
  **- Finding HTML elements by CSS selectors**: ```document.querySelectorAll('p.intro"')```
  ```
  <p>Hello World!</p>
  <p class="intro">The DOM is very useful.</p>
  <p class="intro">This example demonstrates the <b>querySelectorAll</b> method.</p>
  <p id="demo"></p>
  
  var x = document.querySelectorAll("p.intro");
  document.getElementById("demo").innerHTML = The first paragraph (index 0) with class="intro": ' + x[0].innerHTML;
  ```
  **- Finding HTML elements by HTML object collections**: 
    
    - ```document.anchors```
    - ```document.body```
    - ```document.documentElement```
    - ```document.embeds```
    - ```document.forms```
    - ```document.head```
    - ```document.images```
    - ```document.links```
    - ```document.scripts```
    - ```document.title```

  ```javascript
  <form id="frm1" action="/action_page.php">
    First name: <input type="text" name="fname" value="Donald"><br>
    Last name: <input type="text" name="lname" value="Duck"><br><br>
  <input type="submit" value="Submit">
  </form> 
  <p>Click "Try it" to display the value of each element in the form.</p>
  <button onclick="myFunction()">Try it</button>
  <p id="demo"></p>
  
  function myFunction() {
    var x = document.forms["frm1"];
    var text = "";
    var i;
    for (i = 0; i < x.length ;i++) {
        text += x.elements[i].value + "<br>";
    }
    document.getElementById("demo").innerHTML = text;
  }
  ```

### 4. DOM - Changing HTML

  **- Changing the HTML Output Stream**
  ```document.write(Date());```
  
  **- Changing HTML Content**
  ```
  <p id="p1">Hello World!</p>
  document.getElementById("p1").innerHTML = "New text!";
  ```
  
  **- Changing the Value of an Attribute**: ```document.getElementById(id).attribute = new value```
  ```javascript
  <img id="myImage" src="smiley.gif">
  document.getElementById("myImage").src = "landscape.jpg";
  ```

### 5. DOM - Changing CSS

```javascript
document.getElementById('id').style.color = "red";
```

### 6. DOM Animation

```javascript
<!DOCTYPE html>
<html>
<style>
#container {
  width: 400px;
  height: 400px;
  position: relative;
  background: yellow;
}
#animate {
  width: 50px;
  height: 50px;
  position: absolute;
  background-color: red;
}
</style>
<body>
<p>
<button onclick="myMove()">Click Me</button>
</p> 
<div id ="container">
<div id ="animate"></div>
</div>

<script>
function myMove() {
  var elem = document.getElementById("animate");   
  var pos = 0;
  var id = setInterval(frame, 5);
  function frame() {
    if (pos == 350) {
      clearInterval(id);
    } else {
      pos++; 
      elem.style.top = pos + 'px'; 
      elem.style.left = pos + 'px'; 
    }
  }
}

</script>

</body>
</html>
```

### 7. DOM Events

>**onclick()**:
---
```javascript
  <h1 onclick="this.innerHTML = 'Ooops!'">Click on this text!</h1>
  <h1 onclick="changeText(this)">Click on this text!</h1>
  function changeText(id){
    id.innerHTML = 'Ooops!';
  }
```
  
>**onload:** Sự kiện onload và onunload được kích hoạt khi người dùng nhập hoặc thoát khỏi trang.
---
```javascript
<body onload="checkCookies()">
  <p id="demo"></p>
</body>
function checkCookies(){
  var text = '';
  if(navigator.cookieEnabled == true){
    text = 'Cookies are Enable';
  }
  else{
    text = 'Cookies are Disable';
  }
  document.getElementById('demo') = text;
}
```

>**onchange**: Sự kiện onchange thường được sử dụng kết hợp với xác nhận các input fields.
```javascript
<input type="text" id="fname" onchange="myFunction()">
myFunction(){
  var x = document.getElementById('fname');
  x.value = x.value.toUpperCase();
}
```

>**The onmouseover and onmouseout Events**
```javascript
<div onmouseover="mOver(this) onmouseout="mOut(this)">Mouse Over Me</div>
function mOver(obj){
  obj.innerHTML = 'Mouse Out Me'
}
function mOut(obj){
  obj.innerHTML = 'Mouse Over Me'
}
```

### 8. DOM EventListener

```javascript
a
```

### 9. DOM Navigation

```javascript
a
```

### 10. DOM Elements (Nodes)

```javascript
a
```

### 11. DOM Collections

```javascript
a
```

### 12. DOM Node Lists

```javascript
a
```
