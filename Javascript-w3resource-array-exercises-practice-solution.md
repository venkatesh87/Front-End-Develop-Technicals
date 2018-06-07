#### I. JavaScript array - Exercises, Practice, Solution
---
- The ```shift()``` method removes the first item of an array.
- The ```pop()``` method removes the last item of an array.
- ```array.splice(index, howmany, item1, ....., itemX)``` method adds/removes items to/from an array, and returns the removed item(s).
  + ```index```: Số nguyên chỉ định vị trí cần thêm / xóa mục, Sử dụng giá trị âm để chỉ định vị trí từ cuối mảng
  + ```howmany```: Số lượng mục cần xóa. Nếu được đặt thành 0, sẽ không có mục nào bị xóa
  + ```item1, ..., itemX```: The new item(s) to be added to the array

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
```javascript
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
- Vòng lặp lồng vòng lặp: 
  + Chú ý: ```i=0``` thì ```j=0``` cho dù nó vòng lặp lồng nhau nhưng giá trị ban đầu ```j=0``` chứ ko phải ```j=1``` ngay từ ban đầu.
  + Trong vòng lặp bắt đầu từ ```i=0``` thì ```j``` sẽ chạy từ ```0``` đến nhỏ hơn ```arr.length```, trong bài này ```i=0``` thì ```j``` sẽ chạy từ ```0``` đến ```12``` và so sánh ```arr[i=0]``` với ```arr[j=0->12]```. Cứ thế ```i=1``` thì ```j=1``` và so sánh ```arr[i=1]``` với ```a[i=1->12]```. Cứ tiếp tục vòng lặp đến ```i=12, j=12``` thì dứt.
  
>JavaScript Code:
```javascript
var arr = [3, 'a', 'a', 'a', 2, 3, 'a', 3, 'a', 2, 4, 9, 3];
var mf = 1;
var m = 0;
var item;
for (var i = 0; i < arr.length; i++) {
  for (var j = i; j < arr.length; j++) {
    if (arr[i] == arr[j])
      m++;
    if (mf < m) {
      mf = m;
      item = arr[i];
    }
  }
  m = 0;
}
console.log(item + " ( " + mf + " times ) ");
```

>ES6 Version:
```javascript
const arr = [3, 'a', 'a', 'a', 2, 3, 'a', 3, 'a', 2, 4, 9, 3];
let mf = 1;
let m = 0;
let item;
for (let i = 0; i < arr.length; i++) {
  for (let j = i; j < arr.length; j++) {
    if (arr[i] == arr[j])
      m++;
    if (mf < m) {
      mf = m;
      item = arr[i];
    }
  }
  m = 0;
}
console.log(`${item} ( ${mf} times ) `);
```

>Result:
```javascript
a ( 5 times )
```

**7. Write a JavaScript program which accept a string as input and swap the case of each character. For example if you input 'The Quick Brown Fox' the output should be 'tHE qUICK bROWN fOX'.**
- Viết một chương trình JavaScript chấp nhận một chuỗi như là đầu vào và trao đổi các trường hợp của mỗi nhân vật. Ví dụ nếu bạn nhập 'The Quick Brown Fox' đầu ra nên được 'tHE qUICK bROWN fOX'.

>JavaScript Code:
```javascript
str = 'c';
var UPPER = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ';
var LOWER = 'abcdefghijklmnopqrstuvwxyz';
var result = [];

for (var x = 0; x < str.length; x++) {
  if (UPPER.indexOf(str[x]) !== -1) {
    result.push(str[x].toLowerCase());
  } else if (LOWER.indexOf(str[x]) !== -1) {
    result.push(str[x].toUpperCase());
  } else {
    result.push(str[x]);
  }
}
console.log(result.join(''));
```

>ES6 Version:
```javascript
str = 'c';
const UPPER = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ';
const LOWER = 'abcdefghijklmnopqrstuvwxyz';
const result = [];

for (let x = 0; x < str.length; x++) {
  if (UPPER.includes(str[x])) {
    result.push(str[x].toLowerCase());
  } else if (LOWER.includes(str[x])) {
    result.push(str[x].toUpperCase());
  } else {
    result.push(str[x]);
  }
}
console.log(result.join(''));
```

>Result:
```javascript
C
```

**8. Write a JavaScript program which prints the elements of the following array.**
- Viết một chương trình JavaScript in các phần tử của mảng sau.

>JavaScript Code:
```javascript
// a sample 2-D array 
var a = [
  [1, 2, 1, 24],
  [8, 11, 9, 4],
  [7, 0, 7, 27],
  [7, 4, 28, 14],
  [3, 10, 26, 7]
];

