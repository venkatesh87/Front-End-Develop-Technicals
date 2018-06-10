#### I. Memorize the company project GDIT
---

**1. File ```gd.js```**
- ```$.gd``` có nghĩa là

>JavaScript Code:
```javascript
$.gd = {
 Uri: function(d) {
 
 },
 wrapperWidth: function(b) {
 
 },
 searchText: function(e) {
 
 },
 googleSearchImage: function(b) {
 
 },
 textSize: function(d) {
 
 },
 changeStyle: function(g) {
 
 },
 activeLink: function(f) {
 
 },
 rollover: function(f) {
 
 },
 tab: function(f) {
 
 },
 switchMenu: function(m) {
 
 },
 labelClickable: function(d) {
 
 },
 blockSkipExpander: function(b) {
 
 },
 directoryFlg: function(a) {
 
 }
}
```

**2. NIIGATA PREFECTURE Project**
- **Request:** 
- ** Màn hình Intro**
  + **FadeIn** logo 2s
  + **Intro Left**: Fade-in từ trên xuống 2 giây
  + **Intro Right**: Fade-in từ dưới lên 2 giây
  + **Logo**: Vẫn còn giữ
  + Cố định hiển thị 2s
  + **Intro Left**: **FadeOut** xuống dưới 2 giây
  + **Intro Right**: **FadeOut** lên trên 2 giây
  + **Logo**: **FadeOut** cùng lúc với **Intro Left** và **Intro Right**.
  + Header cố định.
- Ở màn hình **新潟県 通常** thì hãy set scroll cho 2 phần ```left``` và ```right```. Scroll bar cho thật đẹp, vào site tham khảo
    http://manos.malihu.gr/repository/custom-scrollbar/demo/examples/complete_examples.html
  + **2 Button Arrow** ```県政情報 を見る```, ```魅力情報 を見る``` neo cố định trong phần content ở dưới
  + Click vào button **県政情報 を見る** **FadeIn** màn hình **新潟県 県民向け** và ẩn màn hình **新潟県 通常**
  + Click vào button **魅力情報 を見る** **FadeIn** màn hình **新潟県 魅力** và ẩn màn hình **新潟県 通常**
- **Menu Responsive:**
  + Fixed header
  + Có nút Back Top.
  + Click button search, button navigation toggle slide content, chuyển đổi trạng thái icon nav open, close
  
>JavaScript Code Navigation:
```javascript
var BackToTop = {
  selector: $('.back-top a'),
  init: function() {
    BackToTop.selector.on('click', function(e) {
      e.preventDefault();
      BackToTop.to_top();
    });
  },
  to_top: function() {
    $('html, body').animate({ scrollTop: 0 }, 1000)
  }
}

$(document).ready(function() {
  BackToTop.init();
  var deviceWidth = $(window).width();
  var temp = "";
  $('.mobile-control li a').on('click', function(e) {
    e.preventDefault();
    var _this = $(this);

    function toggle_nav_sp() {
      if (_this.attr('href') == '#navigation') {
        $('#search').stop(false, true).fadeOut();
        $('.search-link').removeClass('open');
        $('.search-link .nav-text').text('検索');
      } else if (_this.attr('href') == '#search') {
        $('#navigation').stop(false, true).fadeOut();
        $('.navigation-link').removeClass('open');
        $('.navigation-link .nav-text').text('メニュー');
      }
    }
    $('.mobile-control li').removeClass('active');
    $(this).parent().addClass('active');
    if ($(this).parent().hasClass('active')) {
      if (_this.hasClass('open')) {
        _this.removeClass('open');
        _this.children('.nav-text').text(temp);
        $('body').removeClass('overlay');
        $(_this.attr('href')).stop(false, true).slideUp(300);
        toggle_nav_sp();
      } else {
        _this.addClass('open');
        temp = _this.children('.nav-text').text();
        _this.children('.nav-text').text('閉じる');
        $('body').addClass('overlay');
        $(_this.attr('href')).stop(false, true).slideDown(300);
        toggle_nav_sp();
      }
    }
  });

  $('.close-up a').on('click', function(e) {
    e.preventDefault();
    var _this = $('.mobile-control li a.open');
    _this.removeClass('open');
    _this.children('.nav-text').text(temp);
    $('body').removeClass('overlay');
    $(_this.attr('href')).stop().slideUp(200);
  });
});
```

**3. Hướng dẫn kỹ thuật di dời các phần tử khi về thiết bị smartphone**
- Pankuzu.
- Header
- Footer
- Menu

>JavaScript Code:
```javascript

```

**4. Javascript Kobe project**
- Text.

>JavaScript Code:
```javascript

```

**5. 20180411_Iwate**
- Scale div with its content to fit window.

>JavaScript Code:
```javascript

```

**6. **
- Text.

>JavaScript Code:
```javascript

```

**7. **
- Text.

>JavaScript Code:
```javascript

```

**8. **
- Text.

>JavaScript Code:
```javascript

```

**9. **
- Text.

>JavaScript Code:
```javascript

```

**10. **
- Text.

>JavaScript Code:
```javascript

```

**11. **
- Text.

>JavaScript Code:
```javascript

```

**12. **
- Text.

>JavaScript Code:
```javascript

```

**13. **
- Text.

>JavaScript Code:
```javascript

```

**14. **
- Text.

>JavaScript Code:
```javascript

```

**15. **
- Text.

>JavaScript Code:
```javascript

```

**16. **
- Text.

>JavaScript Code:
```javascript

```

**17. **
- Text.

>JavaScript Code:
```javascript

```
