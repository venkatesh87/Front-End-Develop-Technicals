##### 1. Code JavaScript Flag :
---

>**Case 1:**
```javascript
  window.DEBUG = true;

  function log(a, b, c, d) {
       if(DEBUG) {
           console.log(a, b, c, d);
       }
  } 

  if(DEBUG) {
      // Do dev stuff
  } else {
     // Do produection stuff
  }

  log("foobar") // Does not need to be wrapper, as log() itself is functional only in debug mode    
```

>**Case 2:** 

```javascript
var is_playing = true;
if (is_playing) {
  player.pauseVideo();
  playButton.className += " disable";
} else {
  player.playVideo();
  playButton.className = playButton.className.replace('disable', '');
}
```     

##### 2. Check active:
---

>**Switch class active:**

>**Case 1**
```javascript

```

>**Case 5:** Loop active Javascript

**HTML**
```javascript
<ul>
  <li class="panel active">Item 1</li>
  <li class="panel">Item 2</li>
  <li class="panel">Item 3</li>
</ul>
```

**JS**
```javascript
$(function() {
  var lis_count = $('li.panel').length;
  var active_li_index = 0;

  setInterval(function() {
    if ($('li.panel.active').index() == lis_count - 1)
      active_li_index = 0;
    else
      active_li_index++;

    $('li.panel.active').removeClass('active');
    $('li.panel').eq(active_li_index).addClass('active');
  }, 1000);
})
```

```javascript
document.addEventListener('DOMContentLoaded', function() {
  var lis = Array.prototype.slice.call(document.querySelectorAll('li.panel'));
  var lis_count = lis.length;
  var active_li_index = 0;

  setInterval(function() {
    var active_li = document.querySelector('li.panel.active');

    if (lis.indexOf(active_li) == lis_count - 1)
      active_li_index = 0;
    else
      active_li_index++;

    active_li.classList.remove('active');
    document.querySelectorAll('li.panel')[active_li_index].classList.add('active');
  }, 1000);
}, false);
```

**CSS**
```javascript
.active {
  background - color: yellow;
}
```

##### 3. Check length element :
---
>**Case 1: length-of-a-javascript-string**
```javascript
var str = "Hello World!";
var n = str.length;
```

>**Case 2: length-of-a-javascript-object** 

```javascript
Object.size = function(obj) {
  var size = 0,
    key;
  for (key in obj) {
    if (obj.hasOwnProperty(key)) size++;
  }
  return size;
};

// Get the size of an object
var size = Object.size(myArray);

```     

```javascript
Object.keys(myObject).length
```  

##### 4. Object :
---
>**Length of a JavaScript object (or associative array)**

>**The most robust answer:**
```javascript
var myArray = new Object();
myArray["firstname"] = "Gareth";
myArray["lastname"] = "Simpson";
myArray["age"] = 21;

Object.size = function(obj) {
    var size = 0, key;
    for (key in obj) {
        if (obj.hasOwnProperty(key)) size++;
    }
    return size;
};
// Get the size of an object
var size = Object.size(myArray);
```
>**- Here's an update as of 2016 and widespread deployment of ES5 and beyond. For IE9+ and all other modern ES5+ capable browsers, you can use Object.keys() so the above code just becomes:**

```javascript
var size = Object.keys(myObj).length;
```
>**- If you know you don't have to worry about hasOwnProperty checks, you can do this very simply:**

```javascript
Object.keys(myArray).length
```

>**Use something as simple as:**

```javascript
Object.keys(obj).length
```
##### 5. Keyboard
---

>**Disable F12 Key in a Page**

```javascript
document.onkeypress = function (event) {  
  event = (event || window.event);  
  if (event.keyCode == 123) {  
    return false;  
  }                                                           
}  
document.onkeydown = function (event) {  
  event = (event || window.event);  
  if (event.keyCode == 123) {  
    return false;  
  }  
}
```

>**Disable Ctrl+U Key in a Page**

