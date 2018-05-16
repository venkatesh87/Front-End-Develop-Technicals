#### I. Javascript Design Patterns Singleton
---

**1. Singleton là gì**
- Trong trường hợp bạn không quen với mẫu đơn, thì cốt lõi của nó là một mẫu thiết kế hạn chế sự khởi tạo của một lớp đối với một đối tượng. Thông thường, mục tiêu là quản lý trạng thái ứng dụng toàn cầu. Một số ví dụ tôi đã thấy hoặc viết bản thân mình bao gồm việc sử dụng singleton làm nguồn cài đặt cấu hình cho ứng dụng web, phía khách hàng cho bất kỳ thứ gì được bắt đầu bằng khóa API (bạn thường không muốn mạo hiểm gửi nhiều cuộc gọi theo dõi phân tích, ví dụ), và để lưu trữ dữ liệu trong bộ nhớ trong một ứng dụng web phía máy khách (ví dụ các cửa hàng trong Flux).

- Một singleton nên được bất biến bởi mã tiêu thụ, và sẽ không có nguy cơ instantiating nhiều hơn một trong số họ.

>**The Old Way of Creating a Singleton in JavaScript: ** Cách cũ để tạo Singleton trong JavaScript

```javascript
var UserStore = (function(){
  var _data = [];

  function add(item){
    _data.push(item);
  }

  function get(id){
    return _data.find((d) => {
      return d.id === id;
    });
  }

  return {
    add: add,
    get: get
  };
}());
```

- Khi mã đó được diễn giải, UserStore sẽ được đặt thành kết quả của hàm được gọi ngay lập tức đó - một đối tượng hiển thị hai hàm, nhưng điều đó không cấp quyền truy cập trực tiếp vào tập hợp dữ liệu.

**2. The New Way(s)**

- Bằng cách tận dụng các tính năng của ES6, chủ yếu là các mô-đun và khai báo biến const mới, chúng ta có thể viết các trình đơn theo những cách không chỉ ngắn gọn hơn mà còn đáp ứng tốt hơn các yêu cầu của chúng ta.
- Hãy bắt đầu với việc triển khai cơ bản nhất. Dưới đây là cách giải thích hiện đại (gọn gàng hơn và mạnh hơn) của ví dụ trên:

```javascript
const _data = [];

const UserStore = {
  add: item => _data.push(item),
  get: id => _data.find(d => d.id === id)
}

Object.freeze(UserStore);
export default UserStore;
```

- Dưới đây là cách triển khai sẽ trông như thế nào nếu chúng tôi muốn sử dụng các lớp ES6:
- [Object.freeze](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/freeze)

```javascript
class UserStore {
  constructor(){
    this._data = [];
  }

  add(item){
    this._data.push(item);
  }

  get(id){
    return this._data.find(d => d.id === id);
  }
}

const instance = new UserStore();
Object.freeze(instance);

export default instance;
```

- Nhưng giả sử bạn muốn chắc chắn hơn rằng không ai làm rối tung sự đơn độc của singleton của bạn, và bạn cũng muốn nó phù hợp với việc thực hiện các singletons trong thế giới hướng đối tượng thậm chí còn chặt chẽ hơn. Đây là điều bạn có thể làm:
- [ Object.assign.](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign)

```javascript
class UserStore {
  constructor(){
   if(! UserStore.instance){
     this._data = [];
     UserStore.instance = this;
   }

   return UserStore.instance;
  }

 //rest is the same code as preceding example

}

const instance = new UserStore();
Object.freeze(instance);

export default instance;
```
