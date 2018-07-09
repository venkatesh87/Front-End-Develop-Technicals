#### I. JavaScript function string
---
**1. substr ():**

- ```string.substr(start, length)```
- Phương thức ```substr()``` lấy ra các phần của một chuỗi, bắt đầu từ ký tự tại vị trí đã chỉ định và trả về số ký tự được chỉ định.
- ```substr()```: Là phương thức không thay đổi chuỗi gốc.
- ```start```: 
  + Cần thiết, Vị trí bắt đầu khai thác. Ký tự đầu tiên ở chỉ số 0
  + Nếu bắt đầu là dương và lớn hơn, hoặc bằng, với chiều dài của chuỗi, substr() trả về một chuỗi rỗng.
  + Nếu bắt đầu là số âm, substr() sử dụng nó như là một chỉ số ký tự từ cuối của chuỗi.
  + Nếu bắt đầu là số âm hoặc lớn hơn chiều dài của chuỗi, bắt đầu được đặt thành 0
- ```length```: Không bắt buộc, Số ký tự để lấy xuất. Nếu bỏ qua, nó sẽ trích ra phần còn lại của chuỗi

>**Case 1:** Từ chỉ số thứ 1 lấy 4 ký tự
```javascript
function myFunction() {
  var str = "Hello world!";
  var res = str.substr(1, 4);
  document.getElementById("demo").innerHTML = res;
}
```

>Result:
```javascript
ello
```

>**Case 2:** Trả lại các phần tử còn lại của chuỗi từ chỉ số thứ 2

```javascript
function myFunction() {
    var str = "Hello world!";
    var res = str.substr(2);
    document.getElementById("demo").innerHTML=res;
}
```

>Result:
```javascript
llo world!
```

>**Case 3:** Từ chỉ số thứ 11 lấy 1 ký tự
```javascript
function myFunction() {
  var str = "Hello world!";
  var res = str.substr(11, 1);
  document.getElementById("demo").innerHTML = res;
}
```

>Result:
```javascript
!
```

**2. substring():**

- ```string.substring(start, end)```
- Phương thức ```substring()``` lấy ra các ký tự từ một chuỗi, giữa hai chỉ số xác định, và trả về chuỗi con mới.
- Phương pháp này lấy các ký tự trong một chuỗi giữa ```start``` và ```end```, không bao gồm ```end``` chính nó. " chính nó.
- Nếu ```start``` lớn hơn ```end```, phương pháp này sẽ hoán đổi hai đối số, có nghĩa là ```str.substring (1, 4) == str.substring (4, 1)```.
- Nếu ```start``` hoặc ```end``` nhỏ hơn 0, nó sẽ được coi như là 0.
- Phương thức ```substring()``` không thay đổi chuỗi gốc
- ```start```: bắt buộc. Vị trí bắt đầu khai thác. Ký tự đầu tiên ở chỉ số 0
- ```end```: Không bắt buộc. Vị trí (đến, nhưng không bao gồm) nơi để kết thúc khai thác. Nếu bỏ qua, nó sẽ lấy phần còn lại của chuỗi

>**Case 1:**
```javascript
function myFunction() {
  var str = "Hello world!";
  var res = str.substring(1, 4);
  document.getElementById("demo").innerHTML = res;
}
```

>Result:
```javascript
ell
```

>**Case 2:**
```javascript
function myFunction() {
  var str = "Hello world!";
  var res = str.substring(2);
  document.getElementById("demo").innerHTML = res;
}
```

>Result:
```javascript
llo world!
```

>**Case 3:**
```javascript
function myFunction() {
  var str = "Hello world!";
  var res = str.substring(-3);
  document.getElementById("demo").innerHTML = res;
}
```

>Result:
```javascript
Hello world!
```

**3. slice():**

