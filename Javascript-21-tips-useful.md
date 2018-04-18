#### I. 21 THỦ THUẬT JAVASCRIPT HỮU ÍCH.
---

**1. Tạo hàm query DOM ngắn gọn hơn với bind**
- Có thể bạn thừa biết, JavaScript cung cấp phương thức ```document.querySelector()``` cho phép bạn query DOM dựa trên selector. Tuy nhiên, việc sử dụng phương thức này khá dài dòng. Ví dụ:

>JavaScript Code:
```javascript
let ele1 = document.querySelector("#id1");
let ele2 = document.querySelector(".class2");
let ele3 = document.querySelector("div.user-panel.main input[name='login']");
```

>JavaScript Code:
```javascript
let $ = document.querySelector.bind(document);
 
// Usage
let ele1 = $("#id1");
let ele2 = $(".class2");
let ele3 = $("div.user-panel.main input[name='login']");
```
- Ở đây, mình đặt tên hàm mới là ```$```, nên bạn nhìn thấy nó giống với ```jQuery```, nhưng nhớ rằng đây vẫn chỉ là JavaScript thuần mà thôi.

**2. Rút gọn hàm console.log**

- Tương tự như trên, bạn cũng có thể sử dụng bind để rút gọn phương thức console.log như sau:
>JavaScript Code:
```javascript
let log = console.log.bind(document);
log('hello'); // => hello
```

**3. Sao chép (clone) object**

>JavaScript Code:
```javascript
let obj1 = {
  a: 1, 
  b: 2
};
 
let obj2 = obj1;
console.log(obj2 === obj1); // => true
 
obj2.a = 10;
obj2.b = 20;
console.log(obj1.a, obj1.b); // => 10, 20
```

- Bạn có thể thấy là obj2 thực chất là tham chiếu của obj1. Khi obj2 thay đổi thì obj1 cũng sẽ bị thay đổi. Để có thể clone object, tạo ra một object hoàn toàn mới, bạn có thể làm theo 2 cách sau:

>JavaScript Code:
```javascript
// shallow clone an object 
let newObj = Object.assign({}, obj);
 
// deep clone an object
let newObj = JSON.parse(JSON.stringify(obj));
```

**4. Hoán đổi giá trị 2 số**

- Để có thể hoán đổi giá trị 2 biến số trong JavaScript, bạn có thể làm như sau:
>JavaScript Code:
```javascript
let x = 1, y = 2;
console.log(x, y); // 1, 2
 
[x, y] = [y, x];
console.log(x, y); // 2, 1
```

**5. Đặt giá trị mặc định cho tham số của hàm**: Có hai cách để làm việc này:
- ES5: sử dụng toán tử ||

>JavaScript Code:
```javascript
function Person(name, age) {
  this.name = name || "Alex";
  this.age = age || 20; 
}
 
let p1 = new Person();
console.log(p1.name, p1.age) // => Alex, 20
 
let p2 = new Person("John", 25);
console.log(p2.name, p2.age) // => John, 25
```

- ES6: hỗ trợ trực tiếp

>JavaScript Code:
```javascript
function Person(name = "Alex", age = 20) {
  this.name = name;
  this.age = age; 
}
 
let p1 = new Person();
console.log(p1.name, p1.age) // => Alex, 20
 
let p2 = new Person("John", 25);
console.log(p2.name, p2.age) // => John, 25
```

**6. Lấy random trong một đoạn**

>JavaScript Code:
```javascript
let random = (min, max) => Math.floor(Math.random() * (max - min + 1)) + min;
 
// Usage
let a = random(1, 100);
```

**7. Loại bỏ kí tự trống (```trim```) 2 đầu string**
- Bạn có thể sử dụng phương thức ```trim()``` hỗ trợ sẵn của string:

>JavaScript Code:
```javascript
let str = "       Hello World!        ";
console.log(str)         // =>        Hello World!
console.log(str.trim()); // => Hello World!
```
- Trong trường hợp trình duyệt không hỗ trợ phương thức trên, bạn có thể sử dụng ```Regex```:
>JavaScript Code:
```javascript
function trim(x) {
  return x.replace(/^\s+|\s+$/gm,'');
}
 
let str = "       Hello World!        ";
console.log(str)         // =>        Hello World!
console.log(trim(str));  // => Hello World!
```
**8. Chuyển đối tượng arguments thành array**
- ```Hàm số``` trong JavaScript luôn có một đối tượng mặc định là ```arguments``` để quản lý tham số của hàm. Tuy nhiên, đối tượng này không phải là ```array``` nên bạn không thể sử dụng các phương thức như ```forEach```, ```map```,…

>JavaScript Code:
```javascript
let args = Array.prototype.slice.call(arguments);
let args = [].slice.call(arguments);
 
// ES2015
let args = Array.from(arguments);
```

**9. Tìm max và min của các phần tử trong mảng**

>JavaScript Code:
```javascript
let numbers = [1, 8 , 10 , -125 , 28 , 100 , 215, -85]; 
let maxInNumbers = Math.max.apply(Math, numbers); 
let minInNumbers = Math.min.apply(Math, numbers);
 
console.log(maxInNumbers, minInNumbers);
// => 215 -125
```

**10. Đưa mảng về rỗng**
- Nhiều bạn đưa mảng về rỗng bằng cách:

>JavaScript Code:
```javascript
let a = [1, 2, 3];
a = [];
```

- Khi đó, thực chất là bạn đã tạo thêm một mảng mới. Cách đơn giản để giải quyết vấn đề này là:

>JavaScript Code:
```javascript
let a = [1, 2, 3];
a.length = 0;
 
console.log(a); // => []
```
**11. Loại bỏ một phần tử ra khỏi mảng**
- Bạn không nên sử dụng ```delete``` để loại bỏ một phần tử ra khỏi mảng. Hàm này không loại bỏ 1 phần tử ra khỏi mảng mà thay vào đó, nó làm cho giá trị của phần tử đó thành ```undefined``` và độ dài của mảng vẫn không thay đổi.

>JavaScript Code:
```javascript
let arr = ["a", 1, -5, "cde"];
console.log(arr);        // => ["a", 1, -5, "cde"]
 
delete arr[2];
console.log(arr);        // => ["a", 1, undefined, "cde"]
console.log(arr.length); // => 4
```

- Thay vào đó, bạn có thể dùng hàm splice:

>JavaScript Code:
```javascript
let arr = ["a", 1, -5, "cde"];
console.log(arr);        // => ["a", 1, -5, "cde"]
 
arr.splice(2, 1);
console.log(arr);        // => ["a", 1, "cde"]
console.log(arr.length); // => 3
```

**12. Sử dụng and ```(&&)``` và or ```(||)``` thay cho ```if```**
- Giả sử bạn có các câu điều kiện sử dụng if như sau:

>JavaScript Code:
```javascript
let a = 10;
if (a === 10) console.log("a === 10"); // => a === 10
if (a !== 5) console.log("a !== 5"); // => a !== 5
```

- Khi đó, bạn có thể sử dụng toán tử && và || để thay thế như sau:

>JavaScript Code:
```javascript
let a = 10;
a === 10 && console.log("a === 10"); // => a === 10
a === 5 || console.log("a !== 5");   // => a !== 5
```

- Hoặc kết hợp cả hai toán tử, thay vì:
>JavaScript Code:
```javascript
// Hoặc kết hợp cả 2 toán tử
let a = 10;
if (a === 5) console.log("a === 5");
else console.log("a !== 5");
```

- thì bạn có thể làm như sau:
>JavaScript Code:
```javascript
let a = 10;
a === 5 && console.log("a === 5") || console.log("a !== 5");
```

**13. Duyệt tất cả các properties của object sử dụng for-in loop**

>JavaScript Code:
```javascript
for (let name in object) {
    if (object.hasOwnProperty(name)) {
        // do something with name
    }
}
```

**14. Convert Object sang ```JSON``` và ngược lại**

