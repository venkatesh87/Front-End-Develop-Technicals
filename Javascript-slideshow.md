#### I. JavaScript array - Exercises, Practice, Solution
---
##### Slideshow:
- **indexOf() String**: Phương thức ```indexOf()``` trả về vị trí của lần xuất hiện đầu tiên của một giá trị được chỉ định trong một chuỗi.
- **indexOf() Array**: Phương thức ```indexOf()``` tìm kiếm mảng cho mục được chỉ định và trả về vị trí(position) của nó.

>Javascript Code:
```javascript
var slider = document.querySelector('.sliders');
var slide_arr = Array.prototype.slice.call(slider.querySelectorAll('.item_slide'));
var count = slide_arr.length;
var active_index = 0;

setInterval(function() {
  var is_active = slider.querySelector('.active');
  if (slide_arr.indexOf(is_active) == count - 1) {
    active_index = 0;
  } else {
    active_index++;
  }
  is_active.classList.remove('active');
  slide_arr[active_index].classList.add('active');
}, 2000);
```

>HTML Code:
```javascript
<ul class="sliders">
  <li class="item_slide active"><img src="img/images/slider_1.jpg" alt=""></li>
  <li class="item_slide"><img src="img/images/slider_2.jpg" alt=""></li>
  <li class="item_slide"><img src="img/images/slider_3.jpg" alt=""></li>
  <li class="item_slide"><img src="img/images/slider_4.jpg" alt=""></li>
  <li class="item_slide"><img src="img/images/slider_5.jpg" alt=""></li>
</ul>
```

>CSS:
```javascript
.item_slide {
  position: absolute;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  opacity: 0;
  z-index: 1;
  -webkit-transition: opacity 1s;
  -moz-transition: opacity 1s;
  -o-transition: opacity 1s;
  transition: opacity 1s;
}
.item_slide.active {
  opacity: 1;
  z-index: 2;
}
```

##### Slideshow Play/Pause:
- Chú ý phép chia ```%``` lấy phần dư có kết quả như sau, 1%5 = 1, 2%5 = 2, ..., 6%5 = 1.
>Javascript Code:
```javascript
var playing = true;
var current_slide = 0;
var slides = document.querySelectorAll('.sliders .item_slide');
var pause = document.getElementById('pause');
slide_interval = setInterval(next_slide, 1000);
function next_slide() {
  slides[current_slide].className = 'item_slide';
  current_slide = (current_slide+1)%slides.length;
  slides[current_slide].className = 'item_slide active';
}
function pause_slide(){
  playing = false;
  pause.innerHTML = '&#9658;';
  clearInterval(slide_interval);
}
function play_slide(){
  playing = true;
  pause.innerHTML = '&#10074;&#10074;';
  slide_interval = setInterval(next_slide, 1000);
}
pause.addEventListener('click', function(){
  if(playing){
    pause_slide();
  }
  else{
    play_slide();
  }
});
```

>HTML Code:
```javascript
<div class="slideshow">
  <ul class="sliders">
    <li class="item_slide active"><img src="img/images/slider_1.jpg" alt=""></li>
    <li class="item_slide"><img src="img/images/slider_2.jpg" alt=""></li>
    <li class="item_slide"><img src="img/images/slider_3.jpg" alt=""></li>
    <li class="item_slide"><img src="img/images/slider_4.jpg" alt=""></li>
    <li class="item_slide"><img src="img/images/slider_5.jpg" alt=""></li>
  </ul>
  <div class="controls">
    <!-- <button class="press" id="previous">&lt;</button> -->
    <button class="press" id="pause">&#10074;&#10074;</button>
    <!-- <button class="press" id="next">&gt;</button> -->
  </div>
</div>
```

>CSS:
```javascript
.sliders {
  position: relative;
  height: 325px;
  width: 45px;
  margin: 0;
  padding: 0;
  list-style-type: none;
}
.item_slide {
  position: absolute;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  opacity: 0;
  z-index: 1;
  -webkit-transition: opacity 1s;
  -moz-transition: opacity 1s;
  -o-transition: opacity 1s;
  transition: opacity 1s;
}
.active {
  opacity: 1;
  z-index: 2;
}
.press {
  background: #333;
  color: #fff;
  border: none;
  padding: 7px 0px;
  font-size: 15px;
  cursor: pointer;
  border: 2px solid #fff;
  margin: 10px 5px 0 0;
  width: 40px;
}
.press:hover,
.press:focus {
  background: #eee;
  color: #333;
}
.controls {
  position: absolute;
  left: 10px;
  bottom: 10px;
  z-index: 10;
  font-size: 0;
}
.slideshow {
  position: relative;
}
```

##### Slideshow Next/Previous/Play/Pause:

>Javascript Code:
```javascript

```

>HTML Code:
```javascript

```

>CSS:
```javascript

```

##### Slideshow 4:

>Javascript Code:
```javascript

```

>HTML Code:
```javascript

```

>CSS:
```javascript

```

##### Slideshow 5:

>Javascript Code:
```javascript

```

>HTML Code:
```javascript

```

>CSS:
```javascript

```

##### Slideshow 6:

>Javascript Code:
```javascript

```

>HTML Code:
```javascript

```

>CSS:
```javascript

```

##### Slideshow 7:

>Javascript Code:
```javascript

```

>HTML Code:
```javascript

```

>CSS:
```javascript

```

