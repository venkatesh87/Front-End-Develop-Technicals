#### 1. Show message popup
```javascript
 window.alert("Hello");
 var result = confirm('Are you sure to delete this record?');
  if(result== true){
    alert("User Accepted");
  }
  else{
    alert("User Reject");
  }
```

```javascript
var input = prompt("Please tell me your name?", "No name");
alert(input);*/
```

#### 2. Variable

```javascript
  var one = 1;
  var two = 'two';
  var three;
  four = 4; // Neu ko co tu khoa var thi no se hieu la global.
  // OR
  var one = 1, two = 'two', three;
  //document.write(two);
```

#### 3. Javascript Operators: toan tu( +, -,*,/,%,++,-- ), A + B, A, B la toan hang, + la toan tu, bieu thuc 

- Toan tu so sanh == (So sanh gia trị với 2 toan hang), === (So sanh ca gia trị và kieu với 2 toan hang), !=, >, <, >=, <=
- Toan tu logic: &&, ||, !
- Toan tu gan(Assignment operators): =, +=, -=,/=,%=
- Toan tu 3 ngoi(Ternary operator)

```javascript
  var a1 = a==b?1:0;
  if(a==b)
    a1 = 1;
  else
    a1 = 0;
```

- Kieu du lieu(Data type): String, Number, Boolean, Null(Ko co gia tri) ==> kieu object, Undefined(ko xac dinh)==> kieu underfined

#### 4. String Object tra ve string dang object

>**Tìm kiếm chuỗi con**
- ```indexOf()```: Để tìm kiếm chuỗi con thì ta sử dụng hàm String.indexOf(str), trong đó str là chuỗi con và String là chuỗi cha. Hàm này sẽ trả kết quả về kết quả là vị trí xuât hiện đầu tiên của chuỗi (bắt đầu là vị trí 0), nếu không tìm thấy chuỗi con thì nó sẽ trả về -1.

```javascript
var string = "Chào mừng bạn đến với freetuts.net";
document.write("Vị trí xuất hiện chuỗi freetuts.net là: " + string.indexOf("freetuts.net"));
```

- ```lastIndexOf()```: Trường hợp nếu chuỗi con xuất hiện nhiều lần trong chuỗi cha thì kết quả cũng trả về vị trí xuất hiện của chuỗi con đầu tiên. Vậy làm thế nào để lấy vị trí của chuỗi con cuối cùng trong chuỗi cha? Ta sẽ sử dụng hàm String.lastIndexOf(str), hàm này sẽ trả về vị trí xuất hiện của chuỗi con cuối cùng và trả về -1 nếu không tìm thấy.

```javascript
var string = "Website freetuts.net - học lập trình miễn phí tại freetuts.net";
document.write("Vị trí xuất hiện chuỗi freetuts.net là: " + string.lastIndexOf("freetuts.net"));
```
- search(): tác dụng của nó cũng giống như hàm string.indexOf(str).

```javascript
var string = "Chào mừng bạn đến với freetuts.net";
document.write("Vị trí xuất hiện chuỗi freetuts.net là: " + string.search("freetuts.net"));<br>
```

>**Cắt chuỗi con**

>**```slice(start, end)```**: Phương thức trả về các phần tử đã chọn trong một mảng.

>**Nếu tham số truyền vào là số âm thì nó sẽ tính ngược lại, nghĩa là nó sẽ đếm từ cuối lên**

```javascript
var fruits = ["Banana", "Orange", "Lemon", "Apple", "Mango"];
var citrus = fruits.slice(1, 3);
// ==> Orange,Lemon
```

```javascript
var string = "Welcome to freetuts.net";
document.write("Chuỗi cần lấy là: " + string.slice(-12, 23));
```

>**Nếu bạn chỉ truyền một tham số đầu tiên thì nó sẽ tự hiểu vị trí end là vị trí cuối cùng**

```javascript
var string = "Welcome to freetuts.net";
document.write("Chuỗi cần lấy là: " + string.slice(5));
```

>**```substring(start, end)```**: Phương thức substring () trích ra các ký tự từ một chuỗi, giữa hai chỉ số được chỉ định, và trả về chuỗi con mới. 
  + Nếu "start" lớn hơn "end", phương pháp này sẽ hoán đổi hai đối số, có nghĩa là str.substring (1, 4) == str.substring (4, 1).
  + If either "start" or "end" is less than 0, it is treated as if it were 0.

```start```: vị trí bắt đầu, tất cả các vị trí của chuỗi đều bắt đầu từ 0.

```end```: vị trí kết thúc

```javascript
var str = "Hello world!";
var res = str.substring(2);
// ==> llo world!
```

```javascript
// Nếu "start" lớn hơn "end", nó sẽ hoán đổi hai đối số:
var str = "Hello world!";
var res = str.substring(4, 1);
// ==> ell
```

```javascript
// Nếu "start" nhỏ hơn 0, nó sẽ bắt đầu khai thác từ vị trí chỉ số 0
var str = "Hello world!";
var res = str.substring(-3);
// ==> Hello world!
```

