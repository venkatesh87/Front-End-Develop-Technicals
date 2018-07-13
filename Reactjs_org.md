### I. Hello World
---
```javascript
ReactDOM.render(
  <h1>Hello World</h1>,
  document.getElementById('demo1')
);
```

### II. Introducing JSX
---
**1. Khai báo biến**

```javascript
const element = <h1>Hello, world!</h1>;
```

**2. Embedding Expressions in JSX(Nhúng biểu thức trong JSX)**

```javascript
const name = 'Dang Cong Dao';
const element1 = <h1>Hello {name}</h1>;
ReactDOM.render(
  element1,
  document.getElementById('demo2')
);
```

**3. JavaScript expression**

```javascript
function getName(user){
  return user.firstName + ' '+ user.lastName;
}
const user = {
  firstName: 'Dang Cong',
  lastName: 'Dao'
};
const element2 = (
  <h1>Hello {getName(user)}</h1>
);
ReactDOM.render(
  element2,
  document.getElementById('demo3')
);
```

**4. JSX is an Expression Too**

```javascript
function getGreeting(user) {
  if (user) {
    return <h1>Hello, {formatName(user)}!</h1>;
  }
  return <h1>Hello, Stranger.</h1>;
}
```

**5. Specifying Attributes with JSX**

```javascript
const element3 = <div tabIndex="0"></div>;
const element4 = <img src={user.avatarUrl}></img>;
```

**6. Specifying Children with JSX**

**6.1 Nếu thẻ trống, bạn có thể đóng thẻ ngay lập tức bằng ```/>```, như XML:**

```javascript
const element5 = <img src={user.avatarUrl} />;
```

**6.2 Thẻ JSX có thể chứa children**

```javascript
const element6 = (
  <div>
    <h1>Hello!</h1>
    <h2>Good to see you here.</h2>
  </div>
);
```

**7. JSX Represents Objects**

- These two examples are identical:

```javascript
const element7 = (
  <h1 className="greeting">
    Hello, world!
  </h1>
);
```

```javascript
const element8 = React.createElement(
  'h1',
  {className: 'greeting'},
  'Hello World'
);
```

- ```React.createElement()``` thực hiện một vài kiểm tra để giúp bạn viết mã không có lỗi nhưng về cơ bản nó tạo ra một đối tượng như thế này:

```javascript
const element9 = {
  type: 'h1',
  props: {
    className: 'greeting',
    children: 'Hello, world!'
  }
};
```

### III. Rendering Elements
---
```javascript
const element10 = <h1>Hello, world</h1>;
```

**1. Rendering an Element into the DOM**

```javascript
<div id='root'></div>
const element11 = <h1>Hello, world</h1>;
ReactDOM.render(element11, document.getElementById('root'));
```

**2. Updating the Rendered Element**

```javascript
function tick(){
  const element12 = (
    <div>
      <h1>Hello, world</h1>
      <h2>It is {new Date().toLocaleTimeString()}.</h2>
    </div>
  );
  ReactDOM.render(element12, document.getElementById('demo4'));
}
tick();
setInterval(tick, 1000);
```

### IV. Components and Props
---
- Các thành phần cho phép bạn tách giao diện người dùng thành các phần độc lập, có thể tái sử dụng và suy nghĩ về từng phần riêng biệt. Trang này giới thiệu ý tưởng về các thành phần.

**1. Functional and ```Class Components```**

- Cách đơn giản nhất để định nghĩa một Components là viết một Functional JavaScript:

```javascript
function WelcomeTo(props) {
  return <h1>Hello, {props.name}</h1>;
}
```
- Bạn cũng có thể sử dụng một ```Class ES6``` để định nghĩa một ```Components```:

```javascript
class Welcome extends React.Component {
  render(){
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```
- Hai thành phần trên tương đương với quan điểm của React.
- Chúng tôi chỉ gặp phải các phần tử React đại diện cho các thẻ ```DOM```:

```javascript
const element14 = <div />;
```

- We call this object “props”

```javascript
const element15 = <Welcome name="Sara" />;
```

**example**

```javascript
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
const element16 = <Welcome name="Sara" />;
ReactDOM.render(
  element16,
  document.getElementById('demo5')
);
```

**2. Composing Components**

```javascript
function Welcome1(props) {
  return <h1>Hello, {props.name}</h1>
}
function App() {
  return (
    <div>
      <Welcome1 name="Sara" />
      <Welcome1 name="Cahal" />
      <Welcome1 name="Edite" />
    </div>
  );
}
ReactDOM.render(
  <App />,
  document.getElementById('demo6')
);
```

**3. Extracting Components: Trích xuất thành phần**

- Đừng sợ chia thành phần thành các thành phần nhỏ hơn.