for (var i in a) {
  console.log("row " + i);
  for (var j in a[i]) {
    console.log(" " + a[i][j]);
  }
}
```

>ES6 Version:
```javascript
// a sample 2-D array 
const a = [
  [1, 2, 1, 24],
  [8, 11, 9, 4],
  [7, 0, 7, 27],
  [7, 4, 28, 14],
  [3, 10, 26, 7]
];

for (const i in a) {
  console.log(`row ${i}`);
  for (const j in a[i]) {
    console.log(` ${a[i][j]}`);
  }
}
```

>Result:
```javascript
row 0
 1
 2
 1
 24
row 1
 8
 11
 9
 4
row 2
 7
 0
 7
 27
row 3
 7
 4
 28
 14
row 4
 3
 10
 26
 7
```

**9. Write a JavaScript program to find the sum of squares of a numeric vector.**
- Viết một chương trình JavaScript để tìm tổng của hình vuông của một vector số.
- The ```pow(x, y)```: phương thức trả về giá trị của x với x mũ y.

>JavaScript Code:
```javascript
function sum_sq(array) {
  var sum = 0,
    i = array.length;
  while (i--)
    sum += Math.pow(array[i], 2);
  return sum;
}

console.log(sum_sq([0, 1, 2, 3, 4]));
```

>ES6 Version:
```javascript
function sum_sq(array) {
  let sum = 0;
  let i = array.length;
  while (i--)
    sum += array[i] ** 2;
  return sum;
}

console.log(sum_sq([0, 1, 2, 3, 4]));
```

>Result:
```javascript
30
```

**10. Write a JavaScript program to compute the sum and product of an array of integers.**
- Viết một chương trình JavaScript để tính tổng và tính nhân của một mảng các số nguyên.

>JavaScript Code:
```javascript
var array = [1, 2, 3, 4, 5, 6],
  s = 0,
  p = 1,
  i;
for (i = 0; i < array.length; i += 1) {
  s += array[i];
  p *= array[i];
}
console.log('Sum : ' + s + ' Product :  ' + p);
```

>ES6 Version:
```javascript
const array = [1, 2, 3, 4, 5, 6];
let s = 0;
let p = 1;
let i;
for (i = 0; i < array.length; i += 1) {
  s += array[i];
  p *= array[i];
}
console.log(`Sum : ${s} Product :  ${p}`);
```

>Result:
```javascript
Sum: 21 
Multiplication: 720
```

**11. Write a JavaScript program to display the colors in the following way**
- Viết một chương trình JavaScript để hiển thị các màu theo cách sau.
- Here is the sample array:
- ```color = ["Blue ", "Green", "Red", "Orange", "Violet", "Indigo", "Yellow "];```
- ```o = ["th","st","nd","rd"]```
- Output
+ "1st choice is Blue ."
+ "2nd choice is Green."
+ "3rd choice is Red."

>JavaScript Code:
```javascript
var color = ["Blue ", "Green", "Red", "Orange", "Violet", "Indigo", "Yellow "];

function Ordinal(n) {
  var o = ["th", "st", "nd", "rd"],
    x = n % 100;
  return x + (o[(x - 20) % 10] || o[x] || o[0]);
}

for (n = 0; n < color.length; n++) {
  var ordinal = n + 1;
  var output = (Ordinal(ordinal) + " choice is " + color[n] + ".");
  console.log(output);
}
```

>ES6 Version:
```javascript
const color = ["Blue ", "Green", "Red", "Orange", "Violet", "Indigo", "Yellow "];

function Ordinal(n) {
  const o = ["th", "st", "nd", "rd"];
  const x = n % 100;
  return x + (o[(x - 20) % 10] || o[x] || o[0]);
}

