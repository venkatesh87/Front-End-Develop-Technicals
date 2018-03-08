#### I. JavaScript functions - Exercises, Practice, Solution
---

**1. Write a JavaScript function that reverse a number.**
Sample Data and output: 
Example x = 32243; 
Expected Output: 34223

Assume n = 1000. 
Convert a number to a string :
**Code :** -> n = n + "";
**Note :** There are different ways to convert number to string : Có nhiều cách khác nhau để chuyển đổi số thành chuỗi.

**String literal** -> str = "" + num + "";
**String constructor** -> str = String(num);
**toString** -> str = num.toString();
**String Literal simple** -> str = "" + num;
The ```split()``` method is used to split a String object into an array of strings by separating the string into substrings.
**Code :** console.log('1000'.split(""));
**Output :** ["1", "0", "0", "0"]

The ```reverse()``` method is used to reverse an array in place. The first array element becomes the last and the last becomes the first.
**Code :** console.log(["1", "0", "0", "0"].reverse());
**Output :** ["0", "0", "0", "1"]

The ```join()``` method is used to join all elements of an array into a string.
**Code :** console.log(["1", "0", "0", "0"].reverse().join(""));
**Output :** "0001"

>JavaScript Code:
```javascript
function reverse_a_number(n) {
  n = n + "";
  return n.split("").reverse().join("");
}
console.log(reverse_a_number(32243));
```

>Result:
```javascript
34223
```

**2. Write a JavaScript function that checks whether a passed string is palindrome or not?**
- Viết một hàm JavaScript để kiểm tra xem chuỗi đã qua có phải là palindrome hay không? 
- Một chuỗi được gọi là Palindrome nếu sau khi đảo ngược các ký tự của nó, ta nhận được chuỗi ban đầu. Ví dụ: chuỗi "MADAM" là Palindrome.
- The ```toLowerCase()``` method converts a string to lowercase letters.
- The ```replace()``` method searches a string for a specified value, or a regular expression, and returns a new string where the specified values are replaced.(Phương thức ```replace()``` tìm kiếm một chuỗi cho một giá trị được chỉ định, hoặc một biểu thức chính quy, và trả về một chuỗi mới mà các giá trị được chỉ định được thay thế.)

- **Note:** A palindrome is word, phrase, or sequence that reads the same backward as forward, e.g., madam or nurses run. (Lưu ý: Một palindrome là từ, cụm từ hoặc trình tự đọc ngược lại tương tự như chuyển tiếp, ví dụ: madam hoặc các y tá chạy.)
>JavaScript Code:
```javascript
// Write a JavaScript function that checks whether a passed string is palindrome or not? 
function check_Palindrome(str_entry) {
  // Change the string into lower case and remove  all non-alphanumeric characters
  var cstr = str_entry.toLowerCase().replace(/[^a-zA-Z0-9]+/g, '');
  var ccount = 0;
  // Check whether the string is empty or not
  if (cstr === "") {
    alert("Nothing found!");
    return false;
  }
  // Check if the length of the string is even or odd 
  if ((cstr.length) % 2 === 0) {
    ccount = (cstr.length) / 2;
  } else {
    // If the length of the string is 1 then it becomes a palindrome
    if (cstr.length === 1) {
      alert("Entry is a palindrome.");
      return true;
    } else {
      // If the length of the string is odd ignore middle character
      ccount = (cstr.length - 1) / 2;
    }
  }
  // Loop through to check the first character to the last character and then move next
  for (var x = 0; x < ccount; x++) {
    // Compare characters and drop them if they do not match 
    if (cstr[x] != cstr.slice(-1 - x)[0]) {
      alert("Entry is not a palindrome.");
      return false;
    }
  }
  alert("The entry is a palindrome.");
  return true;
}
check_Palindrome('madam');
check_Palindrome('nurses run');
check_Palindrome('fox');
```

