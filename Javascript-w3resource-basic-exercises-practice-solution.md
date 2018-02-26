#### I. JavaScript basic - Exercises, Practice, Solution
---
**1. Write a JavaScript program to display the current day and time in the following format.**
- Today is : Friday. 
- Current time is : 4 PM : 50 : 22

>JavaScript Code:
```javascript
var today = new Date();
var day = today.getDay();
var daylist = ["Sunday", "Monday", "Tuesday", "Wednesday ", "Thursday", "Friday", "Saturday"];
console.log("Today is : " + daylist[day] + ".");
var hour = today.getHours();
var minute = today.getMinutes();
var second = today.getSeconds();
var prepand = (hour >= 12) ? " PM " : " AM ";
hour = (hour >= 12) ? hour - 12 : hour;
if (hour === 0 && prepand === ' PM ') {
  if (minute === 0 && second === 0) {
    hour = 12;
    prepand = ' Noon';
  } else {
    hour = 12;
    prepand = ' PM';
  }
}
if (hour === 0 && prepand === ' AM ') {
  if (minute === 0 && second === 0) {
    hour = 12;
    prepand = ' Midnight';
  } else {
    hour = 12;
    prepand = ' AM';
  }
}
console.log("Current Time : " + hour + prepand + " : " + minute + " : " + second);
```

>ES6 Version:
```javascript
const today = new Date();
const day = today.getDay();
const daylist = ["Sunday", "Monday", "Tuesday", "Wednesday ", "Thursday", "Friday", "Saturday"];
console.log(`Today is : ${daylist[day]}.`);
let hour = today.getHours();
const minute = today.getMinutes();
const second = today.getSeconds();
let prepand = (hour >= 12) ? " PM " : " AM ";
hour = (hour >= 12) ? hour - 12 : hour;
if (hour === 0 && prepand === ' PM ') {
  if (minute === 0 && second === 0) {
    hour = 12;
    prepand = ' Noon';
  } else {
    hour = 12;
    prepand = ' PM';
  }
}
if (hour === 0 && prepand === ' AM ') {
  if (minute === 0 && second === 0) {
    hour = 12;
    prepand = ' Midnight';
  } else {
    hour = 12;
    prepand = ' AM';
  }
}
console.log(`Current Time : ${hour}${prepand} : ${minute} : ${second}`);
```

>Result:
```javascript
Today is : Tuesday.
Current Time : 5 PM  : 51 : 20
```

**2. Write a JavaScript function to print the contents of the current window**

>JavaScript Code:
```javascript
function print_current_page(){
  window.print();
}
```

>ES6 Version:
```javascript
function print_current_page(){
  window.print();
}
```

**3. Write a JavaScript program to get the current date.**
**Expected Output :**
- mm-dd-yyyy, mm/dd/yyyy or dd-mm-yyyy, dd/mm/yyyy

>JavaScript Code:
```javascript
var today = new Date();
var dd = today.getDate();

var mm = today.getMonth() + 1;
var yyyy = today.getFullYear();
if (dd < 10) {
  dd = '0' + dd;
}

if (mm < 10) {
  mm = '0' + mm;
}
today = mm + '-' + dd + '-' + yyyy;
console.log(today);
today = mm + '/' + dd + '/' + yyyy;
console.log(today);
today = dd + '-' + mm + '-' + yyyy;
console.log(today);
today = dd + '/' + mm + '/' + yyyy;
console.log(today);
```

>ES6 Version:
```javascript
let today = new Date();
let dd = today.getDate();

let mm = today.getMonth() + 1;
const yyyy = today.getFullYear();
if (dd < 10) {
  dd = `0${dd}`;
}

if (mm < 10) {
  mm = `0${mm}`;
}
today = `${mm}-${dd}-${yyyy}`;
console.log(today);
today = `${mm}/${dd}/${yyyy}`;
console.log(today);
today = `${dd}-${mm}-${yyyy}`;
console.log(today);
today = `${dd}/${mm}/${yyyy}`;
console.log(today);
```

**4. Write a JavaScript function to find the area of a triangle where lengths of the three of its sides are 5, 6, 7**

>JavaScript Code:
```javascript
var side1 = 5; 
var side2 = 6; 
var side3 = 7; 
var perimeter = (side1 + side2 + side3)/2;
var area =  Math.sqrt(perimeter*((perimeter-side1)*(perimeter-side2)*(perimeter-side3)));
console.log(area);
```