- ```array.slice(start, end)```
- Phương thức ```slice()``` trả về các phần tử đã chọn trong một mảng, như một đối tượng mảng mới.
- Phương thức ```slice()``` chọn các phần tử bắt đầu từ đối số start đã cho, và kết thúc tại, nhưng không bao gồm, đối số kết thúc đã cho.
- ```start```: Không bắt buộc. Một số nguyên xác định nơi bắt đầu lựa chọn (Phần tử đầu tiên có chỉ số 0). Sử dụng số âm để chọn từ cuối mảng. Nếu bỏ qua, nó hoạt động như "0"
- ```end```: Không bắt buộc. Một số nguyên xác định nơi để kết thúc lựa chọn. Nếu bỏ qua, tất cả các yếu tố từ vị trí bắt đầu và đến cuối mảng sẽ được chọn. Sử dụng số âm để chọn từ cuối mảng

>**Case 1:**

```javascript
function myFunction() {
  var fruits = ["Banana", "Orange", "Lemon", "Apple", "Mango"];
  var citrus = fruits.slice(1, 3);
  document.getElementById("demo").innerHTML = citrus;
}
```

>Result:
```javascript
Orange,Lemon
```

>**Case 2:**
```javascript
function myFunction() {
  var fruits = ["Banana", "Orange", "Lemon", "Apple", "Mango"];
  var myBest = fruits.slice(-3, -1);
  document.getElementById("demo").innerHTML = myBest;
}
```

>Result:
```javascript
Lemon,Apple
```

**4. splice():** The splice() method adds/removes items to/from an array, and returns the removed item(s).

```javascript
array.splice(index, howmany, item1, ....., itemX)
```

>**Case 1**
```javascript
var fruits = ["Banana", "Orange", "Apple", "Mango"];
fruits.splice(2, 1, "Lemon", "Kiwi");
```

>**Result 1**

- At position 2, remove 2 items:

```javascript
Banana,Orange,Lemon,Kiwi,Mango
```

>**Case 2**
```javascript
var fruits = ["Banana", "Orange", "Apple", "Mango", "Kiwi"];
fruits.splice(2, 2);
```

>**Result 2**
```javascript
Banana,Orange,Kiwi
```

**5. split():** 
- Phương thức ```split()``` được sử dụng để chia một chuỗi thành một mảng các chuỗi con, và trả về mảng mới.
- Nếu một chuỗi rỗng ("") được sử dụng làm dấu tách, chuỗi được phân chia giữa mỗi ký tự.
- ```string.split(separator, limit)```
- ```separator```: Không bắt buộc, Chỉ định ký tự, hoặc biểu thức chính quy, để sử dụng cho việc chia tách chuỗi. Nếu bỏ qua, toàn bộ chuỗi sẽ được trả lại (một mảng chỉ với một mục)
- ```limit```: Một số nguyên xác định số lượng các phần tách, các mục sau khi giới hạn phân chia sẽ không được bao gồm trong mảng

>**Case 1:**
```javascript
function myFunction() {
  var str = "How are you doing today?";
  var res = str.split(" ");
  document.getElementById("demo").innerHTML = res;
}
```
>Result:
```javascript
How,are,you,doing,today?
```

>**Case 2:**
```javascript
function myFunction() {
  var str = "How are you doing today?";
  var res = str.split(" ", 3);
  document.getElementById("demo").innerHTML = res;
}
```
>Result:
```javascript
How,are,you
```
>**Case 3:**
```javascript
function myFunction() {
  var str = "How are you doing today?";
  var res = str.split("o");
  document.getElementById("demo").innerHTML = res;
}
```
>Result:
```javascript
H,w are y,u d,ing t,day?
```
**6. join():** 

- Phương thức ```join()``` kết hợp các phần tử của một mảng vào một chuỗi, và trả về chuỗi.
- Các phần tử sẽ được phân tách bằng một dấu tách quy định. Dấu tách mặc định là dấu phẩy (,).

```javascript
function myFunction() {
  var fruits = ["Banana", "Orange", "Apple", "Mango"];
  var x = document.getElementById("demo");
  x.innerHTML = fruits.join();
}
```

>Result:
```javascript
Banana,Orange,Apple,Mango
```

