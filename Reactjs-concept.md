# Các khái niệm căn bản của ReactJS

### 1/Babel là gì

 Babel: cũng là một transpilation tool, đồng thời là một polyfill giúp cho chuyển đổi các hàm mà ES6 có nhưng ES5 chưa có (những hàm này trên ES6 được viết bằng C++). Lý do là rất ít trình duyệt support full ES6 (trừ firefox) nên Babel sẽ cung cấp các hàm này viết bằng JS thuần

### 2/ JSX  là gì

JSX = Javascript + XML 
JSX là một dạng ngôn ngữ cho phép viết các mã HTML trong Javascript. Đặc điểm:

- Faster: Nhanh hơn. JSX thực hiện tối ưu hóa trong khi biên dịch sang mã Javacsript. Các mã này cho thời gian thực hiện nhanh hơn nhiều so với một mã tương đương viết trực tiếp bằng Javascript.
- Safer: An toàn hơn. Ngược với Javascript, JSX là kiểu statically-typed , nghĩa là nó được biên dịch trước khi chạy, giống như Java, C++. Vì thế các lỗi sẽ được phát hiện ngay trong quá trình biên dịch. Ngoài ra, nó cũng cung cấp tính năng gỡ lỗi khi biên dịch rất tốt.
- Easier: Dễ dàng hơn. JSX kế thừa dựa trên Javascript, vì vậy rất dễ dàng để cho các lập trình viên Javascripts có thể sử dụng

|         |       | 
| ------------- |:-------------:|
| Tham khảo | https://coddingdaily.blogspot.com/2015/06/reactjs-bai-3-jsx-la-gi.html |
|  | https://jsx.github.io/ |

>React code server.js Khoa Pham
```javascript
var express = require("express");
var app = express();
app.set("view engine", "ejs");
app.set("views", "./views");
app.use(express.static("publics"));
app.listen(8000);

app.get("/", function(req, res){
	res.render("index");
});
```

>React code index.ejs Khoa Pham

```javascript
<!DOCTYPE html>
<html>
<head>
  <title>[:. Grunt Project Layout .:]</title>
  <meta http-equiv="Content-type" content="text/html;charset=UTF-8">
  <meta name="description" content="mô tả website">
  <meta name="keywords" content="những từ khóa của website bạn">
  <meta name="author" content="daodc">
  <meta name="robots" content="index,follow">
  <meta name="SKYPE_TOOLBAR" content="SKYPE_TOOLBAR_PARSER_COMPATIBLE">
  <meta name="format-detection" content="telephone=no">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <!-- HTML5 Shim and Respond.js IE8 support of HTML5 elements and media queries -->
  <!-- WARNING: Respond.js doesn't work if you view the page via file:// -->
  <!--[if lt IE 9]>
    <script src="https://oss.maxcdn.com/libs/html5shiv/3.7.0/html5shiv.js"></script>
    <script src="https://oss.maxcdn.com/libs/respond.js/1.4.2/respond.min.js"></script>
  <![endif]-->
  <link rel="shortcut icon" href="/images/front/favicon.ico" type="image/x-icon" />
  <link rel="icon" href="/images/front/favicon.ico" type="image/x-icon" />
  <link rel="apple-touch-icon" href="webclip.png" />
  <link rel="apple-touch-icon-precomposed" href="webclip.png" />
  <link rel="stylesheet" href="/css/common.css" type="text/css" media="screen" />
</head>

<body>
  <div class="container">
    <h3>1</h3>
    <div class="alert alert-info" id="demo1"></div>
    <hr />
    <h3>2</h3>
    <div class="alert alert-info" id="demo2"></div>
    <hr />
    <h3>3</h3>
    <div class="alert alert-info" id="demo3"></div>
    <hr />
    <h3>4</h3>
    <div class="alert alert-info" id="demo4"></div>
    <hr />
    <h3>5</h3>
    <div id="demo5" class="clearfix"></div>
    <hr />
    <h3>6</h3>
    <div id="demo6" class="clearfix"></div>
    <hr />
    <h3>7</h3>
    <div id="demo7" class="clearfix"></div>
    <hr />
    <h3>8</h3>
    <div id="demo8" class="clearfix"></div>
    <hr />
    <h3>9</h3>
    <div id="demo9" class="clearfix"></div>
    <hr />
    <h3>10</h3>
    <div id="demo10" class="clearfix"></div>
    <hr />
    <h3>11</h3>
    <div id="demo11" class="clearfix"></div>
    <hr />
    <h3>12</h3>
    <div id="demo12" class="clearfix"></div>
    <hr />
    <h3>13</h3>
    <div id="demo13" class="clearfix p10 mt20 mb20"></div>
    <hr />
    <h3>14</h3>
    <div id="demo14" class="clearfix p10 mt20 mb20"></div>
    <hr />
    <h3>15</h3>
    <div id="demo15" class="clearfix p10 mt20 mb20"></div>
    <hr />
  </div>
  
  <script src="./node_modules/react-dom/dist/react-dom.min.js"></script>
  <script src="./node_modules/react/dist/react.min.js"></script> -->
  <script src="/libs/react.min.js"></script>
  <script src="/libs/react-dom.min.js"></script>
  <script src="/libs/browser.min.js"></script>
  <script src="/libs/react-app.js" type="text/babel"></script>
</body>
</html>

```

