## Study-strict-mode

```javascript
// window.alert("Hello");
  /*var result = confirm('Are you sure to delete this record?');
  if(result== true){
    alert("User Accepted");
  }
  else{
    alert("User Reject");
  }*/
  /*var input = prompt("Please tell me your name?", "No name");
  alert(input);*/
  // 2. Variable
  var one = 1;
  var two = 'two';
  var three;
  four = 4; // Neu ko co tu khoa var thi no se hieu la global.
  // OR
  var one = 1, two = 'two', three;
  //document.write(two);
  // 3. Javascript Operators: toan tu(+, -,*,/,%,++,--), A + B, A, B la toan hang, + la toan tu, bieu thuc 
  // Toan tu so sanh ==(So sanh gia trị với 2 toan hang), ===(So sanh ca gia trị và kieu với 2 toan hang), !=, >, <, >=, <=
  // Toan tu logic: &&, ||, !
  // Toan tu gan(Assignment operators): =, +=, -=,/=,%=
  // Toan tu 3 ngoi(Ternary operator)
  /*var a1 = a==b?1:0;
  if(a==b)
    a1 = 1;
  else
    a1 = 0;*/
  // Kieu du lieu(Data type): String, Number, Boolean, Null(Ko co gia tri) ==> kieu object, Undefined(ko xac dinh)==> kieu underfined
  // 4. String Object tra ve string dang object
  // indexOf(SearchString, Position): search vi tri 1 chuoi o trong 1 chuoi khac; lastIndexOf(SearchString, Position): lay vi tri cuoi cung cua chuoi con trong chuoi khac; replace(searchValue, replaceValue): thay the chuoi con voi chuoi khac; substr(start, length): cat chuoi; toLowerCase(); toUpperCase()
  // kiem tra do dai cua chuoi la str.lenght
  var str = new String('Hello World');
  var str1 = "Hello World";
  // 5. Number trong javascript, tat ca ca kieu duoi la kieu number
  var int = 100; //so nguyen
  var float = 100.5; //so thap phan
  var hex = 0xfff; //thap luc phan
  var exponential = 2.56e3; //so mu
  var octal = 030; //so bat phan
  var hex = new Number(0xff)
  console.log(hex.valueOf());

  //4.1 Number properties 
  // MAX_VALUE
  // MIN_VALUE
  // NEGATIVE_INFINITY: am vo cung
  // NaN
  // POSITIVE_INFINITY: duong vo cung
  Number.MAX_VALUE
  // 4.2 phuong thuc cua number (number method)
  //toFixed(fractionDigits);
  //valueOf(); // lay value cua 1 object 
  //toString();
  var str1 = "abc";
  //console.log(isNaN(str1)); // tra ve true
  //isNaN() để kiểm tra dữ liệu có phải là số hay ko?
  // NaN la Not-A-Number
  // Tra ve true neu ko phai la so va tra ve false neu la so
  var str2 = 123;
  //console.log(isNaN(str2)); // tra ve false
  // 5. Boolean co 2 gia tri tra ve la true or false
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
  // 6. Object in javascript(properties, method, constructor, access object keys, pass by reference, Nested object)
  var empetyObject = {}; // Object with no properties or methods
  var person = {firstName: "John"}; // object with single property
  // object with single method
  var message = {
    showMessage: function(val){
      alert(val);
    }
  };
  var person1 = {
    firstName: "John",
    lastName: "Bond",
    age: 30,
    getFullName: function(){
      return this.firstName + ' ' + this.lastName
      // this nay la dai dien cho doi tuong va lay ra firstName, lastName
    }
  };
  console.log(person1.getFullName());
  // Co the Gan gia tri cho Object
  person1.firstName = "Dang Cong";
  person1["lastName"] = "JavaScript";
  console.log(person1.firstName + ' ' + person1.lastName);
  // 6.1 Object Constructor
  var person2 = new Object();
  // Them thuoc tinh va phuong thuc cho person2 object
  person2.firstName = "Nam Mo Bon Su Thich Ca Mau Ni";
  person2.lastName = "Phat";
  person2.getFullName = function(){
    return this.firstName + ' ' + this.lastName;
  };
  console.log(person2.getFullName());
  // 6.2 Undifined property or method
  // kiem tra doi tuong co thuoc tinh hay ko dung phuong thuc hasOwnProperty();
  var person3 = new Object();
  //person3.firstName; // Return undifined
  if(person3.hasOwnProperty("firstName")){
    console.log("person3.firstName");
  }
  else{
    console.log("Unproperties");
  }
  // 6.3 Access object keys: duyet qua tat ca cac phan tu cua mot oobjact bang vong lap for in
  for(var key in person1){
    console.log(key);
  }
  // 6.4 Pass by reference
  // Truyen doi tuong tham chieu tu mot function
  function changeReference(person1){
    person1.firstName = "Steve";
    person1.lastName = "Bill";
  }
  changeReference(person1);
  console.log(person1.getFullName());
  // 6.5 Nested Object: khi gan mot object la thuoc tinh cua object khac
  person1.address = {
    phone: "123456789",
    email: "mail@gmail.com",
    street: "68 Tran Phu"
  }
  console.log(person1);
  console.log(person1.address);
  console.log(person1.address.street);
  // 7 Date trong javascript, bat buoc phai tao bang Constructor, co 3 loai No parammeter, Miliseconds, Date string.
  // var dt = new Date();
  // var dt = new Date(Miliseconds);
  // var dt = new Date(date string);
  // var dt = new Date(year, month[, date, hour, minute, second, miliseconds]);

  var date1 = new Date();
  console.log(date1);

  var date2 = new Date(1000);
  console.log(date2);

  var date3 = new Date("7/10/2017");
  console.log(date3);

  var date4 = new Date("July, 2017, 14");
  console.log(date4);
  // 7.1 Date method
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

  // 7.2 Convert Date Format
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

  // 8. Array co 2 kieu kho tao, khoi tao kieu Literal va Constructor

  // 8.1 Array  Literal
  var stringArray = ["one", "two", "three"];
  var numbericArray = [1, 2, 3, 4, 5];
  var decimalArray = [1.1, 1.2, 1.3, 1.4, 1.5];
  var booleanArray = [true, false, false, true];
  var mixedArray = [1, "two", "three", 4, 5];

  // 8.2 Array Constructor
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

  // 8.3 Truy cap den phan tu trong Array
  var stringArray1 = new Array("one", "two", "three", "four");
  stringArray1[0]; // return "one"
  stringArray1[1]; // return "two"
  stringArray1[2]; // return "three"
  stringArray1[3]; // return "four"
  // 8.4 Array properties
  var stringArray2 = new Array("one", "two", "three", "four");
  for (var i = 0; i < stringArray2.length; i++){
    stringArray2[i];
    console.log(stringArray2[i]);
  }

  // 8.5 Array method reference

  //forEach();
  //indexOf(); // Hàm indexOf sẽ tìm kiếm một phần tử trong mảng dựa vào giá trị của phần tử, hàm sẽ trả về vị trị( khóa) của phần tử nếu tìm thấy và trả về -1 nếu không tìm thấy. array.indexOf(item, start)
  //join(); // Hàm join() sẽ nối các phân tử của mảng lại thành một chuỗi, hàm sẽ trả về chuỗi bao gồm các phần tử của mảng được ngăn cách bằng một kí tự nào đó được truyền vào.
  // join( $char, $arr); Hàm join() sẽ nối các phân tử của mảng lại thành một chuỗi, hàm sẽ trả về chuỗi bao gồm các phần tử của mảng được ngăn cách bằng một kí tự nào đó được truyền vào.
  // $char là kí tự sẽ ngăn cách các phần tử trong chuỗi mới được tạo thành.
  // $arr là mảng dữ liệu truyền vào.
  // echo join('-', $array);
  //lastIndexOf(); // Hàm lastIndexOf sẽ tìm kiếm một phần tử trong mảng dựa vào giá trị của phần tử, hàm sẽ trả về vị trị( khóa) của phần tử nếu tìm thấy và trả về -1 nếu không tìm thấy.
  //map(); // Hàm map() trong Javascript là một hàm dành cho đối tượng array, hàm này có công dụng tương tự như vòng lăp forEach. có lệnh return.
  //pop(); // Hàm array.pop() có chức năng xóa bỏ phần tử cuối cùng của mảng, hàm sẽ trả về phần tử bị xóa.
  //push(); // Hàm push() sẽ thêm mới một hoặc nhiều phần tử vào cuối mảng, hàm trả về chiều dài mảng mới.
  //reverse(); // Hàm reverse có chức năng đúng với tên gọi của nó là đảo ngược thứ tự của các phần tử trong mảng.
  // 9. Null va Undifined
  //undefined khi chua dc gan gia tri vd var a;
  //null la gia tri dac biet va tra ve cua no kieu object, vidu var a, console.log(a) ==> null vi ko gan gia tri cho no
  // 10. Function
  // 10.1 Define a function
  function functionName(){
    // code executed
  }
  // 10.2 Call function
  functionName();
  // 10.3 Function paramater
  function showMessage(firstName, lastName){
    // alert("Hello " +firstName + " " +lastName);
  }
  // showMessage("Dao", "Dang Cong");
  // showMessage("A", "B", "C"); // display Hello A B undefined
  // showMessage("Bill"); // display Hello Bill undefined
  // showMessage(); // display Hello undefined undefined
  // 10.4 Argument object, arguments la key word trong javascript function, ko can phai lay ten co the truy cap thong qua arguments, nos giong mang thi co the truy cap bang index.
  function showMessageArgument(firstName, lastName){
    console.log("Hello " +arguments[0] + " " +arguments[1]);
  }
  showMessageArgument("Dang Cong", "Dao");
  // 10.5 Function thi co return neu can dung den no
  function sum(a, b){
    return a+b;
  }
  console.log(sum(4,5));
  // 10.6 Function returning a function
  function calculate(){
    function add(a, b){
      return a+b;
    }
    return add;
  }
  var fn = calculate();
  console.log(fn(10, 20));
  // 10.7 Function Expression: Javascript cho phep gan mot function cho mot bien, sau do chung ta su dung bien do nhu mot function.
  var addNumber = function(a, b){
    return a*b;
  }
  console.log(addNumber(3,7));
  // 10.8 Anonymous function : ham nac danh, javascript cho phep,huu ich trong truong hop callback function
  var showMessage = function(){
    // alert("Hello World");
  }
  showMessage();

  var sayHello = function(firstName){
    alert("Hello " +firstName);
  }
  console.log("Bill");
  // 10.9 Nested function: Trong javascript thi 1 function co the co nhieu function con. Nested function no co Scope, no se ton tai ben trong function thoi.
  function showMessageNested(firstName){
    function sayHello() {
      console.log("Hello " +firstName);
    }
    return sayHello();
  }
  showMessageNested("Steve");
  // 11. if else condition in javascript
  // if condition
  // if-else condition
  // else if condition
  if(1 > 0){
    console.log("True");
  }
  else{
    console.log("False");
  }
  // else if: Sử dung else if khi có hai điều kiện
  /*var mySal = 500;
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
  }*/
  // 12 Switcth statement in javascript
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
  // 13. For loop in javascript
  /*for (initializer; condition; iteration){

  }*/
  for(var i = 0; i < 5; i++){
    console.log(i);
  }
  // 13.1 for loop to access array
  var arr = [10, 11, 12, 13, 14];
  for(var i = 0; i < 5; i++){
    console.log(arr[i]);
  }
  var sum = 0;
  for(var i = 0; i < 5; i++){
    sum += i;
  }
  console.log('Sum: '+sum);
  // 14. While loop
  // 14.1 While loop: kiểm tra ngay lúc đầu
  var i = 0;
  while(i < 10){
    console.log('while: '+i);
    i++;
  }
  // 14.2 Do While loop: Nó lặp rồi mới kiểm tra điều kiện
  var i1 = 10;
  do{
    console.log('Do white : ' + i1);
    i1--;
  }while(i1>1);
  // 15. Scope in javascript: phamj vi bien trong javascript, no dinh nghia ra kha nang truy cap cua bien, object or function trong javascript
  // 15.1 Global scope: truy cap moi trong noi bat cu function nao. neu khai bao mot bien ko co tu khoa var thi no cung la global.
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
  // 15.2 No block level scope
  if(userName){
    var aa = 1;
    console.log(aa);
  }
  console.log(aa);
  for(var i = 0; i< 10; i++){
    console.log(i);
  }
  console.log(i);
  // 16 Eval function: lay ket qua cua 1 string trong js, khuyen cao ko nen dung ham nay
  var result;
  function Sum(a, b){
    return a+b;
  }
  eval('result = Sum(10, 12)');
  console.log(eval('result = Sum(10, 12)'));
  var strEf = {'firstName': 'Dao', 'lastName': 'Dang Cong'};
  eval(strEf);
  console.log(strEf.firstName);
  // 17. Try Catch trong JS: Xw ly loi
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

  /*try{
    var a = 10;
    var b = 10;
    var result = a/b;
  }
  catch(ex){
    alert(ex);
  }
  finally{
    console.log('Finally block executed.');
  }*/
  /*try{
    var b = 0;
    var result = a/b;
    throw "Error when divi a/b"
  }
  catch(ex){
    console.log(ex);
  }
  finally{
    console.log('Finally block executed.');
  }*/
  /*try{
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
  }*/
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
  // 17. Strict mode: tinh nang nay co bat dau o ECMAScript 5, viet js o che do kiem tra chu phap chuan hon. Strict mode cho phep them vao 1 chuoi: "use strict";
  // vi tri duoc bat dau o dong dau tien cua the script
  // strict mode o muc function
  function foo(){
    "use strict";
    // this function is executed in strict mode
  }
  function foo(){
    // this function is executed in no-strict mode
  }
  // statement: cau lenh
  // browser support: IE10 tro len, Firefox 4 tro len, Chrome 13 tro len, Safari 5.1 tro len, Opera 12 tro len.
  // Strict mode tong quan cua no ko cho phep ban lam nhung dieu sau day:
  // - Ko cho phep su dung bien chua duoc dinh nghia, phai co tu khoa var
  // - Khong dc dat teb bien va function bang tu khoa cua javascript
  // - Ko dat 2 thuoc tinh cung nhau cua 1 object
  // - Ko dc truyen 2 tham so cung ten nhau
  // - Gan thuoc tinh read-only cho mot doi tuong
  // - Thay doi do tuong thuoc tinh argument trong object
  // - Khong duoc sinh nghia theo co so 8
  // - Khong duoc su dung cau lenh with
  // - ham eval(): ko dc phep tao bien
  // - 
  ```
