#### I. JavaScript Recursion - Exercises, Practice, Solution
---
**Recursion**: Đệ qui. Trả lại chính hắn, thông gia tham số mới truyền vào đã được tính toán ở trên.

**1. Write a JavaScript program to calculate the factorial of a number.**
- Viết một chương trình JavaScript để tính toán giai thừa của một số.
- In mathematics, the factorial of a non-negative integer n, denoted by n!, is the product of all positive integers less than or equal to n. For example, 5! = 5 x 4 x 3 x 2 x 1 = 120 (Trong toán học, giai thừa của một số nguyên n không âm, được biểu diễn bởi n !, là sản phẩm của tất cả các số nguyên dương nhỏ hơn hoặc bằng n. Ví dụ, 5! = 5 x 4 x 3 x 2 x 1 = 120)

>JavaScript Code:
```javascript
function factorial(x) {

  if (x === 0) {
    return 1;
  }
  return x * factorial(x - 1);
  console.log(factorial(x - 1));

}
console.log(factorial(5));
```

>Result:
```javascript
120
```

**2. Write a JavaScript program to find the greatest common divisor (gcd) of two positive numbers.**
- Viết một chương trình JavaScript để tìm ước số lớn nhất (gcd) của hai số dương.

>JavaScript Code:
```javascript
var gcd = function(a, b) {
  if (!b) {
    return a;
  }

  return gcd(b, a % b);
};
console.log(gcd(2154, 458));
```

>Result:
```javascript
2
```

**3. Write a JavaScript program to get the integers in range (x, y).**
- Viết một chương trình JavaScript để lấy các số nguyên trong phạm vi (x, y).
- Example : range(2, 9)
- Expected Output : [3, 4, 5, 6, 7, 8]
>JavaScript Code:
```javascript
var range = function(start_num, end_num) {
  if (end_num - start_num === 2) {
    return [start_num + 1];
  } else {
    var list = range(start_num, end_num - 1);
    list.push(end_num - 1);
    return list;
  }
};

console.log(range(2, 9));
```

>Result:
```javascript
[3, 4, 5, 6, 7, 8]
```

**4. Write a JavaScript program to compute the sum of an array of integers.**
Example : var array = [1, 2, 3, 4, 5, 6]
Expected Output : 21
- The ```pop()``` method removes the last element of an array, and returns that element.(Phương thức pop () loại bỏ phần tử cuối cùng của một mảng, và trả về phần tử đó.)
- Tip: To remove the first element of an array, use the shift() method.( Để loại bỏ phần tử đầu tiên của mảng, sử dụng phương thức shift ().)

>JavaScript Code:
```javascript
var array_sum = function(my_array) {
  if (my_array.length === 1) {
    return my_array[0];
  } else {
    return my_array.pop() + array_sum(my_array);
  }
};

console.log(array_sum([1, 2, 3, 4, 5, 6]));
```

>Result:
```javascript
21
```

**5. Write a JavaScript program to compute the exponent of a number.**
- Viết một chương trình JavaScript để tính số mũ của một số.
- **Note:** The exponent of a number says how many times the base number is used as a factor.
- 82 = 8 x 8 = 64. Here 8 is the base and 2 is the exponent.(Ở đây 8 là cơ sở và 2 là số mũ.)

>JavaScript Code:
```javascript
var exponent = function(a, n) {
  if (n === 0) {
    return 1;
  } else {
    return a * exponent(a, n - 1);
  }
};

console.log(exponent(4, 2));
```

>Result:
```javascript
16
```

**6. Write a JavaScript program to get the first n Fibonacci numbers.**
- Viết một chương trình JavaScript để lấy n số Fibonacci đầu tiên.
- **Note:** The Fibonacci Sequence is the series of numbers: 0, 1, 1, 2, 3, 5, 8, 13, 21, 34, . . . Each subsequent number is the sum of the previous two.(Dãy số Fibonacci là chuỗi các số: 0, 1, 1, 2, 3, 5, 8, 13, 21, 34,. . . Mỗi số tiếp theo là tổng của hai lần trước đó.)

>JavaScript Code:
```javascript
var fibonacci_series = function(n) {
  if (n === 1) {
    return [0, 1];
  } else {
    var s = fibonacci_series(n - 1);
    s.push(s[s.length - 1] + s[s.length - 2]);
    return s;
  }
};

console.log(fibonacci_series(8));
```

>Result:
```javascript
[0, 1, 1, 2, 3, 5, 8, 13, 21]
```

**7. Write a JavaScript program to check whether a number is even or not.**
- Viết một chương trình JavaScript để kiểm tra xem một số thậm chí có hay không.
- ```Math.abs(-7.25);``` ==> ```7.25```

>JavaScript Code:
```javascript
function is_even_recursion(number) {
  if (number < 0) {
    number = Math.abs(number);
  }
  if (number === 0) {
    return true;
  }
  if (number === 1) {
    return false;
  } else {
    number = number - 2;
    return is_even_recursion(number);
  }
}
console.log(is_even_recursion(234)); //true
console.log(is_even_recursion(-45)); // false
console.log(is_even_recursion(-45)); // false
```

>Result:
```javascript
true
false
false
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

