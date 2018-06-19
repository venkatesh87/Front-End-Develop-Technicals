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
- **Screen slide animation**
- ![slide 1, 2](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/img-niigata-1.jpg)
- ![slide 3, 4](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/img-niigata-2.jpg)
- ![slide 5, 6](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/img-niigata-3.jpg)
- ![slide 7, 8](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/img-niigata-4.jpg)
- **Request:** 
- **Màn hình Intro**
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
- **Import library:**
  + ```TweenMax.min.js```
  + ```jquery.mCustomScrollbar.concat.min```
  
>JavaScript Code:
```javascript
var ScrollContent = {
  selector: {
    scrollLeft: '.scroll-left',
    scrollRight: '.scroll-right',
    content: '.scroll-main'
  },
  init: function() {
    ScrollContent.calculator();
  },
  calculator: function() {
    $(ScrollContent.selector.content).mCustomScrollbar({
      theme: "minimal"
    });
    $(ScrollContent.selector.scrollLeft).mCustomScrollbar({
      theme: "minimal"
    });
    $(ScrollContent.selector.scrollRight).mCustomScrollbar({
      theme: "minimal"
    });
  }
}
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

var Animation = {
  selector: {
    openning: '.openning',
    introLft: '.intro-lft',
    introRgt: '.intro-rgt',
    control: '.load-control',
    loadChallenge: '.load-challenge',
    loadInfo: '.load-info',
    sectionIntro: '.section-intro',
    sectionChallenge: '.section-challenge',
    sectionCharm: '.section-charm',
    sectionPrefecture: '.section-prefecture',
  },
  handle: {
    main: new TimelineMax(),
    elml: new TimelineMax(),
    elmr: new TimelineMax(),
    ctr: new TimelineMax()
  },
  init: function() {
    Animation.logo_opening();
    Animation.show_challenge();
  },
  logo_opening: function() {
    Animation.handle.main.to($(Animation.selector.openning), 1.5, {
      ease: Power2.easeIn,
      autoAlpha: 1,
      visibility: 'visible',
      onComplete: function() {
        Animation.show_intro();
      }
    });
    Animation.handle.main.to($(Animation.selector.openning), 2.5, { ease: Expo.easeOut, autoAlpha: 1, visibility: 'visible' });
    Animation.handle.main.to($(Animation.selector.openning), 1, {
      ease: Expo.easeOut,
      autoAlpha: 0,
      visibility: 'hidden',
      display: "none",
      onComplete: function() {
        $(Animation.selector.sectionIntro).hide();
      }
    });
  },
  show_intro: function() {
    Animation.handle.elml.to($(Animation.selector.introLft), 1, { ease: Expo.easeIn, y: "0%" });
    Animation.handle.elml.to($(Animation.selector.introLft), 1, { ease: Expo.easeIn, y: "0%" });
    Animation.handle.elml.to($(Animation.selector.introLft), 2.5, { ease: Expo.easeOut, y: "100%" });
    Animation.handle.elmr.to($(Animation.selector.introRgt), 1, { ease: Expo.easeIn, y: "0%" });
    Animation.handle.elmr.to($(Animation.selector.introRgt), 1, { ease: Expo.easeIn, y: "0%" });
    Animation.handle.elmr.to($(Animation.selector.introRgt), 2.5, { ease: Expo.easeOut, y: "-100%" });
  },
  show_challenge: function() {
    Animation.handle.main.to($(Animation.selector.sectionChallenge), 2, {
      ease: Power3.easeOut,
      autoAlpha: 1,
      display: "block",
      onComplete: function() {
        Animation.show_control();
      }
    });
  },
  show_control: function() {
    Animation.handle.ctr.to($(Animation.selector.control), 6, { ease: Power2.easeOut, autoAlpha: 1, y: "0%", visibility: 'visible' });
  }
};

$(document).ready(function() {
  BackToTop.init();
  var deviceWidth = $(window).width();
  if (deviceWidth > 490) {
    Animation.init();
  }
  $(window).on('resize', function() {
    if (deviceWidth > 490) {
      ScrollContent.init();
    }
    if (deviceWidth < 490) {
      $(ScrollContent.selector.content).mCustomScrollbar("destroy"); //destroy scrollbar 
      $(ScrollContent.selector.scrollLeft).mCustomScrollbar("destroy"); //destroy scrollbar 
      $(ScrollContent.selector.scrollRight).mCustomScrollbar("destroy"); //destroy scrollbar 
    }
  }).resize();

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
  /*Rule Hover*/
  $(".gnavi").each(function() {
    $(this).find("li").hover(
      function() {
        if ($(this).find(".sub-menu").length > 0) {
          $('body').addClass('overlay');
          $(".sub-menu").stop(false, true).slideDown();
        }
      },
      function() {
        $('body').removeClass('overlay');
        $(".sub-menu").stop(false, true).slideUp();
      }
    );
  });
  var menuCloseFlag = true;
  $(".gnavi .sub-menu").mouseover(function() {
    menuCloseFlag = false;
    $(this).parent().find("a:first").addClass("hover_rule");
    $('.btn-close-sub').click(function(e) {
      e.preventDefault();
      $(".gnavi .sub-menu").slideUp();
    });
  });
  $(".gnavi .sub-menu").mouseout(function() {
    var self = this;
    menuCloseFlag = true;
    setTimeout(function() {
      if (menuCloseFlag) {
        $(self).parent().find("a:first").removeClass("hover_rule");
      }
    }, 200);
  });
  $('.load-challenge').click(function(e) {
    e.preventDefault();
    $(Animation.selector.sectionChallenge).fadeOut(200);
    $(Animation.selector.sectionCharm).fadeOut(200);
    $(Animation.selector.loadChallenge).fadeOut(200);
    $(Animation.selector.loadInfo).fadeIn(200);
    $(Animation.selector.loadInfo).css({ 'right': 'auto', 'left': '-11px' });
    $(Animation.selector.control).css({ 'width': '125px', 'right': 'auto', 'left': '0', 'margin-left': '0' });
    $(Animation.selector.sectionPrefecture).fadeIn(500);
    if (deviceWidth < 1400) {
      $(Animation.selector.loadInfo).css({ 'right': 'auto', 'left': '0' });
    }
    return false;
  });
  $('.load-info').click(function(e) {
    e.preventDefault();
    $(Animation.selector.sectionChallenge).fadeOut(200);
    $(Animation.selector.sectionPrefecture).fadeOut(200);
    $(Animation.selector.loadInfo).fadeOut(200);
    $(Animation.selector.loadChallenge).fadeIn(200);
    $(Animation.selector.loadChallenge).css({ 'right': 0, 'left': 'auto' });
    $(Animation.selector.control).css({ 'width': '125px', 'left': 'auto', 'right': 0, 'margin-left': '0' });
    $(Animation.selector.sectionCharm).fadeIn(500);
    return false;
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

**4. Javascript Nerima Project**

**▼ Phần sẽ tạo**

    - Tạo HTML dùng để demo cho quận Nerima
      + Toppage (4 page)
      + Endpage　(1 page)
      
**▼ Spec toppage**

    - Chuyển đổi 4 scene trên 1 page
    - Switch thì chuyển đổi mà không di chuyển page bằng Javascript (Giống với demo HTML5)
    - Switch thì slide tổng thể màn hình bằng animation
    - 1. Slide màn hình + Slide animation
    - 2. Fade in header
    - 3. Fade in background
    - 4. Fade in content
    - 5. Nhấn vào＜・＞, di chuyển đến màn hình tiếp theo
    - 6. Navigation của ↓ thì khung ở trung tâm nằm cố định, navigation di chuyển sang trái phải
    
**▼ Endpage**

    - Endpage thì cho xem vùng edit trên CMS
    - Header, navi phải, footer thì dán image capture là OK
    - Vùng edit thì để có thể sử dụng part trên CMS, nhờ các bạn coding nội dung bên dưới
    - Nội dung coding
      + H1,H2,H3
      + Table
      + List
    
**▼ ＜URL＞**		

    - 便利帳	```/benri.html```
    - 手続きガイド	```/tetsuzuki.html```	
    - 地域情報	```/chiiki.html```	
    - 事業者向け	```/jigyosha.html```	
    - 末端ページ ```/Endpage/hikkoshi.html```	
    
**☆ Do hiện đang tạo part của phần End nên nhờ các bạn coding nếu kịp nhé**
- Screen slide animation
![Image of Nerima](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/nerima-animation.jpg)
- Slide the whole screen including Border(Trượt toàn bộ màn hình bao gồm border)
>JavaScript Code:
```javascript

