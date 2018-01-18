
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

### 1. XMLHttpRequest Object Methods
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

### 2. XMLHttpRequest Object Properties
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