**7. indexOf():** 
- ```string.indexOf(searchvalue, start)```
- ```searchvalue```: Cần thiết. Chuỗi để tìm kiếm
- ```start```: Default  0. Tại vị trí nào để bắt đầu tìm kiếm
- Phương thức ```indexOf()``` trả về vị trí của sự xuất hiện đầu tiên của một giá trị được chỉ định trong một chuỗi.
- Phương thức này trả về -1 nếu giá trị tìm kiếm không bao giờ xảy ra.
- Phương thức ```indexOf()``` phân biệt chữ hoa chữ thường.
>**Case 1:**
```javascript
function myFunction() {
  var str = "Hello world, welcome to the universe.";
  var n = str.indexOf("welcome");
  document.getElementById("demo").innerHTML = n;
}
```
>Result:
```javascript
13
```
>**Case 2:**
```javascript
function myFunction() {
  var str = "Hello world, welcome to the universe.";
  var n = str.indexOf("e");
  document.getElementById("demo").innerHTML = n;
}
```
>Result:
```javascript
1
```
>**Case 3:**
```javascript
function myFunction() {
  var str = "Hello world, welcome to the universe.";
  var n = str.indexOf("e", 5);
  document.getElementById("demo").innerHTML = n;
}
```
>Result:
```javascript
14
```

>**indexOf() Array**: Phương thức ```indexOf()``` tìm kiếm mảng cho mục được chỉ định và trả về vị trí(position) của nó.
```javascript
function myFunction() {
  var fruits = ["Banana", "Orange", "Apple", "Mango"];
  var a = fruits.indexOf("Apple");
  document.getElementById("demo").innerHTML = a;
}
```
**==> Result:** 2
**8. lastIndexOf():** 
- ```string.lastIndexOf(searchvalue, start)```
- ```searchvalue```: Cần thiết. Chuỗi để tìm kiếm
- ```start```: Vị trí bắt đầu tìm kiếm (tìm kiếm ngược). Nếu bỏ qua, giá trị mặc định là chiều dài của chuỗi
- Phương thức ```lastIndexOf()``` trả về vị trí của lần xuất hiện cuối cùng của một giá trị được chỉ định trong một chuỗi.
- Chuỗi được tìm kiếm từ cuối đến đầu, nhưng trả về chỉ mục bắt đầu từ đầu, ở vị trí 0.
- Phương thức này trả về -1 nếu giá trị tìm kiếm không bao giờ xảy ra.
- Phương thức ```lastIndexOf()``` phân biệt chữ hoa chữ thường!

>**Case 1:**
```javascript
function myFunction() {
  var str = "Hello planet earth, you are a great planet.";
  var n = str.lastIndexOf("planet");
  document.getElementById("demo").innerHTML = n;
}
```
>Result:
```javascript
36
```
>**Case 2:**
```javascript
function myFunction() {
  var str = "Hello planet earth, you are a great planet.";
  var n = str.lastIndexOf("planet", 20);
  document.getElementById("demo").innerHTML = n;
}
```

**9. charAt():** 

```javascript

```
>Result:
```javascript

```
**10. charCodeAt():** 

```javascript

```
>Result:
```javascript

```

**11. concat():** 

```javascript

```
>Result:
```javascript

```

**12. endsWith():** 

```javascript

```
>Result:
```javascript

```

**13. fromCharCode():** 

```javascript

```
>Result:
```javascript

```

**14. includes():** 

```javascript

```
>Result:
```javascript

```

**15. localeCompare():** 

```javascript

```
>Result:
```javascript

```

**16. match():** 

```javascript

```
>Result:
```javascript

```

**17. repeat():** 

```javascript

```
>Result:
```javascript

```

**18. replace():** 

```javascript

```
>Result:
```javascript

```

**19. search():** 

```javascript

```
>Result:
```javascript

```

**20. startsWith():** 

```javascript

```
>Result:
```javascript

```

**21. toLocaleLowerCase():** 

```javascript

```
>Result:
```javascript

```

**22. toLocaleUpperCase():** 

```javascript

```
>Result:
```javascript

```

**23. toLowerCase():** 

```javascript

```
>Result:
```javascript

```

**24. toString():** 

```javascript

```
>Result:
```javascript

```

**25. toUpperCase():** 

```javascript

```
>Result:
```javascript

```

**26. trim():** 

```javascript

```
>Result:
```javascript

```

**27. valueOf():** 

```javascript

```
>Result:
```javascript

```