```javascript
function Comment(props) {
  return (
    <div className="Comment">
      <div className="UserInfo">
        <img className="Avatar"
          src={props.author.avatarUrl}
          alt={props.author.name}
        />
        <div className="UserInfo-name">
          {props.author.name}
        </div>
      </div>
      <div className="Comment-text">
        {props.text}
      </div>
      <div className="Comment-date">
        {formatDate(props.date)}
      </div>
    </div>
  );
}
```

- author ```(an object)```, text ```(a string)```, and date ```(a date)``` như ```props```
- Đầu tiên, chúng ta sẽ lấy Avatar:

```javascript
function Avatar(props) {
  return (
    <img className="Avatar"
      src={props.user.avatarUrl}
      alt={props.user.name}
    />
  );
}
```

- Bây giờ chúng ta có thể đơn giản hóa ```Comment``` một chút:

```javascript
function Comment(props) {
  return (
    <div className="Comment">
      <div className="UserInfo">
        <Avatar user={props.author} />
        <div className="UserInfo-name">
          {props.author.name}
        </div>
      </div>
      <div className="Comment-text">
        {props.text}
      </div>
      <div className="Comment-date">
        {formatDate(props.date)}
      </div>
    </div>
  );
}
```

- Tiếp theo, chúng tôi sẽ trích xuất component ```UserInfo``` hiển thị Avatar bên cạnh user’s name:

```javascript
function UserInfo(props) {
  return (
    <div className="UserInfo">
      <Avatar user={props.user} />
      <div className="UserInfo-name">
        {props.user.name}
      </div>
    </div>
  );
}
```

- Điều này cho phép chúng tôi đơn giản hóa Comment hơn nữa:

```javascript
function Comment(props) {
  return (
    <div className="Comment">
      <UserInfo user={props.author} />
      <div className="Comment-text">
        {props.text}
      </div>
      <div className="Comment-date">
        {formatDate(props.date)}
      </div>
    </div>
  );
}
```

**4. Props are Read-Only**

- Consider this sum function:

```javascript
function sum(a, b) {
  return a + b;
}
```
- Ngược lại, hàm này là không tinh khiết vì nó thay đổi đầu vào của chính nó:
```javascript
function withdraw(account, amount) {
  account.total -= amount;
}
```

### V. State and Lifecycle(vòng đời)
---

- Ticking clock example

```javascript
function tick() {
  const element = (
    <div>
      <h1>Hello, world!</h1>
      <h2>It is {new Date().toLocaleTimeString()}.</h2>
    </div>
  );
  ReactDOM.render(
    element,
    document.getElementById('root')
  );
}

setInterval(tick, 1000);
```

```javascript
function Clock(props) {
  return (
    <div>
      <h1>Hello, world!</h1>
      <h2>It is {props.date.toLocaleTimeString()}.</h2>
    </div>
  );
}

function tick() {
  ReactDOM.render(
    <Clock date={new Date()} />,
    document.getElementById('demo7')
  );
}

setInterval(tick, 1000);
```

**1. Converting a Function to a Class(Chuyển đổi một Function thành một Class)**

**Bạn có thể chuyển đổi component function như Clock thành một Class theo năm bước:**

  >**Step 1:** Tạo một Class ES6, có cùng tên, Kế thừa(extends) React.Component.
  
  >**Step 2:** Thêm một phương thức rỗng vào nó được gọi là render().
  
  >**Step 3:** Di chuyển phần thân body của function vào phương thức render().
  
  >**Step 4:** Thay thế các props bằng this.props trong phần render().
  
  >**Step 5:** Xóa khai báo hàm rỗng còn lại.

```javascript
class Clock extends React.Component {
  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.props.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}
```

- Đồng hồ bây giờ được định nghĩa là một Class chứ không phải là một function.
- Phương thức render sẽ được gọi mỗi lần cập nhật xảy ra, nhưng miễn là chúng ta trả <Clock /> vào cùng một nút DOM, chỉ có một cá thể duy nhất của class Clock sẽ được sử dụng.

**2. Adding Local State to a Class(Thêm trạng thái cục bộ vào một Class)**
- Chúng tôi sẽ chuyển ngày từ props sang state theo ba bước:

>**Step 1:** Thay thế this.props.date bằng this.state.date trong phương thức render ():
  
```javascript
class Clock extends React.Component {
  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}
```

>**Step 2:** Thêm một class constructor gán giá trị this.state ban đầu:

```javascript
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}
```
- Lưu ý cách chúng ta truyền props cho hàm ```constructor``` cơ bản:
- Một constructor có thể sử dụng từ khóa ```super``` để gọi tới hàm ```constructor``` của ```class``` cha.
- Các Class ```components``` phải luôn gọi hàm ```constructor``` cơ sở với ```props```.

