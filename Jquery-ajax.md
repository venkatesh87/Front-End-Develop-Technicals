### JS AJAX
---
- AJAX là nghệ thuật trao đổi dữ liệu với máy chủ và cập nhật các phần của trang web - mà không cần tải lại toàn bộ trang.
AJAX = Asynchronous JavaScript And XML.
- **responseTxt** - chứa nội dung kết quả nếu cuộc gọi thành công
- **statusTxt** - chứa trạng thái của cuộc gọi
- **xhr** - chứa đối tượng XMLHttpRequest

```javascript
$(document).ready(function() {
  $("button").click(function() {
    $("#div1").load("demo_test.txt");
  });
});
```

**1. jQuery - AJAX load() Method**

```javascript
$(document).ready(function() {
  $("button").click(function() {
    $("#div1").load("demo_test.txt #p1");
  });
});
```

- Ví dụ sau sẽ hiển thị một hộp cảnh báo sau khi phương thức load () hoàn tất. Nếu phương thức load () đã thành công, nó sẽ hiển thị "External content loaded thành công!", Và nếu nó thất bại, nó sẽ hiển thị một thông báo lỗi:

```javascript
$("button").click(function() {
  $("#div1").load("demo_test.txt", function(responseTxt, statusTxt, xhr) {
    if (statusTxt == "success")
      alert("External content loaded successfully!");
    if (statusTxt == "error")
      alert("Error: " + xhr.status + ": " + xhr.statusText);
  });
});
```

**jQuery - AJAX get() and post() Methods**

- Các phương thức ```get()``` và ```post()``` của jQuery được sử dụng để yêu cầu dữ liệu từ máy chủ với yêu cầu ```HTTP``` ```GET``` hoặc ```POST```.
- **GET** - Yêu cầu dữ liệu từ một tài nguyên được chỉ định. GET về cơ bản được sử dụng để chỉ nhận (lấy) một số dữ liệu từ máy chủ. Lưu ý: Phương thức GET có thể trả về dữ liệu được lưu trong bộ nhớ cache.
- **POST** - Gửi dữ liệu được xử lý đến một tài nguyên được chỉ định. POST cũng có thể được sử dụng để lấy một số dữ liệu từ máy chủ. Tuy nhiên, phương thức POST KHÔNG BAO GIỜ lưu trữ dữ liệu và thường được sử dụng để gửi dữ liệu cùng với yêu cầu.

**jQuery $.get() Method**: ```$.get(URL,callback);```

```javascript
$("button").click(function() {
  $.get("demo_test.asp", function(data, status) {
    alert("Data: " + data + "\nStatus: " + status);
  });
});
```

**jQuery $.post() Method**: ```$.post(URL,data,callback);```

```javascript
$("button").click(function() {
  $.post("demo_test_post.asp", {
      name: "Donald Duck",
      city: "Duckburg"
    },
    function(data, status) {
      alert("Data: " + data + "\nStatus: " + status);
    });
});
```

- Gửi một id dưới dạng dữ liệu đến máy chủ, lưu một số dữ liệu vào máy chủ và thông báo cho người dùng khi nó hoàn tất. Nếu yêu cầu không thành công, hãy thông báo cho người dùng.

```javascript
var menuId = $( "ul.nav" ).first().attr( "id" );
var request = $.ajax({
  url: "script.php",
  method: "POST",
  data: { id : menuId },
  dataType: "html"
});
 
request.done(function( msg ) {
  $( "#log" ).html( msg );
});
 
request.fail(function( jqXHR, textStatus ) {
  alert( "Request failed: " + textStatus );
});
```
- Tải và thực thi một tệp JavaScript.

```javascript
$.ajax({
  method: "GET",
  url: "test.js",
  dataType: "script"
});
```

- Lưu một số dữ liệu vào máy chủ và thông báo cho người dùng khi nó hoàn tất.

```javascript
$.ajax({
  method: "POST",
  url: "some.php",
  data: { name: "John", location: "Boston" }
}).done(function(msg) {
  alert("Data Saved: " + msg);
});
```

- Chỉ cần sử dụng 1 hàm này có thể đáp ứng các yêu cầu về thực thi ajax.

```javascript
$('#load-data').click(function(e) {
  e.preventDefault();
  $.ajax({
    url: 'example.php',
    type: 'POST',
    dataType: 'html',
    data: {
      a: "content abc",
      b: "content bcd"
    }
  }).done(function(result) {
    $('#content').html(result);
  });
});
```

1. **url : chuỗi chứa đường dẫn tới file cần lấy và trả về dữ liệu
2. **type : phương thức gửi đi tương tự như của ```<form>```, mặc định là ```GET``` nếu như các bạn không truyền vào.
3. **dataType : xác định dữ liệu trả về thuộc dạng nào? Nếu các bạn không truyền thì jQuery tự động nhận biết kiểu dữ liệu (script, html, json…). Tuy nhiên, tôi khuyến cáo các bạn nên truyền vào đầy đủ để nhận dữ liệu chính xác nhất. Và thông dụng nhất chính là ```html```.
4. **data : truyền dữ liệu sang đường dẫn chỉ định để thực hiện xử lý và trả về dữ liệu. Tương tự như cách truyền dữ liệu của phương thức ```post()```.
5.**done()** : ở loạt các bài viết hướng dẫn các bài viết về kĩ thuật Ajax với phương thức ``` ajax() ``` trước đây trên Internet. Thay vì dùng ```done()``` chúng ta sẽ dùng thuộc tính ```success``` trong đối tượng truyền vào ```ajax()``` nhưng từ các phiên bản mới hơn của jQuery. Họ khuyến cáo chúng ta nên sử dụng các phương thức như ```done() , fail() , always()``` (Tương ứng: Hoàn thành, thất bại và luôn luôn thực hiện). Nên tùy vào nhu cầu mà bạn xài phương thức tương ứng. Và nên nhớ là đi kèm với phương thức ```ajax()``` hoặc lưu vào một tên biến rồi dùng sau để nhận kết quả trả về.

```javascript
jQuery.ajax({
  type: "POST",
  url: url,
  contentType: "application/json",
  dataType: "json",
  data: "SaveRequestingData",
  success: function(resp, status, xhr) {
    alert('in success JSON');
    var msg = "result is: " + resp.result + ", Start: " + resp.start + ", End: " + resp.end + ", issues: " + resp.issues;
    alert(msg);
    jQuery("#successPost").html(msg + " - STATUS: " + xhr.status + " " + xhr.statusText);
  },
  error: function(resp, status, xhr) {
    alert('in error json');
    alert("Error: " + resp.e);
    jQuery("#errorPost").html("Error: " + resp.e + " - STATUS: " + xhr.status + " " + xhr.statusText);
  }
});
```

```javascript
$.ajax({
  url: "/Data.ashx",
  type: "post",
  dataType: "json",
  success: function(d, a, c) {
    console.log(typeof d);
    console.log(d, a, c);
    console.log(d.name);
  },
  error: function(d, a, c) {
    console.log(d, a, c)
  }
})
```