>React code react-app.js Khoa Pham
```javascript
/********************************************************************
function getName global
********************************************************************/
function getName(name){
  console.log(name);
}
// Render có nghĩa là render cái gì và vị tris render ở đâu
ReactDOM.render(<h2> I.Nhúng React vào HTML </h2>, 
  document.getElementById('demo1')
);
/********************************************************************
Component Hello
********************************************************************/
var Hello = React.createClass({
  render: function() {
    return <h2> Hello {
      this.props.name
    } </h2>;
  }
});

ReactDOM.render( <Hello name = "World" /> ,
  document.getElementById('demo2')
);

/********************************************************************
Render Show
********************************************************************/
ReactDOM.render(
  React.createElement("h2", {}, "II. Demo JSX( Ko nên sử dụng thế này vì nó mắc công )"),
  document.getElementById("demo3")
);

ReactDOM.render( <h2 className = "label label-success"> Chèn Class vào thẻ tag HTML sử dụng className </h2>,
  document.getElementById("demo4")
);

/********************************************************************
Lồng Component ComponentNestedReact với nhau
********************************************************************/
var ComponentNestedReact = React.createClass({
  render : function(){
    return(
      <div className = "alert alert-info mb20"> Lồng component với nhau</div>
    );
  }
});
var ComponentReact = React.createClass({
  render : function(){
    return(
      <div>
        <div className = "alert alert-danger mb20"> Sử dụng component trong ReactJS </div>
        <ComponentNestedReact />
      </div>
    );
  }
});
ReactDOM.render(
  <div>
    <ComponentReact />
  </div>,
  document.getElementById('demo5')
);

/********************************************************************
Props trong ReactJS
********************************************************************/
var GiangDay = React.createClass({
  getInfo: function(){
    alert(this.props.children);
  },
  render: function(){
    return(
      <div>
        <h2 className="alert alert-success">{this.props.ten} - {this.props.giangvien} - {this.props.children} - <button className="btn btn-default" onClick={this.getInfo}>Get Info</button></h2>        
      </div>
    );
  }
});

ReactDOM.render(
  <div>
    <GiangDay ten="ReactJS" giangvien="Mr.Binh">Mon Hoc ReactJS</GiangDay>
    <GiangDay ten="NodeJS" giangvien="Mr.Dong">Mon Hoc NodeJS</GiangDay>
  </div>,
  document.getElementById('demo6')
);
/********************************************************************
ComponentParameters
- Props là thuộc tính dành cho component, có thể có nhiều props cho 
component trong suốt quá trình ReactJS thì Dao không bao giờ thay đổi
- this chinh la ComponentParameters
********************************************************************/

var ComponentParameters = React.createClass({
  render : function(){
    return(
      <div className="mb15">
        <div className = "alert alert-info mb20">[Props] Ngôn Ngữ Lập Trình {this.props.name} - {this.props.member}</div>
        <p className="pl15">{this.props.children}</p>               
      </div>
    );
  }
});
ReactDOM.render(
  <div>    
    <ComponentParameters name="React JS">Môn Học React JS</ComponentParameters>
    <ComponentParameters name="Node JS">Môn Học Node JS</ComponentParameters>
    <ComponentParameters name="Angular JS">Môn Học Angular JS</ComponentParameters>
  </div>,
  document.getElementById('demo7')
);
/********************************************************************
ComponentCheck
********************************************************************/
var ComponentCheck = React.createClass({
  checkNote: function(){
    console.log(this.props.children);
  },
  render : function(){
    return(
      <span className="mr15">
        <button className="btn btn-primary" onClick={this.checkNote}>Check Mon Hoc</button>
      </span>
    );
  }
});
ReactDOM.render(
  <div>    
    <ComponentCheck>Môn Học React JS</ComponentCheck>
    <ComponentCheck>Môn Học Node JS</ComponentCheck>
    <ComponentCheck>Môn Học Angular JS</ComponentCheck>
  </div>,
  document.getElementById('demo8')
);

/********************************************************************
ComponentGlobal
********************************************************************/
var ComponentGlobal= React.createClass({
  medial(){
    getName(this.props.member);
  },
  render : function(){
    return(
      <div>
        <button className="btn btn-danger ml15" onClick={getName(this.props.member)}>Global Function</button>
        <button className="btn btn-danger ml15" onClick={this.medial}>Global Function</button>
        <button className="btn btn-success ml15" onClick={()=>{getName(this.props.member)}}>Global Function</button>
        <button className="btn btn-info ml15" onClick={()=>{var str =  this.props.name + ' ' + this.props.member; getName(str)}}>Global Function</button>
      </div>
    );
  }
});
ReactDOM.render(
  <div>    
    <ComponentGlobal name="React JS" member="Mr.Dao">Môn Học React JS</ComponentGlobal>
  </div>,
  document.getElementById('demo9')
);
/********************************************************************
ComponentAscending
********************************************************************/
var ComponentAscending= React.createClass({
  addMember(){
    this.setState({sumMember: this.state.sumMember + 1});
  },
  getInitialState(){
    return {
      sumMember: 10
    }
  },
  render : function(){
    return(
      <div>
        <button className="btn btn-info ml15" onClick={this.addMember}>[State]Tăng lên 1</button>
        <div className="p10">[State]Sum member : {this.state.sumMember}</div>
      </div>
    );
  }
});
ReactDOM.render(
  <div>    
    <ComponentAscending>Môn Học React JS</ComponentAscending>
  </div>,
  document.getElementById('demo10')
);
/********************************************************************
ComponentAscendingAgain
********************************************************************/
var ComponentAscendingAgain= React.createClass({
  addMemberAgain(){
    this.state.sumMemberAgain = parseInt(this.state.sumMemberAgain) + 1;
    this.setState(this.state);
  },
  getInitialState(){
    return {
      sumMemberAgain : this.props.sumMemberProps
    }
  },
  render : function(){
    return(
      <div>
        <button className="btn btn-info ml15" onClick={this.addMemberAgain}>[State]Tăng lên 1</button>
        <div className="p10">[State]Sum member Again : {this.state.sumMemberAgain}</div>
      </div>
    );
  }
});
ReactDOM.render(
  <div>
    <ComponentAscendingAgain sumMemberProps="90">Môn Học Ember JS</ComponentAscendingAgain>
  </div>,
  document.getElementById('demo11')
);
/********************************************************************
InputTag
********************************************************************/
var InputTag = React.createClass({
  showInput(){
    var textInput = this.refs.txt.value;
    alert(textInput);
  },
  showSelect(){
    var textSelect = this.refs.sl.value;
    alert(textSelect);
  },
  render : function(){
    return(
      <div className="col-xs-6">
        <select className="form-control mb20" ref="sl">
          <option value="a">AAA</option>
          <option value="b">BBB</option>
          <option value="c">CCC</option>
        </select>
        <div className="input-group">
          <input type="text" ref="txt" className="form-control" />
          <div className="input-group-btn">
            <button type="button" className="btn btn-success" onClick={this.showInput}>Action Input</button>
            <button type="button" className="btn btn-success" onClick={this.showSelect}>Action Select</button>
          </div>
        </div>
      </div>
   );
  }
});
ReactDOM.render(
  <div>
    <InputTag />
  </div>,
  document.getElementById('demo12')
);
/********************************************************************
Com
********************************************************************/
var Com = React.createClass({
  addUnit: function(){
    this.setState({num: this.state.num + 1});
  },
  getInitialState: function(){
    return { num: 0 }
  },
  render: function(){
    return(
      <div>
        <button type="button" className="btn btn-success" onClick={this.addUnit}>Hello {this.state.num}</button>
      </div>
    );
  }
});
ReactDOM.render(
  <div>
    <Com />
  </div>,
  document.getElementById('demo13')
);
/********************************************************************
Album
********************************************************************/
var Album = React.createClass({
  nextPhoto(){
    this.setState({image: this.state.image == 5 ? 5:this.state.image +1});
  },
  prevPhoto(){
    this.setState({image: this.state.image == 1 ? 1:this.state.image -1});
  },
  getInitialState: function(){
    return {image: 1};
  },
  render: function(){
    return(
      <div>
        <div className="text-center">
          <img src={"/images/sliders/" + this.state.image + ".jpg"} alt=""  width="300" height="300" />
        </div>
        <hr />
        <div className="text-center">
          <button onClick={this.prevPhoto} type="button" className="btn btn-primary ml15">Previous</button>
          <button onClick={this.nextPhoto} type="button" className="btn btn-primary ml15">Next</button>
        </div>
      </div>
    )
  }
});
ReactDOM.render(
  <div>
    <Album />
  </div>,
  document.getElementById("demo14")
);

/********************************************************************
SetIntervalSlider
********************************************************************/
var SetIntervalSlider = React.createClass({
  changeImage(){
    this.setState({image : (this.state.image%5)+1});
  },
  getInitialState(){
    return {image: 1}
  },
  render: function(){
    return (
      <div>
        <hr />
        <div className="text-center">
          <img src={"/images/sliders/" + this.state.image+".jpg"} alt=""  width="300" height="300" />
        </div>
      </div>
    )
  },
  componentDidMount(){
    setInterval(this.changeImage, 1000);
  }
});
ReactDOM.render(
  <div>
    <SetIntervalSlider />
  </div>,
  document.getElementById('demo15')
);

```