>**Step 3:** Loại bỏ date khỏi phần tử <Clock />:

```javascript
ReactDOM.render(
  <Clock />,
  document.getElementById('root')
);
```

- Sau đó chúng tôi sẽ thêm mã bộ hẹn giờ vào chính component đó

```javascript
class Clock extends React.Component {
  constructor(props) {
    super(props);
    console.log(props);
    this.state = {date: new Date()};
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}

ReactDOM.render(
  <Clock />,
  document.getElementById('demo9')
);
```

**3. Adding Lifecycle Methods to a Class**

- Trong các ứng dụng có nhiều ```components```, điều rất quan trọng là giải phóng tài nguyên được thực hiện bởi các ```components``` khi chúng bị phá hủy.
- Chúng tôi muốn thiết lập bộ hẹn giờ bất cứ khi nào ```Clock```  được hiển thị cho ```DOM``` lần đầu tiên. Điều này được gọi là ```"mounting"```(gắn kết-) trong React.
- Chúng tôi cũng muốn xóa bộ định thời đó bất cứ khi nào ```DOM``` được tạo ra bởi ```Clock``` bị xóa. Điều này được gọi là ```"unmounting"```(tháo lắp) trong React.
- Chúng ta có thể khai báo các phương thức đặc biệt trên lớp thành phần để chạy một số mã khi một thành phần gắn kết và tháo gắn kết:

```javascript
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  componentDidMount() {

  }

  componentWillUnmount() {

  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}
```

- Những phương pháp này được gọi là ```lifecycle hooks```(móc vòng đời)
- Hook ```componentDidMount()``` chạy sau khi đầu ra thành phần được trả về ```DOM```. Đây là nơi tốt để thiết lập bộ hẹn giờ:
- Did Mount: đã gắn kết

```javascript
componentDidMount() {
  this.timerID = setInterval(
    () => this.tick(),
    1000
  );
}
```
- Lưu ý cách chúng tôi lưu timerID ngay trên this.
- Trong khi this.props được thiết lập bởi React và ```this.state``` có ý nghĩa đặc biệt, bạn có thể tự do thêm các trường bổ sung vào class theo cách thủ công nếu bạn cần lưu trữ thứ gì đó không tham gia vào luồng dữ liệu (như timer ID).
- Chúng tôi sẽ xé bộ đếm thời gian trong ```lifecycle``` hook(móc vòng đời) ```componentWillUnmount()```:

```javascript
componentWillUnmount() {
  clearInterval(this.timerID);
}
```

- Cuối cùng, chúng ta sẽ thực hiện một method gọi là ```tick()``` mà ```component Clock``` sẽ chạy mỗi giây.
- Nó sẽ sử dụng ```this.setState()``` để lên lịch cập nhật cho ```state```(trạng thái) ```component``` cục bộ:

```javascript
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  componentDidMount() {
    this.timerID = setInterval(
      () => this.tick(),
      1000
    );
  }

  componentWillUnmount() {
    clearInterval(this.timerID);
  }

  tick() {
    this.setState({
      date: new Date()
    });
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}

ReactDOM.render(
  <Clock />,
  document.getElementById('demo9')
);
```

- Bây giờ đồng hồ ve mỗi giây.
  + Khi <Clock /> được chuyển tới ReactDOM.render (), React gọi constructor hàm tạo của component Clock. Vì Clock cần hiển thị thời gian hiện tại, nó khởi tạo this.state với một đối tượng bao gồm cả thời gian hiện tại. Sau đó chúng tôi sẽ cập nhật trạng thái này this state.
  + Sau đó, React gọi phương thức render() của thành phần Clock. Đây là cách React tìm hiểu những gì sẽ được hiển thị trên màn hình. Sau đó, hãy cập nhật DOM để phù hợp với kết xuất hiển thị của Đồng hồ.
  + Khi đầu ra Clock được chèn vào trong DOM, React gọi móc nối vòng đời componentDidMount(). Bên trong nó, thành phần Clock yêu cầu trình duyệt thiết lập bộ hẹn giờ để gọi phương thức tick() của thành phần sau mỗi giây.
  + Mỗi giây trình duyệt gọi phương thức tick (). Bên trong nó, thành phần Clock lên lịch cập nhật giao diện người dùng bằng cách gọi setState() với một đối tượng có chứa thời gian hiện tại. Nhờ có cuộc gọi setState(), React biết trạng thái đã thay đổi, và gọi phương thức render () một lần nữa để tìm hiểu những gì nên có trên màn hình. Lần này, this.state.date trong phương thức render () sẽ khác nhau, và do đó đầu ra render sẽ bao gồm thời gian cập nhật. Phản ứng cập nhật DOM tương ứng. React biết trạng thái đã thay đổi, và gọi phương thức render () một lần nữa để tìm hiểu những gì nên có trên màn hình. Lần này, this.state.date trong phương thức render() sẽ khác nhau, và do đó đầu ra render sẽ bao gồm thời gian cập nhật. Phản ứng cập nhật DOM tương ứng.
  + Nếu component Clock bị loại bỏ khỏi DOM, React gọi móc nối vòng đời componentWillUnmount() để bộ hẹn giờ bị dừng.
  