```

**5. 20180411_Iwate**
- **Request:** 
  + Project name: HTML demo dùng để giới thiệu về tỉnh Iwate
  + Làm giống https://nssg.jp/
  + Chỉ cho hiển thị từ ban đầu phần catch copy, rồi dần dần image khác sẽ được hiện ra.
  + Nhờ các bạn nhận thức về phần Responsive, nhưng khi hiển thị Smartphone thì không hoạt động cũng được.
- ![Image of Iwate](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/img-iwate.jpg)
>JavaScript Code:
```javascript

```

**6. 20171012 HTML5 Landing Page**
- **Sơ đồ di chuyển màn hình**.
[HTML5 Landing Page](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/html5-landing-1.jpg)
- **Full Screen**.
![HTML5 Landing Page](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/html5-landing-2.jpg)
- **Loading**.
![HTML5 Landing Page](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/html5-landing-3.jpg)
- **Openning**.
![HTML5 Landing Page](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/html5-landing-4.jpg)
![HTML5 Landing Page](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/html5-landing-5.jpg)
![HTML5 Landing Page](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/html5-landing-6.jpg)
![HTML5 Landing Page](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/html5-landing-7.jpg)
![HTML5 Landing Page](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/html5-landing-8.jpg)
![HTML5 Landing Page](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/html5-landing-9.jpg)
![HTML5 Landing Page](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/html5-landing-10.jpg)
![HTML5 Landing Page](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/html5-landing-11.jpg)
![HTML5 Landing Page](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/html5-landing-12.jpg)
![HTML5 Landing Page](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/html5-landing-13.jpg)
![HTML5 Landing Page](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/html5-landing-14.jpg)
![HTML5 Landing Page](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/html5-landing-15.jpg)
![HTML5 Landing Page](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/html5-landing-16.jpg)
>JavaScript Code:
```javascript

