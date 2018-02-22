#### I. JavaScript basic - Exercises, Practice, Solution
---

**1. Write a JavaScript program to determine whether a given year is a leap year in the Gregorian calendar.**

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
**2. Write a JavaScript program to find which 1st January is being a Sunday between 2014 and 2050.**

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

**3. Write a JavaScript program where the program takes a random integer between 1 to 10, the user is then prompted to input a guess number. If the user input matches with guess number, the program will display a message "Good Work" otherwise display a message "Not matched".**

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

**4. Write a JavaScript program to calculate number of days left until next Christmas.**

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

**5. Write a JavaScript program to calculate multiplication and division of two numbers (input from user).**

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

**6. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```
**7. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

**8. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

**9. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

**10. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```
**11. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

**12. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

**13. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

**14. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

**15. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

**16. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

**17. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

**18. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```
**19. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

**20. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

**21. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

**22. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

**23. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

**24. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

**25. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

**26. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

**27. **

>JavaScript Code:
```javascript

```

>ES6 Version:
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

**30. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

**31. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

**32. **

>JavaScript Code:
```javascript

```

>ES6 Version:
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

**35. **

>JavaScript Code:
```javascript

```

>ES6 Version:
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

**38. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```
**39. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

**40. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

**41. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

**42. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

**43. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

**44. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

**45. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

**46. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

**47. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

**48. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```
**49. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

**50. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```
