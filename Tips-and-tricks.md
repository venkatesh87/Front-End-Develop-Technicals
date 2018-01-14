# 1 .Five Ways to Hide Elements in CSS

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