```javascript
document.onkeydown = function(e) {
  if (e.ctrlKey &&
    (e.keyCode === 67 ||
      e.keyCode === 86 ||
      e.keyCode === 85 ||
      e.keyCode === 117)) {
    alert('not allowed');
    return false;
  } else {
    return true;
  }
};
```

>**Disable View Page Source Key in a Page Right Click Mouse**

```javascript
<body oncontextmenu="return false">
```

>**Disable keyboard Ctrl+S:**

```javascript
document.onkeydown = function (e) {
    e = e || window.event;//Get event
    if (e.ctrlKey) {
        var c = e.which || e.keyCode;//Get key code
        switch (c) {
            case 83://Block Ctrl+S
                e.preventDefault();     
                e.stopPropagation();
            break;
        }
    }
};
```

>**Rendering a simple list of products with jQuery:**

```javascript
var products = [
  {
    id: 1,
    name: 'Book',
    price: 15
  },
  {
    id: 2,
    name: 'Burrito',
    price: 8
  },
  {
    id: 3,
    name: 'Spaceship',
    price: 999999999
  },
  {
    id: 4,
    name: 'Dinosaur Bones',
    price: 5000000
  }
];

function buyProduct(productId) {
  // buy the product
}

/* -- Just jQuery -- */
function buyButtonJquery(product) {
  var button = $('<button class="buy-button">$' + product.price
    + '</button>');
  
  // handle click event
  $(button).on('click', function(event) {
    event.preventDefault();
    buyProduct(product.id);
  });

  return button;
}

function productListJustJquery(products, element) {
  var list = $('<ul class="product-list"></ul>');

  products.forEach(function(product) {
    var item = $('<li>' + product.name + '</li>');
    item.append(buyButtonJquery(product));
    list.append(item);
  });

  // replace the existing list if there is one
  var currentList = $(element).find('.product-list');
  if (currentList.length) {
    currentList.replaceWith(list);
  } else {
    $(element).append(list);
  }
}
```

##### 5. Scroll
---
>**Case 1: ```document.body.scrollTop > 20 || document.documentElement.scrollTop```**
```javascript
window.onscroll = function() {
    if ($(window).width() < 700) {
        navSticky();
    }
};
function navSticky() {
  if (document.body.scrollTop > 20 || document.documentElement.scrollTop > 20) {
    $('.navigation_top').addClass('sticky');
  } else {
    $('.navigation_top').removeClass('sticky');
  }
}
```
>**Case 2:** Scroll Indicator
```javascript
// When the user scrolls the page, execute myFunction 
window.onscroll = function() {myFunction()};

function myFunction() {
  var winScroll = document.body.scrollTop || document.documentElement.scrollTop;
  var height = document.documentElement.scrollHeight - document.documentElement.clientHeight;
  var scrolled = (winScroll / height) * 100;
  document.getElementById("myBar").style.width = scrolled + "%";
}
```

>**```window.pageYOffset```**
```javascript

```

##### 6 ```e.target``` jQuery. 
---
```javascript
$('#headerCorporateLogo').on("click", function() {
  $('.userMenu').stop(true, true).slideToggle();
});

$('#headerBtnSettings').on("click", function() {
  $('.settingsMenu').stop(true, true).slideToggle();
});

$(document).on('click', function(e) {
  // ２．クリックされた場所の判定
  // console.log($(e.target).closest('#headerCorporateLogo').length );
  // console.log($(e.target).closest('.userMenu').length);
  // console.log(!$(e.target).closest('#headerCorporateLogo').length && !$(e.target).closest('.userMenu').length);

  if(!$(e.target).closest('#headerCorporateLogo').length && !$(e.target).closest('.userMenu').length){
    $('.userMenu').fadeOut();
  }
  if(!$(e.target).closest('#headerBtnSettings').length && !$(e.target).closest('.settingsMenu').length){
    $('.settingsMenu').fadeOut();
  }
});
```
##### 7. 5 Tips to Write Better Conditionals in JavaScript
---
- Khi làm việc với JavaScript, chúng tôi xử lý rất nhiều điều kiện, đây là 5 mẹo để bạn viết điều kiện tốt hơn / sạch hơn.

