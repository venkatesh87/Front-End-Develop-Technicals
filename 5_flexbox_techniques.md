## 5 Flexbox Techniques You Need to Know About

#### 1. Creating Equal Height Columns

**Reference :**
- [Css-Tricks](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)

> **HTML :**

```html
<div class="container">
    <!-- Equal height columns -->
    <div>...</div>
    <div>...</div>
    <div>...</div>
</div>
```

> **CSS :**

```javascript
.container {
        /* Initialize the flex model */
    display: flex;

        /* These are the default values but you can set them anyway */
    flex-direction: row;    /* Items inside the container will be positioned horizontally */
        align-items: stretch;   /* Items inside the container will take up it's entire height */
}
```

#### 2. Reordering Elements

> **HTML :**

```html
<div class="container">

    <!-- These items will appear in reverse order -->

    <div class="blue">...</div>
    <div class="red">...</div>
    <div class="green">...</div>
</div>
```

> **CSS:**

```javascript
.container{
    display: flex;
}

/* Reverse the order of elements */

.blue{
    order: 3;
}

.red{
    order: 2;
}

.green{
    order: 1;
}
```

#### 3. Horizontal And Vertical Centering

```html
<div class="container">
    <!-- Any element placed here will be centered
         both horizonally and vertically -->
    <div>...</div>
</div>
```

> **CSS:**

```javascript
.container{
    display: flex;

    /* Center according to the main axis */
    justify-content: center;

    /* Center according to the secondary axis */
        align-items: center;
}
```


#### 4. Creating Fully Responsive Grids

```html
<div class="container">

    <!-- This column will be 25% wide -->
    <div class="col-1">...</div>

    <!-- This column will be 50% wide -->
    <div class="col-2">...</div>

    <!-- This column will be 25% wide -->
    <div class="col-1">...</div>

</div>
```

> **CSS:**

```javascript
.container{
    display: flex;
}

/* Classes for each column size. */

.col-1{
    flex: 1;
}

.col-2{
    flex: 2;
}

@media (max-width: 800px){
    .container{
        /* Turn the horizontal layout into a vertical one. */
        flex-direction: column;     
    }
}
```


#### 5. Creating The Perfect Sticky Footer

```html
<body>

    <!-- All the page content goes here  -->

    <div class="main">...</div>

    <!-- Our sticky foooter -->

    <footer>...</footer>

</body>
```

> **CSS:**

```javascript
html{
    height: 100%;
}

body{
    display: flex;
    flex-direction: column;
    height: 100%;
}

.main{
   /* The main section will take up all the available free space
      on the page that is not taken up by the footer. */
   flex: 1 0 auto;
}

footer{
   /* The footer will take up as much vertical space as it needs and not a pixel more. */
   flex: 0 0 auto;
}
```

#### 6. Flex centering item and ziczac column

![Image flex ziczac](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/css-flex-ziczac.jpg)

>**HTML**

