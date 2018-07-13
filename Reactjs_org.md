#### I. Hello World
---

>JavaScript Code:
```javascript
ReactDOM.render(
  <h1>Hello World</h1>,
  document.getElementById('demo1')
);
```

#### II. Introducing JSX
---

**.1.Khai báo biến**

```javascript
const element = <h1>Hello, world!</h1>;

**2.Embedding Expressions in JSX(Nhúng biểu thức trong JSX)**

```javascript
const name = 'Dang Cong Dao';
const element1 = <h1>Hello {name}</h1>;
ReactDOM.render(
  element1,
  document.getElementById('demo2')
);
```

**3.JavaScript expression**

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

**4.JSX is an Expression Too**

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
**6.1 Nếu thẻ trống, bạn có thể đóng thẻ ngay lập tức bằng />, như XML:**
const element5 = <img src={user.avatarUrl} />;
**6.2 Thẻ JSX có thể chứa children**
```javascript
const element6 = (
  <div>
    <h1>Hello!</h1>
    <h2>Good to see you here.</h2>
  </div>
);
```
** 7.JSX Represents Objects**

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

- React.createElement () thực hiện một vài kiểm tra để giúp bạn viết mã không có lỗi nhưng về cơ bản nó tạo ra một đối tượng như thế này:

```javascript
const element9 = {
  type: 'h1',
  props: {
    className: 'greeting',
    children: 'Hello, world!'
  }
};
```

#### III. Rendering Elements
---
- .
>JavaScript Code:
```javascript

```

#### IV. Components and Props
---
- .
>JavaScript Code:
```javascript

```

#### V. State and Lifecycle(vòng đời)
---
- .
>JavaScript Code:
```javascript

```

#### VI. Handling Events: Xử lý sự kiện
---
- .
>JavaScript Code:
```javascript

```

#### VII. Conditional Rendering(Hiển thị có điều kiện)
---
- .
>JavaScript Code:
```javascript

```

#### VIII. Lists and Keys: Danh sách và khóa
---
- .
>JavaScript Code:
```javascript

```

#### IX. 
---
- .
>JavaScript Code:
```javascript

```

#### X. 
---
- .
>JavaScript Code:
```javascript

```


