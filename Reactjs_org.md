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
**HTML:**

```javascript
<button onclick="activateLasers()">
  Activate Lasers
</button>
```

**hơi khác trong React:**

```javascript
<button onClick={activateLasers}>
  Activate Lasers
</button>
```
- Một khác biệt nữa là bạn không thể trả về ```false``` để ngăn chặn hành vi mặc định trong React. Bạn phải gọi ```preventDefault``` một cách rõ ràng. Ví dụ: với HTML thuần túy, để ngăn chặn hành vi liên kết mặc định của việc mở một trang mới, bạn có thể viết:

```javascript
<a href="#" onclick="console.log('The link was clicked.'); return false">
  Click me
</a>
```
- Trong React, đây có thể là:

```javascript
function ActionLink() {
  function handleClick(e) {
    e.preventDefault();
    console.log('The link was clicked.');
  }

  return (
    <a href="#" onClick={handleClick}>
      Click me
    </a>
  );
}
```

- Khi sử dụng React, bạn thường không cần phải gọi ```addEventListener``` để thêm người nghe vào một phần tử ```DOM``` sau khi nó được tạo ra. Thay vào đó, chỉ cần cung cấp một trình lắng nghe khi phần tử ban đầu được hiển thị.

- Khi bạn định nghĩa một thành phần sử dụng một ```class ES6```, một mẫu chung là cho trình xử lý sự kiện là một phương thức trên lớp. Ví dụ: thành phần ```Toggle``` này hiển thị nút cho phép người dùng chuyển đổi giữa trạng thái “BẬT” và “TẮT”:

```javascript
class Toggle extends React.Component {
  constructor(props) {
    super(props);
    this.state = {isToggleOn: true};

    // This binding is necessary to make `this` work in the callback
    this.handleClick = this.handleClick.bind(this);
  }

  handleClick() {
    this.setState(prevState => ({
      isToggleOn: !prevState.isToggleOn
    }));
  }

  render() {
    return (
      <button onClick={this.handleClick}>
        {this.state.isToggleOn ? 'ON' : 'OFF'}
      </button>
    );
  }
}

ReactDOM.render(
  <Toggle />,
  document.getElementById('root')
);
```

- Nếu liên kết gọi điện thoại làm phiền bạn, có hai cách bạn có thể giải quyết vấn đề này. Nếu bạn đang sử dụng cú pháp các trường công khai thử nghiệm, bạn có thể sử dụng các trường lớp để ràng buộc đúng các cuộc gọi lại:

```javascript
class LoggingButton extends React.Component {
  // This syntax ensures `this` is bound within handleClick.
  // Warning: this is *experimental* syntax.
  handleClick = () => {
    console.log('this is:', this);
  }

  render() {
    return (
      <button onClick={this.handleClick}>
        Click me
      </button>
    );
  }
}
```

- Nếu bạn không sử dụng cú pháp trường lớp, bạn có thể sử dụng ```arrow function``` trong gọi lại:

```javascript
class LoggingButton extends React.Component {
  handleClick() {
    console.log('this is:', this);
  }

  render() {
    // This syntax ensures `this` is bound within handleClick
    return (
      <button onClick={(e) => this.handleClick(e)}>
        Click me
      </button>
    );
  }
}
```

- Passing Arguments to ```Event Handlers```(Chuyển đối số cho trình xử lý sự kiện)
- Bên trong một vòng lặp nó là phổ biến để muốn vượt qua một tham số thêm vào một xử lý sự kiện. Ví dụ: nếu id là ID hàng, một trong các cách sau sẽ hoạt động:

```javascript
<button onClick={(e) => this.deleteRow(id, e)}>Delete Row</button>
<button onClick={this.deleteRow.bind(this, id)}>Delete Row</button>
```
- Hai dòng trên là tương đương, và sử dụng các ```arrow function``` và ```Function.prototype.bind``` tương ứng.

### VII. Conditional Rendering(Hiển thị có điều kiện)
- Hãy xem xét hai thành phần sau:

```javascript
function UserGreeting(props) {
  return <h1>Welcome back!</h1>;
}

function GuestGreeting(props) {
  return <h1>Please sign up.</h1>;
}
```

- Chúng tôi sẽ tạo thành phần ```Greeting``` hiển thị một trong các thành phần này tùy thuộc vào việc người dùng có đăng nhập hay không:

```javascript
function Greeting(props) {
  const isLoggedIn = props.isLoggedIn;
  if (isLoggedIn) {
    return <UserGreeting />;
  }
  return <GuestGreeting />;
}

ReactDOM.render(
  // Try changing to isLoggedIn={true}:
  <Greeting isLoggedIn={false} />,
  document.getElementById('root')
);
```

- Ví dụ này ám một lời chào khác nhau tùy thuộc vào giá trị của ```isLoggedIn prop```.

**1. Element Variables(Biến phần tử)**
- Bạn có thể sử dụng các biến để lưu trữ các phần tử. Điều này có thể giúp bạn điều kiện hiển thị một phần của thành phần trong khi phần còn lại của đầu ra không thay đổi.
- Xem xét hai thành phần mới này đại diện cho nút Đăng xuất và Đăng nhập:

```javascript
function LoginButton(props) {
  return (
    <button onClick={props.onClick}>
      Login
    </button>
  );
}

function LogoutButton(props) {
  return (
    <button onClick={props.onClick}>
      Logout
    </button>
  );
}
```

- Trong ví dụ dưới đây, chúng ta sẽ tạo một thành phần có trạng thái được gọi là ```LoginControl```.
- Nó sẽ hiển thị ```<LoginButton />``` hoặc ```<LogoutButton />``` tùy thuộc vào trạng thái hiện tại của nó. Nó cũng sẽ hiển thị ```<Greeting />``` từ ví dụ trước:

```javascript
class LoginControl extends React.Component {
  constructor(props) {
    super(props);
    this.handleLoginClick = this.handleLoginClick.bind(this);
    this.handleLogoutClick = this.handleLogoutClick.bind(this);
    this.state = {isLoggedIn: false};
  }

  handleLoginClick() {
    this.setState({isLoggedIn: true});
  }

  handleLogoutClick() {
    this.setState({isLoggedIn: false});
  }

  render() {
    const isLoggedIn = this.state.isLoggedIn;
    let button;

    if (isLoggedIn) {
      button = <LogoutButton onClick={this.handleLogoutClick} />;
    } else {
      button = <LoginButton onClick={this.handleLoginClick} />
    }

    return (
      <div>
        <Greeting isLoggedIn={isLoggedIn} />
        {button}
      </div>
    );
  }
}

ReactDOM.render(
  <LoginControl />,
  document.getElementById('root')
);
```

**2. Inline If with Logical && Operator(Inline Nếu với Logical && Operator)**

- Bạn có thể nhúng bất kỳ biểu thức nào trong JSX bằng cách gói chúng trong các dấu ngoặc nhọn. Điều này bao gồm toán tử ```logic && JavaScript```. Nó có thể thuận tiện cho điều kiện bao gồm một phần tử:

```javascript
function Mailbox(props) {
  const unreadMessages = props.unreadMessages;
  return (
    <div>
      <h1>Hello!</h1>
      {unreadMessages.length > 0 &&
        <h2>
          You have {unreadMessages.length} unread messages.
        </h2>
      }
    </div>
  );
}

const messages = ['React', 'Re: React', 'Re:Re: React'];
ReactDOM.render(
  <Mailbox unreadMessages={messages} />,
  document.getElementById('root')
);
```

- Nó hoạt động bởi vì trong JavaScript, ```true && expression``` luôn luôn đánh giá ```expression```, và ```false && expression``` luôn luôn đánh giá ```false```.
- Do đó, nếu điều kiện là ```true```, phần tử ngay sau && sẽ xuất hiện trong đầu ra. Nếu nó ```false```, React sẽ bỏ qua và bỏ qua nó.
- Một phương pháp khác để điều kiện nội dung dựng hình nội tuyến là sử dụng điều kiện toán tử ```condition ? true : false```.
- Trong ví dụ dưới đây, chúng tôi sử dụng nó để điều kiện hiển thị một khối văn bản nhỏ.

