
### I. JS AJAX
---

AJAX = Asynchronous JavaScript And XML.
Một đối tượng XMLHttpRequest được xây dựng trong trình duyệt (để request data từ một máy chủ web

```javascript
function loadDoc() {
  var xhttp = new XMLHttpRequest();
  xhttp.onreadystatechange = function() {
    if (this.readyState == 4 && this.status == 200) {
     document.getElementById("demo").innerHTML = this.responseText;
    }
  };
  xhttp.open("GET", "ajax_info.txt", true);
  xhttp.send();
}
```

### II. AJAX Works
---

![Image of Yaktocat](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/pic_ajax.gif  "Image of Yaktocat w3c")

### III. AJAX - The XMLHttpRequest Object
--- 

### 1.Create an XMLHttpRequest Object
---
All modern browsers (Chrome, Firefox, IE7+, Edge, Safari, Opera) have a built-in XMLHttpRequest object.

```var xhttp = new XMLHttpRequest();```

### 2. Older Browsers (IE5 and IE6)
---

Old versions of Internet Explorer (5/6) use an ActiveX object instead of the XMLHttpRequest object:

```variable = new ActiveXObject("Microsoft.XMLHTTP");```

### 3. XMLHttpRequest Object Methods
---

Method | Description
------------ | -------------
new XMLHttpRequest()  | 	Creates a new XMLHttpRequest object
abort()  | Cancels the current request
getAllResponseHeaders()  | Returns header information
getResponseHeader()  | Returns specific header information(Trả về thông tin tiêu đề cụ thể)
open(method, url, async, user, psw)  | Specifies the request **;** method: the request type GET or POST **;** url: the file location **;** async: true (asynchronous) or false (synchronous) **;** user: optional user name **;** psw: optional password.
send()  | Sends the request to the server, Used for GET requests
send(string)  | Sends the request to the server, Used for POST requests
setRequestHeader()  | Adds a label/value pair to the header to be sent

### 4. XMLHttpRequest Object Properties
---

First Header | Second Header
------------ | -------------
onreadystatechange  | Content
readyState  | 	Defines a function to be called when the readyState property changes
readyState  | Holds the status of the XMLHttpRequest.
readyState  | 0: request not initialized 
readyState  | 1: server connection established
readyState  | 2: request received 
readyState  | 3: processing request 
readyState  | 4: request finished and response is ready
responseText  | Returns the response data as a string
responseXML  | 	Returns the response data as XML data
status  | Returns the status-number of a request
status  | 200: "OK"
status  | 403: "Forbidden"
status  | 404: "Not Found"
statusText  | Returns the status-text (e.g. "OK" or "Not Found")

### IV. AJAX - Send a Request To a Server
---
>**Send a Request To a Server**: To send a request to a server, we use the open() and send() methods of the XMLHttpRequest object:

```javascript
xhttp.open('GET', 'ajax_info.txt', true);
xhttp.send();
```

First Header | Second Header
------------ | -------------

Method	Description open(method, url, async)  | Specifies the type of request

Method	Description open(method, url, async)  | ```method```: the type of request: GET or POST
Method	Description open(method, url, async)  | ```url```: the server (file) location
Method	Description open(method, url, async)  | ```async```: ```true``` (asynchronous) or ```false``` (synchronous)
send()  | Sends the request to the server (used for GET)
send(string)  | Sends the request to the server (used for POST)

>**1. GET requests**

**A simple GET request:**
```javascript
function loadDoc() {
  var xhttp = new XMLHttpRequest();
  xhttp.onreadystatechange = function() {
    if (this.readyState == 4 && this.status == 200) {
      document.getElementById("demo").innerHTML = this.responseText;
    }
  };
  xhttp.open("GET", "demo_get.asp", true);
  xhttp.send();
}
```

**In the example above, you may get a cached result. To avoid this, add a unique ID to the URL:**

```javascript
function loadDoc() {
  var xhttp = new XMLHttpRequest();
  xhttp.onreadystatechange=function() {
    if (this.readyState == 4 && this.status == 200) {
      document.getElementById("demo").innerHTML = this.responseText;
    }
  };
  xhttp.open("GET", "demo_get.asp?t=" + Math.random(), true);
  xhttp.send();
}
```

**If you want to send information with the GET method, add the information to the URL:**

```javascript
function loadDoc() {
  var xhttp = new XMLHttpRequest();
  xhttp.onreadystatechange = function() {
    if (this.readyState == 4 && this.status == 200) {
      document.getElementById("demo").innerHTML = this.responseText;
    }
  };
  xhttp.open("GET", "demo_get2.asp?fname=Henry&lname=Ford", true);
  xhttp.send();
}
```

>**2. POST Requests**

**A simple POST request:**

```javascript
function loadDoc() {
  var xhttp = new XMLHttpRequest();
  xhttp.onreadystatechange = function() {
    if (this.readyState == 4 && this.status == 200) {
      document.getElementById("demo").innerHTML = this.responseText;
    }
  };
  xhttp.open("POST", "demo_post.asp", true);
  xhttp.send();
}
```

**To POST data like an HTML form, add an HTTP header with setRequestHeader(). Specify the data you want to send in the send() method:**

```javascript
function loadDoc() {
  var xhttp = new XMLHttpRequest();
  xhttp.onreadystatechange = function() {
    if (this.readyState == 4 && this.status == 200) {
      document.getElementById("demo").innerHTML = this.responseText;
    }
  };
  xhttp.open("POST", "demo_post2.asp", true);
  xhttp.setRequestHeader("Content-type", "application/x-www-form-urlencoded");
  xhttp.send("fname=Henry&lname=Ford");
}
```

```setRequestHeader(header, value)```: 
   - Adds HTTP headers to the request
   - ```header```: specifies the header name
   - ```value```: specifies the header value

**The url - A File On a Server**
  - The url parameter of the open() method, is an address to a file on a server:
  - The file can be any kind of file, like .txt and .xml, or server scripting files like .asp and .php (which can perform actions on the server before sending the response back).

```javascript
xhttp.open("GET", "ajax_test.asp", true);
```

****

```javascript

```

### V. AJAX - Server Response
---

### VI. AJAX XML Example
---

### VII. AJAX PHP Example
---

### VIII. AJAX ASP Example
---

### IX. AJAX Database Example
---

### X. XML Applications
---
