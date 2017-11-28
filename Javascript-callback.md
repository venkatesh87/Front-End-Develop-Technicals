### CallBack trong javascript

#### I.Basic Principles when Implementing Callback Functions: Các nguyên tắc cơ bản khi thực hiện Callback Functions.

##### 1. Use Named OR Anonymous Functions as Callbacks
***

```javascript
// global variable​
​
var allUserData = [];​​ // generic logStuff function that prints to console​
​
function logStuff(userData) {
  if (typeof userData === "string") {
    console.log(userData);
  } else if (typeof userData === "object") {
    for (var item in userData) {
      console.log(item + ": " + userData[item]);
    }​
  }​
}​​ // A function that takes two parameters, the last one a callback function​
​
function getInput(options, callback) {
  allUserData.push(options);
  callback(options);​
}​​ // When we call the getInput function, we pass logStuff as a parameter.​
​ // So logStuff will be the function that will called back (or executed) inside the getInput function​
getInput({ name: "Rich", speciality: "JavaScript" }, logStuff);​ //  name: Rich​
​ // speciality: JavaScript
```
