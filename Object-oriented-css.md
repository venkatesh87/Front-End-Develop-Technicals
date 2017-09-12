## OOCSS (CSS hướng đối tượng):
- Nhằm giúp hạn chế khả năng trùng lặp CSS(Don’t Repeat Yourself), cũng như dễ bảo dưỡng nếu sau này có nhu cầu sửa lại.

## I. Tách biệt cấu trúc/giao diện :

Đây chính là nguyên tắc đầu tiên, không viết các thuộc tính liên quan tới giao diện(background, border, color…), cấu trúc (position, float, margin, padding….) vào 1 class. Ví dụ trên giao diện của bạn có màu đỏ thì bạn nên có 1 class riêng là .red và nó có thể sử dụng ở rất nhiều nơi. Bởi lẽ cái button, link, footer cũng có thể có màu đỏ.

## II. Tách biệt container và content :

Bạn đã bao giờ gặp trường hợp box search đang được để trên header nhưng giờ chuyển xuống footer thì bỗng dưng bị vỡ style. Điều này có nghĩa là box search(content) đang bị phụ thuộc vào khung chứa nó là cái header (container). Nguyên tắc 2 ám chỉ rằng bạn không nên để những trường hợp như vậy xảy ra. Giờ ta đi sâu vào ví dụ cụ thể cho dễ hiểu.
Làm theo cách này bạn sẽ thấy mã HTML của mình phức tạp hơn vì nó có nhiều class hơn, nhưng về lâu dài chúng ta có thể tạo ra các phần tử mà không cần động chạm nhiều đến css. Nếu muốn một section heading trên trang html mới, bạn chỉ cần sử dụng class section-heading, hay nếu cần một thẻ ul không có các bullet thì chỉ cần dùng item-list.

## Bình thường :

``` html
<aside>
<h1>Latest News</h1>
<ul>
<li>
<h3><a href="”#”">Lorem Ipsum Dolor</a></h3>
<p>Lorem ipsum dolor sit amet, consectetur adipiscing elit.</p>
</li>
<li>
<h3><a href="”#”">Lorem Ipsum Dolor</a></h3>
<p>Lorem ipsum dolor sit amet, consectetur adipiscing elit.</p>
</li>
<li>
<h3><a href="”#”">Lorem Ipsum Dolor</a></h3>
<p>Lorem ipsum dolor sit amet, consectetur adipiscing elit.</p>
</li>
</ul>
</aside>
```

``` javascript
aside {
float: right;
width: 15em;
padding: 2em;
}

aside h1 {
margin: 0;
font-size: 1.25em;
border-bottom: 1px dashed #ccc;
}

aside ul {
margin: 0;
padding: 0;
list-style: none;
}

aside ul li {
margin: 1em 0;
padding-bottom: .5em;
border-bottom: 1px dashed #ccc;
}

aside h3 {
margin: 0;
font-size: 1em;
}

aside h3 a {
color: #000;
text-decoration: none;
}

aside h3 a:hover {
color: #1c86a1;
}

aside p {
margin: .5em 0;
font-size: .938em;
line-height: 1.188em;
}
```

## Kiểu OOCSS:

``` html
<aside class="cont-right">
<h1 class="section-heading no-margin separated">Latest News</h1>
<ul class="item-list no-margin">
<li class="item-list--item separated">
<h3 class="area-heading no-margin"><a href="”#”">Lorem Ipsum Dolor</a></h3>
<p class="item-content">Lorem ipsum dolor sit amet, consectetur adipiscing elit.</p>
</li>
<li class="item-list--item separated">
<h3 class="area-heading no-margin"><a href="”#”">Lorem Ipsum Dolor</a></h3>
<p class="item-content">Lorem ipsum dolor sit amet, consectetur adipiscing elit.</p>
</li>
<li class="item-list--item separated">
<h3 class="area-heading no-margin"><a href="”#”">Lorem Ipsum Dolor</a></h3>
<p class="item-content">Lorem ipsum dolor sit amet, consectetur adipiscing elit.</p>
</li>
</ul>
</aside>
```

``` javascript
.cont-right {
float: right;
width: 15em;
padding: 2em;
}

.section-heading {
font-size: 1.25em;
}

.separated {
border-bottom: 1px dashed #ccc;
}

.no-margin {
margin: 0;
}

.item-list {
padding: 0;
list-style: none;
}

.item-list--item {
margin: 1em 0;
padding-bottom: .5em;
}

.area-heading {
font-size: 1em;
}

.area-heading a {
color: #000;
text-decoration: none;
}

.area-heading a:hover {
color: #1c86a1;
}

.item-content {
margin: .5em 0;
font-size: .938em;
line-height: 1.188em;
}
```

## HTML :

```html
<div class="box box1"></div>
<div class="box box2"></div>
```

## CSS :

```javascript
.box {
width: 25%;
height: 150px;
float: left;
}

.box1 { background: red }
.box2 { background: blue }
```
## HTML:

```html
<aside class="cont-right">
<h1 class="section-heading no-margin separated">Latest News</h1>
<ul class="item-list no-margin">
<li class="item-list--item separated">
<h3 class="area-heading no-margin"><a href="”#”">Lorem Ipsum Dolor</a></h3>
<p class="item-content">Lorem ipsum dolor sit amet, consectetur adipiscing elit.</p>
</li>
<li class="item-list--item separated">
<h3 class="area-heading no-margin"><a href="”#”">Lorem Ipsum Dolor</a></h3>
<p class="item-content">Lorem ipsum dolor sit amet, consectetur adipiscing elit.</p>
</li>
<li class="item-list--item separated">
<h3 class="area-heading no-margin"><a href="”#”">Lorem Ipsum Dolor</a></h3>
<p class="item-content">Lorem ipsum dolor sit amet, consectetur adipiscing elit.</p>
</li>
</ul>
</aside>
```

## CSS :

```javascript
.cont-right {
float: right;
width: 15em;
padding: 2em;
}

.section-heading {
font-size: 1.25em;
}

.separated {
border-bottom: 1px dashed #ccc;
}

.no-margin {
margin: 0;
}

.item-list {
padding: 0;
list-style: none;
}

.item-list--item {
margin: 1em 0;
padding-bottom: .5em;
}

.area-heading {
font-size: 1em;
}

.area-heading a {
color: #000;
text-decoration: none;
}

.area-heading a:hover {
color: #1c86a1;
}

.item-content {
margin: .5em 0;
font-size: .938em;
line-height: 1.188em;
}
```