for (n = 0; n < color.length; n++) {
  const ordinal = n + 1;
  const output = (`${Ordinal(ordinal)} choice is ${color[n]}.`);
  console.log(output);
}
```

>Result:
```javascript
1st choice is Blue .
2nd choice is Green.
3rd choice is Red.
4th choice is Orange.
5th choice is Violet.
6th choice is Indigo.
7th choice is Yellow .
```

**12. Find the leap years in a given range of years.**
- Tìm năm nhuận trong một phạm vi nhất định của năm.
- The ```forEach()``` method calls a provided function once for each element in an array, in order.(Phương thức ```forEach()``` gọi một hàm được cung cấp một lần cho mỗi phần tử trong một mảng, theo thứ tự.)
- ```forEach()``` does not execute the function for array elements without values.(```forEach()``` không thực hiện chức năng cho các phần tử mảng không có giá trị.)

>JavaScript Code:
```javascript
function leap_year_range(st_year, end_year) {
  var year_range = [];
  for (var i = st_year; i <= end_year; i++) {
    year_range.push(i);
  }
  var new_array = [];

  year_range.forEach(
    function(year) {
      if (test_LeapYear(year))
        new_array.push(year);
    });

  return new_array;
}

function test_LeapYear(year) {
  if ((year % 4 === 0 && year % 100 !== 0) || (year % 100 === 0 && year % 400 === 0)) {
    return year;
  } else {
    return false;
  }
}

console.log(leap_year_range(2000, 2012));
```

>ES6 Version:
```javascript
function leap_year_range(st_year, end_year) {
  const year_range = [];
  for (let i = st_year; i <= end_year; i++) {
    year_range.push(i);
  }
  const new_array = [];

  year_range.forEach(
    year => {
      if (test_LeapYear(year))
        new_array.push(year);
    });

  return new_array;
}

function test_LeapYear(year) {
  if ((year % 4 === 0 && year % 100 !== 0) || (year % 100 === 0 && year % 400 === 0)) {
    return year;
  } else {
    return false;
  }
}

console.log(leap_year_range(2000, 2012));
```

>Result:
```javascript
[2000,2004,2008,2012]
```

**13. Write a JavaScript program to shuffle an array.**
**Hay**
- Viết một chương trình JavaScript để xáo trộn một mảng.

>JavaScript Code:
```javascript
function shuffle(arra1) {
  var ctr = arra1.length,
    temp, index;

  // While there are elements in the array
  while (ctr > 0) {
    // Pick a random index
    index = Math.floor(Math.random() * ctr);
    // Decrease ctr by 1
    ctr--;
    // And swap the last element with it
    temp = arra1[ctr];
    arra1[ctr] = arra1[index];
    arra1[index] = temp;
  }
  return arra1;
}
var myArray = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];
console.log(shuffle(myArray));
```

>ES6 Version:
```javascript
function shuffle(arra1) {
  let ctr = arra1.length;
  let temp;
  let index;

  // While there are elements in the array
  while (ctr > 0) {
    // Pick a random index
    index = Math.floor(Math.random() * ctr);
    // Decrease ctr by 1
    ctr--;
    // And swap the last element with it
    temp = arra1[ctr];
    arra1[ctr] = arra1[index];
    arra1[index] = temp;
  }
  return arra1;
}
const myArray = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];
console.log(shuffle(myArray));
```

>Result:
```javascript
[5,3,0,9,8,2,1,4,7,6]
```

**14. There are two arrays with individual values, write a JavaScript program to compute the sum of each individual index value from the given arrays.**
- Có hai mảng với các giá trị riêng, viết một chương trình JavaScript để tính tổng của mỗi giá trị chỉ số cá nhân từ các mảng cho trước.
- Phương thức ```push()``` thêm các mục mới vào cuối mảng, và trả về chiều dài mới.

**Sample array:**
- ```array1 = [1,0,2,3,4];```
- ```array2 = [3,5,6,7,8,13];```
**Expected Output:** 
- ```[4, 5, 8, 10, 12, 13]```

>JavaScript Code:
```javascript
function Arrays_sum(array1, array2) {
  var result = [];
  var ctr = 0;
  var x = 0;

  if (array1.length === 0)
    return "array1 is empty";
  if (array2.length === 0)
    return "array2 is empty";

  while (ctr < array1.length && ctr < array2.length) {
    result.push(array1[ctr] + array2[ctr]);
    ctr++;
  }

  if (ctr === array1.length) {
    for (x = ctr; x < array2.length; x++) {
      result.push(array2[x]);
    }
  } else {
    for (x = ctr; x < array1.length; x++) {
      result.push(array1[x]);
    }
  }
  return result;
}

