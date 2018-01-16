
### JS AJAX
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

### AJAX Works
---

![Image of Yaktocat](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/pic_ajax.gif  "Image of Yaktocat w3c")

### Create an XMLHttpRequest Object
---

### XMLHttpRequest Object Methods
---

Method | Description
------------ | -------------
new XMLHttpRequest()  | 	Creates a new XMLHttpRequest object
abort()  | Cancels the current request
getAllResponseHeaders()  | Returns header information
getResponseHeader()  | Returns specific header information(Trả về thông tin tiêu đề cụ thể)
open(method, url, async, user, psw)  | Specifies the request, method: the request type GET or POST, url: the file location, async: true (asynchronous) or false (synchronous), user: optional user name, psw: optional password
send()  | Sends the request to the server, Used for GET requests
send(string)  | Sends the request to the server, Used for POST requests
setRequestHeader()  | Adds a label/value pair to the header to be sent

### XMLHttpRequest Object Properties
---

First Header | Second Header
------------ | -------------
Content  | Content
Content  | Content
Content  | Content
Content  | Content
Content  | Content
Content  | Content
Content  | Content
Content  | Content
Content  | Content