**4. Using State Correctly**
- Có ba điều bạn nên biết về ```setState()```.

**4.1. Do Not Modify State Directly**
```javascript
// Wrong
this.state.comment = 'Hello';
```

```javascript
// Correct
this.setState({comment: 'Hello'});
```
- Nơi duy nhất bạn có thể gán this.state là hàm tạo.

**4.2. State Updates May Be Asynchronous(Cập nhật nhà nước có thể không đồng bộ)**

- React có thể thực hiện nhiều đợt setState () gọi thành một bản cập nhật duy nhất cho hiệu suất.
- Bởi vì this.props và this.state có thể được cập nhật không đồng bộ, bạn không nên dựa vào các giá trị của chúng để tính trạng thái tiếp theo.
- Ví dụ: mã này có thể không cập nhật được bộ đếm:

```javascript
// Wrong
this.setState({
  counter: this.state.counter + this.props.increment,
});
```

- Để khắc phục nó, sử dụng một dạng thứ hai của ```setState()``` chấp nhận một hàm thay vì một đối tượng. Hàm đó sẽ nhận trạng thái trước đó làm đối số đầu tiên và các ```props``` tại thời điểm cập nhật được áp dụng làm đối số thứ hai:

```javascript
// Correct
this.setState((prevState, props) => ({
  counter: prevState.counter + props.increment
}));
// Chúng tôi đã sử dụng chức năng mũi tên ở trên, nhưng nó cũng hoạt động với các chức năng thông thường:
// Correct
this.setState(function(prevState, props) {
  return {
    counter: prevState.counter + props.increment
  };
});
```
+ State Updates are Merged(Cập nhật trạng thái được hợp nhất)

**4.3. State Updates are Merged**
- Khi bạn gọi setState(), React sẽ kết hợp đối tượng mà bạn cung cấp vào trạng thái hiện tại.
- State của bạn có thể chứa một số biến độc lập:

```javascript
constructor(props) {
  super(props);
  this.state = {
    posts: [],
    comments: []
  };
}
```
- Sau đó, bạn có thể cập nhật chúng một cách độc lập với các lệnh gọi setState() riêng biệt:

```javascript
componentDidMount() {
  fetchPosts().then(response => {
    this.setState({
      posts: response.posts
    });
  });

  fetchComments().then(response => {
    this.setState({
      comments: response.comments
    });
  });
}
```

**5. The Data Flows Down(Dữ liệu chảy xuống)**

- Cả cha lẫn mẹ cũng không phải thành phần con có thể biết liệu một thành phần nào đó có trạng thái ```stateful``` là ```stateful``` hay không trạng thái ```stateless``` và chúng không nên quan tâm liệu nó có được định nghĩa là một function hay một ```class``` hay không.
- Một thành phần có thể chọn chuyển state của nó xuống dưới dạng các props cho các thành phần con của nó:
```<h2>It is {this.state.date.toLocaleTimeString()}.</h2>```
- Điều này cũng hoạt động cho các thành phần do người dùng xác định:
```<FormattedDate date={this.state.date} />```
- Thành phần FormattedDate sẽ nhận ngày tháng trong props của nó và sẽ không biết nó có xuất phát từ trạng thái của ```Clock’s``` hay không, từ các ```props``` của ```Clock’s``` hoặc được nhập bằng tay:
- Để chỉ ra rằng tất cả các thành phần đều thực sự bị cô lập, chúng ta có thể tạo một thành phần ứng dụng để hiển thị ba ```<Clock>```:
  
```javascript
function App() {
  return (
    <div>
      <Clock />
      <Clock />
      <Clock />
    </div>
  );
}

ReactDOM.render(
  <App />,
  document.getElementById('root')
);
```

### VI. Handling Events: Xử lý sự kiện
---
- .
>JavaScript Code:
```javascript

```

### VII. Conditional Rendering(Hiển thị có điều kiện)
---
- .
>JavaScript Code:
```javascript

```

### VIII. Lists and Keys: Danh sách và khóa
---
- .
>JavaScript Code:
```javascript

```

### IX. 
---
- .
>JavaScript Code:
```javascript

```

### X. 
---
- .
>JavaScript Code:
```javascript

```


