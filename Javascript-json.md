### I. JS JSON
---

- JSON: JavaScript Object Notation.
- JSON is a syntax for storing and exchanging data.
- JSON is text, written with JavaScript object notation.

**1. Exchanging Data**
---
```javascript

```

**2. Sending Data**
---
- If you have data stored in a JavaScript object, you can convert the object into JSON, and send it to a server:
- ```JSON.stringify(myObj)```: Convert the object into JSON
```javascript
var myObj = { "name":"John", "age":31, "city":"New York" };
var myJSON = JSON.stringify(myObj);
window.location = "demo_json.php?x=" + myJSON;
alert('myJSON');
```

**3. Receiving Data**
---
- If you receive data in JSON format, you can convert it into a JavaScript object:
```javascript
var myJSON = '{ "name":"John", "age":31, "city":"New York" }';
var myObj = JSON.parse(myJSON);
document.getElementById("demo").innerHTML = myObj.name;
```

**4. Storing Data**
---
- When storing data, the data has to be a certain format, and regardless of where you choose to store it, text is always one of the legal formats.
- JSON makes it possible to store JavaScript objects as text.
- ```localStorage.setItem()```, ```localStorage.getItem()```
```<p id="demo"></p>```

```javascript
var myObj, myJSON, text, obj;

//Storing data:
myObj = { "name":"John", "age":31, "city":"New York" };
myJSON = JSON.stringify(myObj);
localStorage.setItem("testJSON", myJSON);

//Retrieving data:
text = localStorage.getItem("testJSON");
obj = JSON.parse(text);
document.getElementById("demo").innerHTML = obj.name;
```

**5. Exchanging Data**

```javascript

```

### II. JSON Syntax

>**JSON Data - A Name and a Value**
```"name":"John"```
>**JSON**
```{ "name":"John" }```

>**JavaScript**
```{ name:"John" }```

>**JSON Values**:
- **In JSON**, values must be one of the following data types: 
 + a string
 + a number
 + an object (JSON object)
 + an array
 + a boolean
 + null
- **In JavaScript** values can be all of the above, plus any other valid JavaScript expression, including:
 + a function
 + a date
 + undefined
>**JSON Uses JavaScript Syntax**

**You can access a JavaScript object like this:**
```javascript
var myObj, x;
myObj = { "name":"John", "age":30, "city":"New York" };
x = myObj.name;
document.getElementById('demo').innerHTML = x;
```

**It can also be accessed like this:**
```javascript
var myObj, x;
myObj = { "name":"John", "age":30, "city":"New York" };
x = myObj[name];
document.getElementById('demo').innerHTML = x;
```

**Data can be modified like this:**
```javascript
var myObj;
myObj = { "name":"John", "age":30, "city":"New York" };
myObj.name = "Dao";
document.getElementById('demo').innerHTML = myObj.name;
```

**It can also be modified like this:**
```javascript
var myObj;
myObj = { "name":"John", "age":30, "city":"New York" };
myObj[name] = "Dao";
document.getElementById('demo').innerHTML = myObj[name];
```