**1. Sử dụng Array.includes cho nhiều tiêu chí**
- Thoạt nhìn, ví dụ trên có vẻ tốt. Tuy nhiên, điều gì sẽ xảy ra nếu chúng ta nhận được nhiều trái cây màu đỏ hơn, nói cherry và cranberries? Chúng ta sẽ mở rộng tuyên bố với nhiều hơn || ?
```javascript
// condition
function test(fruit) {
  if (fruit == 'apple' || fruit == 'strawberry') {
    console.log('red');
  }
}
```

- Chúng ta có thể viết lại điều kiện ở trên bằng cách sử dụng ```Array.includes``` (Array.includes)
```javascript
function test(fruit) {
  // extract conditions to array
  const redFruits = ['apple', 'strawberry', 'cherry', 'cranberries'];

  if (redFruits.includes(fruit)) {
    console.log('red');
  }
}
```

**2. Ít Nesting, trở về sớm**
- Hãy mở rộng ví dụ trước để bao gồm hai điều kiện nữa:
  + Nếu không có trái cây cung cấp, ```throw error``` ném lỗi.
  + Chấp nhận và in số lượng quả nếu vượt quá 10.
```javascript
function test(fruit, quantity) {
  const redFruits = ['apple', 'strawberry', 'cherry', 'cranberries'];

  // condition 1: fruit must has value
  if (fruit) {
    // condition 2: must be red
    if (redFruits.includes(fruit)) {
      console.log('red');

      // condition 3: must be big quantity
      if (quantity > 10) {
        console.log('big quantity');
      }
    }
  } else {
    throw new Error('No fruit!');
  }
}

// test results
test(null); // error: No fruits
test('apple'); // print: red
test('apple', 20); // print: red, big quantity
```

- Nhìn vào đoạn mã trên, chúng ta có:
  + Câu lệnh 1 if / other lọc ra điều kiện không hợp lệ
  + 3 mức lồng nhau nếu câu lệnh (điều kiện 1, 2 & 3)
- Một quy tắc chung mà cá nhân tôi tuân theo là trở về sớm khi tìm thấy điều kiện không hợp lệ.

```javascript
/_ return early when invalid conditions found _/

function test(fruit, quantity) {
  const redFruits = ['apple', 'strawberry', 'cherry', 'cranberries'];

  // condition 1: throw error early
  if (!fruit) throw new Error('No fruit!');

  // condition 2: must be red
  if (redFruits.includes(fruit)) {
    console.log('red');

    // condition 3: must be big quantity
    if (quantity > 10) {
      console.log('big quantity');
    }
  }
}
```

- Bằng cách này, chúng ta có một mức độ ít hơn của câu lệnh lồng nhau. Phong cách mã hóa này là tốt đặc biệt là khi bạn có câu lệnh if dài (hãy tưởng tượng bạn cần cuộn xuống phía dưới cùng để biết có một câu lệnh khác, không hay).
- Chúng ta có thể giảm thêm việc làm tổ nếu, bằng cách đảo ngược các điều kiện và quay lại sớm. Nhìn vào điều kiện 2 dưới đây để xem cách chúng tôi làm điều đó:

```javascript
/_ return early when invalid conditions found _/

function test(fruit, quantity) {
  const redFruits = ['apple', 'strawberry', 'cherry', 'cranberries'];

  if (!fruit) throw new Error('No fruit!'); // condition 1: throw error early
  if (!redFruits.includes(fruit)) return; // condition 2: stop when fruit is not red

  console.log('red');

  // condition 3: must be big quantity
  if (quantity > 10) {
    console.log('big quantity');
  }
}
```

