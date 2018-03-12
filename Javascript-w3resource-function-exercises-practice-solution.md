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
- ```array.slice(start, end)```: The ```slice()``` method returns the selected elements in an array, as a new array object. Phương thức slice () trả về các phần tử đã chọn trong một mảng, như một đối tượng mảng mới.
- Use negative numbers to select from the end of an array(Sử dụng số âm để chọn từ cuối mảng)
- **Note:** A palindrome is word, phrase, or sequence that reads the same backward as forward, e.g., madam or nurses run. (Lưu ý: Một palindrome là từ, cụm từ hoặc trình tự đọc ngược lại tương tự như chuyển tiếp, ví dụ: madam hoặc các y tá chạy.)
- Thay đổi chuỗi thành chữ thường và loại bỏ tất cả các ký tự không phải là chữ và số
- Kiểm tra xem chuỗi có rỗng hay không
- Kiểm tra xem chiều dài của chuỗi có bằng nhau hay không
- Nếu chiều dài của chuỗi là 1 sau đó nó sẽ trở thành một palindrome
- Nếu chiều dài của chuỗi là lẻ bỏ qua nhân vật trung gian
- Lặp qua để kiểm tra ký tự đầu tiên cho nhân vật cuối cùng và sau đó di chuyển tiếp theo

// So sánh các ký tự và thả chúng nếu chúng không khớp
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
- The ```pow(x, y)``` method returns the value of x to the power of y (x mũ y). 
- ```Math.pow(2, 3);``` ==> ```8```; ```Math.pow(4, 3);``` ==> ```64```
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

**4. Write a JavaScript function that returns a passed string with letters in alphabetical order.**
Example string: 'webmaster' 
Expected Output: 'abeemrstw'
- Viết một hàm JavaScript trả về một chuỗi được truyền với các chữ cái theo thứ tự chữ cái. 
- The ```split()``` method is used to split a String object into an array of strings by separating the string into substrings.
Code : console.log('32243'.split(""));
Output : ["3", "2", "2", "4", "3"]

- The ```sort()``` method is used to sort the elements of an array in place and returns the array.
Code : console.log(["3", "2", "2", "4", "3"].sort());
Output : ["2", "2", "3", "3", "4"]

- The ```join()``` method is used to join all elements of an array into a string.
Code : console.log(["2", "2", "3", "3", "4"].join(""));
Output : "22334"

>JavaScript Code:
```javascript
function alphabet_order(str)
  {
return str.split('').sort().join('');
  }
console.log(alphabet_order("webmaster"));
```

>Result:
```javascript
abeemrstw
```

**5. Write a JavaScript function that accepts a string as a parameter and converts the first letter of each word of the string in upper case.**
- Viết một hàm JavaScript chấp nhận một chuỗi như một tham số và chuyển đổi chữ cái đầu tiên của mỗi từ của chuỗi thành chữ hoa.
- Example string: 'the quick brown fox' 
- Expected Output: 'The Quick Brown Fox '
- Assume str = "the quick brown fox";

- The ```split()``` method is used to split a String object into an array of strings by separating the string into substrings.
- console.log(str.split(' ')); 
- Output : ```["the", "quick", "brown", "fox"]```
- First substrings -> "the"
- Code to convert first character of the above sting to upper case-> ```array1[x].charAt(0).toUpperCase()```
- ```console.log(array1[x].charAt(0).toUpperCase()); [here x=0] ```
- Output : "T"
- Rest part of the string "the" -> ```array1[x].slice(1)```
- ```console.log(array1[0].slice(1));```
- Output : "he"
- Final string :
- ```console.log(array1[0].charAt(0).toUpperCase()+array1[0].slice(1));```
- Output : "The"
- Now insert the above string into another array :
- ```newarray1.push(array1[x].charAt(0).toUpperCase()+array1[x].slice(1));```
- Used functions :
- The ```charAt()``` method is used to get the specified character from a string.
- Syntax : str.charAt(index). Where index represents an integer between 0 and 1-less-than the length of the string.
- The toUpperCase() method is used to convert the string value to uppercase.
- The ```slice()``` method returns a shallow copy of a portion of an array into a new array object.
- The ```push()``` method is used to add one or more elements to the end of an array and returns the new length of the array.
- After completing the for loop return the final string :
- return newarray1.join(' ');
- The ```join()``` method joins all elements of an array into a string.

>JavaScript Code 1:
```javascript
function uppercase(str){
  return str.charAt(0).toUpperCase() + str.slice(1);
}
console.log(uppercase("abcde"));
```
>Result:
```javascript
Abcde
```

