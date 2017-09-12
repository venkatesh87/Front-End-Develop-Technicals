### Functions for loading and sending data between client and server without a browser page refresh.

#### I. Making CORS Ajax GET requests

- Asynchronous loading of data from a server in a different domain with modern browsers.

- Retrieving data asynchronously from a server in a different domain in vanilla JavaScript is straight forward and very similar to same-origin ```Ajax GET requests```. The following helper works in modern browsers and Internet Explorers 9+:

```javascript
function getCORS(url, success) {
    var xhr = new XMLHttpRequest();
    if (!('withCredentials' in xhr)) xhr = new XDomainRequest(); // fix IE8/9
    xhr.open('GET', url);
    xhr.onload = success;
    xhr.send();
    return xhr;
}

// example request
getCORS('http://foo.bar/?p1=1&p2=Hello+World', function(request){
    var response = request.currentTarget.response || request.target.responseText;
    console.log(response);
});
```

- Instead of ```onreadystatechange```, the ```onload``` callback is used in CORS for receiving the returned data. The callback gets passed as single argument, the request object. Depending on the browser, the actual response is found in ```currentTarget.response``` or ```target.responseText```.

#### II. JSONP Ajax requests

- JSONP allows asynchronous loading of data, even from servers in a different domain.

- JSONP is used for requesting data asynchronously from a server in a different domain:

```javascript
// define a callback function, which accepts the returned JSON data as its only argument
function response(data) {
  // JSON data in form of a JavaScript object
  console.log(data);
}

// create a script tag with the external request URL
// include "response" as value of the GET param "callback" in the URL
var script = document.createElement('script');
script.src = 'https://foo.bar/api/?callback=response';
document.body.appendChild(script);
```

- The function "response" gets called as soon as the data is successfully retrieved. It accepts as its first and only argument the parsed JSON data returned form the server.

- In general it's recommended to use ```cross-origin resource sharing (CORS)``` for such requests instead (IE8+). Yet, JSONP is simple to implement and it's cross-browser safe.

#### III. Load a script file asynchronously

- How to load a JavaScript file asynchronously from the server and automatically execute it.

- Loading an external script asynchronously is simple. Create a script tag, set its ```src``` attribute, and inject it into the DOM tree:

```javascript
var script = document.createElement('script'),
    scripts = document.getElementsByTagName('script')[0];
script.src = url;
scripts.parentNode.insertBefore(script, scripts);
```

- The returned JavaScript file is executed automatically by the browser. Loading the Facebook Like button and Google Analytics are two examples that make use of this technique. Tip: When such script files are requested on page load, it's recommended to use a standard script tag with the ```async``` (and ```defer```) attribute included:

```javascript
<script src="https://platform.twitter.com/widgets.js" async defer></script>
```

- The HTML5 attribute ```async``` tells the browser to load this script without blocking the page. ```defer``` does essentially the same, but works on several older browsers, too.

#### IV. Send Ajax GET and POST requests

- Load data asynchronously from the server using GET or POST HTTP requests. Set data type (xml, json, script, text, html) and decode returned data.

- The following helper function allows sending an Ajax request via GET method - an equivalent to jQuery's ```$.get()```. Its ```url``` argument must contain the full request path including all GET parameters:

```javascript
function getAjax(url, success) {
  var xhr = window.XMLHttpRequest ? new XMLHttpRequest() : new ActiveXObject('Microsoft.XMLHTTP');
  xhr.open('GET', url);
  xhr.onreadystatechange = function() {
    if (xhr.readyState > 3 && xhr.status == 200) success(xhr.responseText);
  };
  xhr.setRequestHeader('X-Requested-With', 'XMLHttpRequest');
  xhr.send();
  return xhr;
}

// example request
getAjax('http://foo.bar/?p1=1&p2=Hello+World', function(data) { console.log(data); });
```

-The header ```X-Requested-With``` allows server side frameworks, such as Django or RoR, to identify Ajax requests. It's optional, but can be useful.

- If the server returns a JSON string, it needs to be parsed inside the callback function (```$.getJSON``` in jQuery):

```javascript
getAjax('http://foo.bar/?p1=1&p2=Hello+World', function(data){
  var json = JSON.parse(data);
  console.log(json); 
});
```

- In case the returned JSON string might be invalid, wrap the parser into a try-catch statement.

- Sending POST requests is quite similar (```$.post()``` in jQuery). However, there are lots of options available - more than can be covered in one post. Here's a useful helper function to get you started:

```javascript
function postAjax(url, data, success) {
  var params = typeof data == 'string' ? data : Object.keys(data).map(
    function(k) { return encodeURIComponent(k) + '=' + encodeURIComponent(data[k]) }
  ).join('&');

  var xhr = window.XMLHttpRequest ? new XMLHttpRequest() : new ActiveXObject("Microsoft.XMLHTTP");
  xhr.open('POST', url);
  xhr.onreadystatechange = function() {
    if (xhr.readyState > 3 && xhr.status == 200) { success(xhr.responseText); }
  };
  xhr.setRequestHeader('X-Requested-With', 'XMLHttpRequest');
  xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
  xhr.send(params);
  return xhr;
}

// example request
postAjax('http://foo.bar/', 'p1=1&p2=Hello+World', function(data) { console.log(data); });

// example request with data object
postAjax('http://foo.bar/', { p1: 1, p2: 'Hello World' }, function(data) { console.log(data); });
```

- The Mozilla Developer Network provides a bunch of interesting Ajax examples and solutions. It's possible to send data in various formats, such as xml, json, script, text, and html. Modern browsers allow sending files and provide form serialization tools.

#### V. Serialize form data into an array

- Encode a set of form elements as an array of names and values.

- The following helper function ```serializeArray()``` takes one argument, a form node, and returns the form data as an array of name/value pairs:

```javascript
function serializeArray(form) {
  var field, l, s = [];
  if (typeof form == 'object' && form.nodeName == "FORM") {
    var len = form.elements.length;
    for (var i = 0; i < len; i++) {
      field = form.elements[i];
      if (field.name && !field.disabled && field.type != 'file' && field.type != 'reset' && field.type != 'submit' && field.type != 'button') {
        if (field.type == 'select-multiple') {
          l = form.elements[i].options.length;
          for (j = 0; j < l; j++) {
            if (field.options[j].selected)
              s[s.length] = { name: field.name, value: field.options[j].value };
          }
        } else if ((field.type != 'checkbox' && field.type != 'radio') || field.checked) {
          s[s.length] = { name: field.name, value: field.value };
        }
      }
    }
  }
  return s;
}
```

- The result is identical to what jQuery's ```$.serializeArray()``` returns.

#### VI. Serialize form data into a query string

- Encode a set of form elements as a string for submission.

- The following helper function ```serialize()``` takes one argument, a form node, and returns the form data as URL-encoded query string:

```javascript
function serialize(form) {
  var field, l, s = [];
  if (typeof form == 'object' && form.nodeName == "FORM") {
    var len = form.elements.length;
    for (var i = 0; i < len; i++) {
      field = form.elements[i];
      if (field.name && !field.disabled && field.type != 'file' && field.type != 'reset' && field.type != 'submit' && field.type != 'button') {
        if (field.type == 'select-multiple') {
          l = form.elements[i].options.length;
          for (var j = 0; j < l; j++) {
            if (field.options[j].selected)
              s[s.length] = encodeURIComponent(field.name) + "=" + encodeURIComponent(field.options[j].value);
          }
        } else if ((field.type != 'checkbox' && field.type != 'radio') || field.checked) {
          s[s.length] = encodeURIComponent(field.name) + "=" + encodeURIComponent(field.value);
        }
      }
    }
  }
  return s.join('&').replace(/%20/g, '+');
}
```

- The result is identical to what jQuery's ```$.serialize()``` returns.
