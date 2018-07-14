Referencer: [viblo.asia](https://viblo.asia/p/tim-hieu-cac-method-cua-component-trong-react-js-voi-es6-bxjvZYpBkJZ)

#Tìm hiểu các method của component trong React js với ES6

### I. Khái niệm Component
---
- Trong React, chúng ta xây dựng trang web sử dụng những thành phần (```component```) nhỏ. Chúng ta có thể tái sử dụng một ```component``` ở nhiều nơi, với các trạng thái hoặc các thuộc tính khác nhau, trong một component lại có thể chứa thành phần khác. Mỗi ```component``` trong React có một trạng thái riêng, có thể thay đổi, và React sẽ thực hiện cập nhật ```component``` dựa trên những thay đổi của trạng thái.

- Khái niệm ```component``` trong React là một trong những thành phần quan trọng nhất của React. Do vậy việc tìm hiểu rõ các ```method```, cách thức hoạt động cũng như vai trò của các method đều rất cần thiết.

### II. Danh sách các hàm/phương thức của Component
---
**1. constructor(props):**

- Hàm này Thực hiện việc thiết lập ```state``` cho ```component```.
- Việc sử dụng ```super(props)``` là để có thể sử dụng ```this.props``` trong phạm vi hàm ```constructor``` này

```javascript
constructor(props){
  super(props)
}
```

**2. componentWillMount()**

- Thực hiện một số tác vụ, hàm này được gọi một lần trên cả ```client``` và ```server``` trước khi render diễn ra.

**3. componentDidMount()**

- Thực hiện một số tác vụ, hàm này được gọi một lần chỉ trên client, sau khi render.
- Hàm này rất hữu dụng khi bạn làm việc thêm với ```Map```, bởi vì ```map``` chỉ ```render``` được khi có ```node(id)``` trong DOM

**4. componentWillReceiveProps(nextProps) :**

- Hàm này thực hiện liên tục mỗi khi ```props``` thay đổi

**5. shouldComponentUpdate(nextProps, nextState)**

- Thực hiện khi ```state``` và ```props``` thay đổi
- Hàm này sẽ trả về kết quả ```true/false```, bạn sẽ cần sử dụng đến hàm này để xử lý xem có cần update ```component``` không.

**6. componentWillUpdate(nextProps, nextState)**

- Hàm này thực hiện dựa vào kết quả của hàm trên (```shouldComponentUpdate```)
- Nếu hàm trên trả về ```false```, thì React sẽ không gọi hàm này

**7. componentDidUpdate(prevProps, prevState)**

- Hàm này thực hiện sau khi ```component``` được ```render``` lại, từ kết quả của ```componentWillUpdate```

**8. render()**

```javascript
render() {
  return (
    <div>
      // thực hiện việc render
    </div>
  );
}
```

**9. Khai báo kiểu biến cho props**

```javascript
User.propTypes = {};
```

**10. Khai báo giá trị mặc định cho props**

```javascript
User.defaultProps = {}
```

### III. Vòng đời của 1 Component
---
**1. Khởi tạo Component**

- Khởi tạo ```Class``` (đã thừa kế từ ```class Component``` của React)
- Khởi tạo giá trị mặc định cho ```Props``` (```defaultProps```)
- Khởi tạo giá trị mặc định cho ```State``` (trong hàm ```constuctor```)
- Gọi hàm ```componentWillMount()```
- Gọi hàm ```render()```
- Gọi hàm ```componentDidMount()```

**2. Khi ```State``` thay đổi**

- Cập nhật giá trị cho ```state```
- Gọi hàm ```shouldComponentUpdate()```
- Gọi hàm ```componentWillUpdate()``` – với điều kiện hàm trên ```return true```
- Gọi hàm ```render()```
- Gọi hàm ```componentDidUpdate()```

**3. Khi ```Props``` thay đổi**

Cập nhật giá trị cho ```props```
Gọi hàm ```componentWillReceiveProps()```
Gọi hàm ```shouldComponentUpdate()```
Gọi hàm ```componentWillUpdate()``` – với điều kiện hàm trên ```return true```
Gọi hàm ```render()```
Gọi hàm ```componetDidUpdate()```

**4. Khi Unmount component**

- Gọi hàm ```componentWillUnmount()```
