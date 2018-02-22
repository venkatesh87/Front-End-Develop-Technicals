#### I. JavaScript basic - Exercises, Practice, Solution
---

**1. Write a JavaScript program to determine whether a given year is a leap year in the Gregorian calendar.**

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
**2. Write a JavaScript program to find which 1st January is being a Sunday between 2014 and 2050.**

```javascript
for (let year = 2014; year <= 2050; year++) {
  const date = new Date(year, 0, 1);
  if (date.getDay() === 0) {
    console.log("1st January is being a Sunday  " + year);
  }
}
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

```javascript

```

**5. **

```javascript

```

**6. **

```javascript

```

**7. **

```javascript

```

**8. **

```javascript

```

**9. **

```javascript

```
