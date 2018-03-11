#### I. Demystifying JavaScript Variable Scope and Hoisting
---

>**1. Variable Scope**

```javascript
var locales = {
  europe: function() {          // The Europe continent's local scope
    var myFriend = "Monique";

    var france = function() {   // The France country's local scope
      var paris = function() {  // The Paris city's local scope
        console.log(myFriend);
      };

      paris();
    };

    france();
  }
};

locales.europe();
```


```javascript
var test = "I'm global";

function testScope() {
  var test = "I'm local";

  console.log (test);     
}

testScope();           // output: I'm local

console.log(test);     // output: I'm global
```

```javascript
var test = "I'm global";

function testScope() {
  test = "I'm local";

  console.log(test);     
}

console.log(test);     // output: I'm global

testScope();           // output: I'm local

console.log(test);     // output: I'm local (the global variable is reassigned)
```

>**2. Hoisting**

```javascript
var state;             // variable declaration
state = "ready";       // variable definition (assignment)

var state = "ready";   // declaration plus definition
```

```javascript
console.log(state);   // output: undefined
var state = "ready";
```

```javascript
var state;           // moved to the top
console.log(state);   
state = "ready";     // left in place
```

```javascript
function showState() {}          // function declaration
var showState = function() {};   // function expression
```

```javascript
showState();            // output: Ready

function showState() {
  console.log("Ready");
} 

var showState = function() {
  console.log("Idle");
};
```

```javascript
function showState() {     // moved to the top (function declaration)
  console.log("Ready");
} 

var showState;            // moved to the top (variable declaration)

showState();  

showState = function() {   // left in place (variable assignment)
  console.log("Idle");
};
```

```javascript
var showState = function() {
  console.log("Idle");
};

function showState() {
  console.log("Ready");
} 

showState();            // output: Idle
```

```javascript
function showState(){        // moved to the top (function declaration)
  console.log("Ready");
} 

var showState;               // moved to the top (variable declaration)

showState = function(){      // left in place (variable assignment)
  console.log("Idle");
};

showState();
```