```javascript
// Giải nén chỉ ký tự đầu tiên
var str = "Hello world!";
var res = str.substring(0, 1);
// ==> H
```

```javascript
// Giải nén chỉ ký tự cuối cùng
var str = "Hello world!";
var res = str.substring(11, 12);
// ==> !
```

>**```substr(start, length)```**

- Phương thức substr () trích ra các phần của một chuỗi, bắt đầu từ ký tự tại vị trí đã chỉ định và trả về số ký tự được chỉ định.
  + **start**: 
    + Cần thiết. Vị trí bắt đầu khai thác. Nhân vật đầu tiên là chỉ số 0.
    + Nếu bắt đầu là dương và lớn hơn, hoặc bằng, với chiều dài của chuỗi, substr () trả về một chuỗi rỗng.
    + 
    + 

  + **length**: Optional. The number of characters to extract. If omitted, it extracts the rest of the string
- ```replace(searchValue, replaceValue)```: thay the chuoi con voi chuoi khac;

- ```toLowerCase()```

- ```toUpperCase()```

- kiem tra do dai cua chuoi la str.lenght

```javascript
  var str = new String('Hello World');
  var str1 = "Hello World";
```

#### 5. Number trong javascript, tat ca ca kieu duoi la kieu number

```javascript
  var int = 100; //so nguyen
  var float = 100.5; //so thap phan
  var hex = 0xfff; //thap luc phan
  var exponential = 2.56e3; //so mu
  var octal = 030; //so bat phan
  var hex = new Number(0xff)
  console.log(hex.valueOf());
```

#### 4.1 Number properties 
```javascript
  // MAX_VALUE
  // MIN_VALUE
  // NEGATIVE_INFINITY: am vo cung
  // NaN
  // POSITIVE_INFINITY: duong vo cung
  Number.MAX_VALUE
```
#### 4.2 phuong thuc cua number (number method)

```javascript
  //toFixed(fractionDigits);
  //valueOf(); // lay value cua 1 object 
  //toString(); // Chuyển đổi số thành chuỗi.
  var num = 15;
  var n = num.toString();
  ==> Result n: 15
  var str1 = "abc";
  //console.log(isNaN(str1)); // tra ve true
  //isNaN() để kiểm tra dữ liệu có phải là số hay ko?
  // NaN la Not-A-Number
  // Tra ve true neu ko phai la so va tra ve false neu la so
  var str2 = 123;
  //console.log(isNaN(str2)); // tra ve false
```
#### 5. Boolean co 2 gia tri tra ve la true or false

```javascript
  var bool0 = true;
  var bool1 = new Boolean(""); // false
  var bool2 = new Boolean(0); // false
  var bool3 = new Boolean(undefined); // false
  var bool4 = new Boolean(null); // false
  var bool5 = new Boolean(NaN); // false
  var bool6 = new Boolean("Some text"); // true
  var bool7 = new Boolean(1); // true
  // boolean co cac phuong thuc 
  //toLocalString()
  //toString()
  //valueOf()
  console.log(bool0);
```

#### 6. Object in javascript(properties, method, constructor, access object keys, pass by reference, Nested object)

```javascript
var empetyObject = {}; // Object with no properties or methods
var person = {firstName: "John"}; // object with single property
// object with single method
var message = {
  showMessage: function(val){
    alert(val);
  }
};
var person = {
  firstName: "John",
  lastName: "Bond",
  age: 30,
  getFullName: function(){
    return this.firstName + ' ' + this.lastName
    // this nay la dai dien cho doi tuong va lay ra firstName, lastName
  }
};
console.log(person.getFullName());
// Co the Gan gia tri cho Object
person.firstName = "Dang Cong";
person["lastName"] = "JavaScript";
console.log(person.firstName + ' ' + person.lastName);
```

#### 6.1 Object Constructor

```javascript
  var person = new Object();
  // Them thuoc tinh va phuong thuc cho person2 object
  person.firstName = "Nam Mo Bon Su Thich Ca Mau Ni";
  person.lastName = "Phat";
  person.getFullName = function(){
    return this.firstName + ' ' + this.lastName;
  };
  console.log(person.getFullName());
```

#### 6.2 Undifined property or method

```javascript
  // kiem tra doi tuong co thuoc tinh hay ko dung phuong thuc hasOwnProperty();
  var person = new Object();
  //person.firstName; // Return undifined
  if(person.hasOwnProperty("firstName")){
    console.log("person.firstName");
  }
  else{
    console.log("Unproperties");
  }
```

#### 6.3 Access object keys: duyet qua tat ca cac phan tu cua mot object bang vong lap for in

```javascript
  for(var key in person1){
    console.log(key);
  }
```
#### 6.4 Pass by reference

```javascript
  // Truyen doi tuong tham chieu tu mot function
  function changeReference(person){
    person.firstName = "Steve";
    person.lastName = "Bill";
  }
  changeReference(person);
  console.log(person.getFullName());
```

#### 6.5 Nested Object: khi gan mot object la thuoc tinh cua object khac