>ES6 Version:
```javascript
const side1 = 5; 
const side2 = 6; 
const side3 = 7; 
const perimeter = (side1 + side2 + side3)/2;
const area =  Math.sqrt(perimeter*((perimeter-side1)*(perimeter-side2)*(perimeter-side3)));
console.log(area);
```
>Result:
```javascript
14.696938456699069
```

**5. Rotate the string 'w3resource' in right direction by periodically removing one letter from the end of the string and attaching it to the front**

>JavaScript Code:
```javascript
function animate_string(id) {
  var element = document.getElementById(id);
  var textNode = element.childNodes[0]; // assuming no other children
  var text = textNode.data;

  setInterval(function() {
    text = text[text.length - 1] + text.substring(0, text.length - 1);
    textNode.data = text;
  }, 100);
}
```

>ES6 Version:
```javascript
function animate_string(id) {
  const element = document.getElementById(id);
  const textNode = element.childNodes[0]; // assuming no other children
  let text = textNode.data;

  setInterval(() => {
    text = text[text.length - 1] + text.substring(0, text.length - 1);
    textNode.data = text;
  }, 100);
}
```

**6. Write a JavaScript program to determine whether a given year is a leap year in the Gregorian calendar.**

>JavaScript Code:
```javascript
year = window.prompt("Input a Year : ");
x = (year % 100 === 0) ? (year % 400 === 0) : (year % 4 === 0);
console.log(x);
```

```javascript
var elm = document.getElementById('year_check');
elm.addEventListener('input', leapYear);

function leapYear() {
  if (this.value % 4 === 0) {
    if (this.value % 100 === 0) {
      if (this.value % 400 === 0) {
        document.getElementById('demo').innerHTML = 'Năm ' + this.value + ' Là Năm Nhuận';
      } else {
        document.getElementById('demo').innerHTML = 'Năm ' + this.value + ' Không Phải Là Năm Nhuận';
      }
    } else {
      document.getElementById('demo').innerHTML = 'Năm ' + this.value + ' Là Năm Nhuận';
    }
  } else {
    document.getElementById('demo').innerHTML = 'Năm ' + this.value + ' Không Phải Là Năm Nhuận';
  }
}
```

>ES6 Version:
```javascript
year = window.prompt("Input a Year : ");
x = (year % 100 === 0) ? (year % 400 === 0) : (year % 4 === 0);
console.log(x);
```

**7. Write a JavaScript program to find which 1st January is being a Sunday between 2014 and 2050.**

>JavaScript Code:
```javascript
for (let year = 2014; year <= 2050; year++) {
  const date = new Date(year, 0, 1);
  if (date.getDay() === 0) {
    console.log("1st January is being a Sunday  " + year);
  }
}
```

>ES6 Version:
```javascript
console.log('--------------------');
for (let year = 2014; year <= 2050; year++){
  const d = new Date(year, 0, 1);
  if ( d.getDay() === 0 )
     console.log(`1st January is being a Sunday  ${year}`);
}
console.log('--------------------');
```

**8. Write a JavaScript program where the program takes a random integer between 1 to 10, the user is then prompted to input a guess number. If the user input matches with guess number, the program will display a message "Good Work" otherwise display a message "Not matched".**

>JavaScript Code:
```javascript
// Get a random integer from 1 to 10 inclusive
 var num = Math.ceil(Math.random() * 10);
 var gnum = prompt('Guess the number between 1 and 10 inclusive');
 if (gnum == num)
   alert('Matched');
  else
   alert('Not matched, the number was ' + num);
```

>ES6 Version:
```javascript
const num = Math.ceil(Math.random() * 10);
const gnum = prompt('Guess the number between 1 and 10 inclusive');
if (gnum == num)
  alert('Matched');
else
  alert('Not matched, the number was ${num}');
```

**9. Write a JavaScript program to calculate number of days left until next Christmas.**

>JavaScript Code:
```javascript
today=new Date();
var cmas=new Date(today.getFullYear(), 11, 25);
if (today.getMonth()==11 && today.getDate()>25) {
  cmas.setFullYear(cmas.getFullYear()+1); 
}
// convert to milliseconds for a day
var one_day=1000*60*60*24;
console.log(Math.ceil((cmas.getTime()-today.getTime())/(one_day))+" days left until Christmas!");
```

