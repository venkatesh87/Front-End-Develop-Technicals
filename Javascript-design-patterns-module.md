#### I. Javascript Design Module Pattern
---
**Reference**: https://viblo.asia/p/javascript-design-pattern-constructor-pattern-bJzKmMyPK9N

- Module pattern là một loại pattern khá mạnh và được sử dụng rất phổ biến, với một số các đặc điểm sau:

  + Sử dụng Object ```Literals ({})```

  + Cung cấp khả năng đóng gói dữ liệu với cả thuộc tính và phương thức dạng **public/private**, giúp tránh xung đột về tên đối với các ```function``` ở các script khác trên trang web.
  
**1. Ví dụ sử dụng Module Pattern**
---

```javascript
var countModule = (function(){
  var count = 0;
  var log = function(funcName) {
    console.log(funcName, count);
  }
  return {
    increase: function() {
      count++;
      log("increase");
    },
    decrease: function() {
      count--;
      log("decrease");
    },
    reset: function() {
      count = 0;
      log("reset");
    }
  }
})();

// Usage:
countModule.increase(); // increase 1
countModule.increase(); // increase 2
countModule.decrease(); // increase 1
countModule.reset();    // reset 0
```

**2. Giải thích**
---

- Ví dụ trên định nghĩa một module tên là: **countModule**. Có thể bạn sẽ thắc mắc về cú pháp sau:

```javascript
var countModule = (function(){

})();
```

- Thực chất, đoạn code trên có thể tách ra làm 2 phần: Khai báo hàm và gọi hàm.

```javascript
// Khai báo hàm
var funcModule = function(){

}
// Gọi hàm
var countModule = funcModule();
```

- Do đó, nếu muốn truyền tham số vào function (chẳng hạn như **jQuery**) thì bạn có thể viết như sau:

```javascript
var countModule = (function(jQ){

})(jQuery);
```

- Theo cách phân tích trên, thực chất **countModule** là thành phần **return** của function - dạng **object ({})**. Do đó, ta chỉ có thể truy cập đến những thuộc tính bên trong object này là: **increase**, **decrease**, **reset**. Hay nói cách khác, những hàm số này thuộc dạng **public**.

- Ngược lại, biến số **count**, **log** chỉ truy cập được ở trong hàm số trên, nên thuộc dạng **private**.

**3. Revealing Module Pattern**
---
- **Module Pattern** có một nhược điểm là khó theo dõi các phương thức được public. Sau đây là cách sử dụng **Revealing Module Pattern** để khắc phục nhược điểm này:

```javascript
var countModule = (function(){
  var count = 0;
  var log = function(funcName) {
    console.log(funcName, count);
  }
  function increaseFunc() {
    count++;
    log("increase");
  }
  function decreaseFunc() {
    count--;
    log("decrease");
  }
  function resetFunc() {
    count = 0;
    log("reset");
  }
  return {
    increase: increaseFunc,
    decrease: decreaseFunc,
    reset: resetFunc
  }
})();

// Usage:
countModule.increase(); // increase 1
countModule.increase(); // increase 2
countModule.decrease(); // increase 1
countModule.reset();    // reset 0
```

- Bây giờ, ta có thể dễ dàng thấy rằng **countModule** có 3 phương thức được public là: **increase**, **decrease**, **reset**.
