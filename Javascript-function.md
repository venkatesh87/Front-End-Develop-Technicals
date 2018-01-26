### I. Function Definitions
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
### II. Function Parameters
---
- Function parameters are the names listed in the function definition.
- Function arguments are the real values passed to (and received by) the function.

>**1. Function Parameters**
```javascript
functionName(parameter1, parameter2, parameter3) {
    code to be executed
}
```
>**2. Parameter Rules**
- JavaScript function definitions do not specify data types for parameters.
- JavaScript functions do not perform type checking on the passed arguments.
- JavaScript functions do not check the number of arguments received.

>**3. Parameter Defaults**
- If a function is called with missing arguments (less than declared), the missing values are set to: undefined
- Sometimes this is acceptable, but sometimes it is better to assign a default value to the parameter:

```javascript
function myFunction(x, y) {
    if (y === undefined) {
        y = 1;
    }    
    return x * y;
}
document.getElementById("demo").innerHTML = myFunction(4);
```

>**4. The Arguments Object**
```javascript
function findMax() {
    var i;
    var max = -Infinity;
    for(i = 0; i < arguments.length; i++) {
        if (arguments[i] > max) {
            max = arguments[i];
        }
    }
    return max;
} 
document.getElementById("demo").innerHTML = findMax(4, 5, 6);
```
```javascript
function sumAll() {
    var i;
    var sum = 0;
    for(i = 0; i < arguments.length; i++) {
        sum += arguments[i];
    }
    return sum;
} 
document.getElementById("demo").innerHTML =
sumAll(1, 2, 3, 4, 5, 6);
```
### III. Function Invocation
---

>**1. Invoking a Function as a Function**
```javascript
function myFunction(a, b) {
    return a * b;
}
myFunction(10, 2); 
```
- In JavaScript there is always a default global object 
- myFunction() and window.myFunction() is the same function

```javascript
function myFunction(a, b) {
    return a * b;
}
window.myFunction(10, 2);
```

>**2. The this Keyword**

- In JavaScript, the thing called **this**, is the object that "owns" the current code.
- The value of **this**, when used in a function, is the object that "owns" the function.
- Note that **this** is not a variable. It is a keyword. You cannot change the value of **this**.

>**3. The Global Object**
- When a function is called without an owner object, the value of this becomes the global object.
- In a web browser the global object is the browser window.
- This example returns the window object as the value of this

>**4. Invoking a Function as a Method**
- In JavaScript you can define function as object methods.
- The following example creates an object (myObject), with two properties (firstName and lastName), and a method (fullName):

```javascript
var myObject = {
    firstName:"John",
    lastName: "Doe",
    fullName: function () {
        return this.firstName + " " + this.lastName;
    }
}
myObject.fullName(); 
```

The fullName method is a function. The function belongs to the object. myObject is the owner of the function.
The thing called this, is the object that "owns" the JavaScript code. In this case the value of this is myObject.

```
var myObject = {
    firstName:"John",
    lastName: "Doe",
    fullName: function () {
        return this;
    }
}
myObject.fullName(); 
```

>**5. Invoking a Function with a Function Constructor**

```
// This is a function constructor:
function myFunction(arg1, arg2) {
    this.firstName = arg1;
    this.lastName  = arg2;
}
// This creates a new object
var x = new myFunction("John", "Doe");
x.firstName;
```
### IV. Function Call
---

>**1. Functions are Object Methods**
```javascript
var person = {
    firstName:"John",
    lastName: "Doe",
    fullName: function () {
        return this.firstName + " " + this.lastName;
    }
}
person.fullName();         // Will return "John Doe"
```

>**2. The JavaScript call() Method**
- With call(), you can use a method belonging to another object.
```javascript
var person = {
    firstName:"John",
    lastName: "Doe",
    fullName: function() {
        return this.firstName + " " + this.lastName;
    }
}
var myObject = {
    firstName:"Mary",
    lastName: "Doe",
}
person.fullName.call(myObject);  // Will return "Mary Doe"
```

### V. Function Apply
---

>**1. The ```apply()``` method is similar to the ```call()``` method:**
```javascript
var person = {
    firstName:"John",
    lastName: "Doe",
    fullName: function() {
        return this.firstName + " " + this.lastName;
    }
}
var myObject = {
    firstName:"Mary",
    lastName: "Doe",
}
person.fullName.apply(myObject);  // Will return "Mary Doe"
```

>**2. The Difference Between ```call()``` and ```apply()```**
- ```call()``` takes any function arguments separately.
- ```apply()``` takes any function arguments as an array.
- If you want to obtain the largest number in a list of numbers you can use the ```Math.max()``` method:
```javascript
Math.max(1,2,3);  // Will return 3
```
```javascript
Math.max(1,2,3);  // Will return 3
```
- Since JavaScript arrays do not have a ```max()``` method, you can apply the ```Math.max()``` instead.
```javascript
Math.max.apply(null,[1,2,3]); // Will also return 3
```
### V. JavaScript Closures
---

- JavaScript variables can belong to the local or global scope.
- Global variables can be made local (private) with closures.


>**1.Global Variables**
- A function can access all variables defined inside the function, like this
```javascript
function myFunction() {
    var a = 4;
    return a * a;
}
```
- But a function can also access variables defined outside the function, like this:
```javascript
var a = 4;
function myFunction() {
    return a * a;
}
```

>**2. Variable Lifetime**
- Global variables live as long as your application (your window / your web page) lives.
- Local variables have short lives. They are created when the function is invoked, and deleted when the function is finished.
```javascript

```

>**3.A Counter Dilemma**
- Suppose you want to use a variable for counting something, and you want this counter to be available to all functions.
- You could use a global variable, and a function to increase the counter:

**Increase one unit on click**
```javascript
var counter = 0;

function add() {
    return counter += 1;
}

function myFunction(){
    document.getElementById("demo").innerHTML = add();
}
// Increase one unit on click
```

**Increases only 1**
```javascript
function add() {
    var counter = 0;
    return counter += 1;
}
function myFunction(){
    document.getElementById("demo").innerHTML = add();
}
```

>**4.JavaScript Nested Functions**
```javascript
document.getElementById("demo").innerHTML = add();
function add() {
    var counter = 0;
    function plus() {counter += 1;}
    plus();    
    return counter; // 1
}
```

>**5. self-invoking functions**
```javascript
var add = (function () {
    var counter = 0;
    return function () {return counter += 1;}
})();

function myFunction(){
    document.getElementById("demo").innerHTML = add();
}
```
