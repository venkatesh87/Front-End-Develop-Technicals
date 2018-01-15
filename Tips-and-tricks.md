# 1. Five Ways to Hide Elements in CSS

  1a. Opacity
  ---

  > HTML
  ```javascript
  <div>1</div>
    <div class="o-hide">2</div>
  <div>3</div>
  ```
  > CSS
  ```javascript
  div {
    padding: 60px;
    width: 60px;
    font-size: 3em;
    background: pink;
    text-align: center;
    margin: 1%;
    display: inline-block;
    float: left;
    cursor: pointer;
    font-family: 'Lato';
  }

  .o-hide {
    opacity: 0;
    transition: all ease 0.8s;
  }

  .o-hide:hover {
    opacity: 1;
  }
  ```

  1b. Visibility
  ---
  > HTML
  ```javascript
  <div>1</div>
  <div class="o-hide"><p>2</p></div>
  <div>3</div>
  ```
  > CSS
  ```javascript
  div {
    padding: 60px;
    width: 60px;
    font-size: 3em;
    background: pink;
    text-align: center;
    margin: 1%;
    display: inline-block;
    float: left;
    cursor: pointer;
    font-family: 'Lato';
  }

  .o-hide {
    visibility: hidden;
    transition: all ease 0.8s;
  }

  .o-hide:hover {
    visibility: visible;
  }

  .o-hide p {
    visibility: visible;
    margin: 0;
    padding: 0;
  }
  ```

  > JS
  ```javascript
  var oHide = document.querySelector(".o-hide");
  var oHideP = document.querySelector(".o-hide p");
  var count = oHideP.innerHTML;

  oHide.addEventListener("click", function(){
    count++;
    oHideP.innerHTML = count;
  });
  ```