>ES6 Version:
```javascript
today=new Date();
const cmas=new Date(today.getFullYear(), 11, 25);
if (today.getMonth()==11 && today.getDate()>25) {
  cmas.setFullYear(cmas.getFullYear()+1); 
}
// convert to milliseconds for a day
const one_day=1000*60*60*24;
console.log(`${Math.ceil((cmas.getTime()-today.getTime())/(one_day))} days left until Christmas!`);
```

**10. Write a JavaScript program to calculate multiplication and division of two numbers (input from user).**

>HTML:
```javascript
<form>
  1st Number : <input type="text" id="firstNumber" /><br>
  2nd Number: <input type="text" id="secondNumber" /><br>
  <input type="button" onClick="multiplyBy()" Value="Multiply" />
  <input type="button" onClick="divideBy()" Value="Divide" />
</form>
<p>The Result is : <br>
  <span id = "result"></span>
</p>
```

>JavaScript Code:
```javascript
function multiplyBy(){
  num1 = document.getElementById("firstNumber").value;
  num2 = document.getElementById("secondNumber").value;
  document.getElementById("result").innerHTML = num1 * num2;
}

function divideBy() { 
  num1 = document.getElementById("firstNumber").value;
  num2 = document.getElementById("secondNumber").value;
  document.getElementById("result").innerHTML = num1 / num2;
}
```

>ES6 Version:
```javascript
function multiplyBy(){
  num1 = document.getElementById("firstNumber").value;
  num2 = document.getElementById("secondNumber").value;
  document.getElementById("result").innerHTML = num1 * num2;
}

function divideBy() { 
  num1 = document.getElementById("firstNumber").value;
  num2 = document.getElementById("secondNumber").value;
  document.getElementById("result").innerHTML = num1 / num2;
}
```

**11. Write a JavaScript program to get the website URL (loading page).**

>JavaScript Code:
```javascript
alert(document.URL);
```

>ES6 Version:
```javascript
alert(document.URL);
```

**12. Write a JavaScript exercise to create a variable using a user-defined name.**

>JavaScript Code:
```javascript
var var_name = 'abcd';
var n = 120;
this[var_name] = n;
console.log(this[var_name])
```

>ES6 Version:
```javascript
const var_name = 'abcd';
const n = 120;
this[var_name] = n;
console.log(this[var_name])
```

**13. Write a JavaScript exercise to get the extension of a filename.**
- The ```split()``` method is used to split a string into an array of substrings, and returns the new array.
- The ```pop()``` method removes the last element of an array, and returns that element.

>JavaScript Code:
```javascript
filename = "system.php"
console.log(filename.split('.').pop());
filename = "abc.js"
console.log(filename.split('.').pop());
```

>ES6 Version:
```javascript
filename = "system.php"
console.log(filename.split('.').pop());
filename = "abc.js"
console.log(filename.split('.').pop());
```

**14. Write a JavaScript program to get the difference between a given number and 13, if the number is greater than 13 return double the absolute difference.**

>JavaScript Code:
```javascript
function difference(n)
 {
    if (n <= 13)
        return 13 - n;
    else
        return (n - 13) * 2;
 }
console.log(difference(50))
console.log(difference(10))
```

>ES6 Version:
```javascript
function difference(n){
    if (n <= 13)
        return 13 - n;
    else
        return (n - 13) * 2;
 }
console.log(difference(50))
console.log(difference(10))
```

**15. Write a JavaScript program to compute the sum of the two given integers. If the two values are same, then returns triple their sum.**

>JavaScript Code:
```javascript
function sumTriple(x, y){
  if(x == y){
    return 3*(x+y);
  }
  else{
    return (x+y);
  }
}
console.log(sumTriple(10, 20));
console.log(sumTriple(10, 10));
```

>ES6 Version:
```javascript
function sumTriple (x, y) {
  if (x == y) {
    return 3 * (x + y);
    } 
   else
   {
    return (x + y);
   }
 }
console.log(sumTriple(10, 20));
console.log(sumTriple(10, 10));
```

**16. Write a JavaScript program to compute the absolute difference between a specified number and 19. Returns triple their absolute difference if the specified number is greater than 19.**

>JavaScript Code:
```javascript
function diff_num(n) {
  if (n <= 19) {
    return (19 - n);
  }
  else{
     return (n - 19) * 3;
  }
}

console.log(diff_num(12));
console.log(diff_num(19));
console.log(diff_num(22));
```