```javascript
  person.address = {
    phone: "123456789",
    email: "mail@gmail.com",
    street: "68 Tran Phu"
  }
  console.log(person);
  console.log(person.address);
  console.log(person.address.street);
```

#### 7. Date trong javascript, bat buoc phai tao bang Constructor, co 3 loai No parammeter, Miliseconds, Date string.

```javascript
  var dt = new Date();
  var dt = new Date(Miliseconds);
  var dt = new Date(date string);
  var dt = new Date(year, month[, date, hour, minute, second, miliseconds]);

  var date1 = new Date();
  console.log(date1);

  var date2 = new Date(1000);
  console.log(date2);

  var date3 = new Date("7/10/2017");
  console.log(date3);

  var date4 = new Date("July, 2017, 14");
  console.log(date4);
```

#### 7.1 Date method

```javascript
  var date5 = new Date("7/14/2017");
  date5.getDay(); // return 0
  date5.getYear(); // return 115, no of year after 1900
  date5.getFullYear(); // return 2015
  date5.getMonth(); // return 3, starting 0 with jan
  date5.getUTCDate(); // returns 31
  console.log(date5.getDay());
  console.log(date5.getYear());
  console.log(date5.getFullYear());
  console.log(date5.getMonth());
  console.log(date5.getUTCDate());
```

#### 7.2 Convert Date Format

```javascript
  var date = new Date("2017-07-1410T100:13:55.5000z");
  date; // Default format
  date.toDateString();
  date.toLocaleDateString();
  date.toGMTString(); // GMT format
  //date.toISOString();
  date.toLocaleString();
  date.toLocaleTimeString();
  date.toString(); // 15:42:50
  date.toUTCString(); // UTC format
```

```javascript
toLocaleString(): Chuyển đổi đối tượng Date sang chuỗi. Theo qui ước dưới local.

var d = new Date();
var n = d.toLocaleString();

The result of n will be: 10/21/2017, 11:25:56 PM
```

#### 8. Array co 2 kieu kho tao, khoi tao kieu Literal va Constructor

#### 8.1 Array  Literal

```javascript
  var stringArray = ["one", "two", "three"];
  var numbericArray = [1, 2, 3, 4, 5];
  var decimalArray = [1.1, 1.2, 1.3, 1.4, 1.5];
  var booleanArray = [true, false, false, true];
  var mixedArray = [1, "two", "three", 4, 5];
```

#### 8.2 Array Constructor

```javascript
  var stringArray = new Array();
  stringArray[0] = "one";
  stringArray[1] = "two";
  stringArray[2] = "three";
  stringArray[3] = "four";

  var numbericArray = new Array();
  numbericArray[0] = 1;
  numbericArray[1] = 2;
  numbericArray[2] = 3;

  var mixedArray = new Array(1, "two", 3, "four");
```

#### 8.3 Truy cap den phan tu trong Array

```javascript
  var stringArray1 = new Array("one", "two", "three", "four");
  stringArray1[0]; // return "one"
  stringArray1[1]; // return "two"
  stringArray1[2]; // return "three"
  stringArray1[3]; // return "four"
```

#### 8.4 Array properties

```javascript
  var stringArray2 = new Array("one", "two", "three", "four");
  for (var i = 0; i < stringArray2.length; i++){
    stringArray2[i];
    console.log(stringArray2[i]);
  }
```
#### 8.5 Array method reference

  > **forEach()**;

  > **indexOf();** // Hàm indexOf sẽ tìm kiếm một phần tử trong mảng dựa vào giá trị của phần tử, hàm sẽ trả về vị trị( khóa) của phần tử nếu tìm thấy và trả về -1 nếu không tìm thấy. array.indexOf(item, start)

  > **join();** // Hàm join() sẽ nối các phân tử của mảng lại thành một chuỗi, hàm sẽ trả về chuỗi bao gồm các phần tử của mảng được ngăn cách bằng một kí tự nào đó được truyền vào.

  > **join( $char, $arr);** Hàm join() sẽ nối các phân tử của mảng lại thành một chuỗi, hàm sẽ trả về chuỗi bao gồm các phần tử của mảng được ngăn cách bằng một kí tự nào đó được truyền vào.

    - $char là kí tự sẽ ngăn cách các phần tử trong chuỗi mới được tạo thành.

    - $arr là mảng dữ liệu truyền vào.

    - echo join('-', $array);

  > **lastIndexOf(); // Hàm lastIndexOf sẽ tìm kiếm một phần tử trong mảng dựa vào giá trị của phần tử, hàm sẽ trả về vị trị( khóa) của phần tử nếu tìm thấy và trả về -1 nếu không tìm thấy.

  > **map();** // Hàm map() trong Javascript là một hàm dành cho đối tượng array, hàm này có công dụng tương tự như vòng lăp forEach. có lệnh return.

  > **pop();** // Hàm array.pop() có chức năng xóa bỏ phần tử cuối cùng của mảng, hàm sẽ trả về phần tử bị xóa.

  > **push();** // Hàm push() sẽ thêm mới một hoặc nhiều phần tử vào cuối mảng, hàm trả về chiều dài mảng mới.

  > **reverse();** // Hàm reverse có chức năng đúng với tên gọi của nó là đảo ngược thứ tự của các phần tử trong mảng.

