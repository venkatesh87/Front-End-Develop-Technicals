**Reference:** https://developer.mozilla.org/vi/docs/Web/JavaScript/Reference/Classes

- Class trong javascript được giới thiệu trong ECMAScript 2015 chủ yếu là các cú pháp cải tiến, thừa kế và dựa trên nền tảng có sẵn có trong Javascript. Cú pháp trong class không giới thiệu về một mô hình thừa kế hướng đối tượng mới cho Javascript (nghĩa là cải tiến những cái có sẵn chứ không phải là đột phá tạo ra một mô hình mới).
- Các ```class``` trong Javascript cung cấp cú pháp đơn giản và rõ ràng rành mạch hơn rất nhiều để tạo object và đối ứng với tính chất thừa kế, cái vốn có trong các ngôn ngữ hướng đối tượng.

#### Định nghĩa class
- Thực tế các class giống như một một "function đặc biệt", và cũng giống như bạn có thể định nghĩa hàm biểu thức (function expressions)  và khai báo hàm (function declarations), cú pháp class có hai thành phần: biểu thức class (class expressions) và khai báo lớp (class declarations).

##### Class declarations
- Một cách để định nghĩa class là sử dụng ```class declaration```. Để khai báo một class, bạn sử dụng từ khóa class  với tên của ```class``` đằng sau. Ví dụ như ("Rectangle" như dưới đây).

```javascript
class Rectangle {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
}
```

##### Hoisting (khái niệm cơ bản khi học javascript)
- Một sự khác biệt quan trọng giữa khai báo hàm khai báo class mà các bạn cần chú ý đó là khai báo function thì hoisted, và khai báo class thì không. Bạn cần khai báo class của bạn trước tiên sau đó mới có thể gọi và sử dụng nó, ngược lại nếu viết code giống như phía dưới đây thì sẽ xảy ra lỗi ```ReferenceError```:

```javascript
var p = new Rectangle(); // ReferenceError

class Rectangle {}
```

##### Class expressions
- Một biểu thức class là một cách khác để khai báo một class. Biểu thức class có thể có tên hoặc không tên. Tên được đặt cho biểu thức lớp là tên đại diện cho phần thân của class @@ (hiểu mà khó dịch quá). Xem code bạn sẽ hiểu rõ hơn

```javascript
// không tên
var Rectangle = class {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
};

// đặt tên
var Rectangle = class Rectangle {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
};
```
- **Chú ý:** Các biểu thức lớp cũng sẽ có tồn tại vấn đề hoisting bên trong nó (như đã đề cập ở trên).

#### Phần thân class và định nghĩa phương thức

##### Strict mode
- Các phần tử khai báo trong class declarations và class expressions đã được thực hiện ở chế độ strict mode như constructor, static tương tự đối với prototype methods, setter, getter functions. (Nếu bạn chưa hiểu chế độ strict mode thì hãy tìm hiểu thêm [tại đây](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode)).