console.log(Arrays_sum([1, 0, 2, 3, 4], [3, 5, 6, 7, 8, 13]));
```

>ES6 Version:
```javascript
function Arrays_sum(array1, array2) {
  const result = [];
  let ctr = 0;
  let x = 0;

  if (array1.length === 0)
    return "array1 is empty";
  if (array2.length === 0)
    return "array2 is empty";

  while (ctr < array1.length && ctr < array2.length) {
    result.push(array1[ctr] + array2[ctr]);
    ctr++;
  }

  if (ctr === array1.length) {
    for (x = ctr; x < array2.length; x++) {
      result.push(array2[x]);
    }
  } else {
    for (x = ctr; x < array1.length; x++) {
      result.push(array1[x]);
    }
  }
  return result;
}

console.log(Arrays_sum([1, 0, 2, 3, 4], [3, 5, 6, 7, 8, 13]));
```

>Result:
```javascript
[4,5,8,10,12,13]
```

**15. Write a JavaScript program to find duplicate values in a JavaScript array.**
- Viết chương trình JavaScript để tìm các giá trị trùng lặp trong một mảng JavaScript.
>JavaScript Code:
```javascript
function find_duplicate_in_array(arra1) {
  var i,
  len=arra1.length,
  result = [],
  obj = {}; 
  for (i=0; i<len; i++)
  {
  obj[arra1[i]]=0;
  }
  for (i in obj) {
  result.push(i);
  }
  return result;
  }
var arr = [1, 2, -2, 4, 5, 4, 7, 8, 7, 7, 71, 3, 6];
console.log(find_duplicate_in_array(arr));
```

>ES6 Version:
```javascript
function find_duplicate_in_array(arra1) {
  let i;
  const len=arra1.length;
  const result = [];
  const obj = {};
  for (i=0; i<len; i++){
    obj[arra1[i]]=0;
  }
  for (i in obj) {
    result.push(i);
  }
  return result;
}
const arr = [1, 2, -2, 4, 5, 4, 7, 8, 7, 7, 71, 3, 6];
console.log(find_duplicate_in_array(arr));
```

>Result:
```javascript
["1","2","3","4","5","6","7","8","71","-2"]
```

**16. Write a JavaScript program to compute the union of two arrays.**
- Viết một chương trình JavaScript để tính toán sự kết hợp của hai mảng.
>JavaScript Code:
```javascript
function union(arra1, arra2) {
  if ((arra1 == null) || (arra2 == null))
    return void 0;
  var obj = {};
  for (var i = arra1.length - 1; i >= 0; --i)
    obj[arra1[i]] = arra1[i];
  for (var i = arra2.length - 1; i >= 0; --i)
    obj[arra2[i]] = arra2[i];
  var res = [];
  for (var n in obj) {
    if (obj.hasOwnProperty(n))
       res.push(obj[n]);
  }
  return res;
}
console.log(union([1, 2, 3], [100, 2, 1, 10]));
```

>ES6 Version:
```javascript
function union(arra1, arra2) {
  if ((arra1 == null) || (arra2 == null))
    return void 0;
  const obj = {};
  for (var i = arra1.length - 1; i >= 0; --i)
    obj[arra1[i]] = arra1[i];
  for (var i = arra2.length - 1; i >= 0; --i)
    obj[arra2[i]] = arra2[i];
  const res = [];
  for (const n in obj) {
    if (obj.hasOwnProperty(n))
      res.push(obj[n]);
  }
  return res;
}
console.log(union([1, 2, 3], [100, 2, 1, 10]));
```

>Result:
```javascript
[1,2,3,10,100]
```

**17. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

>Result:
```javascript

```

**18. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

>Result:
```javascript

```

**19. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

>Result:
```javascript

```

**20. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

>Result:
```javascript

```

**21. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

>Result:
```javascript

```

**22. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

>Result:
```javascript

```

**23. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

>Result:
```javascript

```

**24. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

>Result:
```javascript

```

**25. **

>JavaScript Code:
```javascript

```

>ES6 Version:
```javascript

```

>Result:
```javascript

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

>Result:
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

