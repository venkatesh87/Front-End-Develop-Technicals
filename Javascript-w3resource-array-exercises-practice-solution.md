#### I. JavaScript array - Exercises, Practice, Solution
---

**1. Write a JavaScript function to check whether an 'input' is an array or not.**
- Viết một hàm JavaScript để kiểm tra xem một 'đầu vào' là một mảng hay không.
- Phương thức ```toString()``` trả về một chuỗi đại diện cho object.
- The call() method is a predefined JavaScript function method.(Phương thức call () là một hàm JavaScript được xác định trước.)
- It can be used to invoke (call) a function with an owner object as the first argument (parameter).(Nó có thể được sử dụng để gọi ```(call)``` một hàm với một đối tượng chủ sở hữu như là đối số đầu tiên ```(parameter)```)

**call()**
```
var person = {
  firstName: "John",
  lastName: "Doe",
  fullName: function() {
    return this.firstName + " " + this.lastName;
  }
}
var myObject = {
  firstName: "Mary",
  lastName: "Doe",
}
person.fullName.call(myObject); // Will return "Mary Doe"
```

>JavaScript Code:
```javascript
is_array = function(input) {
  if (toString.call(input) === "[object Array]")
    return true;
  return false;
};
console.log(is_array('w3resource'));
console.log(is_array([1, 2, 4, 0]));
```

>ES6 Version:
is_array = input => {
  if (toString.call(input) === "[object Array]")
    return true;
  return false;
};
console.log(is_array('w3resource'));
console.log(is_array([1, 2, 4, 0]));
```

>Result:
```javascript
false
true
```

**2. Write a JavaScript function to clone an array.**
- Viết một hàm JavaScript để nhân một mảng.
- The ```slice()``` method returns the selected elements in an array, as a new array object. (Phương thức `` slice () `` `trả về các phần tử đã chọn trong một mảng, như một đối tượng mảng mới)
- ``array.slice(start, end)```
  + **start**: Optional. An integer that specifies where to start the selection (The first element has an index of 0). Use negative numbers to select from the end of an array. If omitted, it acts like "0"(Không bắt buộc. Một số nguyên xác định nơi bắt đầu lựa chọn (Phần tử đầu tiên có chỉ số 0). Sử dụng số âm để chọn từ cuối mảng. Nếu bỏ qua, nó hoạt động như "0")
  + **end**: Optional. An integer that specifies where to end the selection. If omitted, all elements from the start position and to the end of the array will be selected. Use negative numbers to select from the end of an array(Không bắt buộc. Một số nguyên xác định nơi để kết thúc lựa chọn. Nếu bỏ qua, tất cả các yếu tố từ vị trí bắt đầu và đến cuối mảng sẽ được chọn. Sử dụng số âm để chọn từ cuối mảng)
  
>JavaScript Code:
```javascript
array_Clone = function(arra1) {
  return arra1.slice(0);
};
console.log(array_Clone([1, 2, 4, 0]));
console.log(array_Clone([1, 2, [4, 0]]));
```

>ES6 Version:
array_Clone = arra1 => arra1.slice(0);
console.log(array_Clone([1, 2, 4, 0]));
console.log(array_Clone([1, 2, [4, 0]]));
```

>Result:
```javascript
[1,2,4,0]
[1,2,[4,0]]
```

**3. **

>JavaScript Code:
```javascript

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

