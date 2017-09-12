#### I. Map(): 

- Hàm map của array trong Javascript, hàm này giống như vòng lặp vậy, nó có một tham số truyền vào và đó là một callback function, hàm callback function này sẽ có hai tham số truyền vào đại diện cho value và key của mỗi phần tử trong mảng.
- Sử dụng hàm map để chuyển đổi các giá trị của các phần tử trong mảng sang chữ in hoa.

```javascript
var domain = ["freetuts.net", 'qa.freetuts.net', 'demo.freetuts.net'];
 
domain.map(function(val, key){
    console.log(val.toUpperCase());   
});
 
console.log(domain);
```
#### II. sort():
- sắp xếp các hạng mục của một mảng.
- Thứ tự sắp xếp có thể là chữ hoặc số, và hoặc tăng dần (up) hoặc giảm dần (giảm).
- Theo mặc định, function sort() sắp xếp các giá trị như các chuỗi trong thứ tự chữ cái và tăng dần.
- Hoạt động tốt trong chuỗi strings ("Apple" comes before "Banana"). Tuy nhiên, nếu number được sắp xếp như strings, "25" là lớn hơn "100", bởi vì "2" là lớn hơn "1".

#### III. Các hàm String trong javascript:
##### 1. split(separator, limit): được sử dụng để tách một chuỗi thành một mảng của chuỗi con, và trả về mảng mới.
- separator : Xác định ký tự sử dụng để chia chuỗi đó. Nếu separator bị bỏ quên, mảng trả về chứa một phần tử chứa cả chuỗi đó.
- limit: Số integer xác định một giới hạn về số các phần chia.

```javascript
var str = "How are you doing today?";
var res = str.split(" ");
```
==> Result: How,are,you,doing,today?

```javascript
var str = "How are you doing today?";
var res = str.split(" ", 3);
```
==> Result: How,are,you

```javascript
var str = "How are you doing today?1";
var res = str.split("?")[0];
```
==> Result: How are you doing today

```javascript
var str = "How are you doing today?1";
var res = str.split("?")[1];
```
==> Result: 1

##### 2. Math.floor() : function returns the largest integer less than or equal to a given number. Hàm trả về số nguyên lớn nhất nhỏ hơn hoặc bằng một số nhất định.
- Vòng một số xuống số nguyên gần nhất
- Using Math.floor()

```javascript
Math.floor( 45.95); //  45
Math.floor( 45.05); //  45
Math.floor(  4   ); //   4
Math.floor(-45.05); // -46 
Math.floor(-45.95); // -46
```

##### 4. Math.random(): Trả về một số ngẫu nhiên giữa 0 (inclusive) và 1 (exclusive):

- inclusive: bao hàm
- exclusive: độc quyền

```javascript
function getRandom() {
  return Math.random();
}
```

- Case 1: ```Math.floor((Math.random() * 10) + 1)``` Có nghĩa là Click vào ```button```để hiển thị một số ngẫu nhiên giữa 1 và 10

```html 
<button onclick="myFunction()">Try it</button>
```

```javascript
function myFunction() {
    var x = Math.floor((Math.random() * 10) + 1);
    document.getElementById("demo").innerHTML = x;
}
```

- Case 1: ```Math.floor((Math.random() * 10))``` Có nghĩa là Click vào ```button```để hiển thị một số ngẫu nhiên giữa 0 và 10

```javascript
function myFunction() {
    var x = Math.floor((Math.random() * 10));
    document.getElementById("demo").innerHTML = x;
}
```


##### 5. indexOf():
##### 6. lastIndexOf():
##### 7. search():
##### 8. slice(start, end):
##### 9. substring(start, end):
##### 10. substr(start, length):