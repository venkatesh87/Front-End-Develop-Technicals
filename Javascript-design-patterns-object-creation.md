#### I. JavaScript Object Creation: Patterns and Best Practices
---

>**1.Object Literals**
- Phương pháp tạo đối tượng JavaScript đơn giản tuyệt đối - ```object literal```.

```javascript
var o = {
  x: 42,
  y: 3.14,
  f: function() {},
  g: function() {}
};
```
- Nhưng có một nhược điểm. Nếu chúng ta cần tạo cùng một loại đối tượng ở những nơi khác, thì chúng tôi sẽ kết thúc copy-pasting the object’s methods, data, and initialization đối tượng. Chúng ta cần một cách để tạo ra không chỉ một object mà còn là một nhóm object.

>**2.Factory Functions**
- Đây là cách đơn giản nhất tuyệt đối để tạo ra một họ các đối tượng chia sẻ cùng một cấu trúc, giao diện và thực hiện. Thay vì tạo một đối tượng object literal trực tiếp, thay vào đó chúng ta trả về một đối tượng theo nghĩa đen từ một function. Bằng cách này, nếu chúng ta cần tạo cùng một loại đối tượng nhiều lần hoặc ở nhiều nơi, chúng ta chỉ cần gọi hàm:

```javascript
function thing() {
  return {
    x: 42,
    y: 3.14,
    f: function() {},
    g: function() {}
  };
}

var o = thing();
```
- Cách tiếp cận này của việc tạo đối tượng JavaScript có thể gây ra bloat bộ nhớ, vì mỗi đối tượng chứa bản sao riêng của từng chức năng. Lý tưởng nhất, chúng tôi muốn mọi đối tượng chỉ chia sẻ một bản sao các chức năng của nó.

>**3.Prototype Chains**
- JavaScript cung cấp cho chúng ta một cơ chế tích hợp để chia sẻ dữ liệu trên các đối tượng, được gọi là ```Prototype Chains```. Khi chúng ta truy cập một thuộc tính trên một đối tượng, nó có thể thực hiện yêu cầu đó bằng cách ủy nhiệm cho một số đối tượng khác. Chúng ta có thể sử dụng và thay đổi factory function để mỗi đối tượng mà nó tạo ra chỉ chứa dữ liệu duy nhất cho đối tượng cụ thể đó và ủy quyền tất cả các yêu cầu thuộc tính khác cho một đối tượng chia sẻ duy nhất.

```javascript
var thingPrototype = {
  f: function() {},
  g: function() {}
};

function thing() {
  var o = Object.create(thingPrototype);

  o.x = 42;
  o.y = 3.14;

  return o;
}

var o = thing();
```

- Trong thực tế, đây là một mô hình phổ biến mà ngôn ngữ đã hỗ trợ sẵn cho nó. Chúng ta không cần tạo đối tượng chia sẻ của riêng mình (the prototype object). Thay vào đó, một ```prototype object``` được tạo ra cho chúng ta tự động cùng với mọi hàm, và chúng ta có thể đặt dữ liệu được chia sẻ của chúng ta ở đó:

```javascript
thing.prototype.f = function() {};
thing.prototype.g = function() {};

function thing() {
  var o = Object.create(thing.prototype);

  o.x = 42;
  o.y = 3.14;

  return o;
}

var o = thing();
```
Nhưng có một nhược điểm. Điều này sẽ dẫn đến một số sự lặp lại. Các dòng đầu tiên và cuối cùng của hàm chức năng sẽ được lặp lại gần như delegating-to-prototype factory function.

>**4.ES5 Classes**
- Chúng ta có thể cô lập các đường lặp đi lặp lại bằng cách di chuyển chúng vào chức năng riêng của chúng. Hàm này sẽ tạo một đối tượng đại diện cho một số nguyên mẫu của hàm tùy ý khác, sau đó gọi hàm đó với đối tượng mới được tạo làm đối số và cuối cùng trả về đối tượng:

```javascript
function create(fn) {
  var o = Object.create(fn.prototype);

  fn.call(o);

  return o;
}

// ...

Thing.prototype.f = function() {};
Thing.prototype.g = function() {};

function Thing() {
  this.x = 42;
  this.y = 3.14;
}

var o = create(Thing);
```

- Trong thực tế, điều này cũng là một mô hình phổ biến mà ngôn ngữ có một số hỗ trợ tích hợp cho nó. Hàm ```create``` mà chúng ta đã định nghĩa thực sự là một phiên bản thô sơ của từ khóa ```new```, và chúng ta có thể thả vào thay thế ```create``` bằng ```new```:

```javascript
Thing.prototype.f = function() {};
Thing.prototype.g = function() {};

function Thing() {
  this.x = 42;
  this.y = 3.14;
}

var o = new Thing();
```

>**5.ES6 Classes**
- Một bổ sung tương đối gần đây cho JavaScript là các ```ES6 Classes```, cung cấp một cú pháp rõ ràng hơn cho việc thực hiện cùng một điều:

```javascript
class Thing {
  constructor() {
    this.x = 42;
    this.y = 3.14;
  }

  f() {}
  g() {}
}

const o = new Thing();
```