```

**7. 20171122 Minoh City**
- **Main Visual**: 
  + Tại image background, số lượng setting tối đa thì hãy hiển thị bằng chuyển đổi fade 5 image.
  + Trường hợp height của image lớn hơn size image được đề xuất thì sẽ là 556px, trường hợp Width lớn thì sẽ là trạng thái hiển thị cắt phía trái phải của image, trường hợp nhỏ thì sẽ được phóng to hiển thị cho khớp với height 556px.
  + Ngoài ra, data image thì nhờ các bạn loading, và setting bằng xml.
  
  + http://www.city.miura.kanagawa.jp/
  
　+ http://www.city.miura.kanagawa.jp/shared/js/top_gallery.xml
 
  ![Minoh City](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/minho-city-1.jpg)
  
**Di chuyển bằng slide nghiêng chéo**
  + **Khái quát**: Lấy image banner cố định làm image background, hiển thị chuyển đổi bằng thời gian hoặc Sendpage. Khi 3 image đang được hiển thị, thì image khác nhau sẽ được hiển thị khi được hiển thị tại vùng trung tâm (ở giữa). Ngoài ra, size hiển thị giữa lúc PC và smartphone sẽ khác nhau.
  + **Số image đăng ký**: Tối đa 3 cái
  + **Size image**
    + Image PC lớn：width 294px　 heigh t294px
    + Image PC nhỏ：width 166px　 height 166px
    + Smartphone：width 197px　 height 197px
 + **Thời gian chuyển đổi**: 5s
 + **Phương pháp chuyển đổi**: Slide (Di chuyển nghiêng chéo)
 + **Khi Javascript OFF**: 5s
    + Ba image đã được setting sẽ được hiển thị nhưng phần chuyển đổi tại thao tác slide thì không hoạt động
 + **Remark**
    + Image active thì size image sẽ khác nhau Có link
    
 ![Minoh City](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/minho-city-2.jpg)

**Hoạt động「電車/tàu điện」chạy**
 + Hãy set để image của tàu điện đang được hiển thị ở Footer di chuyển từ「このページの先頭へ戻る」đến bên ngang của bụi cỏ.
 + Khi hiển thị SP thì không hoạt động cũng được.
 + Nhờ các bạn set để sau khi di chuyển đến bụi cỏ thì nó biến mất đi.
 + Về FLASH, trên site hiện tại thì nó nằm trong phần Footer của Toppage. http://www.city.minoh.lg.jp/
 ![Minoh City](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/minho-city-3.jpg)

**Hoạt động「もみじの葉っぱ/lá đỏ」rơi**
 + Hãy set để khoảng ba lá đỏ kiểu đang rơi phấp phới xuống dưới 2 bên trái phải một cách tự động, khác với lá đỏ đang được hiển thị trên Main visual. Khi hiển thị SP thì không hoạt động cũng được.
 + Nhờ các bạn hình dung kiểu như sakura_demo/demo.html.
 + Ngoài ra, demo là cái dùng để test nên các bạn chỉnh sửa hay làm lại cũng không sao nhé
![Minoh City](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/minho-city-4.jpg)

>JavaScript Code:
```javascript

```
**8. 20180313 Booking HTML5 RakuRaKu**
- Text.

>JavaScript Code:
```javascript

```

**9. 20180508 ChartJS**
- Text.

>JavaScript Code:
```javascript

```

**10. 20180509 Plugin SmartPhone**
- Text.

>JavaScript Code:
```javascript

```

**11. 20180511 Foreign Language Tokyo**
- Text.

>JavaScript Code:
```javascript

```

**12. 20171211 Chiba Kun’s Hiroba FE**
- Text.

>JavaScript Code:
```javascript

```

**13. 20170718 Koufu**
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

**18. **
- Text.

>JavaScript Code:
```javascript

```

**19. **
- Text.

>JavaScript Code:
```javascript

```

**20. **
- Text.

>JavaScript Code:
```javascript

```

**21. **
- Text.

>JavaScript Code:
```javascript

```

**22. **
- Text.

>JavaScript Code:
```javascript

```

**23. **
- Text.

>JavaScript Code:
```javascript

```

**24. **
- Text.

>JavaScript Code:
```javascript

```

**25. **
- Text.

>JavaScript Code:
```javascript

```

**26. **
- Text.

>JavaScript Code:
```javascript

```

**27. **
- Text.

>JavaScript Code:
```javascript

```

**28. **
- Text.

>JavaScript Code:
```javascript

```

**29. **
- Text.

>JavaScript Code:
```javascript

```

**30. **
- Text.

>JavaScript Code:
```javascript

```


