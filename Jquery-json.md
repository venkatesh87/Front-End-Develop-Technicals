### JS JSON
---

- JSON: JavaScript Object Notation.
- JSON is a syntax for storing and exchanging data.
- JSON is text, written with JavaScript object notation.

#### jQuery getJSON() Method

- Nhận dữ liệu JSON bằng cách sử dụng yêu cầu AJAX và xuất kết quả:
- **Syntax:** $(selector).getJSON(url,data,success(data,status,xhr))
  + url	Required. Chỉ định url để gửi yêu cầu đến 13 dữ liệu Tùy chọn. Chỉ định dữ liệu được gửi đến máy chủ.
  + success(data,status,xhr)	Optional. Chỉ định hàm chạy nếu yêu cầu thành công
  + data - chứa dữ liệu được trả về từ máy chủ.
  + status - chứa một chuỗi chứa trạng thái yêu cầu ("success", "notmodified", "error", "timeout", or "parsererror").
xhr - chứa đối tượng ```XMLHttpRequest```

```javascript
$("button").click(function() {
  $.getJSON("demo_ajax_json.js", function(result) {
    $.each(result, function(i, field) {
      $("div").append(field + " ");
    });
  });
});
```
- Đây là một hàm Ajax viết tắt, tương đương với:

```javascript
$.ajax({
  dataType: "json",
  url: url,
  data: data,
  success: success
});
```

- Hầu hết các triển khai sẽ chỉ định một trình xử lý thành công:

```javascript
$.getJSON("ajax/test.json", function(data) {
  var items = [];
  $.each(data, function(key, val) {
    items.push("<li id='" + key + "'>" + val + "</li>");
  });

  $("<ul/>", {
    "class": "my-new-list",
    html: items.join("")
  }).appendTo("body");
});
```

```javascript
// Assign handlers immediately after making the request,
// and remember the jqxhr object for this request
var jqxhr = $.getJSON("example.json", function() {
    console.log("success");
  })
  .done(function() {
    console.log("second success");
  })
  .fail(function() {
    console.log("error");
  })
  .always(function() {
    console.log("complete");
  });

// Perform other work here ...

// Set another completion function for the request above
jqxhr.complete(function() {
  console.log("second complete");
});
```

- Tải bốn hình ảnh gần đây nhất của Mount Rainier từ API JSONr của Flickr. 

```javascript
(function() {
  var flickerAPI = "https://api.flickr.com/services/feeds/photos_public.gne?jsoncallback=?";
  $.getJSON(flickerAPI, {
      tags: "mount rainier",
      tagmode: "any",
      format: "json"
    })
    .done(function(data) {
      $.each(data.items, function(i, item) {
        $("<img>").attr("src", item.media.m).appendTo("#images");
        if (i === 3) {
          return false;
        }
      });
    });
})();
```

```javascript
$.getJSON("test.js", function(json) {
  console.log("JSON Data: " + json.users[3].name);
});

$.getJSON("test.js", { name: "John", time: "2pm" })
  .done(function(json) {
    console.log("JSON Data: " + json.users[3].name);
  })
  .fail(function(jqxhr, textStatus, error) {
    var err = textStatus + ", " + error;
    console.log("Request Failed: " + err);
});
```

##### jQuery.parseJSON():
- Việc sử dụng JSON phổ biến là trao đổi dữ liệu đến / từ một máy chủ web.
- Khi nhận dữ liệu từ máy chủ web, dữ liệu luôn là chuỗi.
- Phân tích cú pháp dữ liệu bằng ```JSON.parse()``` và dữ liệu trở thành đối tượng JavaScript.
- Hãy tưởng tượng chúng tôi đã nhận được văn bản này từ một máy chủ web:
- Sử dụng hàm JavaScript ```JSON.parse()``` để chuyển đổi văn bản thành đối tượng JavaScript:

```javascript
'{ "name":"John", "age":30, "city":"New York"}'
```

- Tạo đối tượng từ chuỗi JSON

```javascript
var txt = '{"name":"John", "age":30, "city":"New York"}'
var obj = JSON.parse(txt);
document.getElementById("demo").innerHTML = obj.name + ", " + obj.age;
```

```javascript
var xmlhttp = new XMLHttpRequest();
xmlhttp.onreadystatechange = function() {
  if (this.readyState == 4 && this.status == 200) {
    var myObj = JSON.parse(this.responseText);
    document.getElementById("demo").innerHTML = myObj.name;
  }
};
xmlhttp.open("GET", "json_demo.txt", true);
xmlhttp.send();
```

-Khi sử dụng JSON.parse () trên một JSON có nguồn gốc từ một mảng, phương thức sẽ trả về một mảng JavaScript, thay vì một đối tượng JavaScript. 

```javascript
var xmlhttp = new XMLHttpRequest();
xmlhttp.onreadystatechange = function() {
  if (this.readyState == 4 && this.status == 200) {
    var myArr = JSON.parse(this.responseText);
    document.getElementById("demo").innerHTML = myArr[0];
  }
};
xmlhttp.open("GET", "json_demo_array.txt", true);
xmlhttp.send();
```