```javascript
<div class="intro-list">
  <div class="intro-item">
    <div class="intro-flex">
      <div class="intro-col">
        <div class="intro-caption">
          <h3 class="intro-heading">
            <a href="#">Tổng quan</a>
          </h3>
          <p class="para-intro">Trung tâm đào tạo thiết kế chuyên nghiệp iDesign với sứ mệnh đào tạo và cung cấp nguồn nhân lực chất lượng cao cho ngành thiết kế đồ họa, thiết kế web và thiết kế nội thất cho thị trường Đà Nẵng và khu vực miền trung. Đồng thời tạo ra cơ hội việc làm cho các bạn trẻ đam mê chuyên ngành thiết kế.</p>
          <p>Với mong muốn tạo ra các đội ngũ chuyên nghiệp trong các lĩnh vực này, iDesign cam kết đem đến các chương trình đào tạo chất lượng, hiệu quả và giúp các bạn trẻ có được việc làm ổn định và phát triển nghề nghiệp lâu dài.</p>
          <p>Chúng tôi cam kết: Đã học là có việc làm.</p>
        </div>
      </div>
      <div class="intro-col">
        <figure class="figure-image">
          <img src="app/images/photos/img_intro_1.jpg" alt="" width="550" height="364">
        </figure>
      </div>
    </div>
  </div>
  <!--end intro-item-->
  <div class="intro-item">
    <div class="intro-flex">
      <div class="intro-col">
        <div class="intro-caption">
          <h3 class="intro-heading">
            <a href="#">Ưu điểm của iDesign</a>
          </h3>
          <ul class="info_list">
            <li><a href="#">Học để làm việc</a></li>
            <li><a href="#">Làm việc với các chuyên gia</a></li>
            <li><a href="#">Cập nhật kiến thức, công nghệ mới nhất</a></li>
            <li><a href="#">Có kinh nghiệm làm dự án khi đang học</a></li>
            <li><a href="#">Thời gian học ngắn, chi phí ít, biết nhiều</a></li>
            <li><a href="#">Cam kết hỗ trợ tìm việc cho đến khi có việc làm</a></li>
            <li><a href="#">Bảo đảm nghề nghiệp trong 3 năm sau tốt nghiệp</a></li>
          </ul>
        </div>
      </div>
      <div class="intro-col">
        <figure class="figure-image">
          <img src="app/images/photos/img_intro_2.jpg" alt="" width="550" height="364">
        </figure>
      </div>
    </div>
  </div>
  <!--end intro-item-->
  <div class="intro-item">
    <div class="intro-flex">
      <div class="intro-col">
        <div class="intro-caption">
          <h3 class="intro-heading">
            <a href="#">Đội ngũ giảng viên</a>
          </h3>
          <p class="para-intro">Đội ngũ giảng viên quy tụ những chuyên gia làm việc lâu năm trong ngành thiết kế và có nhiều kinh nghiệm trong các lĩnh vực thu hút nhân lực hiện nay. </p>
          <p>Các giáo viên hầu hết có thâm niên thực hiện dự án liên quan đến khóa học và có kinh nghiệm truyền đạt, hướng dẫn để giúp bạn dễ dàng tiếp cận các kiến thức, kỹ năng và kinh nghiệm.</p>
        </div>
      </div>
      <div class="intro-col">
        <figure class="figure-image">
          <img src="app/images/photos/img_intro_3.jpg" alt="" width="550" height="364">
        </figure>
      </div>
    </div>
  </div>
  <!--end intro-item-->
  <div class="intro-item">
    <div class="intro-flex">
      <div class="intro-col">
        <div class="intro-caption">
          <h3 class="intro-heading">
            <a href="#">Phương pháp giảng dạy</a>
          </h3>
          <p class="para-intro">Phương pháp giảng dạy đa phương thức, kết hợp giữa lý thuyết, thực hành, rèn luyện kỹ năng và chia sẻ kinh nghiệm từ các chuyên gia.</p>
          <p>Với quan điểm trên chúng tôi tin tưởng sẽ giúp được nhiều bạn trẻ thành công trong việc lựa chọn và phát triển nghề nghiệp, đồng thời góp phần giải quyết những khó khăn về nhân lực cho ngành thiết kế hiện nay.</p>
        </div>
      </div>
      <div class="intro-col">
        <figure class="figure-image">
          <img src="app/images/photos/img_intro_4.jpg" alt="" width="550" height="364">
        </figure>
      </div>
    </div>
  </div>
  <!--end intro-item-->
</div>
<!--end intro-list-->
```

>**Css**
```javascript
.intro-list {
  padding: 0;
  margin: 0;
  list-style: none;
  .intro-item {
    margin: 0 -22px;
    padding: 30px 0;
    .intro-flex {
      @include flexbox();
      -webkit-flex-flow: row wrap;
      flex-flow: row wrap;
      align-items: center;
      justify-content: center;
      .intro-col{
        padding: 0 22px;
        float: left;
        width: 49.8%;
        @media (max-width: 1180px) {
          padding: 0 15px;
        }
        @media (max-width: 690px) {
          width: 100%;
          float: none;
        }
      }
    }
    &:nth-child(even) {
      .intro-flex {
        flex-direction: row-reverse;
      }
    }
    @media (max-width: 1180px) {
      margin: 0 -15px;
    }
    @media (max-width: 1050px) {
      padding: 20px 0;
    }
    @media (max-width: 690px) {
      padding: 0 0 10px;
    }
  }
}
```

#### 7. Grid with flex

```javascript

```

#### 8. ý nghĩa của flex-flow column

```javascript

```

#### 9. Equal height item with flex

```javascript

```