#### 9. Null va Undifined

        - undefined khi chua dc gan gia tri vd var a;
        - null la gia tri dac biet va tra ve cua no kieu object, vidu var a, console.log(a) ==> null vi ko gan gia tri cho no

#### 10. Function

#### 10.1 Define a function

```javascript
  function functionName(){
    // code executed
  }
```
#### 10.2 Call function

```javascript
  functionName();
```
#### 10.3 Function paramater

```javascript
  function showMessage(firstName, lastName){
    // alert("Hello " +firstName + " " +lastName);
  }
  // showMessage("Dao", "Dang Cong");
  // showMessage("A", "B", "C"); // display Hello A B undefined
  // showMessage("Bill"); // display Hello Bill undefined
  // showMessage(); // display Hello undefined undefined
```
#### 10.4 Argument object, arguments la key word trong javascript function, ko can phai lay ten co the truy cap thong qua arguments, nos giong mang thi co the truy cap bang index.
```javascript
  function showMessageArgument(firstName, lastName){
    console.log("Hello " +arguments[0] + " " +arguments[1]);
  }
  showMessageArgument("Dang Cong", "Dao");
```
#### 10.5 Function thi co return neu can dung den no

```javascript
  function sum(a, b){
    return a+b;
  }
  console.log(sum(4,5));
```
#### 10.6 Function returning a function

```javascript
  function calculate(){
    function add(a, b){
      return a+b;
    }
    return add;
  }
  var fn = calculate();
  console.log(fn(10, 20));
```
#### 10.7 Function Expression: Javascript cho phep gan mot function cho mot bien, sau do chung ta su dung bien do nhu mot function.

```javascript
  var addNumber = function(a, b){
    return a*b;
  }
  console.log(addNumber(3,7));
```
#### 10.8 Anonymous function : ham nac danh, javascript cho phep,huu ich trong truong hop callback function

```javascript
  var showMessage = function(){
    // alert("Hello World");
  }
  showMessage();

  var sayHello = function(firstName){
    alert("Hello " +firstName);
  }
  console.log("Bill");
```
#### 10.9 Nested function: Trong javascript thi 1 function co the co nhieu function con. Nested function no co Scope, no se ton tai ben trong function thoi.

```javascript
  function showMessageNested(firstName){
    function sayHello() {
      console.log("Hello " +firstName);
    }
    return sayHello();
  }
  showMessageNested("Steve");
```

#### 11. if else condition in javascript 

  > ** if condition**
  > ** if-else condition**
  > ** else if condition**
 
```javascript
if(1 > 0){
    console.log("True");
  }
  else{
    console.log("False");
  }
```

  > ** else if: Sử dung else if khi có hai điều kiện**

```javascript 
  var mySal = 500;
  var yourSal = 1000;
  if(mySal > yourSal){
    console.log("My Salary is greater than your salary");
  }
  else if(mySal < yourSal){
    console.log("My Salary is less than your salary");
  }
  var age = prompt();
  var ageNumber = parseInt(age);
  if (ageNumber < 16) {
    console.log("You dont have permission access this page.");
  }
  else if(ageNumber < 18) {
    console.log("You have permission access this page.");
  }
```

#### 12. Switcth statement in javascript

```javascript
var a = 12;
  switch(a/3){
    case 3:
      console.log('You don\'t enough to age access this page.');
      break;
    case 4:
      console.log('You have permission access this page.');
      break;
    default:
      console.log('Welcome to this page');
      break;
  }
```

#### 13. For loop in javascript

```javascript for (initializer; condition; iteration){}```

```javascript
  for(var i = 0; i < 5; i++){
    console.log(i);
  }
```

#### 13.1 for loop to access array

```javascript
var arr = [10, 11, 12, 13, 14];
  for(var i = 0; i < 5; i++){
    console.log(arr[i]);
  }
  var sum = 0;
  for(var i = 0; i < 5; i++){
    sum += i;
  }
  console.log('Sum: '+sum);
```

#### 14. While loop

##### 14.1 While loop: kiểm tra ngay lúc đầu
```javascript
var i = 0;
while(i < 10){
  console.log('while: '+i);
  i++;
}
```

##### 14.2 Do While loop: Nó lặp rồi mới kiểm tra điều kiện

```javascript
var i1 = 10;
do{
  console.log('Do white : ' + i1);
  i1--;
}while(i1>1);
```

#### 15. Scope in javascript: phamj vi bien trong javascript, no dinh nghia ra kha nang truy cap cua bien, object or function trong javascript

##### 15.1 Global scope: truy cap moi trong noi bat cu function nao. neu khai bao mot bien ko co tu khoa var thi no cung la global.

```javascript
var userName = "Dao";
function modifyUserName(){
  userName = "Steve";
  console.log(userName);
};
function showUserName(){
  console.log(userName);
};
modifyUserName();
showUserName()
```