1c. Display
---
  > HTML
  ```javascript
  <div>Hover!</div>
  <div class="o-hide"><p>0</p></div>
  <div>0</div>
  ```
  > CSS
  ```javascript
  div {
    height: 60px;
    padding: 60px 0;
    width: 180px;
    font-size: 2em;
    line-height: 60px;
    background: pink;
    text-align: center;
    margin: 1%;
    display: block;
    float: left;
    cursor: pointer;
    font-family: 'Lato';
  }

  .o-hide {
    display: none;
    transition: all ease 0.8s;
  }

  .o-hide:hover {
    display: block;
  }

  .o-hide p {
    display: block;
    margin: 0;
    padding: 0;
  }
  ```
  > JS
  ```javascript
  var count = 0;
  var oHide = document.querySelector(".o-hide");
  var firstDiv = document.querySelector("div:nth-child(1)");

  firstDiv.addEventListener("mouseover", function(){
    count++;
    oHide.innerHTML = '<p>' + count + '</p>';
  });

  firstDiv.addEventListener("click", function(){
    oHide.style.display = "block";
  });
  ```
  1d. Position
  ---
  > HTML
  ```javascript
  <div>Hover!</div>
  <div class="o-hide"><p>0</p></div>
   <div>0</div>
  ```
  > CSS
  ```javascript
  div {
    height: 60px;
    padding: 60px 0;
    width: 180px;
    font-size: 2em;
    line-height: 60px;
    background: pink;
    text-align: center;
    margin: 1%;
    display: block;
    float: left;
    cursor: pointer;
    font-family: 'Lato';
  }

  .o-hide {
    position: absolute;
    top: -9999px;
    left: -9999px;
  }

  .o-hide:hover {
    position: static;
  }
  ```
  > JS
  ```javascript
  var count = 0;
  var oHide = document.querySelector(".o-hide");
  var firstDiv = document.querySelector("div:nth-child(1)");

  firstDiv.addEventListener("mouseover", function(){
    count++;
    oHide.innerHTML = count;
  });

  firstDiv.addEventListener("click", function(){
      oHide.style.position = "static";
  });
  ```

  1e. Clip-path
  ---
  > HTML
  ```javascript
  <div>Hover!</div>
  <div class="o-hide">0</div>
  <div>0</div>
  ```

  > CSS
  ```javascript
  div {
    height: 60px;
    padding: 60px 0;
    width: 180px;
    font-size: 2em;
    line-height: 60px;
    background: pink;
    text-align: center;
    margin: 1%;
    display: block;
    float: left;
    cursor: pointer;
    font-family: 'Lato';
  }

  .o-hide {
    clip-path: polygon(0px 0px, 0px 0px, 0px 0px, 0px 0px);
  }
  ```

  > JS
  ```javascript
  var count = 0;
  var oHide = document.querySelector(".o-hide");
  var firstDiv = document.querySelector("div:nth-child(1)");

  firstDiv.addEventListener("mouseover", function(){
      count++;
      oHide.innerHTML = count;
  });


  firstDiv.addEventListener("click", function(){
      oHide.className = "";
  });
  ```
  # 2 .Equal item tag ```<li>```

  > CSS
  ```javascript
  li{
    padding:8px 0;
    width:339px;
    font-size:0.915em;
    min-height:37px;
    display:-moz-inline-stack;
    display:inline-block;
    vertical-align:top;
    zoom:1;
    *display:inline;
  }
  ```

  3 . Centering CSS
  ---

  4 . CSS Property: background-image
  ---
  - You can specify more than one background image by separating each value using a comma. The image you set first will be displayed on the top layer.
  ```javascript
  background-image:
    url("https://preview.ibb.co/iaBzBm/butterflies.png"),
    url("https://preview.ibb.co/eaasWm/grey.png");
  ```
  5. Không nên nhầm lẫn giữa <b> với các thẻ <strong>, <em> hay <mark>
  ---
  - **```<b>```**: Đơn thuần chỉ là để làm đậm văn bản mà không truyền đạt thêm thông tin ngữ nghĩa nào
  - **```<strong>```**: Dùng để thể hiện tầm quan trọng của đoạn văn bản đặt trong nó.
  - **```<em>```**: Đặt một mức độ nhấn mạnh nào đó vào văn bản trong nó.
  - **```<mark>```**: Dùng để thể hiện phần văn bản liên quan trong nó.
  
  6 . CSS Unit: 
  ---
  >6.1 **vw & vh**: 
  
  - Sử dụng vh, vw khi bạn muốn sử dụng chiều rộng hoặc chiều cao của khung nhìn thay vì chiều rộng của phần tử gốc
    - ```1 vw = 1%``` chiều ngang của trình duyệt.
    - ```1 vh = 1%``` chiều cao của trình duyệt.
    - Nó khác biệt với ```%``` ở chỗ, khi dùng % thì phần thử con set height ```%``` nó thừa hưởng height của cấp cha gần nhất với nó.
    - Còn đối với ```vh``` và ```vw``` nó thừa hưởng từ cấp root(html) tức là bạn cứ hiểu cái trình duyệt của bạn hay điện thoại bạn rộng bao nhiêu thì nó sẽ lấy bấy nhiêu đó làm ```%``` để tính cho đối tượng mà bạn muốn qui định.
    - Phần tử vh bằng 1/100 chiều cao của khung nhìn
    
  >6.2 **vmin and vmax**: 
  
  - vmin và vmax có liên quan đến chiều cao và chiều rộng tối đa hoặc tối thiểu, tùy thuộc vào kích thước nhỏ hơn và lớn hơn. Ví dụ: nếu trình duyệt được đặt chiều rộng 1100px và chiều cao 700px, 1vmin sẽ là 7px và 1vmax sẽ là 11px. Tuy nhiên, nếu chiều rộng được đặt là 800px và chiều cao đặt là 1080px, vmin sẽ bằng 8px trong khi vmax sẽ được đặt thành 10.8px.
  
  >6.3 **ex & ch**:
  
  >6.4 **rem & em**:
  
  >6.5 **inch**:
