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

```javascript
a
```
**2.1 Finding HTML Elements**
---

- **document.getElementById(id)** -->	Find an element by element id
- **document.getElementsByTagName(name)** -->	Find elements by tag name
- **document.getElementsByClassName(name)** -->	Find elements by class name

**2.2 Changing HTML Elements**
---

- **element.innerHTML =  new html content** -->	Change the inner HTML of an element
- **element.attribute = new value** -->	Change the attribute value of an HTML element
- **element.setAttribute(attribute, value)** --> Change the attribute value of an HTML element
- **element.style.property = new style** --> Change the style of an HTML element

**2.3 Adding and Deleting Elements**
---

- **document.createElement(element)** -->	Create an HTML element
- **document.removeChild(element)** -->	Remove an HTML element
- **document.appendChild(element)** -->	Add an HTML element
- **document.replaceChild(element)** -->	Replace an HTML element
- **document.write(text)** -->	Write into the HTML output stream

**2.4 Adding Events Handlers**
---

- **document.getElementById(id).onclick = function(){code}** --> Adding event handler code to an onclick event

**2.5 Finding HTML Objects**
---

- **document.anchors** -->	Returns all <a> elements that have a name attribute	1
- **document.applets** -->	Returns all <applet> elements (Deprecated in HTML5)	1
- **document.baseURI** -->	Returns the absolute base URI of the document	3
  
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

- **document.cookie** -->	Returns the document's cookie	1
- **document.doctype** -->	Returns the document's doctype	3
- **document.documentElement** -->	Returns the <html> element	3
- **document.documentMode** -->	Returns the mode used by the browser	3
- **document.documentURI** -->	Returns the URI of the document	3
- **document.domain** -->	Returns the domain name of the document server	1
- **document.domConfig** -->	Obsolete. Returns the DOM configuration	3
- **document.embeds** -->	Returns all <embed> elements	3
- **document.forms** -->	Returns all <form> elements	1
- **document.head** -->	Returns the <head> element	3
- **document.images** -->	Returns all <img> elements	1
- **document.implementation** -->	Returns the DOM implementation	3
- **document.inputEncoding** -->	Returns the document's encoding (character set)	3
- **document.lastModified** -->	Returns the date and time the document was updated	3
- **document.links** -->	Returns all <area> and <a> elements that have a href attribute	1
- **document.readyState** -->	Returns the (loading) status of the document	3
- **document.referrer** -->	Returns the URI of the referrer (the linking document)	1
- **document.scripts** -->	Returns all <script> elements	3
- **document.strictErrorChecking** -->	Returns if error checking is enforced	3
- **document.title** -->	Returns the <title> element	1
- **document.URL** -->	Returns the complete URL of the document

### 3. DOM Elements

```javascript
a
```

### 4. DOM - Changing HTML

```javascript
a
```

### 5. DOM - Changing CSS

```javascript
a
```

### 6. DOM Animation

```javascript
a
```

### 7. DOM Events

```javascript
a
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
