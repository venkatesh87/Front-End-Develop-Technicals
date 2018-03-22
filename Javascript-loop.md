#### I. JavaScript Loop
---

**1. forEach.**

- The ```forEach()``` method calls a provided function once for each element in an array, in order.(Phương thức ```forEach()``` gọi một hàm được cung cấp một lần cho mỗi phần tử trong một mảng, theo thứ tự.)
- ```forEach()``` does not execute the function for array elements without values.(```forEach()``` không thực hiện chức năng cho các phần tử mảng không có giá trị.)

>**Syntax**

```javascript
arr.forEach(function callback(currentValue[, index[, array]]) {
  //your iterator
}[, thisArg]);
```

- ```currentValue```: Giá trị của phần tử hiện tại được xử lý trong mảng. 
- ```index```: Chỉ mục của phần tử hiện tại đang được xử lý trong mảng đó.
- ```array```: Mảng mà forEach () đang được áp dụng.
- ```thisArg```: Value to use as this (i.e the reference Object) when executing callback.

>JavaScript forEach():
```javascript
var array1 = ['a', 'b', 'c'];

array1.forEach(function(element) {
  console.log(element);
});

// expected output: "a"
// expected output: "b"
// expected output: "c"
```

**Reference**: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach

**1a. Converting from ```for``` to ```forEach```**

>**before**
```javascript
const items = ['item1', 'item2', 'item3'];
const copy = [];
for (let i = 0; i < items.length; i++) {
  copy.push(items[i])
}
```

>**after**
```javascript
const items = ['item1', 'item2', 'item3'];
const copy = [];
items.forEach(function(item) {
  copy.push(item)
});
```

>**1b. Printing the contents of an array**

```javascript
function logArrayElements(element, index, array) {
  console.log('a[' + index + '] = ' + element);
}

// Notice that index 2 is skipped since there is no item at
// that position in the array.
[2, 5, , 9].forEach(logArrayElements);
// logs:
// a[0] = 2
// a[1] = 5
// a[3] = 9
```

>**1c. Using thisArg**

```javascript
function Counter() {
  this.sum = 0;
  this.count = 0;
}
Counter.prototype.add = function(array) {
  array.forEach(function(entry) {
    this.sum += entry;
    ++this.count;
  }, this);
  // ^---- Note
};

const obj = new Counter();
obj.add([2, 5, 9]);
obj.count;
// 3 
obj.sum;
// 16
```

>**1d. An object copy function**

```javascript
function copy(obj) {
  const copy = Object.create(Object.getPrototypeOf(obj));
  const propNames = Object.getOwnPropertyNames(obj);

  propNames.forEach(function(name) {
    const desc = Object.getOwnPropertyDescriptor(obj, name);
    Object.defineProperty(copy, name, desc);
  });

  return copy;
}

const obj1 = { a: 1, b: 2 };
const obj2 = copy(obj1); // obj2 looks like obj1 now
```

>**1e. If the array is modified during iteration, other elements might be skipped.**

```javascript
var words = ['one', 'two', 'three', 'four'];
words.forEach(function(word) {
  console.log(word);
  if (word === 'two') {
    words.shift();
  }
});
// one
// two
// four
```

