### HTML5 Web Storage
---
**Reference**: https://www.taniarascia.com/how-to-use-local-storage-with-javascript/

> **1. Local Storage**

```javascripts
// Lưu dữ liệu vào local store hiện tại
localStorage.setItem("username", "John");
// Truy cập một số dữ liệu được lưu trữ
alert( "username = " + localStorage.getItem("username"));
```

- Đoạn mã sau truy cập đối tượng Lưu trữ cục bộ của miền hiện tại và thêm mục dữ liệu vào đối tượng đó bằng cách sử dụng ```Storage.setItem()```.

```javascripts
localStorage.setItem('myCat', 'Tom');
```

- Cú pháp để đọc mục ```localStorage``` như sau:

```javascripts
var cat = localStorage.getItem('myCat');
```

- Cú pháp để loại bỏ mục ```localStorage``` như sau:

```javascripts
localStorage.removeItem('myCat');
```

- Cú pháp để loại bỏ tất cả các mục ```localStorage``` như sau:

```javascripts
// clear all items
localStorage.clear();
```