#### 15.2 No block level scope

```javascript
if(userName){
  var aa = 1;
  console.log(aa);
}
console.log(aa);
for(var i = 0; i< 10; i++){
  console.log(i);
}
console.log(i);
```

#### 16 Eval function: lay ket qua cua 1 string trong js, khuyen cao ko nen dung ham nay

```javascript
var result;
function Sum(a, b){
  return a+b;
}
eval('result = Sum(10, 12)');
console.log(eval('result = Sum(10, 12)'));
var strEf = {'firstName': 'Dao', 'lastName': 'Dang Cong'};
eval(strEf);
console.log(strEf.firstName);
```

#### 16. Try Catch trong JS: Xw ly loi 

```javascript
try{
    // code that may throw an error: Neu co loi thi se nem ra loi
    // bao quanh vung loi kha nghi
    throw "Error occurred"; // la tu khoa de nem ra loi 
}
catch(ex){
  // code to be excuted if an error occurs: Se bat loi day, ex co th la tham so, no co the nem vao tham so expression nay, trong catch nay co the viet code de xu ly loi do.
  // trong try no nem ra cai ji thi catch bat cai day
}
finally{
  // code to be executed regardless of an error occurs or not : no se luon luon chay de xu ly, vd nhu khoi tao bien, huy bien ...
  }
```

```javascript
try{
  var a = 10;
  var b = 10;
  var result = a/b;
}
catch(ex){
  alert(ex);
}
finally{
  console.log('Finally block executed.');
}
```

```javascript
try{
  var b = 0;
  var result = a/b;
  throw "Error when divi a/b"
}
catch(ex){
  console.log(ex);
}
  finally{
    console.log('Finally block executed.');
  }
```

```javascript
try{
  var a = 10;
  var b = 0;
  var result = a/b;
  throw {
    code: 101,
    message: "Error division"
  };
}
catch(ex){
  console.log(ex.message);
}
 finally{
  console.log('Finally block executed.');
}
```

```javascript
try{
  var a = 10;
  var b = 0;
  var result = a/b;
  throw {
    code: 101,
    message: "Error division"
  };
}
catch(ex){
  document.getElementById('errorMessage').innerHTML = ex.message;
}
finally{
  console.log('Finally block executed.');
}
```
#### 17. Strict mode: tinh nang nay co bat dau o ECMAScript 5, viet js o che do kiem tra chu phap chuan hon. Strict mode cho phep them vao 1 chuoi: ```"use strict"```

>**vi tri duoc bat dau o dong dau tien cua the script**

>**strict mode o muc function**

```javascript
function foo(){
    "use strict";
    // this function is executed in strict mode
  }
  function foo(){
    // this function is executed in no-strict mode
  }
```

> **statement: cau lenh**

- browser support: IE10 tro len, Firefox 4 tro len, Chrome 13 tro len, Safari 5.1 tro len, Opera 12 tro len.
- Strict mode tong quan cua no ko cho phep ban lam nhung dieu sau day:
- Ko cho phep su dung bien chua duoc dinh nghia, phai co tu khoa var
- Khong dc dat teb bien va function bang tu khoa cua javascript
- Ko dat 2 thuoc tinh cung nhau cua 1 object
- Ko dc truyen 2 tham so cung ten nhau
- Gan thuoc tinh read-only cho mot doi tuong
- Thay doi do tuong thuoc tinh argument trong object
- Khong duoc sinh nghia theo co so 8
- Khong duoc su dung cau lenh with
- ham eval(): ko dc phep tao bien

```javascript
"use strict";
function foo(){
  var x, y;
  x = 1;
  y = 2;
  z = x+y;
  console.log(z);
}
```

```javascript
function foo(){
  "use strict";
  var x, y;
  x = 1;
  y = 2;
  z = x+y;
  console.log(z);
}
foo();
```
#### 18. Hosting: la  khái niệm trong js, no ko phai la tinh nang. Trong js biên or function co the dc su dung truoc khi khai bao ma ko can phai doi den luc khai bao. Su dung truoc roi khai bao sau, js trinh bien dich cua nó se chuyen cai khai bao len truoc viec su dung và ko xay ra loi gì, từ động làm dc viec ấy gọi là Hosting.

#### 18.1 Hosting Variable: 

```javascript
x = 1;
  console.log('x =' + x); // display x = 1
  var x;
```
>** Hosting chi co tac dung voi khai bao thoi con viec khoi tao thi no se ko move**

```javascript
  console.log('y =' + y); // display y = undefined
  var y = 1;
```

#### 18.2 Hosting Function: Cunng tuong tu nhu vay co the dung function truoc roi khai bao ben duoi

```javascript
console.log(sumVal(5, 5));

function sumVal(val1, val2) {
  return val1 + val2;
}
```


#### 19. Class in javascript: 

- ECMAScript 5 chua ho tro viet class, tat ca cac class, object nhu chung ta tao function. Trong ECMAScript 6 thi dc.
#### 19.1 Class in js va add method getFullName() trong Class

