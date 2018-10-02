#### 1. CSS multiline text with ellipsis
---
**Reference :**

- [http://hackingui.com/front-end/a-pure-css-solution-for-multiline-text-truncation/](http://hackingui.com/front-end/a-pure-css-solution-for-multiline-text-truncation/)

- [https://css-tricks.com/line-clampin/](https://css-tricks.com/line-clampin/)

- [http://codepen.io/martinwolf/pen/qlFdp](http://codepen.io/martinwolf/pen/qlFdp)

**HTML :**

```html
<h2>Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et.</h2>
```

**CSS :**

```javascript
h2 {
  display: block;
  /* Fallback for non-webkit */
  display: -webkit-box;
  max-width: 400px;
  height: 109.2px;
  /* Fallback for non-webkit */
  margin: 0 auto;
  font-size: 26px;
  line-height: 1.4;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
  text-overflow: ellipsis;
}
```

#### 2. Thuộc tính css3 mới: 

#### 2. 1 CSS background-blend-mode Property

```javascript
div { 
    width: 200px;
    height: 200px;
    background-size: 200px 200px;
    background-repeat:no-repeat;
    background-image: linear-gradient(to right, black 0%, white 100%), url('w3css.gif');
    background-blend-mode: color-dodge;
}
```

##### CSS Syntax

```javascript
background-blend-mode: normal|multiply|screen|overlay|darken|lighten|color-dodge|saturation|color|luminosity;
```

#### 2. 2. object-fit

```html
<div class="image">
  <p>object-fit: cover</p>
  <img class="object-fit_cover" src="https://s3-us-west-2.amazonaws.com/s.cdpn.io/14179/image.png">
</div>
```
##### CSS Syntax

```javascript
object-fit: | contain | cover | none | scale-down
```

#### 2. 3. object-position

```javascript

```
#### 2. 4. image-orientation

```javascript

```
#### 2.5. image-rendering

```javascript

```
#### 2.6. image-resolution

```javascript

```

#### 3. width fit-content

```javascript 
.center ul{
    width: -moz-fit-content;
    width: -webkit-fit-content;
    width: fit-content;
    margin: auto;   
} 
```

#### 4. ```-webkit-overflow-scrolling``` Khi style ```scroll``` cho một phần tử với ```overflow: auto``` thì nên để giá trị này vào:
- Thuộc tính CSS ```-webkit-overflow-scrolling``` kiểm soát xem thiết bị cảm ứng có sử dụng cuộn dựa trên động lượng cho một phần tử đã cho hay không..

```javascript 
.table-responsive {
  display: block;
  width: 100%;
  overflow-x: auto;
  -webkit-overflow-scrolling: touch;
  -ms-overflow-style: -ms-autohiding-scrollbar;
}
} 
```

#### 5 Flexbox Techniques You Need to Know About

#### 1. Mobile
---

>**1. Nếu làm Responsive cho Mobile thì nên set các thuộc tính dưới đây:**

html{
    -webkit-text-size-adjust: 100%;
      -ms-text-size-adjust: 100%;
}
* {
    -webkit-box-sizing: border-box;
    -moz-box-sizing: border-box;
    box-sizing: border-box;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    -webkit-tap-highlight-color: transparent;
}

>**1. Nếu làm Popop up cho Mobile, thì nên set thuộc tính này trong vùng scroll**
2. 
.modal{
  -webkit-overflow-scrolling: touch;
}

#### CSS Tips
---
**1. Five Ways to Hide Elements in CSS**

  **1.1. Opacity**

  >HTML
  ```
  <div>1</div>
  <div class="o-hide">2</div>
  <div>3</div>
  ```

  >CSS
  ```
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

  **1.2. Visibility**

  >HTML
  ```
  <div>1</div>
  <div class="o-hide"><p>2</p></div>
  <div>3</div>
  ```

  >CSS
  ```
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

  >JS
  ```javascript
  var oHide = document.querySelector(".o-hide");
  var oHideP = document.querySelector(".o-hide p");
  var count = oHideP.innerHTML;
  oHide.addEventListener("click", function(){
    count++;
    oHideP.innerHTML = count;
  });
  ```

  **1.3. Display**

  >HTML
  ```
  <div>Hover!</div>
  <div class="o-hide"><p>0</p></div>
  <div>0</div>
  ```

  >CSS
  ```
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

  >JS
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

  **1.4. Position**

  >HTML
  ```
  <div>Hover!</div>
  <div class="o-hide"><p>0</p></div>
   <div>0</div>
  ```

  >CSS
  ```
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

  >JS
  ```
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

  **1.5. Clip-path**

  >HTML
  ```
  <div>Hover!</div>
  <div class="o-hide">0</div>
  <div>0</div>
  ```

  >CSS
  ```
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

  >JS
  ```
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
  **2 .Equal item tag ```<li>```**

  >CSS
  ```
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

  **3. Centering CSS**


  **4. CSS Property: ```background-image```**

    - You can specify more than one background image by separating each value using a comma. The image you set first will be displayed on the top layer.
  
    ```
    background-image:
      url("https://preview.ibb.co/iaBzBm/butterflies.png"),
      url("https://preview.ibb.co/eaasWm/grey.png");
    ```

  **5. Không nên nhầm lẫn giữa ```<b>``` với các thẻ ```<strong>```, ```<em>``` hay ```<mark>```**

    - **```<b>```**: Đơn thuần chỉ là để làm đậm văn bản mà không truyền đạt thêm thông tin ngữ nghĩa nào
    - **```<strong>```**: Dùng để thể hiện tầm quan trọng của đoạn văn bản đặt trong nó.
    - **```<em>```**: Đặt một mức độ nhấn mạnh nào đó vào văn bản trong nó.
    - **```<mark>```**: Dùng để thể hiện phần văn bản liên quan trong nó.
  
  **6. CSS Unit:**

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
   
   >6.5 **PX, PT**: 
   
   >6.6 **%**:
   
   >6.6 **In**:
  
**7. Advanced Text Styling and Positioning with CSS(3)**

  **Refer:** https://developer.mozilla.org/en-US/docs/Web/CSS/writing-mode

  - The **writing-mode** CSS property defines whether lines of text are laid out horizontally or vertically, as well as the direction in which blocks progress.

  **Syntax**

    ```
    /* Keyword values */
    writing-mode: horizontal-tb;
    writing-mode: vertical-rl;
    writing-mode: vertical-lr;

    /* Global values */
    writing-mode: inherit;
    writing-mode: initial;
    writing-mode: unset;
    ```

  - The ```writing-mode``` property is specified as one of the values listed below.
  - ```horizontal-tb``` Content flows horizontally from left to right, vertically from top to bottom. The next horizontal line is positioned below the previous line.
  - ```vertical-rl```: Content flows vertically from top to bottom, horizontally from right to left. The next vertical line is positioned to the left of the previous line.
  - ```vertical-lr``` Content flows vertically from top to bottom, horizontally from left to right. The next vertical line is positioned to the right of the previous line.
  - ```sideways-rl``` Content flows vertically from top to bottom and all the glyphs, even those in vertical scripts, are set sideways toward the right.
  - ```sideways-lr``` Content flows vertically from top to bottom and all the glyphs, even those in vertical scripts, are set sideways toward the left.
  - ```lr``` Deprecated except for SVG1 documents. For CSS, use horizontal-tb instead.
  - ```lr-```*: Deprecated except for SVG1 documents. For CSS, use horizontal-tb instead.
  - ```rl``` Deprecated except for SVG1 documents. For CSS, use horizontal-tb instead.
  - ```tb``` Deprecated except for SVG1 documents. For CSS, use vertical-lr instead.
  - ```tb-rl``` Deprecated except for SVG1 documents. For CSS, use vertical-rl instead.

  >**HTML**
  - The HTML is simply a ```<table>``` with each writing mode in a row with a column showing text in various scripts using that writing mode.
    
  ```
  <table>
    <tr>
      <th>Value</th>
      <th>Vertical script</th>
      <th>Horizontal script</th>
      <th>Mixed script</th>
    </tr>
    <tr>
      <td>horizontal-tb</td>
      <td class="example Text1"><span>我家没有电脑。</span></td>
      <td class="example Text1"><span>Example text</span></td>
      <td class="example Text1"><span>1994年に至っては</span></td>
    </tr>
    <tr>
      <td>vertical-lr</td>
      <td class="example Text2"><span>我家没有电脑。</span></td>
      <td class="example Text2"><span>Example text</span></td>
      <td class="example Text2"><span>1994年に至っては</span></td>
    </tr>
    <tr>
      <td>vertical-rl</td>
      <td class="example Text3"><span>我家没有电脑。</span></td>
      <td class="example Text3"><span>Example text</span></td>
      <td class="example Text3"><span>1994年に至っては</span></td>
    </tr>
    <tr>
      <td>sideways-lr</td>
      <td class="example Text4"><span>我家没有电脑。</span></td>
      <td class="example Text4"><span>Example text</span></td>
      <td class="example Text4"><span>1994年に至っては</span></td>
    </tr>
    <tr>
      <td>sideways-rl</td>
      <td class="example Text5"><span>我家没有电脑。</span></td>
      <td class="example Text5"><span>Example text</span></td>
      <td class="example Text5"><span>1994年に至っては</span></td>
    </tr>
  </table>
  ```

  >**CSS**
  - The CSS that adjusts the directionality of the content looks like this:

```
  .example.Text1 span, .example.Text1 {
    writing-mode: horizontal-tb;
    -webkit-writing-mode: horizontal-tb;
    -ms-writing-mode: horizontal-tb;
  }

  .example.Text2 span, .example.Text2 {
    writing-mode: vertical-lr;
    -webkit-writing-mode: vertical-lr;
    -ms-writing-mode: vertical-lr;
  }

  .example.Text3 span, .example.Text3 {
    writing-mode: vertical-rl;
    -webkit-writing-mode: vertical-rl;
    -ms-writing-mode: vertical-rl;
  }

  .example.Text4 span, .example.Text4 {
    writing-mode: sideways-lr;
    -webkit-writing-mode: sideways-lr;
    -ms-writing-mode: sideways-lr;
  }

  .example.Text5 span, .example.Text5 {
    writing-mode: sideways-rl;
    -webkit-writing-mode: sideways-rl;
    -ms-writing-mode: sideways-rl;
  }
```

  Reference: ![alt text](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/writing-mode-actual-result.png)

**8.:first-letter**

  https://css-tricks.com/almanac/properties/w/writing-mode/

**8. Scroll**

- Khi scroll window muốn neo(anchor) một thành phần thì hãy sử dụng ```postion: sticky```.
- Sticky: Phần tử được định vị dựa trên vị trí cuộn của người dùng.
- Một element ```sticky``` toggles giữa ```relative``` and ```fixed```, tùy thuộc vào vị trí di chuyển. Nó được định vị tương đối cho đến khi một vị trí bù đắp nhất định được đáp ứng trong khung nhìn - sau đó nó "dính" tại chỗ (như ```position:fixed```).
- Không hỗ trợ trong ```IE/Edge 15``` hoặc cũ hơn. Được hỗ trợ trong Safari từ phiên bản 6.1 với ```-webkit- prefix```.

```
<img class="sticky" src="img_avatar.png" alt="Avatar">
img.sticky {
  position: -webkit-sticky;
  position: sticky;
  top: 0;
  width: 200px;
}
```

**8. Filter**

[Apply A filter to a background image](https://css-tricks.com/apply-a-filter-to-a-background-image/)