**3. Write a JavaScript function that generates all combinations of a string.**
- Viết một hàm JavaScript tạo ra tất cả các kết hợp của một chuỗi.
- Example string: 'dog' 
- Expected Output: d,o,do,g,dg,og,dog

>JavaScript Code:
```javascript
//Write a JavaScript function that generates all combinations of a string.
function substrings(str1) {
  var array1 = [];
  for (var x = 0, y = 1; x < str1.length; x++, y++) {
    array1[x] = str1.substring(x, y);
  }
  var combi = [];
  var temp = "";
  var slent = Math.pow(2, array1.length);

  for (var i = 0; i < slent; i++) {
    temp = "";
    for (var j = 0; j < array1.length; j++) {
      if ((i & Math.pow(2, j))) {
        temp += array1[j];
      }
    }
    if (temp !== "") {
      combi.push(temp);
    }
  }
  console.log(combi.join("\n"));
}

substrings("dog");
```

>Result:
```javascript

```

**4. **

>JavaScript Code:
```javascript

```

>ES6 Version:

```

>Result:
```javascript

```

**5. **

>JavaScript Code:
```javascript

```

>ES6 Version:

```

>Result:
```javascript

```

**6. **

>JavaScript Code:
```javascript

```

>ES6 Version:

```

>Result:
```javascript

```

**7. **

>JavaScript Code:
```javascript

```

>ES6 Version:

```

>Result:
```javascript

```

**8. **

>JavaScript Code:
```javascript

```

>ES6 Version:

```

>Result:
```javascript

```

**9. **

>JavaScript Code:
```javascript

```

>ES6 Version:

```

>Result:
```javascript

```

**10. **

>JavaScript Code:
```javascript

```

>ES6 Version:

```

>Result:
```javascript

```

**11. **

>JavaScript Code:
```javascript

```

>ES6 Version:

```

>Result:
```javascript

```

**12. **

>JavaScript Code:
```javascript

```

>ES6 Version:

```

>Result:
```javascript

```

**13. **

>JavaScript Code:
```javascript

```

>ES6 Version:

```

>Result:
```javascript

```

**14. **

>JavaScript Code:
```javascript

```

>ES6 Version:

```

>Result:
```javascript

```

**15. **

>JavaScript Code:
```javascript

```

>ES6 Version:

```

>Result:
```javascript

```

**16. **

>JavaScript Code:
```javascript

```

>ES6 Version:

```

>Result:
```javascript

```

**17. **

>JavaScript Code:
```javascript

```

>ES6 Version:

```

>Result:
```javascript

```

**18. **

>JavaScript Code:
```javascript

```

>ES6 Version:

```

>Result:
```javascript

```

**19. **

>JavaScript Code:
```javascript

```

>ES6 Version:

```

>Result:
```javascript

```

**20. **

>JavaScript Code:
```javascript

```

>ES6 Version:

```

>Result:
```javascript

```

**21. **

>JavaScript Code:
```javascript

```

>ES6 Version:

```

>Result:
```javascript

```

**22. **

>JavaScript Code:
```javascript

```

>ES6 Version:

```

>Result:
```javascript

```

**23. **

>JavaScript Code:
```javascript

```

>ES6 Version:

```

>Result:
```javascript

```

**24. **

>JavaScript Code:
```javascript

```

>ES6 Version:

```

>Result:
```javascript

```

**25. **

>JavaScript Code:
```javascript

```

>ES6 Version:

```

>Result:
```javascript

```

**26. **

>JavaScript Code:
```javascript

```

>ES6 Version:

```

>Result:
```javascript

```

**27. **

>JavaScript Code:
```javascript

```

>ES6 Version:

```

>Result:
```javascript

```

**28. **

>JavaScript Code:
```javascript

```

>ES6 Version:

```

>Result:
```javascript

```

**29. **

>JavaScript Code:
```javascript

```

>ES6 Version:

```

>Result:
```javascript

```