##### Constructor (hàm khởi tạo)
- Hàm khởi tạo (constructor) là một hàm đặc biệt, nhiệm vụ của nó là khởi tạo một đối tượng cho một class. Trong một class chỉ có thể tồn tại duy nhất một hàm khởi tạo, nghĩa là bạn chỉ có thể khai báo duy nhất một hàm với tên "constructor". Nếu bạn cố gắng làm ngược lại (khai báo nhiều hơn một hàm constructor thì sẽ xuất hiện lỗi SyntaxError.

- Một constructor có thể sử dụng từ khóa super để gọi tới hàm constructor của class cha.

##### Phương thức Prototype

```javascript
class Rectangle {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
  
  get area() {
    return this.calcArea();
  }

  calcArea() {
    return this.height * this.width;
  }
}

const square = new Rectangle(10, 10);

console.log(square.area);
```

##### Phương thức Static (phương thức tĩnh)
- Từ khóa ```static``` định nghĩa một hàm static (hàm tĩnh) trong một class. Nếu muốn gọi hàm static này thì bạn không cần gọi chúng thông qua các ```instantiating``` của class đó và bạn cũng không thể gọi chúng thông qua cách khởi tạo class. Hàm static thường được sử dụng vào mục đích tạo ra một hàm tiện ích (có thể gọi là hàm dùng chung) cho cả một ứng dụng.

```javascript
class Point {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }

  static distance(a, b) {
    const dx = a.x - b.x;
    const dy = a.y - b.y;

    return Math.hypot(dx, dy);
  }
}

const p1 = new Point(5, 5);
const p2 = new Point(10, 10);

console.log(Point.distance(p1, p2));
```

##### Boxing với phương thức prototype và static

- Khi hai hàm static và prototype được gọi trực tiếp (không cần tạo đối tượng có giá trị "this") thì bây giờ bên trong hàm gọi, giá trị this sẽ là **undefine**. Autoboxing sẽ không xảy ra. Hành vi này sẽ giống nhau ngay cả khi chúng ta viết code ở strict mode bởi vì tất cả các hàm, phương thức, hàm khởi tạo, setter và getter đều thực thi mặc định ở strict mode. Chính vì vậy nếu chúng ta không chỉ định giá trị "this" thì giá trị của "this" sẽ là **undefined**.

```javascript
class Animal { 
  speak() {
    return this;
  }
  static eat() {
    return this;
  }
}

let obj = new Animal();
obj.speak(); // Animal {}
let speak = obj.speak;
speak(); // undefined

Animal.eat() // class Animal
let eat = Animal.eat;
eat(); // undefined
```

- Nếu chúng ta chỉnh sửa code như trên bằng cách sửa dụng prototype thì autoboxing sẽ tự động hiểu rằng giá trị this bấy giờ là dựa trên cái hàm được gọi. Tham khảo code bên dưới.

>JavaScript Code:
```javascript
function Animal() { }

Animal.prototype.speak = function() {
  return this;
}

Animal.eat = function() {
  return this;
}

let obj = new Animal();
let speak = obj.speak;
speak(); // global object

let eat = Animal.eat;
eat(); // global object
```

#### Tạo lớp con với extends
- Từ khóa ```extends``` được sử dụng trong ```class declarations``` hoặc ```class expressions``` để tạo ra một class con kế thừa từ một class sẵn có (class cha).

```javascript
class Animal { 
  constructor(name) {
    this.name = name;
  }
  
  speak() {
    console.log(this.name + ' makes a noise.');
  }
}

class Dog extends Animal {
  speak() {
    console.log(this.name + ' barks.');
  }
}

var d = new Dog('Mitzie');
d.speak(); // Mitzie barks.
```

- Nếu có một constructor trong lớp con (sub-class), nó cần gọi hàm super() trước khi có thể sử dụng "this".

- Một cách khác cũng có thể gọi và mở rộng hàm có sẵn là dùng prototype:

```javascript
function Animal (name) {
  this.name = name;  
}

Animal.prototype.speak = function () {
  console.log(this.name + ' makes a noise.');
}

class Dog extends Animal {
  speak() {
    console.log(this.name + ' barks.');
  }
}

var d = new Dog('Mitzie');
d.speak(); // Mitzie barks.
```

- Cần lưu ý rằng các class không thể extend một object bình thường trong javascript (regular object). Do đó nếu bạn muốn kế thừa một hàm từ object bình thường này, bạn cần thay thế và sử dụng ```Object.setPrototypeOf()```:

```javascript
var Animal = { // regular object
  speak() {
    console.log(this.name + ' makes a noise.');
  }
};

class Dog { //
  constructor(name) {
    this.name = name;
  }
}

Object.setPrototypeOf(Dog.prototype, Animal);// Nếu bạn không làm điều này khi gọi hàm speak thì sẽ sinh ra lỗi

var d = new Dog('Mitzie'); // đối tượng của class Dog
d.speak(); // Mitzie makes a noise.
```

#### Species
- Bạn có thể muốn trả về các đối tượng ```Array``` trong mảng của class ```MyArray```. Mô hình species sẽ cho phép bạn ghi đè lên các hàm khởi tạo mặc định.

- Ví dụ, khi sử dụng những phương thức như là ```map()``` điều đó sẽ trả về giá trị khởi tạo mặc định, bạn muốn những phương thức đó trả về một mảng đối tượng của Array, thay vì đối tượng của ```MyArray```. ```Symbol.species```  sẽ cho phép bạn thực hiện điều này:

```javascript
class MyArray extends Array {
  // Overwrite species to the parent Array constructor
  static get [Symbol.species]() { return Array; }
}

var a = new MyArray(1,2,3);
var mapped = a.map(x => x * x);

console.log(mapped instanceof MyArray); // false
console.log(mapped instanceof Array);   // true
```

#### Gọi class cha sử dụng super
- Từ khóa ```super``` dùng để gọi một hàm có sẵn ở đối tượng cha.

```javascript
class Cat { 
  constructor(name) {
    this.name = name;
  }
  
  speak() {
    console.log(this.name + ' makes a noise.');
  }
}

class Lion extends Cat {
  speak() {
    super.speak();
    console.log(this.name + ' roars.');
  }
}

var l = new Lion('Fuzzy');
l.speak(); 
// Fuzzy makes a noise.
// Fuzzy roars.
```

#### Mix-ins
- Tập hợp các class con hoặc mix-ins được gọi là khuôn mẫu cho các class. Trong ECMAScript một class chỉ có thể có một lớp cha, vì vậy để thừa kế từ tập hợp các class (kế thừa nhiều class) là điều không thể. Các chức năng phải được cung cấp bởi lớp mà nó kế thừa (cung cấp bởi lớp cha).

- Một hàm mà đã được định nghĩa ở lớp cha và lớp con muốn kế thừa và mở rộng hàm đó ra thì có thể sự dụng các lệnh mix-ins trong  ECMAScript như sau:

```javascript
var calculatorMixin = Base => class extends Base {
  calc() { }
};

var randomizerMixin = Base => class extends Base {
  randomize() { }
};
```

- Một class để sử dụng mix-ins này có thể viết code như thế này:

```javascript
class Foo { }
class Bar extends calculatorMixin(randomizerMixin(Foo)) { }
```