```javascript
render() {
  const isLoggedIn = this.state.isLoggedIn;
  return (
    <div>
      The user is <b>{isLoggedIn ? 'currently' : 'not'}</b> logged in.
    </div>
  );
}
```

- Nó cũng có thể được sử dụng cho các biểu thức lớn hơn mặc dù nó ít rõ ràng hơn những gì đang xảy ra:

```javascript
render() {
  const isLoggedIn = this.state.isLoggedIn;
  return (
    <div>
      {isLoggedIn ? (
        <LogoutButton onClick={this.handleLogoutClick} />
      ) : (
        <LoginButton onClick={this.handleLoginClick} />
      )}
    </div>
  );
}
```

**3. Preventing Component from Rendering**(Ngăn Component khỏi Rendering)

- Trong ví dụ bên dưới, ```<WarningBanner />``` được hiển thị tùy thuộc vào giá trị của ```prop``` được gọi là cảnh báo. Nếu giá trị của giá trị giả là ```false```, thì thành phần sẽ không hiển thị:

```javascript
function WarningBanner(props) {
  if (!props.warn) {
    return null;
  }

  return (
    <div className="warning">
      Warning!
    </div>
  );
}

class Page extends React.Component {
  constructor(props) {
    super(props);
    this.state = {showWarning: true};
    this.handleToggleClick = this.handleToggleClick.bind(this);
  }

  handleToggleClick() {
    this.setState(prevState => ({
      showWarning: !prevState.showWarning
    }));
  }

  render() {
    return (
      <div>
        <WarningBanner warn={this.state.showWarning} />
        <button onClick={this.handleToggleClick}>
          {this.state.showWarning ? 'Hide' : 'Show'}
        </button>
      </div>
    );
  }
}

ReactDOM.render(
  <Page />,
  document.getElementById('root')
);

```

### VIII. Lists and Keys: Danh sách và khóa
---
- Với đoạn mã dưới đây, chúng ta sử dụng hàm map() để lấy một mảng các số và nhân đôi giá trị của chúng. Chúng ta gán mảng mới được ```map()``` trả về cho biến được nhân đôi và ghi nó:

```javascript
const numbers = [1, 2, 3, 4, 5];
const doubled = numbers.map((number) => number * 2);
console.log(doubled);
```

- Mã này ghi nhật ký ```[2, 4, 6, 8, 10]``` vào bảng điều khiển.
- 1.Rendering Multiple Components: Hiển thị nhiều components
- Bạn có thể xây dựng các bộ sưu tập các phần tử và bao gồm chúng trong JSX bằng cách sử dụng các dấu ngoặc nhọn ```{}```.
- Dưới đây, chúng ta lặp qua mảng số bằng cách sử dụng hàm JavaScript ```map()```. Chúng tôi trả về một phần tử ```<li>``` cho mỗi mục. Cuối cùng, chúng ta gán mảng kết quả của các phần tử cho ```listItems```:
  
```javascript
const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map((number) =>
  <li>{number}</li>
);
```

- Chúng tôi bao gồm toàn bộ mảng ```listItems``` bên trong phần tử ```<ul>``` và hiển thị nó cho ```DOM```:

```javascript
ReactDOM.render(
  <ul>{listItems}</ul>,
  document.getElementById('root')
);
```
  
**2. Basic List Component**
  
- Thông thường, bạn sẽ hiển thị danh sách bên trong một thành phần.
- Chúng ta có thể cấu trúc lại ví dụ trước đó thành một thành phần chấp nhận một mảng các số và xuất ra một danh sách các phần tử không có thứ tự.

```javascript
function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    <li>{number}</li>
  );
  return (
    <ul>{listItems}</ul>
  );
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers={numbers} />,
  document.getElementById('root')
);
```

- Hãy gán một khóa cho các mục danh sách của chúng tôi bên trong ```numbers.map()``` và sửa vấn đề quan trọng còn thiếu.