>JavaScript Code:
```javascript
let obj1 = {a: 1, b: 2};
 
// Object => JSON string
let strJSON = JSON.stringify(obj1);
console.log(strJSON); // => {"a":1,"b":2}
 
// JSON string => object
let obj2 = JSON.parse(strJSON);
console.log(obj2);   // => {a: 1, b: 2}
```

**15. Viết hàm ngắn hơn với arrow function**

- Ví dụ sau sử dụng map để trả về mảng mới với mỗi phần tử là bình phương của mỗi phần tử trong mảng ban đầu:
>JavaScript Code:
```javascript
let a = [1, 2, 3, 4, 5];
let a2 = a.map(function(item) {
  return item * item; 
});
 
console.log(a2);
// => [1, 4, 9, 16, 25]
```

- Nếu sử dụng arrow function thì sẽ thế này:
>JavaScript Code:
```javascript
let a = [1, 2, 3, 4, 5];
let a2 = a.map(item => item * item);
 
console.log(a2);
// => [1, 4, 9, 16, 25]
```

**16. Sử dụng string template literals thay vì +**

- Có phải bạn thường sử dụng toán tử + để cộng (ghép) string, ví dụ:
>JavaScript Code:
```javascript
let a = 10, b = 20;
console.log("Sum of " + a + " and " + b + " is " + (a + b) + ".");
// => Sum of a and b is 30.
```

- Thay vào đó, bạn có thể sử dụng string template literals:
>JavaScript Code:
```javascript
let a = 10, b = 20;
console.log(`Sum of ${a} and ${b} is ${a + b}.`);
// => Sum of 10 and 20 is 30.
```

**17. Sao chép (copy) mảng**

>JavaScript Code:
```javascript
let a = [1, 2, 3];
let b = a.slice();
 
console.log(b);       // => [1, 2, 3]
console.log(b === a); // => false
```

**18. Sử dụng Promise thay vì dùng callback**
- Code khi sử dụng callback:
>JavaScript Code:
```javascript
func1(function (value1) {
    func2(value1, function (value2) {
        func3(value2, function (value3) {
            func4(value3, function (value4) {
                func5(value4, function (value5) {
                    // Do something with value 5
                });
            });
        });
    });
});
```

- Code khi implement bằng Promise:
>JavaScript Code:
```javascript
func1(value1)
    .then(func2)
    .then(func3)
    .then(func4)
    .then(func5, value5 => {
        // Do something with value 5
    });
```

**19. Nối mảng**

- Có 3 cách nối mảng như sau:
>JavaScript Code:
```javascript
let one = ['a', 'b', 'c']
let two = ['d', 'e', 'f']
let three = ['g', 'h', 'i']
 
// Old way #1
const result1 = one.concat(two, three);
console.log(result1);
// => ["a", "b", "c", "d", "e", "f", "g", "h", "i"]
 
// Old way #2
const result2 = [].concat(one, two, three);
console.log(result2);
// => ["a", "b", "c", "d", "e", "f", "g", "h", "i"]
 
// New
const result3 = [...one, ...two, ...three];
console.log(result3);
// => ["a", "b", "c", "d", "e", "f", "g", "h", "i"]
```

**20. Clone object và array sử dụng Spread**

- Clone object:
>JavaScript Code:
```javascript
let obj = {a: 1, b: 2};
let obj2 = {...obj};
console.log(obj2); // => {a: 1, b: 2};
```

- Clone mảng:
>JavaScript Code:
```javascript
let arr = [1, 2];
let arr2 = [...arr];
console.log(arr2); // => [1, 2];
```

**21. Set key của object một cách linh động**

- Với cách thông thường:
>JavaScript Code:
```javascript
let myKey = 'key3';
let obj = {
    key1: 'One',
    key2: 'Two'
};
obj[myKey] = 'Three';
console.log(obj); // => {key1: "One", key2: "Two", variableKey: "Three"}
```

- Với cách ngắn gọn hơn sử dụng []:
>JavaScript Code:
```javascript
let myKey = 'variableKey';
let obj = {
    key1: 'One',
    key2: 'Two',
    [myKey]: 'Three'
};
console.log(obj); // => {key1: "One", key2: "Two", variableKey: "Three"}
```