>JavaScript Code 2:
function uppercase(str) {
  var array1 = str.split(' ');
  var newarray1 = [];
  for (var x = 0; x < array1.length; x++) {
    newarray1.push(array1[x].charAt(0).toUpperCase() + array1[x].slice(1));
  }
  return newarray1.join(' ');
}
console.log(uppercase("the quick brown fox"));
```

>Result:
```javascript
The Quick Brown Fox
```

**6. Write a JavaScript function that accepts a string as a parameter and find the longest word within the string.**
- Write a JavaScript function that accepts a string as a parameter and find the longest word within the string.
- Viết một hàm JavaScript chấp nhận một chuỗi như một tham số và tìm thấy từ dài nhất trong chuỗi.
- Sample Data and output: 
- Example string: 'Web Development Tutorial' 
- Expected Output: 'Development'

**Explanation:**
- Assume str = '@Web Development #Tutorial';
- The ```match()``` method is used to retrieve the matches when matching a string against a regular expression.
- The match() method searches a string for a match against a regular expression, and returns the matches, as an Array object.(Phương thức match () tìm kiếm một chuỗi cho một đối sánh với một biểu thức chính quy và trả về các đối sánh, như một đối tượng Array.)
- Therefore ```str.match(/\w[a-z]{0,}/gi)``` will ```return ["Web", "Development", "Tutorial"]```.
- For loop checks the length of the array element and compare with previous one and finally return the longest string.
- The length property represents an unsigned, 32-bit integer that is always numerically greater than the highest index in the array.
```Syntax -> arr.length```

>JavaScript Code:
```javascript
function find_longest_word(str) {
  var array1 = str.match(/\w[a-z]{0,}/gi);
  var result = array1[0];

  for (var x = 1; x < array1.length; x++) {
    if (result.length < array1[x].length) {
        result = array1[x];
    }
  }
  return result;
}
console.log(find_longest_word('Web Development Tutorial'));
```

>Result:
```javascript
Development
```

**7. Write a JavaScript function that accepts a string as a parameter and counts the number of vowels within the string.**
**Note:** As the letter 'y' can be regarded as both a vowel and a consonant, we do not count 'y' as vowel here.
**Sample Data and output:** 
**Example string:** 'The quick brown fox' 
**Expected Output:** 5
**Explanation:** 
- The ```indexOf()``` method returns the index within the calling String object of the first occurrence of the specified value, starting the search at fromIndex. Returns -1 if the value is not found.
Syntax -> ```str.indexOf(searchValue[, fromIndex])```
**Parameters :**
- ```searchValue``` : A string representing the value to search for. 
- ```fromIndex(Optional)```-> The index at which to start the searching forwards in the string. It can be any integer.
- The character(s) of the string will be counted as vowel if the condition (```vowel_list.indexOf(str1[x]) !== -1```) matched.

>JavaScript Code:
```javascript
function vowel_count(str1) {
  var vowel_list = 'aeiouAEIOU';
  var vcount = 0;

  for (var x = 0; x < str1.length; x++) {
    if (vowel_list.indexOf(str1[x]) !== -1) {
      vcount += 1;
    }

  }
  return vcount;
}
console.log(vowel_count("The quick brown fox"));
```

>Result:
```javascript
5
```

**8. Write a JavaScript function that accepts a number as a parameter and check the number is prime or not.**

- Viết một hàm JavaScript chấp nhận một số như một tham số và kiểm tra số đó là số nguyên tố hay không.
- Số nguyên tố là số tự nhiên chỉ có hai ước số dương phân biệt là 1 và chính nó. Các số có nhiều hơn 2 ước số dương được gọi là hợp số.
- Do số 1 chỉ có một (1) ước số dương là chính nó, nên số 1 không phải là số nguyên tố và cũng không phải là hợp số.
- Các số nguyên tố từ 2 đến 100:
```2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47, 53, 59, 61, 67, 71, 73, 79, 83, 89, 97```
- Số 2 là số nguyên tố nhỏ nhất, và cũng là số nguyên tố chẵn duy nhất. 

>JavaScript Code:
```javascript
function test_prime(n) {

  if (n === 1) {
    return false;
  } else if (n === 2) {
    return true;
  } else {
    for (var x = 2; x < n; x++) {
      if (n % x === 0) {
        return false;
      }
    }
    return true;
  }
}

console.log(test_prime(37));
```

>Result:
```javascript
true
```

**9. Write a JavaScript function which accepts an argument and returns the type.**
- Viết một hàm JavaScript chấp nhận đối số và trả về kiểu.
- **Note** : There are six possible values that typeof returns: object, boolean, function, number, string, and undefined.

>JavaScript Code:
```javascript
function detect_data_type(value) {
  var dtypes = [Function, RegExp, Number, String, Boolean, Object],
    x, len;

  if (typeof value === "object" || typeof value === "function") {
    for (x = 0, len = dtypes.length; x < len; x++) {
      if (value instanceof dtypes[x]) {
        return dtypes[x];
      }
    }
  }

  return typeof value;
}
console.log(detect_data_type(12));
console.log(detect_data_type('w3resource'));
console.log(detect_data_type(false));
```

>Result:

```javascript
number
string
boolean
```

**10. Write a JavaScript function which returns the n rows by n columns identity matrix**

>JavaScript Code:
```javascript
function matrix(n) {
  var i;
  var j;

  for (i = 0; i < n; i++) {
    for (j = 0; j < n; j++) {
      if (i === j) {
        console.log(' 1 ');
      } else {
        console.log(' 0 ');
      }
    }
    console.log('----------');
  }
}
matrix(4);
```

>Result:
```javascript
1 
 0 
 0 
 0 
----------
 0 
 1 
 0 
 0 
----------
 0 
 0 
 1 
 0 
----------
 0 
 0 
 0 
 1 
----------
```

**11. Write a JavaScript function which will take an array of numbers stored and find the second lowest and second greatest numbers, respectively.**
- Viết một hàm JavaScript sẽ lấy một mảng số được lưu trữ và tìm số thứ hai thấp nhất thứ hai và thứ hai lớn nhất, tương ứng.
>JavaScript Code:
```javascript

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