>ES6 Version:
```javascript
function diff_num(n) {
  if (n <= 19) {
    return (19 - n);
  }
  else {
     return (n - 19) * 3;
  }
}

console.log(diff_num(12));
console.log(diff_num(19));
console.log(diff_num(22));
```

**17. Write a JavaScript program to check two given numbers and return true if one of the number is 50 or if their sum is 50.**

>JavaScript Code:
```javascript
function test50(x, y){
  if((x == 50 || y == 50) || (x+y == 50)){
    return true;
  }
  else{
    return false;
  }
 }
  console.log(test50(10, 10));
  console.log(test50(25, 25));
  console.log(test50(25, 50));
  console.log(test50(50, 25));
```

```javascript
function test50(x, y) {
  return ((x == 50 || y == 50) || (x + y == 50));
}
console.log(test50(50, 50))
console.log(test50(20, 50))
console.log(test50(20, 20))
console.log(test50(20, 30))
```

>ES6 Version:
```javascript
function test50(x, y) {
  return ((x == 50 || y == 50) || (x + y == 50));
}
console.log(test50(50, 50))
console.log(test50(20, 50))
console.log(test50(20, 20))
console.log(test50(20, 30))
```

**18. Write a JavaScript program to check a given integer is within 20 of 100 or 400**

>JavaScript Code:
```javascript
function testhundred(x) {
  return ((Math.abs(100 - x) <= 20) ||
	 (Math.abs(400 - x) <= 20));
}

console.log(testhundred(10));
console.log(testhundred(90));
console.log(testhundred(99));
console.log(testhundred(199));
console.log(testhundred(200));
```

>ES6 Version:
```javascript
function testhundred(x) {
  return ((Math.abs(100 - x) <= 20) ||
	 (Math.abs(400 - x) <= 20));
}

console.log(testhundred(10));
console.log(testhundred(90));
console.log(testhundred(99));
console.log(testhundred(199));
console.log(testhundred(200));
```

```javascript
false
true
true
false
false
```

**19. Write a JavaScript program to check from two given integers, if one is positive and one is negative**

>JavaScript Code:
```javascript
function positive_negative(x, y){
  if ((x < 0 && y > 0) || x > 0 && y < 0) {
    return true;
  }
  else {
    return false;
  }
}
console.log(positive_negative(2, 2));
console.log(positive_negative(-2, 2));
console.log(positive_negative(2, -2));
console.log(positive_negative(-2, -2));
```

>ES6 Version:
```javascript
function positive_negative(x, y){
  if ((x < 0 && y > 0) || x > 0 && y < 0) {
    return true;
  }
  else {
    return false;
  }
}
console.log(positive_negative(2, 2));
console.log(positive_negative(-2, 2));
console.log(positive_negative(2, -2));
console.log(positive_negative(-2, -2));
```

**20. Write a JavaScript program to create a new string adding "Py" in front of a given string. If the given string begins with "Py" then return the original string.**

>JavaScript Code:
```javascript
function string_check(str1) {
  if (str1 === null || str1 === undefined || str1.substring(0, 2) === 'Py') {
    return str1;
  }
  return "Py"+str1;
}

console.log(string_check("Python"));
console.log(string_check("thon"));
console.log(string_check(""));
console.log(string_check());
```

>ES6 Version:
```javascript
function string_check(str1) {
  if (str1 === null || str1 === undefined || str1.substring(0, 2) === 'Py') {
    return str1;
  }
  return `Py${str1}`;
}

console.log(string_check("Python"));
console.log(string_check("thon"));
console.log(string_check(""));
console.log(string_check());
```

**21. Write a JavaScript program to remove a character at the specified position of a given string and return the new string**

>JavaScript Code:
```javascript
function remove_character(str, char_pos){
  part1 = str.substring(0, char_pos);
  part2 = str.substring(char_pos+1, str.length);
  return part1 + part2;
}
console.log(remove_character('Python', 2));
console.log(remove_character('Python', 3));
console.log(remove_character('Python', 5));
```

>ES6 Version:
```javascript
function remove_character(str, char_pos) {
  part1 = str.substring(0, char_pos);
  part2 = str.substring(char_pos + 1, str.length);
  return (part1 + part2);
 }

console.log(remove_character("Python",0));
console.log(remove_character("Python",3));
console.log(remove_character("Python",5));
```
>Result:
```javascript
"ython"
"Pyton"
"Pytho"
```

