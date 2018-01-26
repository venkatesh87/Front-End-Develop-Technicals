### I. JavaScript Function
---

**1. JavaScript Function Definitions**
---
- JavaScript functions are defined with the function keyword.
- You can use a function declaration or a function expression.

**2. Function Declarations**
---
```javascript
function functionName(parameters) {
  code to be executed
}
```
```javascript
var x = myFunction(4, 3);
document.getElementById("demo").innerHTML = x;

function myFunction(a, b) {
    return a * b;
}
```

**3. Function Expressions**
---
- A JavaScript function can also be defined using an expression.
- A function expression can be stored in a variable:
```javascript
var x = function (a, b) {return a * b};
document.getElementById("demo").innerHTML = x;
```

- After a function expression has been stored in a variable, the variable can be used as a function:
```javascript
var x = function (a, b) {return a * b};
var z = x(4, 3);
```

**4. The Function() Constructor**
---

```javascript
var myFunction = new Function("a", "b", "return a * b");
document.getElementById("demo").innerHTML = myFunction(4, 3);
```

**5. Function Hoisting**
---

```javascript
myFunction(5);

function myFunction(y) {
    return y * y;
}
```

**6. Self-Invoking Functions**
---
- Function expressions can be made "self-invoking".
- A self-invoking expression is invoked (started) automatically, without being called.
- Function expressions will execute automatically if the expression is followed by ().
- You cannot self-invoke a function declaration.
- You have to add parentheses around the function to indicate that it is a function expression:
```javascript
(function () {
    var x = "Hello!!";      // I will invoke myself
})();
```

**7. Functions Can Be Used as Values**
---
**JavaScript functions can be used as values:**
```javascript
function myFunction(a, b) {
    return a * b;
}
var x = myFunction(4, 3);
document.getElementById("demo").innerHTML = x;
```

**JavaScript functions can be used in expressions:**
```javascript
function myFunction(a, b) {
    return a * b;
}
var x = myFunction(4, 3) * 2;
```
**8. Functions are Objects**
---
- The typeof operator in JavaScript returns "function" for functions.
- But, JavaScript functions can best be described as objects.
- JavaScript functions have both properties and methods.
- The arguments.length property returns the number of arguments received when the function was invoked:

```javascript
function myFunction(a, b, c) {
    return arguments.length;
}
document.getElementById("demo").innerHTML = myFunction(4, 3, 3);
```

```javascript
function myFunction(a, b) {
    return a * b;
}
document.getElementById("demo").innerHTML = myFunction.toString();
```
