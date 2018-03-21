#### I. JavaScript array - Exercises, Practice, Solution
---

**1. Write a JavaScript function to check whether an 'input' is an array or not.**
- Viết một hàm JavaScript để kiểm tra xem một 'đầu vào' là một mảng hay không.
- Phương thức ```toString()``` trả về một chuỗi đại diện cho object.
- The call() method is a predefined JavaScript function method.(Phương thức call () là một hàm JavaScript được xác định trước.)
- It can be used to invoke (call) a function with an owner object as the first argument (parameter).(Nó có thể được sử dụng để gọi ```(call)``` một hàm với một đối tượng chủ sở hữu như là đối số đầu tiên ```(parameter)```)


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
```javascript
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
```javascript
array_Clone = arra1 => arra1.slice(0);
console.log(array_Clone([1, 2, 4, 0]));
console.log(array_Clone([1, 2, [4, 0]]));
```

>Result:
```javascript
[1,2,4,0]
[1,2,[4,0]]
```

**3. Write a simple JavaScript program to join all elements of the following array into a string.**
- Viết một chương trình JavaScript đơn giản để nối tất cả các phần tử của mảng sau vào một chuỗi.

>JavaScript Code:
```javascript
myColor = ["Red", "Green", "White", "Black"];
console.log(myColor.toString());
console.log(myColor.join());
console.log(myColor.join('+'));
console.log(myColor.join(' '));
```

>ES6 Version:
```javascript
myColor = ["Red", "Green", "White", "Black"];
console.log(myColor.toString());
console.log(myColor.join());
console.log(myColor.join('+'));
console.log(myColor.join(' '));
```

>Result:
```javascript
Red,Green,White,Black
Red,Green,White,Black
Red+Green+White+Black
Red Green White Black
```

**4. Write a JavaScript program which accept a number as input and insert dashes (-) between each two even numbers. For example if you accept 025468 the output should be 0-254-6-8**
- Viết một chương trình JavaScript chấp nhận một số như đầu vào và chèn dấu gạch ngang (-) giữa hai số chẵn. Ví dụ nếu bạn chấp nhận 025468 đầu ra phải là 0-254-6-8
- The ```toString()``` method converts a number to a string: Phương thức ```toString()``` chuyển đổi một số thành một chuỗi.
- The push() method adds new items to the end of an array, and returns the new length: Phương thức push () thêm các mục mới vào cuối mảng, và trả về chiều dài mới.
- ```str[x-1]``` và ```str[x]``` là 2 chuỗi liền kề nhau trong mảng.

>JavaScript Code:
```javascript
var num = window.prompt();
var str = num.toString();
var result = [str[0]];

for (var x = 1; x < str.length; x++) {
  if ((str[x - 1] % 2 === 0) && (str[x] % 2 === 0)) {
    result.push('-', str[x]);
  } else {
    result.push(str[x]);
  }
}
console.log(result.join(''));
```

>ES6 Version:
```javascript
const num = window.prompt();
const str = num.toString();
const result = [str[0]];

for (let x = 1; x < str.length; x++) {
  if ((str[x - 1] % 2 === 0) && (str[x] % 2 === 0)) {
    result.push('-', str[x]);
  } else {
    result.push(str[x]);
  }
}
console.log(result.join(''));
```

**5. Write a JavaScript program to sort the items of an array.**
- Viết một chương trình JavaScript để sắp xếp các mục của một mảng.

>JavaScript Code:
```javascript
var arr1 = [-3, 8, 7, 6, 5, -4, 3, 2, 1];
var arr2 = [];
var min = arr1[0];
var pos;
max = arr1[0];
for (i = 0; i < arr1.length; i++) {
  if (max < arr1[i]) max = arr1[i];
}

for (var i = 0; i < arr1.length; i++) {
  for (var j = 0; j < arr1.length; j++) {
    if (arr1[j] != "x") {
      if (min > arr1[j]) {
        min = arr1[j];
        pos = j;
      }
    }
  }
  arr2[i] = min;
  arr1[pos] = "x";
  min = max;
}
console.log(arr2);
```

>ES6 Version:
const arr1 = [-3, 8, 7, 6, 5, -4, 3, 2, 1];
const arr2 = [];
let min = arr1[0];
let pos;
max = arr1[0];
for (i = 0; i < arr1.length; i++) {
  if (max < arr1[i]) max = arr1[i];
}

for (var i = 0; i < arr1.length; i++) {
  for (let j = 0; j < arr1.length; j++) {
    if (arr1[j] != "x") {
      if (min > arr1[j]) {
        min = arr1[j];
        pos = j;
      }
    }
  }
  arr2[i] = min;
  arr1[pos] = "x";
  min = max;
}
console.log(arr2);
```

>Result:
```javascript
[-4,-3,1,2,3,5,6,7,8]
```

**6. Write a JavaScript program to find the most frequent item of an array.**
- Viết một chương trình JavaScript để tìm ra mục thường gặp nhất của một mảng.
- Sample array : ```var arr1=[3, 'a', 'a', 'a', 2, 3, 'a', 3, 'a', 2, 4, 9, 3];```
- Sample Output : a ( 5 times )

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

