- Có hai kiểu của data trong React đó là props và state:
  + Props thì mang tính external, và không bị kiểm soát bởi bản thân component. Nó được truyền từ component cao hơn theo phân cấp, hay có thể hiểu đơn giản là truyền từ component cha xuống component con. Ở ví dụ trên ```<HelloMessage name="Duyệt" />``` thì name là một props. Nó ko thay đổi.
  + Props : thì nó là một thuộc tính và ko thay đổi trong thời gian sống của Component. Vd : một nười sinh ra có một cái tên và tên đó ko thay đổi trong toàn bộ cuộc đời.
  + State biểu diễn  "trạng thái" của Component, state là private và chỉ có thể được thay đổi bên trong bản thân component, khi thay đổi state thì view cũng thay đổi theo.
+ State: là trạng thái ví dụ như chiều cao, cân nặng của một người sẽ thay đổi, khi state thay đổi nó sẽ tự tộng keo theo layout của chúng ta sẽ thay đổi. Bở vì ReactJS được thiết kế theo mô hình MVVM
- Props thì tạo ra bằng cách có thể thêm thuộc tính vào, tuy nhiên State thì ko thể tạo ra bằng cách thêm vào mà phải tạo bằng hàm getInitialState: function(){})
+ State có function setState();

```ReactDOM.render(<h2>I. Nhúng React vào HTML</h2>, document.getElementById('demo'));``` : Có 2 giá trị render cái gì? và render nó ở đâu.
- Mục đích của việc sử dụng thư viện Babel-core.
- Báo lỗi thiếu thẻ bao bọc bên ngoài. (browser.min.js:27 Uncaught SyntaxError: embedded: Adjacent JSX elements must be wrapped in an enclosing tag)
- Trong ReactDOM.render tại vị trí render cái gì thì phải có một block bọc các block con, root block.
- Khi đặt tên component thì chữ đầu tiên phải viết hoa.
- Trong javascript có định nghĩa nhanh một function() bằng cách: 

**Basic Syntax**

```javascript
(param1, param2, …, paramN) => { statements }
(param1, param2, …, paramN) => expression
// equivalent to: (param1, param2, …, paramN) => { return expression; }

// Parentheses are optional when there's only one parameter:
(singleParam) => { statements }
singleParam => { statements }

// A function with no parameters requires parentheses:
() => { statements }
() => expression // equivalent to: () => { return expression; }
```

**Advanced Syntax**

```javascript
// Parenthesize the body to return an object literal expression:
params => ({foo: bar})

// Rest parameters and default parameters are supported
(param1, param2, ...rest) => { statements }
(param1 = defaultValue1, param2, …, paramN = defaultValueN) => { statements }

// Destructuring within the parameter list is also supported
var f = ([a, b] = [1, 2], {x: c} = {x: a + b}) => a + b + c;
f();  // 6
```
### Comment code ReactJS:


- ```this.setText() nó truyền vào đối tượng state ```

- ```ref``` trong ReactJS tương tự như hàm ```val, text,html``` của jQuery, và ```document.get.ElementById``` trong javascript.

- Trong React JS phải có thẻ đóng ```/> ```, ```<input type="text" ref="text" className="form-control" />``` thì mới hoạt động.

- ```getInitialState()``` là ```function``` của ```state```, đã là ```state``` thì phải gọi hàm ```getInitialState()```

- Ý nghĩa của hàm setState() :

-  ```componentDidMount()``` : Hàm này sẽ được thực thi khi render xong.