```javascript
function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    <li key={number.toString()}>
      {number}
    </li>
  );
  return (
    <ul>{listItems}</ul>
  );
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers={numbers} />,
  document.getElementById('root')
);
```

**3. Keys**

- ```Keys``` giúp React xác định những mục nào đã thay đổi, được thêm vào hoặc bị xóa. Các phím nên được trao cho các phần tử bên trong mảng để cung cấp cho các yếu tố một bản sắc ổn định:

```javascript
const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map((number) =>
  <li key={number.toString()}>
    {number}
  </li>
);
```

- Cách tốt nhất để chọn khóa là sử dụng một chuỗi xác định duy nhất một mục danh sách trong số các anh chị em của nó. Thông thường, bạn sẽ sử dụng ```ID``` từ dữ liệu của mình dưới dạng khóa:

```javascript
const todoItems = todos.map((todo) =>
  <li key={todo.id}>
    {todo.text}
  </li>
);
```

- Khi bạn không có ```ID``` ổn định cho các mục được hiển thị, bạn có thể sử dụng chỉ mục mục làm khóa làm phương sách cuối cùng:

```javascript
const todoItems = todos.map((todo, index) =>
  // Only do this if items have no stable IDs
  <li key={index}>
    {todo.text}
  </li>
```

**4. Extracting Components with Keys**

- Example: Incorrect Key Usage

```javascript
function ListItem(props) {
  const value = props.value;
  return (
    // Wrong! There is no need to specify the key here:
    <li key={value.toString()}>
      {value}
    </li>
  );
}

function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    // Wrong! The key should have been specified here:
    <ListItem value={number} />
  );
  return (
    <ul>
      {listItems}
    </ul>
  );
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers={numbers} />,
  document.getElementById('root')
);
```

- Example: Correct Key Usage

```javascript
function ListItem(props) {
  // Correct! There is no need to specify the key here:
  return <li>{props.value}</li>;
}

function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    // Correct! Key should be specified inside the array.
    <ListItem key={number.toString()}
              value={number} />

  );
  return (
    <ul>
      {listItems}
    </ul>
  );
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers={numbers} />,
  document.getElementById('root')
);
```

**5. Keys Must Only Be Unique Among Siblings: Chìa khóa chỉ phải duy nhất trong số các anh chị em**

- Các phím được sử dụng trong các mảng phải là duy nhất trong số các anh chị em của chúng. Tuy nhiên, chúng không cần phải là duy nhất toàn cầu. Chúng ta có thể sử dụng các khóa giống nhau khi chúng ta tạo ra hai mảng khác nhau:

```javascript
function Blog(props) {
  const sidebar = (
    <ul>
      {props.posts.map((post) =>
        <li key={post.id}>
          {post.title}
        </li>
      )}
    </ul>
  );
  const content = props.posts.map((post) =>
    <div key={post.id}>
      <h3>{post.title}</h3>
      <p>{post.content}</p>
    </div>
  );
  return (
    <div>
      {sidebar}
      <hr />
      {content}
    </div>
  );
}

const posts = [
  {id: 1, title: 'Hello World', content: 'Welcome to learning React!'},
  {id: 2, title: 'Installation', content: 'You can install React from npm.'}
];
ReactDOM.render(
  <Blog posts={posts} />,
  document.getElementById('root')
);
```

**6.Embedding map() in JSX: Nhúng bản đồ () vào JSX **

- Trong các ví dụ trên, chúng tôi đã khai báo một biến listItems riêng biệt và bao gồm nó trong JSX:

```javascript
function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    <ListItem key={number.toString()}
              value={number} />

  );
  return (
    <ul>
      {listItems}
    </ul>
  );
}
```

- JSX cho phép nhúng bất kỳ biểu thức nào trong các dấu ngoặc nhọn để chúng ta có thể inline kết quả ```map()```:

```javascript
function NumberList(props) {
  const numbers = props.numbers;
  return (
    <ul>
      {numbers.map((number) =>
        <ListItem key={number.toString()}
                  value={number} />

      )}
    </ul>
  );
}
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