```javascript
function ClassPerson() {
    this.firstName = "Unknown";
    this.lastName = "Unknown";
    this.getFullName = function() {
      return this.firstName + ' ' + this.lastName;
    }
  }

  var ClassPerson1 = new ClassPerson();
  ClassPerson1.firstName = "Nguyen";
  ClassPerson1.lastName = "Van A";

  console.log('Method : ' + ClassPerson1.getFullName());
  console.log('Class 1 : ' + ClassPerson1.firstName + ' ' + ClassPerson1.lastName);

  var ClassPerson2 = new ClassPerson();
  ClassPerson2.firstName = "Nguyen";
  ClassPerson2.lastName = "Van B";
  console.log('Class 2 : ' + ClassPerson2.firstName + ' ' + ClassPerson2.lastName);
```

#### 19.2 Constructor trong lap trinh huong doi tuong thi Class co the co 1 or  nhieu Constructor

```javascript
function ClassPersonConstructor(_firstName, _lastName, _age) {
    this.firstName = _firstName;
    this.lastName = _lastName;
    this.age = _age;
    this.getFullName = function() {
      return this.firstName + ' ' + this.lastName;
    }
  }
  var ClassPersonConstructor1 = new ClassPersonConstructor("Nguyen", "Van Nam", 30);
  var ClassPersonConstructor2 = new ClassPersonConstructor("Nguyen", "Van Phat", 30);
  console.log(ClassPersonConstructor1.getFullName());
  console.log(ClassPersonConstructor2.firstName + ' ' + ClassPersonConstructor2.lastName);
```

#### 19.3 Properties with getters and setters, phuong thuc Object.defineProperty()

- Trong phuong thuc Object.defineProperty() co 2 tham so
- Thu nhat tu khoa this, tu this dai dien cho doi tuong cua Class
- Thu 2 la 1 Object chua danh sach thuoc tinh, co 2 phuong thuc set va get.

```javascript
function Student() {
    var _firstName = "Unknown";

    Object.defineProperties(this, {
      "FirstName": {
        set: function(value) {
          _firstName = value;
        },
        get: function() {
          return _firstName;
        }
      },
      "LasttName": {
        set: function(value) {
          _lastName = value;
        },
        get: function() {
          return _lastName;
        }
      }
    });
  }
  var student1 = new Student();
  student1.FirstName = "Bat Nha";
  student1.LastName = "Kinh";
  console.log(student1.FirstName);
  console.log(student1.LastName);
```

- Neu comment set thi no se tra ve gia tri mac dinh. Do la Read-Only properties no chi co GET chi Ko co Set.

#### 20. Tim hieu sau ve Object trong JS

#### 20.1 De nhan tat ca cac thuoc tinh, ten thuoc tinh thi chung ta su dung phuong thuc Object.keys()

> **Cach 1:**

```javascript
function Bloke() {
  this.firstName = "Dao",
    this.lastName = "Dang Cong",
    this.age = 31
}
var bloke1 = new Bloke();
bloke1.firstName = "Hello";
bloke1.lastName = "World";
console.log(Object.keys(bloke1));
```

> **Cach 2:**

```javascript
for (var prop in bloke1) {
  console.log(prop);
}
```

#### 20.2 Property Descriptor 

- Moi 1 thuoc tinh trong Object theo co 1 doi tuong descriptor de mieu ta meta, data cua thuoc tinh day, thuoc tinh la su dung phuong thuc Object.getOwnPropertyDescriptor(), phuong thuc nay tra ve mot doi tuong discriptor, phuong thuc nay dc dinh nghia thong qua prototype.

```javascriptconsole.log(Object.getOwnPropertyDescriptor(bloke1, "firstName"));```

- value: Chua gia tri thuoc tinh
- writeable: Chi ra thuoc tinh co phai read only ko? neu true thi gia tri co the thay doi duoc, false thi la thuoc tinh read-only tcc la ko co set ma chi co get thoi.
- enumerable: khi dung phuong thuc Object.keys() or for each de list ra danh sach properties, neu la false thi ko the doc dc Object.keys() neu true thi doc dc.
- configurable: khi no true thi 4 thuoc tinh deu co the thay doi trong phuong thuc ObjectdefineProperty().

#### 21. Tu khoa this: chon den doi tuong cu the trong js, no phu thuoc vao noi ma tu khoa this nay dc chon.
     
> **Rules This:**

- Global Scope
- Object's Method
- call() or apply method
- bind() method

#### 21.1 Global Scope 

```javascript
var myVar = 100;

function WhoIsThis() {
  var myVar = 200;
  console.log(myVar); // 200
  console.log(this.myVar); // 100
}
```

- Neu bien khai bao global, khi dung this.variable thi no se tro den doi tuong  window.
- Trong strict mode thi no yeu cau bao mat nen ko tro den doi tuong window
WhoIsThis();

#### 21.2 This inside object's method

