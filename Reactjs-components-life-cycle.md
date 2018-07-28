**Referencer:**

1. https://viblo.asia/p/vong-doi-cua-component-trong-react-gGJ59XaJlX2
1. https://viblo.asia/p/vong-doi-cua-mot-component-trong-reactjs-voi-es6-aWj531qPZ6m
1. https://viblo.asia/p/vong-doi-cua-mot-react-component-RQqKLMRzZ7z

### I. Vòng đời của component trong React
---
**1. Mounting**
- Một component thực hiện "mount" chỉ khi nó render trong lần đầu tiên. Có 3 mounting lifecycle methods:
  + componentWillMount
  + render
  + componentDidMount

- Khi một component "mount" nó sẽ tự động gọi lần lượt 3 method trên, mounting lifecycle method đầu tiên được gọi là componentWillMount. Khi một component được render trong lần đầu tiên thì componentWillMount sẽ được gọi trước khi render. Ví dụ:

```javascript
var React = require('react');
var ReactDOM = require('react-dom');

var Example = React.createClass({
  componentWillMount: function () {
    alert('componentWillMount sẽ được gọi ở đây');
  },

  render: function () {
    return <h1>Hello world</h1>;
  }
});

ReactDOM.render(
  <Example />,
  document.getElementById('app')
);	

setTimeout(function(){
  ReactDOM.render(
    <Example />,
    document.getElementById('app')
  );
}, 2000);
```

- Ở đoạn code trên, khi chạy thì trong lần render đầu tiên, lần lượt sẽ bắn ra ```alert("componentWillMount sẽ được gọi ở đây")```, sau đó màn hình hiển thị render text: Hello world. Từ những lần sau, khi render lại component Example, được gọi trong setTimeout thì alert sẽ không được gọi lại nữa.

- Sau khi ```componentWillMount``` thực hiện xong, sẽ đến render(cho lần đầu tiên), và sau đó sẽ gọi method ```componentDidMount()```, ```componentDidMount()``` được sử dụng rất nhiều. Nếu ứng dụng React của bạn đang sử dụng ```AJAX``` để fetch những dữ liệu khởi tạo từ một API thì ```componentDidMount``` là nơi để thực hiện lời gọi ```AJAX``` đó. Nói chung, ```componentDidMount``` là một nơi thích hợp để kết nối một ứng dụng React với một ứng dụng bên ngoài như một web API hay một javascript framework. ```componentDidMount``` cũng là nơi để các method set time như: ```setTimeout``` và ```setInterval```.

```javascript
var React = require('react');

var Example = React.createClass({
  componentDidlMount: function () {
    alert('component just finished mounting!');
  },

  render: function () {
    return <h1>Hello world</h1>;
  }
});
```

**2. Updating**

- Sau khi component ```render``` lần đầu tiên, các ```lifecycle methods``` của Updating sẽ được gọi bắt đầu với lần ```render``` thứ hai. Với cơ chế automatic binding của mình thì chắc chắn các component sẽ được render nhiều lần trong ứng dụng của bạn. Có 5 method trong lifecycle updating:

  1.componentWillReceiveProps
  1.shouldComponentUpdate
  1.componentWillUpdate
  1.render
  1.componentDidUpdate

- Mỗi khi một instance(lời yêu cầu) của component được update, nó sẽ tự động gọi lần lượt 5 methods trên. Updating lifecycle methods đầu tiên là componentWillReceiveProps, khi một instance của component được update, ```componentWillReceiveProps``` sẽ được gọi trước khi ```render```. Có một chú ý ở đây là: ```componentWillReceiveProps``` chỉ được gọi nếu component được nhận một prop:

```javascript
// componentWillReceiveProps will get called here:
ReactDOM.render(
  <Example prop="myVal" />,
  document.getElementById('app')
);

// componentWillReceiveProps will NOT get called here:
ReactDOM.render(
  <Example />,
  document.getElementById('app')
);
```

- ```componentWillReceiveProps``` tự động được truyền vào một argument, được gọi là nextProps, nextProps chính là giá trị preview của prop mà component sắp được nhận để render. Ví dụ

**componentWillReceiveProps**

```javascript
var React = require('react');

var Example = React.createClass({
  componentWillReceiveProps: function (nextProps) {
    alert("Check out the new props.text that "
    	+ "I'm about to get:  " + nextProps.text);
  },

  render: function () {
    return <h1>{this.props.text}</h1>;
  }
});


// The first render won't trigger
// componentWillReceiveProps:
ReactDOM.render(
	<Example text="Hello world" />,
	document.getElementById('app')
);

// After the first render, 
// subsequent renders will trigger
// componentWillReceiveProps:
setTimeout(function () {
	ReactDOM.render(
		<Example text="Hello world" />,
		document.getElementById('app')
	);
}, 1000);
```

