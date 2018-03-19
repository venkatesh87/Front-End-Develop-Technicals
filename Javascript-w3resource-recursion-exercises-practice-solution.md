#### I. JavaScript Recursion - Exercises, Practice, Solution
---
**Recursion**: Đệ qui.

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

>ES6 Version:

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