```javascript
var myVar1 = 100;
function WhoIsThis1() {
  this.myVar1 = 200;
}
WhoIsThis1();
var objVar1 = new WhoIsThis1();
var objVar2 = new WhoIsThis1();
objVar2.myVar1 = 300;
console.log(objVar1.myVar1); // 200
console.log(objVar2.myVar1); // 300
```

- khi go this trong console chrome thi no se ra dc doi tuong window.

#### 21.3 Call and Apply

- Khi goi function trong javascript thi cos 3 cach goi.
- Goi Call va Aplly thuong thi set tu khoa this trong function, phu thuoc vao doi tuong nao.

```javascript
var myVariabale = 1000;

function CallBackFunction() {
  console.log(this.myVariabale);
}
var objCallBack1 = { myVariabale: 2000, callBackFunction: CallBackFunction };
var objCallBack2 = { myVariabale: 3000, callBackFunction: CallBackFunction };
CallBackFunction(); // 'this' se tro den doi tuong window
CallBackFunction.call(objCallBack1); // 'this' se tro den objCallBack1
CallBackFunction.apply(objCallBack2); // 'this' se tro den objCallBack2
objCallBack1.callBackFunction.call(window); // 'this' se tro den doi tuong window
```

#### 21.4 Bind 

- Duoc su dung trong ECMAScript 5, duoc dung de set ngu canh cho tu khoa 'this', co tac dung set 'this' cho ham callback.
- someFunction() la function chua function callback()

```javascript
var myBind = 100;

function someFunction(callback) {
  var myBind = 200;
  callback();
}
var objectBind = {
  myBind: 300,
  WhoIsThis3: function() {
    console.log("'this' points to" + this + ", myBind = " + this.myBind);
  }
};
someFunction(objectBind.WhoIsThis3);
someFunction(objectBind.WhoIsThis3.bind(objectBind));
```

#### 22. Tu khoa new trong qua trinh khoi tao object, co 1 ham ten la myFunc ham nay co tu khoa 'this', bien property bind den x = 100. Va khoi tao doi tuong object 1 bang tu khoa new 

- Bat cu fnction nao deu co thuoc tinh chung cua no la prototype

```javascript
function myFunction() {
    this.x = 100;
  }
  var object1 = new myFunction();
  object1.x;
  myFunction.prototype.y = 200; // function myFunction duoc bo xung gia tri la 20
  console.log(object1.x);
  console.log(object1.y);
```

#### 23. Prototype: la doi tuong lien ket ca function voi object. prototype cua function thi co the dc truy cap va chinh sua dc 

```javascript
function Person() {
    this.name = "Javascript";
    this.gender = "Hello"
  }
  Person.prototype.age = 15;
  var object5 = new Person();
  console.log(object5.age); // 15
  var object7 = new Person();
  console.log(object7.age); // 15
```

    - no share chung het ne ket qua la 15

#### 23.1 Object prototype su dung phuong thuc Object.getPrototypeOf(stuObjOne)

```javascript
function StudentProto() {
    this.name = 'John';
    this.gender = 'M';
  }
  var stuObj = new StudentProto();
  Student.prototype.sayHi = function() {
    console.log('John');
  };
  var stuObjOne = new StudentProto();
  var proto = Object.getPrototypeOf(stuObjOne); // Return student's prototype object
  console.log(proto.constructor); // Returns Student function
```

> ** Object prototype: bao gom cac thuoc tinh, phuong thuc duoi day**

- Property:

  + constructor: Return a function
  + _proto: Return a prototype object

- Method:

  + hasOwnproperty() : The hasOwnProperty() method returns a boolean indicating whether the object has the specified property as own (not inherited) property.
  + isPrototypeOf(): The isPrototypeOf() method checks if an object exists in another object's prototype chain.
  + propertyIsEnumerable(): The propertyIsEnumerable() method returns a Boolean indicating whether the specified property is enumerable.
  + toLocaleString(): The toLocaleString() method returns a string representing the object. This method is meant to be overridden by derived objects for locale-specific purposes.
  + toString(): The toString() method returns a string representing the object.
  + valueOf: The valueOf() method returns the primitive value of the specified object.

#### 24. Kế thừa(Inheritance in javascript)

- Có thể tái sử dụng lại code từ class cha, function cha sử dụng trong function con ma ko can khai bao lai.
- Ke thua duoc ho tro boi prototype object.

#### 24.1 Inheritance in js

```javascript
function Person (firstName, lastName){
  this.FirstName = firstName || "Unknown";
  this.LastName = lastName || "Unknown";
};
Person.prototype.getFullName = function(){
  return this.FirstName + " " + this.LastName;
}
function Student(firstName, lastName, schoolName, grade){
  Person.call(this, firstName, lastName);
   this.schoolName = schoolName || "Unknown";
   this.Grade = grade || 0;
}
```

- Student.prototype = Person.prototype;
- Day moi la trong tam, chung ta gan prototype cua Person vao prototype cua Student. Tuong duong voi cach ma new 1 doi tuong Person va gan vao prototype cua Student day chinh la cach ma de chung ta ke thua.