- giá trị của ```nextProps.text``` trong ```componentWillReceiveProps``` là "Hello world".

**componentWillReceiveProps**
- Updating lifecycle method thứ hai là ```shouldComponentUpdate```. Khi một component update, ```shouldComponentUpdate``` sẽ được gọi sau ```componentWillReceiveProps``` nhưng vẫn trước render. Ví dụ:

```javascript
var React = require('react');

var Example = React.createClass({
  getInitialState: function () {
    return { subtext: 'Put me in an <h2> please.' };
  },

  shouldComponentUpdate: function (nextProps, nextState) {
    if ((this.props.text == nextProps.text) && 
      (this.state.subtext == nextState.subtext)) {
      alert("Props and state haven't changed, so I'm not gonna update!");
      return false;
    } else {
      alert("Okay fine I will update.");
      return true;
    }
  },

  render: function () {
    return (
      <div>
        <h1>{this.props.text}</h1>
        <h2>{this.state.subtext}</h2>
      </div>
    );
  }
});
```

**shouldComponentUpdate**
- ```shouldComponentUpdate``` sẽ trả về ```true``` hoặc ```false```. Nếu trả về ```true```, việc update sẽ diễn ra bình thường. Nhưng nếu trả về ```false```, tất cả method còn lại của updating cycle method sẽ không được gọi nữa, kể cả render và component sẽ không được update, shouldComponentUpdate tự động nhận vào 2 argument là: ```nextProps``` và ```nextState```, ```nextProps``` và ```nextState``` là ```prop``` và ```state``` được truyền từ một ```component``` khác đến, hay chính là giá trị prop và state nếu component được update, shouldComponentUpdate sẽ kiểm tra 2 giá trị này với ```prop``` và ```state``` hiện tại của nó. Nếu khác nhau sẽ tiến hành update component, còn không thì dừng hẳn lại update component. Điều này rất quan trọng nếu bạn muốn tăng performance cho React app của bạn(good). Ví du:

```javascript
var React = require('react');

var Example = React.createClass({
  getInitialState: function () {
    return { subtext: 'Put me in an <h2> please.' };
  },

  shouldComponentUpdate: function (nextProps, nextState) {
    if ((this.props.text == nextProps.text) && 
      (this.state.subtext == nextState.subtext)) {
      alert("Props and state haven't changed, so I'm not gonna update!");
      return false;
    } else {
      alert("Okay fine I will update.");
      return true;
    }
  },

  render: function () {
    return (
      <div>
        <h1>{this.props.text}</h1>
        <h2>{this.state.subtext}</h2>
      </div>
    );
  }
});
```

**componentWillUpdate**
- Method thứ 3 trong updating lifecycle method là ```componentWillUpdate```. Nó được gọi giữa ```shouldComponentUpdate``` và ```render```. Nó cũng nhận vào 2 argument và ```nextProps``` và ```nextState```.

```javascript
var React = require('react');

var Example = React.createClass({
  componentWillUpdate: function (nextProps, nextState) {
    alert('Component is about to update!  Any second now!');
  },

  render: function () {
    return <h1>Hello world</h1>;
  }
});
```

- Có một điều chú ý ở đây là, bạn không thể gọi this.setState trong componentWillUpdate. Mục tiêu chính của componentWillUpdate là tương tác những thứ bên ngoài kiến trúc React. Nếu bạn cần set up một cái gì đó ngoài React, như check window size hay tương tác với một API thì componentWillUpdate là nơi thích hợp để thực hiện điều đó.

**componentDidUpdate**

- Tiếp theo là method render và cuối cùng trong updating lifecycle method là ```componentDidUpdate```. Khi một component instance update, ```componentDidUpdate``` sẽ được gọi sau khi render HTML được loading xong.

```javascript
var React = require('react');

var Example = React.createClass({
  componentDidUpdate: function (prevProps, prevState) {
    alert('Component is done rendering!');
  },

  render: function () {
    return <h1>Hello world</h1>;
  }
});
```
**componentDidUpdate**

- ```componentDidUpdate``` tự động được truyền vào 2 argument là ```prevProps``` và ```prevState```. ```prevProps``` và ```prevState``` sẽ tham chiếu đến prop và state của component trước khi quá trình update component bắt đầu. Chúng ta có thể so sánh 2 argument này với giá trị hiện tại của prop và state. componentDidUpdate thường được sử dụng để tương tác với một số thứ bên ngoài vào môi trường React như là browser hay APIs. Nó tương tự như ```componentWillUpdate``` ngoại trừ việc nó được gọi sau method render.

**3. Unmounting**

- Quá trình unmounting của component xảy ra khi component bị removed từ một DOM. Việc này có thể xảy ra khi một DOM được render mà không có component hoặc nếu user chuyển hướng đến một trang web khác hoặc khi trình duyệt được đóng. Chỉ có duy nhất một method trong quá trình này là: ```componentWillUnmount```, ```componentWillUnmount``` sẽ được gọi trước khi một component bị remove khỏi một DOM. Nếu một component khởi tạo bất kì một method nào mà method đó yêu cầu phải clean up thì ```componentWillUnmount``` sẽ là nơi bạn nên đặt clean up.

```javascript
var React = require('react');

var Example = React.createClass({
  componentWillUnmount: function () {
    alert('Goodbye world');
  },

  render: function () {
    return <h1>Hello world</h1>;
  }
});
```

### II. Vòng đời của một component trong reactjs với ES6
---
**1. Tổng Quan**

- Khi tiếp xúc với react thì chắc hẳn khái niệm component không còn xa lạ gì. Có thể nói component trong react là một trong những thành phần quan trọng nhất của React. Do đó, việc hiểu rõ được vòng đời của một component thật sự rất quan trọng. Mặc dù mới tiếp xúc với react nhưng trong bài này mình sẽ trình bày về cái mình hiểu về vòng đời của một component

```javascript
import React, {Component, PropTypes} from 'react';

class User extends Component {
  constructor(props){
    super(props)
   // Hàm này Thực hiện việc thiết lập state cho component
   // Việc sử dụng super(props) là để có thể sử dụng this.props trong phạm vi hàm constructor này
  }
  
  componentWillMount() {
    // Thực hiện một số tác vụ, hàm này chỉ thực hiện 1 lần duy nhất
    
  }
  componentDidMount() {
    // Thực hiện một số tác vụ, hàm này chỉ thực hiện 1 lần duy nhất
    // Hàm này rất hữu dụng khi bạn làm việc thêm với Map, bởi vì map chỉ render được 
    // khi có node (id) trong DOM  
    // Nói tóm lại, hàm này được gọi để thông báo component đã tồn tại trên DOM, 
    // từ đó các thao tác trên DOM sẽ có thể thực hiện bình thường đối với component này
  }
  componentWillUnmount() {
    // Hàm này thực hiện một lần duy nhất, khi component sẽ unmount
    // Hàm này hữu dụng khi bạn cần xoá các timer không còn sử dụng
  }
  componentWillReceiveProps(nextProps) {
    // Hàm này thực hiện liên tục mỗi khi props thay đổi
    // (1) Sử dụng để thay đổi trạng thái (state) của component phụ thuộc props
    // (2) Sử dụng các kết quả, khởi tạo biến có tính chất async. Ví dụ: Khởi tạo Google Map Api, đây là quá trình async,
    // do vậy, bạn không thể biết được khi nào khởi tạo xong, thì khi khởi tạo xong có thể truyền xuống component thông qua
    // props, và từ đó bạn có thể khởi tạo các dịch vụ khác.
  }
  shouldComponentUpdate(nextProps, nextState) {
    // Hàm này thực hiện khi state và props thay đổi
    // Hàm này sẽ trả về kết quả true/false, bạn sẽ cần sử dụng đến hàm này để xử lý xem có cần update component không
  }
  
  componentWillUpdate(nextProps, nextState) {
    // Hàm này thực hiện dựa vào kết quả của hàm trên (shouldComponentUpdate)
    // Nếu hàm trên trả về false, thì React sẽ không gọi hàm này
  }  
  componentDidUpdate(prevProps, prevState) {
    // Hàm này thực hiện sau khi component được render lại, từ kết quả của componentWillUpdate
  }
  
  render() {
    return (
      <div>
        // thực hiện việc render
      </div>
    );
  }
}

User.propTypes = {
  //Khai báo kiểu biến cho props
};
User.defaultProps = {
  //Khai báo giá trị mặc định cho props
}
export default User;
```

**2. Vòng đời component**

- Mỗi component có một số "lifecycle methods" cái mà bạn sẽ có thể ghi đè để chạy code với thời gian cụ thể trong tiến trình. Phương thức bắt đầu với will sẽ được gọi ngay trước khi có một điều gì đó xảy ra. Các phương thức bắt đầu với did sẽ được gọi ngay sau khi có điều gì đó xảy ra. React dùng virtual-DOM để cài thiện tốc độ. Nên khi các virtual-DOM tương tác với các DOM thật thì xảy ra các quá trình:

**Khởi tạo Component**

- Lần lượt các hành động sau để khởi tạo component:

```javascript
Khởi tạo Class (đã thừa kế từ class Component của React)
Khởi tạo giá trị mặc định cho Props (defaultProps)
Khởi tạo giá trị mặc định cho State (trong hàm constuctor)
Gọi hàm componentWillMount()
Gọi hàm render()
Gọi hàm componentDidMount()
Khi State thay đổi
```

**Cập nhật giá trị cho state**