- Bằng cách đảo ngược các điều kiện của điều kiện 2, mã của chúng tôi hiện không có câu lệnh lồng nhau. Kỹ thuật này rất hữu ích khi chúng ta có logic dài và chúng ta muốn dừng quá trình tiếp theo khi một điều kiện không được đáp ứng.
- Tuy nhiên, đó không phải là quy tắc cứng để làm điều này. Hãy tự hỏi, phiên bản này (không lồng nhau) tốt hơn / dễ đọc hơn phiên bản trước (điều kiện 2 với lồng nhau)?
- Đối với tôi, tôi sẽ chỉ để nó như phiên bản trước (điều kiện 2 với lồng nhau). Đó là vì:
  + Mã ngắn và thẳng về phía trước, rõ ràng hơn với lồng nhau nếu
  + Điều kiện đảo ngược có thể phát sinh quá trình suy nghĩ nhiều hơn (tăng tải nhận thức)
- Do đó, luôn luôn nhắm đến việc ít làm tổ và trở về sớm nhưng đừng lạm dụng nó. Có một bài viết & thảo luận về StackOverflow sẽ nói thêm về chủ đề này nếu bạn quan tâm:

**3. Use Default Function Parameters and Destructuring:** Sử dụng các tham số chức năng mặc định và phá hủy

- Tôi đoán mã bên dưới có thể trông quen thuộc với bạn, chúng tôi luôn cần kiểm tra giá trị null / không xác định và gán giá trị mặc định khi làm việc với JavaScript:

```javascript
function test(fruit, quantity) {
  if (!fruit) return;
  const q = quantity || 1; // if quantity not provided, default to one

  console.log(`We have ${q} ${fruit}!`);
}

//test results
test('banana'); // We have 1 banana!
test('apple', 2); // We have 2 apple!
```

- Trong thực tế, chúng ta có thể loại bỏ biến ```q``` bằng cách gán các tham số hàm mặc định.

```javascript
function test(fruit, quantity = 1) { // if quantity not provided, default to one
  if (!fruit) return;
  console.log(`We have ${quantity} ${fruit}!`);
}

//test results
test('banana'); // We have 1 banana!
test('apple', 2); // We have 2 apple!
```

- Dễ dàng hơn nhiều và trực quan phải không? Xin lưu ý rằng mỗi tham số có thể có tham số chức năng mặc định riêng. Ví dụ: chúng ta cũng có thể gán giá trị mặc định cho trái cây:

```
function test(fruit = 'unknown', quantity = 1).
```
- Nếu trái cây của chúng ta là một đối tượng thì sao? Chúng ta có thể gán tham số mặc định?
```
function test(fruit) { 
  // printing fruit name if value provided
  if (fruit && fruit.name)  {
    console.log (fruit.name);
  } else {
    console.log('unknown');
  }
}

//test results
test(undefined); // unknown
test({ }); // unknown
test({ name: 'apple', color: 'red' }); // apple
```
- Nhìn vào ví dụ trên, chúng tôi muốn in tên trái cây nếu có hoặc chúng tôi sẽ in không xác định. Chúng ta có thể tránh việc kiểm tra ```fruit && fruit.name``` có điều kiện với tham số chức năng mặc định & hủy.

```javascript
// destructing - get name property only
// assign default empty object {}
function test({name} = {}) {
  console.log (name || 'unknown');
}

//test results
test(undefined); // unknown
test({ }); // unknown
test({ name: 'apple', color: 'red' }); // apple
```

- Dưới đây là một ví dụ về việc sử dụng Lodash:
```javascript
// Include lodash library, you will get _
function test(fruit) {
  console.log(__.get(fruit, 'name', 'unknown'); // get property name, if not available, assign default value 'unknown'
}

//test results
test(undefined); // unknown
test({ }); // unknown
test({ name: 'apple', color: 'red' }); // apple
```

**4. Favor Map / Object Literal than Switch Statement:** Bản đồ ủng hộ / Đối tượng theo nghĩa đen hơn là Tuyên bố chuyển đổi
- Hãy xem ví dụ dưới đây, chúng tôi muốn in trái cây dựa trên màu sắc:

```javascript
function test(color) {
  // use switch case to find fruits in color
  switch (color) {
    case 'red':
      return ['apple', 'strawberry'];
    case 'yellow':
      return ['banana', 'pineapple'];
    case 'purple':
      return ['grape', 'plum'];
    default:
      return [];
  }
}

//test results
test(null); // []
test('yellow'); // ['banana', 'pineapple']
```

- Đoạn mã trên có vẻ không có gì sai, nhưng tôi thấy nó khá dài dòng. Kết quả tương tự có thể đạt được với đối tượng bằng chữ với cú pháp sạch hơn:

```javascript
// use object literal to find fruits in color
  const fruitColor = {
    red: ['apple', 'strawberry'],
    yellow: ['banana', 'pineapple'],
    purple: ['grape', 'plum']
  };

function test(color) {
  return fruitColor[color] || [];
}

```

- Ngoài ra, bạn có thể sử dụng Bản đồ để đạt được kết quả tương tự:

```javascript
// use Map to find fruits in color
  const fruitColor = new Map()
    .set('red', ['apple', 'strawberry'])
    .set('yellow', ['banana', 'pineapple'])
    .set('purple', ['grape', 'plum']);

function test(color) {
  return fruitColor.get(color) || [];
}
```

**TL; DR; Tái cấu trúc cú pháp**
- Đối với ví dụ trên, chúng ta thực sự có thể cấu trúc lại mã của mình để đạt được kết quả tương tự với ```Array.filter```.

```javascript
const fruits = [
    { name: 'apple', color: 'red' }, 
    { name: 'strawberry', color: 'red' }, 
    { name: 'banana', color: 'yellow' }, 
    { name: 'pineapple', color: 'yellow' }, 
    { name: 'grape', color: 'purple' }, 
    { name: 'plum', color: 'purple' }
];

function test(color) {
  // use Array filter to find fruits in color

  return fruits.filter(f => f.color == color);
}
```
- Luôn có nhiều hơn 1 cách để đạt được kết quả tương tự. Chúng tôi đã chỉ ra 4 với ví dụ tương tự. Viết mã là niềm vui! 5. Sử dụng Array.every

**5. Use Array.every & Array.some for All / Partial Criteria:** Sử dụng Array.every & Array.some cho tất cả / Tiêu chí từng phần

- Mẹo cuối cùng này là về việc sử dụng chức năng Javascript Array mới (nhưng không quá mới) để giảm các dòng mã. Nhìn vào mã dưới đây, chúng tôi muốn kiểm tra xem tất cả các loại trái cây có màu đỏ không:

```javascript
const fruits = [
    { name: 'apple', color: 'red' },
    { name: 'banana', color: 'yellow' },
    { name: 'grape', color: 'purple' }
  ];

function test() {
  let isAllRed = true;

  // condition: all fruits must be red
  for (let f of fruits) {
    if (!isAllRed) break;
    isAllRed = (f.color == 'red');
  }

  console.log(isAllRed); // false
}
```
- Mã quá dài! Chúng tôi có thể giảm số lượng dòng với Array.every:

```javascript
const fruits = [
    { name: 'apple', color: 'red' },
    { name: 'banana', color: 'yellow' },
    { name: 'grape', color: 'purple' }
  ];

function test() {
  // condition: short way, all fruits must be red
  const isAllRed = fruits.every(f => f.color == 'red');

  console.log(isAllRed); // false
}
```
- Bây giờ sạch hơn nhiều phải không? Theo cách tương tự, nếu chúng ta muốn kiểm tra xem có bất kỳ quả nào có màu đỏ hay không, chúng ta có thể sử dụng Array.some để đạt được nó trong một dòng.

```javascript
const fruits = [
    { name: 'apple', color: 'red' },
    { name: 'banana', color: 'yellow' },
    { name: 'grape', color: 'purple' }
];

function test() {
  // condition: if any fruit is red
  const isAnyRed = fruits.some(f => f.color == 'red');

  console.log(isAnyRed); // true
}
```