```javascript
Student.prototype = new Person();
// Van dam bao constructor cua Student la chinh no
Student.prototype.constructor = Student;
// khai bao doi tuong cua student voi first name, last name
var std = new Student("James", "Bond", "XYZ", 10);
// Su dung dc method getFullName cua Person.
console.log(std.getFullName()); //  James Bond
// std la con cua 2 object Student va Person
console.log(std instanceof Student); //  true
console.log(std instanceof Person); //  true
```

#### 25. Closure in javascript: Nghia la mot function con co the viet long ben trong function cha, va function con nay co the truy cap dc vao bien va phuong thuc cua function cha, ngay ca khi no dc goi, sau cau lenh return.

>**Case 1:**

```javascript
function OuterFunction(){
  var outerVariable = 1;
  function InnerFunction(){
    console.log(outerVariable);
  }
  return InnerFunction();
}
OuterFunction();
```
>**Case 2:**

#### 10.9 

```javascript
var outerVariable = 100;
function OuterFunction(){
  function InnerFunction(){
    console.log(outerVariable);
    outerVariable++;
  }
  return InnerFunction();
}
OuterFunction();
OuterFunction();
OuterFunction();
```

>**TIPS:**

- Bien ben ngoai co the giu duoc trang thai thong qua nhieu lan goi
- inner function no reference den bien outer, gia tri cua no dc thay doi khi ham con cua no dc thay doi.
- Mot function co the tra ve function khac, function duoc gan bien goi la function expression.

```javascript
function Counter(){
  var counter = 0;
  function IncreaseCounter(){
    return counter += 1;
  };
  return IncreaseCounter;
}
var counter = Counter();
console.log(counter()); // 1
console.log(counter()); // 2
console.log(counter()); // 3
console.log(counter()); // 4
```

#### 25.1 when to use closure: tinh dong goi linh hoat.

```javascript
var counter =  (function(){
  var privateCounter = 0;
  function changeBy(val){
    privateCounter += val;
  }
  return {
    increment: function(){
      changeBy(1);
    },
    decrement: function(){
      changeBy(-1);
    },
    value: function(){
      return privateCounter;
    }
  };
})();
console.log(counter.value()); // 0
counter.increment();
counter.increment();
console.log(counter.value()); // 2
counter.decrement();
console.log(counter.value()); // 1
counter.value();
```

#### 26. Immerdiataly Invoked, function expression - IIFE, IIFE la bieu thuc goi ham truc tiep.

- Immerdiataly Invoked Function Expression: IIFE.
>**Rule:**

```javascript
var myIIFE = function() {
  // write your js code here
};
//==> Boc () toan bo function
(function(){
  // write your js code here
});
// ==> Them 1 cap ngoac don sau function, Day la bieu thuc IIFE, ham nay sau khi khai bao se chay luon chu ko phai doi call nua.
(function(){
  // write your js code here
})();
```

>**Case 1: myScript1.js**

```javascript
var userName = "Bill";
function display(name){
  console.log("myScript1: "+ name);
}
display(userName);
```

>**Case 2: myScript2.js**

```javascript
var userName = "Steve";
function display(name){
  console.log("myScript2: "+ name);
}
display(userName);
```

- Neu de 2 function tren chay thi usename luon bi ghi de va myScript1 se chay sai va ko chay de giai quyet truong hop nay
- Solution: de gia quyet van de nay ko phai bi xung dot thi.

```javascript
(function (){
  var userName = "A Dai";
  function display(name){
    console.log("myScript1: "+ name);
  }
  display(userName);
})();
```

>**Co the truyen doi so tu ben ngoai thong qua bieu thuc IIFE**

```javascript
var userName  = "Hello";
(function(name){
  function display(name){
    console.log("myScript2: "+ name);
  }
  display(name);
})(userName);
```
#### Phan biet 2 truong hop

>**Case 1: Khi call funtion no moi chay**

```javascript
function callIIFE(name){
  console.log(name);
}
callIIFE();
```

>**Case 2: chay truc tiep luon, mo len la da chay roi**

```javascript
var userName = "Sleep";
(function(name){
  console.log(name);
})(userName);
```

- Co tac dung trong u an thuc te
  + Ko tao bien global va function global khong can thiet
  + Function va cac bien duoc dinh nghia trong IIFE ko bi confilict voi function & Variable  cung ten o noi khac.
  + To chuc code javascript tot hon
  + Lam cho javascript cua ban co the de dang maintainable hon.

#### 27. Json

1. ```parse()```: Accepts a JSON object in text string form as a parameter, and returns the corresponding object.

```javascript
var text = '{"employees":[' +
'{"firstName":"John","lastName":"Doe" },' +
'{"firstName":"Anna","lastName":"Smith" },' +
'{"firstName":"Peter","lastName":"Jones" }]}';

obj = JSON.parse(text);
document.getElementById("demo").innerHTML =
obj.employees[1].firstName + " " + obj.employees[1].lastName;
```

2, ```stringify()```: Accepts a JSON object as a parameter, and returns the equivalent text string form.