```javascript
Gọi hàm shouldComponentUpdate()
Gọi hàm componentWillUpdate() – với điều kiện hàm trên return true
Gọi hàm render()
Gọi hàm componentDidUpdate()
Khi Props thay đổi
```

**Cập nhật giá trị cho props**

```javascript
Gọi hàm componentWillReceiveProps()
Gọi hàm shouldComponentUpdate()
Gọi hàm componentWillUpdate() – với điều kiện hàm trên return true
Gọi hàm render()
Gọi hàm componetDidUpdate()
```

**Khi Unmount component**

```javascript
Gọi hàm componentWillUnmount()
```

**3. Nói thêm về phương thức setState() trong reactjs**

- Trong react bạn chỉ khởi tạo thís.state một lần duy nhất trong hàm constructor. Nếu muốn thay đổi giá trị của nó thì bạn phải dùng method this.setState(). Khi sử dụng setState là chúng ta đã kích hoạt danh sách các phương thức thuộc vòng đời của component. Một điều lưu ý:
  
  + ```this.setState``` là hàm ```async```. Nên ngay sau khi ```setState``` thì ta truy cập thís.state thì giá trị không thay đổi.

  + ```SetState``` sẽ luôn luôn dẫn tới việc ```re-render``` trừ khi hàm ```shouldComponentUpdate()``` trả lại giá trị ```false```.

  + để tránh việc ```re-render``` lai các component con mà không có sự thay đôi thì ta dùng hàm ```componentWillReceiveProps(nextProps)```. nếu ```nextProps``` giống với ```props``` hiện tại thì sẽ không phải ```re-render```

  + Nhiều khi ta chỉ muốn copy giá trị của ```state```, nhưng nếu ta truyền ```this.setState``` thì nó sẽ làm thay đổi giả trị, trong trường hợp này ta cần copy nó. Ta có thể dùng Immutability Helpers. Nó sẽ tạo ra một thể hiện của ```states``` mình có thể tùy ý sử dụng nó. Sau đó nếu muốn setState thì ta vẫn có thể ```setState``` bình thường.

### III. Vòng đời của một React Component
---

[life-cycle](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/life-cycle.png)

**1. constructor(props)**

- Được gọi khi một thể hiện của component được tạo ra.

- Có thể dùng để khởi tạo state cho component.

- Cũng có thể dùng để "bind" các hàm của component.

- Nếu phải cài đặt hàm này thì phải khai báo 1 tham số props cho nó và phải gọi super(props) đầu tiên.

- Nếu không làm gì thì không phải cài đặt hàm này.

**2. componentWillMount()**

- Được gọi trước khi render().

- Dùng để đăng ký các sự kiện toàn cục.

- Dựa vào các props để tính toán và set lại state

**3. render()**

- Hàm này bắt buộc phải có trong component().

- Trả về 1 đối tượng JSX (có thể lồng các đối tượng với nhau nhưng phải có 1 đối tượng gói tất cả các đối tượng lại) để hiển thị hoặc null / false nếu không muốn hiển thị gì.

- Không được gọi setState() trong hàm này (cũng như trong các hàm mà hàm này gọi đến), bởi khi gọi setState() thì hàm render sẽ được gọi => gây ra lặp vô hạn.

**4. componentDidMount()**

- Ngay sau khi hàm render được gọi đến lần đầu tiên chạy xong thì hàm này sẽ được chạy.

- Thường dùng để fetch dữ liệu từ server và sau đó setState để render dữ liệu ra.

- Đến đây thì các phần tử đã được sinh ra rồi, và có thể tương tác với DOM bằng JS trong hàm này.

**5. componentWillReceiveProps(nextProps)**

- Hàm này được chạy khi mà props của component đã được sinh ra có sự thay đổi.

- Phải gọi setState() nếu muốn render lại.

**6. shouldComponentUpdate(nextProps, nextState)**

- Được gọi trước render.

- Trả về true / false. Nếu false thì sẽ không render lại. Mặc định là true.

**7. componentWillUpdate(nextProps, nextState)**

- Được gọi ngay sau shouldComponentUpdate() nếu hàm này trả về true.

- Không gọi setState() trong hàm này bởi hàm này là để chuẩn bị update cho đối tượng chứ không phải tạo ra 1 update mới, sẽ tạo ra lặp vô hạn.

- Hàm render sẽ được gọi ngay sau hàm này.

**8. componentDidUpdate(prevProps, prevState)**

- Được gọi ngay sau render() từ lần render thứ 2 trở đi.

- Đây cũng là 1 cơ hội để thao tác với các phần tử DOM bằng JS.

**9. componentWillUnmount()**

- Được gọi khi 1 component được loại bỏ khỏi DOM.

- Thực hiện các thao tác dọn dẹp như huỷ các timer, loại bỏ các phần tử thừa, ...