**22. Write a JavaScript program to create a new string from a given string changing the position of first and last characters. The string length must be greater than or equal to 1**
- The ```charAt()``` method returns the character at the specified index in a string.
- The ```index``` of the first character is ```0```, the second character is ```1```, and so on.
- Return the first character of a string: ```var str = "HELLO WORLD"; str.charAt(0)```

>JavaScript Code:
```javascript
function first_last(str1) {
  if (str1.length <= 1){
    return str1;
  }
  mid_char = str1.substring(1, str1.length - 1);
  return (str1.charAt(str1.length - 1)) + mid_char + str1.charAt(0);
}
console.log(first_last('a'));
console.log(first_last('ab'));
console.log(first_last('abc'));
```

>ES6 Version:
```javascript
function first_last(str1) {
  if (str1.length <= 1){
    return str1;
  }
  mid_char = str1.substring(1, str1.length - 1);
  return (str1.charAt(str1.length - 1)) + mid_char + str1.charAt(0);
}
console.log(first_last('a'));
console.log(first_last('ab'));
console.log(first_last('abc'));
```

>Result:
```javascript
a
ba
cba
```

**23. Write a JavaScript program to create a new string from a given string with the first character of the given string added at the front and back**

>JavaScript Code:
```javascript
function front_back(str){
  first = str.substring(0,1);
  return first + str + first;
}
console.log(front_back('a'));
console.log(front_back('ab'));
console.log(front_back('abc'));
```

>ES6 Version:
```javascript
function front_back(str){
  first = str.substring(0,1);
  return first + str + first;
}
console.log(front_back('a'));
console.log(front_back('ab'));
console.log(front_back('abc'));
```

>Result:
```javascript
aaa
aaba
aabca
```

**24. Write a JavaScript program check if a given positive number is a multiple of 3 or a multiple of 7**

>JavaScript Code:
```javascript
function test37(x) {
  if (x % 3 == 0 || x % 7 == 0) {
    return true;
  } 
  else {
    return false;
  }
}

console.log(test37(12));
console.log(test37(14));
console.log(test37(10));
console.log(test37(11));
```

>ES6 Version:
```javascript
function test37(x) {
  if (x % 3 == 0 || x % 7 == 0) {
    return true;
  } else {
    return false;
  }
}

console.log(test37(12));
console.log(test37(14));
console.log(test37(10));
console.log(test37(11));
```
>Result:
```javascript
true
true
false
false
```
**25. Write a JavaScript program to create a new string from a given string taking the last 3 characters and added at both the front and back. The string length must be 3 or more.**

>JavaScript Code:
```javascript
function front_back3(str){
  if (str.length>=3){
   back = str.substring(str.length-3);
   return back + str + back;
  }
  else
   return false;
 }
console.log(front_back3("abc"));
console.log(front_back3("ab"));
console.log(front_back3("abcd"));

```

>ES6 Version:
```javascript
function front_back3(str) {
  if (str.length >= 3) {
    str_len = 3;

    back = str.substring(str.length - 3);
    return back + str + back;
  } else
    return false;
}
console.log(front_back3("abc"));
console.log(front_back3("ab"));
console.log(front_back3("abcd"));
```
>Result:
```javascript
abcabcabc
false
bcdabcdbcd
```
**26. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```
>Result:
```javascript

```
**27. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```
>Result:
```javascript

```

**28. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

**29. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```
>Result:
```javascript

```

**30. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```
>Result:
```javascript

```

**31. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```
>Result:
```javascript

```

**32. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```
>Result:
```javascript

```

**33. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```
**34. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```
>Result:
```javascript

```

**35. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```
>Result:
```javascript

```

**36. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

**37. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

>Result:
```javascript

```

**38. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

>Result:
```javascript

```

**39. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

>Result:
```javascript

```

**40. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

>Result:
```javascript

```

**41. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

>Result:
```javascript

```

**42. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

>Result:
```javascript

```

**43. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

>Result:
```javascript

```

**44. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

>Result:
```javascript

```

**45. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

>Result:
```javascript

```

**46. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

>Result:
```javascript

```

**47. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

>Result:
```javascript

```

**48. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

>Result:
```javascript

```

**49. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

>Result:
```javascript

```

**50. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

>Result:
```javascript

```

**51. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

>Result:
```javascript

```

**52. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

>Result:
```javascript

```

**53. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

>Result:
```javascript

```

**54. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

>Result:
```javascript

```

**55. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

>Result:
```javascript

```
