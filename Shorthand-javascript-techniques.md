### 1. If true … else Shorthand

**Longhand:**

```javascript
var big;
if (x > 10) {
  big = true;
} else {
  big = false;
}
```

**Shorthand:**

```javascript
var big = (x > 10) ? true : false;
```

**If you rely on some of the weak typing characteristics of JavaScript, this can also achieve more concise code. For example, you could reduce the preceding code fragment to this:**

```javascript
var big = (x > 10);

//further nested examples
var x = 3,
  big = (x > 10) ? "greater 10" : (x < 5) ? "less 5" : "between 5 and 10";
console.log(big); //"less 5"

var x = 20,
  big = { true: x > 10, false: x < = 10 };
console.log(big); //"Object {true=true, false=false}"
```

### 2. Null, Undefined, Empty Checks Shorthand

**When creating new variables sometimes you want to check if the variable your referencing for it’s value isn’t null or undefined. I would say this is a very common check for JavaScript coders.**

**Longhand:**

```javascript
if (variable1 !== null || variable1 !== undefined || variable1 !== '') {
  var variable2 = variable1;
}
```

**Shorthand:**

```javascript
var variable2 = variable1  || '';
```

### 3. Object Array Notation Shorthand

**Useful way of declaring small arrays on one line.**

**Longhand:**

```javascript
var a = new Array();
a[0] = "myString1";
a[1] = "myString2";
a[2] = "myString3";
```

** Shorthand:**

```javascript
var a = ["myString1", "myString2", "myString3"];
```

### 4. Associative Array Notation Shorthand

**The old school way of setting up an array was to create a named array and then add each named element one by one. A quicker and more readable way is to add the elements at the same time using the object literal notation. Please note that Associative Array are essentially JavaScript Objects with properties.**

**Longhand:**

```javascript
var skillSet = new Array();
skillSet['Document language'] = 'HTML5';
skillSet['Styling language'] = 'CSS3';
skillSet['Javascript library'] = 'jQuery';
skillSet['Other'] = 'Usability and accessibility';
```

**Shorthand:**

```javascript
var skillSet = {
    'Document language' : 'HTML5',
    'Styling language' : 'CSS3',
    'Javascript library' : 'jQuery',
    'Other' : 'Usability and accessibility'
};
```

**Don’t forget to omit the final comma otherwise certain browsers will complain (not naming any names, IE).**

### 5. Declaring variables Shorthand

**It is sometimes good practice to including variable assignments at the beginning of your functions. This shorthand method can save you lots of time and space when declaring multiple variables at the same time.**

**Longhand:**

```javascript
var x;
var y;
var z = 3;
```

** Shorthand:**

```javascript
var x, y, z=3;
```

### 6. Assignment Operators Shorthand

**Assignment operators are used to assign values to JavaScript variables and no doubt you use arithmetic everyday without thinking (no matter what programming language you use Java, PHP, C++ it’s essentially the same principle).**

**Longhand:**

```javascript
x=x+1;
minusCount = minusCount - 1;
y=y*10;
```

** Shorthand:**

```javascript
x++;
minusCount --;
y*=10;
```
**Other shorthand operators, given that x=10 and y=5, the table below explains the assignment operators:**

```javascript
x += y //result x=15
x -= y //result x=5
x *= y //result x=50
x /= y //result x=2
x %= y //result x=0
```
### 7. RegExp Object Shorthand

**Example to avoid using the RegExp object.**

**Longhand:**

```javascript
var re = new RegExp("\d+(.)+\d+","igm"),
result = re.exec("padding 01234 text text 56789 padding");
console.log(result); //"01234 text text 56789"
```

** Shorthand:**

```javascript
var result = /d+(.)+d+/igm.exec("padding 01234 text text 56789 padding");
console.log(result); //"01234 text text 56789"
```

### 8. If Presence Shorthand

**This might be trivial, but worth a mention. When doing “if checks” assignment operators can sometimes be ommited.**

**Longhand:**

```javascript
if (likeJavaScript == true)
```

** Shorthand:**

```javascript
if (likeJavaScript)
```
**Here is another example. If “a” is NOT equal to true, then do something.**

**Longhand:**

```javascript
var a;
if ( a != true ) {
// do something...
}
```

**Shorthand:**

```javascript
var a;
if ( !a ) {
// do something...
}
```

### 9. Function Variable Arguments Shorthand

**Object literal shorthand can take a little getting used to, but seasoned developers usually prefer it over a series of nested functions and variables. You can argue which technique is shorter, but I enjoy using object literal notation as a clean substitute to functions as constructors.**

**Longhand:**

```javascript
function myFunction( myString, myNumber, myObject, myArray, myBoolean ) {
    // do something...
}
myFunction( "String", 1, [], {}, true );
```

**Shorthand (looks long but only because I have console.log’s in there!):**

```javascript
function myFunction() {
    console.log( arguments.length ); // Returns 5
    for ( i = 0; i < arguments.length; i++ ) {
        console.log( typeof arguments[i] ); // Returns string, number, object, object, boolean
    }
}
myFunction( "String", 1, [], {}, true );
```

### 10. JavaScript foreach Loop Shorthand

**This little tip is really useful if you want plain JavaScript and hence can’t use jQuery.each or Array.forEach().**

**Longhand:**

```javascript
for (var i = 0; i < allImgs.length; i++)
```

**Shorthand:**

```javascript
for(var i in allImgs)
```

**Shorthand for Array.forEach:**

```javascript
function logArrayElements(element, index, array) {
    console.log("a[" + index + "] = " + element);
}
[2, 5, 9].forEach(logArrayElements);
// logs:
// a[0] = 2
// a[1] = 5
// a[2] = 9
```

### 11. charAt() Shorthand

**You can use the eval() function to do this but this bracket notation shorthand technique is much cleaner than an evaluation, and you will win the praise of colleagues who once scoffed at your amateur coding abilities!**

**Longhand:**

```javascript
"myString".charAt(0);
```

**Shorthand:**

```javascript
"myString"[0]; // Returns 'm'
```

### 12. Comparison returns

**We’re no longer relying on the less reliable == as !(ret == undefined) could be rewritten as !(ret) to take advantage of the fact that in an or expression, ret (if undefined or false) will skip to the next condition and use it instead. This allows us to trim down our 5 lines of code into fewer characters and it’s once again, a lot more readable.**

**Longhand:**

```javascript
if (!(ret == undefined)) {
      return ret;
  } else{
     return fum('g2g');
}
```

**Shorthand:**

```javascript
return ret || fum('g2g');
```

### 13. Short function calling

**Just like #1 you can use ternary operators to make function calling shorthand based on a conditional.**

**Longhand:**

```javascript
function x() { console.log('x') };

function y() { console.log('y') };
var z = 3;
if (z == 3) {
  x();
} else {
  y();
}

```

**Shorthand:**

```javascript
function x() {console.log('x')};function y() {console.log('y')};var z = 3;
(z==3?x:y)(); // Short version!
```

### 14. Switch Knightmare

**Everyone loves switch statements, cough. Here is how you might avoid switch case syndrome.**

**Longhand:**

```javascript
switch (something) {

  case 1:
    doX();
    break;

  case 2:
    doY();
    break;

  case 3:
    doN();
    break;

    // And so on...

}

```

**Shorthand:**

```javascript
var cases = {
  1: doX,
  2: doY,
  3: doN
};
if (cases[something]) {
  cases[something]();
}

```

### 15. Decimal base exponents

**You may have seen this one around it’s essentially a fancy way to write without the zeros. 1e7 essentially means 1 followed by 7 zeros – it represents a decimal base (JS interprets as a float type) equal to 10,000,000.**

**Longhand:**

```javascript
for (var i = 0; i < 10000; i++) {
```

**Shorthand:**

```javascript
for (var i = 0; i < 1e7; i++) {
```

### 16. Decimal base exponents

**You can use 1 and 0 to represent true and false. I’ve seen this used in JavaScript game development in shorthand while loops. Note that if you use the negative start your array may be in reverse. You can also use while(i++<10) and you don’t have to add the i++ later on inside the while.**

**Longhand:**

```javascript
var i = 0;
while (i & lt; 9) {
  //do stuff
  i++; //say
}

```

**Shorthand:**

```javascript
var i = 9;
while (i--) {
  //goes until i=0
}

or

var i = -9;
while (i++) {
  //goes until i=0
}

```

### 17. Shorter IF’z

**If you have mutiple IF variable value comparisons you can simply ass them to an array and check for presence. You could use $.inArray as an alternative.**

**Longhand:**

```javascript
if( myvar==1 || myvar==5 || myvar==7 || myvar==22 ) alert('yeah')
```

**Shorthand:**

```javascript
if([1,5,7,22].indexOf(myvar)!=-1) alert('yeah baby!')
```

### 18. Lookup Tables Shorthand

**If you have code that behaves differently based on the value of a property, it can often result in conditional statements with multiple else ifs or a switch cases. You may prefer to use a lookup table if there is more than two options (even a switch statement looks ugly!).**

**Longhand:**

```javascript
if (type === 'aligator') {
  aligatorBehavior();
} else if (type === 'parrot') {
  parrotBehavior();
} else if (type === 'dolphin') {
  dolphinBehavior();
} else if (type === 'bulldog') {
  bulldogBehavior();
} else {
  throw new Error('Invalid animal ' + type);
}

```

**Shorthand:**

```javascript
var types = {
  aligator: aligatorBehavior,
  parrot: parrotBehavior,
  dolphin: dolphinBehavior,
  bulldog: bulldogBehavior
};

var func = types[type];
if (!func) throw new Error('Invalid animal ' + type);
func();

```

### 19. Double Bitwise

**The double bitwise trick provides us with some pretty nifty shorthand tricks. Read more about it here: [Double bitwise NOT (~~)](http://james.padolsey.com/javascript/double-bitwise-not/).**

**Longhand:**

```javascript
Math.floor(4.9) === 4  //true
```

**Shorthand:**

```javascript
~~4.9 === 4  //true
```
