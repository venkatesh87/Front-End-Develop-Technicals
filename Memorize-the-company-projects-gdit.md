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

#### Version 1

**>Demo 1**

>JavaScript Code:
```javascript
var header = document.getElementById('header');
var logoCenter = document.querySelector('.logo_center');
var Animation2 = {
  init: function() {
    header.addEventListener('webkitAnimationEnd', Animation2.ShowLogo);
    header.addEventListener('animationend', Animation2.ShowLogo);

    logoCenter.addEventListener('webkitAnimationEnd', Animation2.showGrid);
    logoCenter.addEventListener('animationend', Animation2.showGrid);
  },
  prepareGrid: function(e) {
    $('.frame').not('.logo_center').addClass('prepare');
  },
  showGrid: function(e) {
    var arr = [];
    for (var i = 0; i < $('.frame').length - 1; i++) {
      arr[i] = i;
    }
    shuffle(arr);
    $('.frame').each(function(index) {
      $(this).find('img').css({
        'animation-delay': (arr[index] * 120) + 'ms'
      });
      if (arr[index] == arr.length - 1) {
        $(this)[0].addEventListener('webkitAnimationEnd', Animation2.showEmergency);
        $(this)[0].addEventListener('animationend', Animation2.showEmergency);

        $(this)[0].addEventListener('webkitAnimationEnd', Animation2.showMoutain);
        $(this)[0].addEventListener('animationend', Animation2.showMoutain);

        $(this)[0].addEventListener('webkitAnimationEnd', Animation2.showCricle);
        $(this)[0].addEventListener('animationend', Animation2.showCricle);

        $('.menu_primary')[0].addEventListener('webkitAnimationEnd', Animation2.showPrimary);
        $('.menu_primary')[0].addEventListener('animationend', Animation2.showPrimary);
      }
    });
    setTimeout(function() {
      $('.frame').not('.logo_center').addClass('start');
      $('.frame').not('.logo_center').find('img').addClass('fadeIn')
    }, 50)
  },
  ShowLogo: function() {
    setTimeout(function() {
      $('.logo_center').addClass('fadeIn');
    }, 200)
  },
  showPrimary: function() {
    setTimeout(function() {
      $('.menu_primary .list').addClass('fadeInUpSmall');
    }, 80)
  },
  showEmergency: function() {
    $('.emergency_panel').addClass('fadeInDownSmall');
  },
  showMoutain: function() {
    $('.menu_primary').addClass('showMoutain');
  },
  showCricle: function() {
    $('.link_primary').addClass('active');
    $('.link_cr').addClass('bounceIn');
  }
}
$(window).on('load', function() {
  Animation2.init();
});

function shuffle(a) {
  var j, x, i;
  for (i = a.length - 1; i > 0; i--) {
    j = Math.floor(Math.random() * (i + 1));
    x = a[i];
    a[i] = a[j];
    a[j] = x;
  }
}
```

>CSS Code:
```javascript
#header {
  position: relative;
  z-index: 1;
}

.logo {
  background-color: #ffffff;
}

.logo_center {
  opacity: 0;
}

@keyframes logo {
  0% {
    opacity: 0;
    transform: scale(1.2);
    -moz-transform: scale(1.2);
    -webkit-transform: scale(1.2);
  }
  100% {
    transform: scale(1);
    -moz-transform: scale(1);
    -webkit-transform: scale(1);
    opacity: 1;
  }
}

.logo_center.active {
  -webkit-animation-name: logo;
  animation-name: logo;
  -webkit-animation-duration: 0.7s;
  animation-duration: 0.7s;
  -webkit-animation-fill-mode: both;
  animation-fill-mode: both;
}

#frame-grid .logo_center a:before,
#frame-grid .logo_center a:after {
  -webkit-transition: 0.2s ease all;
  -o-transition: 0.2s ease all;
  transition: 0.2s ease all;
}

.frame:not(.logo_center) img {
  opacity: 0;
}

.frame.start img {
  animation-fill-mode: forwards;
  animation-timing-function: cubic-bezier(.7, 0, .3, 1);
  animation-duration: .9s;
}

.logo_center figure:before {
  /* content: ''; */
  position: absolute;
  bottom: 15px;
  width: 40px;
  height: 375px;
  left: 135px;
  z-index: 9;
  background-color: #ffffff;
}

.show_logo img {
  opacity: 1;
}

.show_logo figure:before {
  /*animation: show_text 2.4s 1;
  -webkit-animation: show_text 2.4s 1;
  -moz-animation: show_text 2.4s 1;
  animation-fill-mode: forwards;*/
}

@keyframes show_text {
  0% {
    height: 375px;
  }
  50% {
    height: 375px;
  }
  100% {
    height: 0px;
  }
}

@-webkit-keyframes pulse {
  from {
    -webkit-transform: scale3d(1, 1, 1);
    transform: scale3d(1, 1, 1);
  }

  50% {
    -webkit-transform: scale3d(1.05, 1.05, 1.05);
    transform: scale3d(1.05, 1.05, 1.05);
  }

  to {
    -webkit-transform: scale3d(1, 1, 1);
    transform: scale3d(1, 1, 1);
  }
}

@keyframes pulse {
  from {
    -webkit-transform: scale3d(1, 1, 1);
    transform: scale3d(1, 1, 1);
  }

  50% {
    -webkit-transform: scale3d(1.05, 1.05, 1.05);
    transform: scale3d(1.05, 1.05, 1.05);
  }

  to {
    -webkit-transform: scale3d(1, 1, 1);
    transform: scale3d(1, 1, 1);
  }
}

.pulse {
  -webkit-animation-name: pulse;
  animation-name: pulse;
}

@-webkit-keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

.fadeIn {
  -webkit-animation-name: fadeIn;
  animation-name: fadeIn;
  animation-fill-mode: forwards;
}
```
>HTML Code:
```javascript
<div id="wrapper">
  <header id="header" class="fadeInDown">
    <div class="container">
      <h1 class="logo">
        <a href="#">
          <picture>
            <source media="(max-width: 650px)" srcset="./img/front/sp_logo.png" width="152" height="88">
            <img src="./img/front/logo.png" alt="logo" width="200" height="200">
          </picture>
        </a>
      </h1>
      <ul class="navigation_sp">
        <li>
          <a href="#">
            <span class="symbol">
              <i class="icons_marker">&nbsp;</i>
            </span>
            <span class="nav_text">アクセス</span>
          </a>
        </li>
        <li>
          <a href="#">
            <span class="symbol">
              <i class="icons_phone">&nbsp;</i>
            </span>
            <span class="nav_text">直通電話</span>
          </a>
        </li>
        <li>
          <a href="#">
            <span class="symbol">
              <i class="icons_nav">&nbsp;</i>
            </span>
            <span class="nav_text">メニュー</span>
          </a>
        </li>
      </ul>
      <div class="top_header">
        <div class="search_panel">
          <label>サイト内検索</label>
          <div class="search_action">
            <form class="search_form" action="" method="">
              <input type="text" placeholder="Google カスタム検索">
              <button type="submit" class="btn_search">Search</button>
            </form>
          </div>
        </div>
        <div class="setting">
          <ul class="clearfix">
            <li><a href="#">文字サイズ・色合い変更</a></li>
            <li><a href="#">音声読み上げ</a></li>
            <li><a href="#">Foreign Language</a></li>
          </ul>
        </div>
      </div>
    </div>
  </header>
  <!--end header-->
  <main id="main-content">
    <div class="container">
      <img src="./img/front/grid/mobile.jpg" class="show_on_mobile" alt="">
      <div id="frame-grid-wrapper">
        <div id="frame-grid">
          <div class="emergency_panel clearfix">
            <label>緊急情報</label>
            <a href="#">弾道ミサイル落下時の行動等について</a>
          </div>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img1.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img2.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img3.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img4.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img5.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img6.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img7.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame logo_center">
            <a href="#">
              <figure><img src="./img/front/grid/logo_center.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img8.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img9.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img10.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img11.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img12.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img13.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img14.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img15.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img16.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img17.jpg" alt=""></figure>
            </a>
          </article>
        </div>
      </div>
      <div class="link_primary">
          <a href="#" class="link_cr">
            <span class="icons_people">&nbsp;</span>
            <span class="txt">県民向け<br/>
            情報</span>
          </a>
          <a href="#" class="link_cr">
            <span class="icons_build">&nbsp;</span>
            <span class="txt">事業者<br/>
            情報</span>
          </a>
          <a href="#" class="link_cr">
            <span class="icons_camera">&nbsp;</span>
            <span class="txt">魅力・観光<br/>
            情報</span>
          </a>
        </div>
        <div class="menu_primary">
          <div class="list">
            <a href="#"><span>復興のその先へ</span></a>
            <a href="#"><span>移住定住応援</span></a>
            <a href="#"><span>仕事・就職応援</span></a>
          </div>
        </div>
        <div class="action_control">
            <button class="button_slider button_play">PLAY</button>
            <button class="button_slider button_pause">STOP</button>
        </div>
        <img src="./img/front/footer_bottom.png" class="show_on_mobile bottom" alt="">
    </div>
  </main>
  <!--end main-->
  <footer id="footer" class="fadeInUp">
    <div class="footer_top">
      <div class="container">
        <h2 class="logo_footer">岩手県庁</h2>
        <address class="address_footer">
          <span>法人番号：4000020030007</span>
          <span>〒020-8570 岩手県盛岡市内丸10番1号</span>
          <span>電話番号：019-651-3111（総合案内）</span>
        </address>
      </div>
    </div>
    <div class="footer_copyright">
      <div class="container"><p>Copyright © Iwate Prefecture Government All Rights Reserved.</p></div>
    </div>
  </footer>
  <!--end footer-->
</div>
```

**>Demo 2**

>JavaScript Code:
```javascript
var logoCenter = document.querySelector('.logo_center'),
  logoCenter_a = document.querySelector('.logo_center a'),
  animationEndEvent = (function detectAnimationEndEvent() {
    var el = document.createElement('div')
    var eventNames = {
      'animation': 'animationend',
      'WebkitAnimation': 'webkitAnimationEnd',
      'MozAnimation': 'animationend',
      'OAnimation': 'oanimationend',
      'msAnimation': 'MSAnimationEnd'
    }
    for (var i in eventNames) {
      if (el.style[i] !== undefined) {
        return eventNames[i]
      }
    }
    return false
  })(),
  animationStartEvent = (function detectAnimationStartEvent() {
    var el = document.createElement('div')
    var eventNames = {
      'animation': 'animationstart',
      'WebkitAnimation': 'webkitAnimationStart',
      'MozAnimation': 'animationstart',
      'OAnimation': 'oanimationstart',
      'msAnimation': 'MSAnimationStart'
    }
    for (var i in eventNames) {
      if (el.style[i] !== undefined) {
        return eventNames[i]
      }
    }
    return false
  })();
var Animation2 = {
  init: function() {
    $('#wrapper').addClass('ready');
    logoCenter_a.addEventListener(animationEndEvent, Animation2.showGrid);

    logoCenter_a.addEventListener(animationStartEvent, Animation2.prepareGrid);

    logoCenter_a.className += ' show_logo';

    logoCenter.addEventListener(animationEndEvent, Animation2.showHeaderFooter);

  },
  prepareGrid: function(e) {
    $('.frame').not('.logo_center').addClass('prepare');
  },
  showGrid: function(e) {
    var arr = [];
    for (var i = 0; i < $('.frame').length - 1; i++) {
      arr[i] = i;
    }
    shuffle(arr);
    $('.frame').not('.logo_center').each(function(index) {
      $(this).find('img').css({
        'animation-delay': (arr[index] * 200) + 'ms'
      });
      if (arr[index] == arr.length - 1) {

        $(this)[0].addEventListener('webkitAnimationEnd', Animation2.pulseLogo);
        $(this)[0].addEventListener('animationend', Animation2.pulseLogo);

        $(this)[0].addEventListener('webkitAnimationEnd', Animation2.showEmergency);
        $(this)[0].addEventListener('animationend', Animation2.showEmergency);

        $(this)[0].addEventListener('webkitAnimationEnd', Animation2.showMoutain);
        $(this)[0].addEventListener('animationend', Animation2.showMoutain);

        $(this)[0].addEventListener('webkitAnimationEnd', Animation2.showCricle);
        $(this)[0].addEventListener('animationend', Animation2.showCricle);

        $('.menu_primary')[0].addEventListener('webkitAnimationEnd', Animation2.showPrimary);
        $('.menu_primary')[0].addEventListener('animationend', Animation2.showPrimary);

      }
    });
    setTimeout(function() {
      $('.frame').not('.logo_center').addClass('start');
      $('.frame').not('.logo_center').find('img').addClass('zoomIn')
    }, 400)
  },
  pulseLogo: function() {
    $('.logo_center').addClass('pulse');
  },
  showHeaderFooter: function(e) {
    if ($('.logo_center').hasClass('pulse')) {
      $('#header').addClass('active');
      $('#footer').addClass('active');
    }
  },
  showPrimary: function() {
    $('.menu_primary .list').addClass('fadeInUpSmall');
  },
  showEmergency: function() {
    $('.emergency_panel').addClass('fadeInDownSmall');
  },
  showMoutain: function() {
    $('.menu_primary').addClass('showMoutain');
  },
  showCricle: function() {
    $('.link_primary').addClass('active');
    $('.link_cr').addClass('bounceIn');
  }
}
$(window).on('load', function() {
  setTimeout(function() {
    Animation2.init();
  }, 400)
});

function shuffle(a) {
  var j, x, i;
  for (i = a.length - 1; i > 0; i--) {
    j = Math.floor(Math.random() * (i + 1));
    x = a[i];
    a[i] = a[j];
    a[j] = x;
  }
}
```
>CSS Code:
```javascript
@media(min-width: 376px) {
  /* Ready state */
  #wrapper.ready #header {
    transition: 0.6s ease all;
    -webkit-transition: 0.6s ease all;
    -moz-transition: 0.6s ease all;
  }
  #wrapper.ready #header .logo {
    transition: 0.5s ease all;
    -webkit-transition: 0.5s ease all;
    -moz-transition: 0.5s ease all;
    /*     transition-delay: 1s;
    -webkit-transition-delay: 1s;
    -o-transition-delay: 1s; */
  }
  #wrapper.ready #header .logo img {
    transition: opacity 0.3s ease-in-out 0.5s, transform 0.3s ease-in-out 0.5s;
    -moz-transition: opacity 0.3s ease-in-out 0.5s, transform 0.3s ease-in-out 0.5s;
    -webkit-transition: opacity 0.3s ease-in-out 0.5s, transform 0.3s ease-in-out 0.5s;
    /*     transition-delay: 2s;
    -webkit-transition-delay: 1.8s;
    -o-transition-delay: 2s; */
  }
  #wrapper.ready #footer .footer_container {
    transition: 0.6s ease all;
    -webkit-transition: 0.6s ease all;
    -moz-transition: 0.6s ease all;
  }
  #wrapper.ready .logo_center img {
    -webkit-transition: 1s ease opacity;
    -o-transition: 1s ease opacity;
    transition: 1s ease opacity;
  }
  /* Header */
  #header {
    transform: translate(0, -101%);
    -moz-transform: translate(0, -101%);
    -webkit-transform: translate(0, -101%);
    position: relative;
    z-index: 99;
  }
  #header.active {
    transform: none;
    -webkit-transform: none;
    -moz-transform: none;
  }
  #header .logo {
    background-color: #ffffff;
    transform: translate(-50%, 0);
    -moz-transform: translate(-5%, 0);
    -webkit-transform: translate(-50%, 0);
    opacity: 0;
  }
  #header .logo img {
    -ms-filter: "progid:DXImageTransform.Microsoft.Alpha(Opacity=0)";
    filter: alpha(opacity=0);
    -moz-opacity: 0;
    -khtml-opacity: 0;
    opacity: 0;
    transform: scale(1.2);
    -moz-transform: scale(1.2);
    -webkit-transform: scale(1.2);
  }
  #header.active .logo {
    transform: translate(0, 0);
    -moz-transform: translate(0, 0);
    -webkit-transform: translate(0, 0);
    opacity: 1;
  }
  #header.active .logo img {
    -ms-filter: "progid:DXImageTransform.Microsoft.Alpha(Opacity=100)";
    filter: alpha(opacity=100);
    -moz-opacity: 1;
    -khtml-opacity: 1;
    opacity: 1;
    transform: scale(1);
    -moz-transform: scale(1);
    -webkit-transform: scale(1);
  }
  /* Footer */
  #footer {
    position: relative;
    z-index: 99;
    overflow: hidden;
  }
  #footer .footer_container {
    transform: translate(0, 65px);
    -moz-transform: translate(0, 65px);
    -webkit-transform: translate(0, 65px);
    opacity: 0;
  }
  #footer.active .footer_container {
    transform: none;
    -webkit-transform: none;
    -moz-transform: none;
    opacity: 1;
  }
  /* Grid */
  #frame-grid .logo_center a:before {
    background-position: right bottom;
  }
  #frame-grid .logo_center a:after {
    background-position: left top;
  }
  #frame-grid .logo_center a:before,
  #frame-grid .logo_center a:after {
    width: 0;
    -webkit-transition: 0.8s ease all;
    -o-transition: 0.8s ease all;
    transition: 0.8s ease all;
  }
  #frame-grid .logo_center.pulse a:before,
  #frame-grid .logo_center.pulse a:after {
    width: 58px;
  }
  .logo_center img {
    opacity: 0;
  }
  .frame:not(.logo_center) img {
    opacity: 0;
  }
  .frame.start img {
    animation-fill-mode: forwards;
    animation-timing-function: ease-out;
    animation-duration: 500ms;
  }
  .logo_center .light {
    content: '';
    position: absolute;
    bottom: 15px;
    width: 40px;
    height: 375px;
    left: 135px;
    z-index: 9;
    background-color: #ffffff;
  }
  .show_logo img {
    opacity: 1;
  }
  .show_logo .light {
    animation: show_text 2.4s 1;
    -webkit-animation: show_text 2.4s 1;
    -moz-animation: show_text 2.4s 1;
    animation-fill-mode: forwards;
  }

  @keyframes show_text {
    0% {
      height: 375px;
    }
    50% {
      height: 375px;
    }
    100% {
      height: 0px;
    }
  }

  @-webkit-keyframes pulse {
    from {
      -webkit-transform: scale3d(1, 1, 1);
      transform: scale3d(1, 1, 1);
    }

    50% {
      -webkit-transform: scale3d(1.05, 1.05, 1.05);
      transform: scale3d(1.05, 1.05, 1.05);
    }

    to {
      -webkit-transform: scale3d(1, 1, 1);
      transform: scale3d(1, 1, 1);
    }
  }

  @keyframes pulse {
    from {
      -webkit-transform: scale3d(1, 1, 1);
      transform: scale3d(1, 1, 1);
    }

    50% {
      -webkit-transform: scale3d(1.05, 1.05, 1.05);
      transform: scale3d(1.05, 1.05, 1.05);
    }

    to {
      -webkit-transform: scale3d(1, 1, 1);
      transform: scale3d(1, 1, 1);
    }
  }

  .pulse {
    -webkit-animation-name: pulse;
    animation-name: pulse;
  }

  @-webkit-keyframes zoomIn {
    from {
      opacity: 0;
      -webkit-transform: scale3d(0.3, 0.3, 0.3);
      transform: scale3d(0.3, 0.3, 0.3);
    }

    50% {
      opacity: 1;
    }
    to {
      opacity: 1;
    }
  }

  @keyframes zoomIn {
    from {
      opacity: 0;
      -webkit-transform: scale3d(0.3, 0.3, 0.3);
      transform: scale3d(0.3, 0.3, 0.3);
    }

    50% {
      opacity: 1;
    }

    to {
      opacity: 1;
    }
  }

  .zoomIn {
    -webkit-animation-name: zoomIn;
    animation-name: zoomIn;
  }
}
```
>HTML Code:
```javascript
<div id="wrapper">
  <header id="header">
    <div class="container">
      <h1 class="logo">
        <a href="#">
          <picture>
            <source media="(max-width: 650px)" srcset="./img/front/sp_logo.png" width="152" height="88">
            <img src="./img/front/logo.png" alt="logo" width="200" height="200">
          </picture>
        </a>
      </h1>
      <ul class="navigation_sp">
        <li>
          <a href="#">
            <span class="symbol">
              <i class="icons_marker">&nbsp;</i>
            </span>
            <span class="nav_text">アクセス</span>
          </a>
        </li>
        <li>
          <a href="#">
            <span class="symbol">
              <i class="icons_phone">&nbsp;</i>
            </span>
            <span class="nav_text">直通電話</span>
          </a>
        </li>
        <li>
          <a href="#">
            <span class="symbol">
              <i class="icons_nav">&nbsp;</i>
            </span>
            <span class="nav_text">メニュー</span>
          </a>
        </li>
      </ul>
      <div class="top_header">
        <div class="search_panel">
          <label>サイト内検索</label>
          <div class="search_action">
            <form class="search_form" action="" method="">
              <input type="text" placeholder="Google カスタム検索">
              <button type="submit" class="btn_search">Search</button>
            </form>
          </div>
        </div>
        <div class="setting">
          <ul class="clearfix">
            <li><a href="#">文字サイズ・色合い変更</a></li>
            <li><a href="#">音声読み上げ</a></li>
            <li><a href="#">Foreign Language</a></li>
          </ul>
        </div>
      </div>
    </div>
  </header>
  <!--end header-->
  <main id="main-content">
    <div class="container">
      <img src="./img/front/grid/mobile.jpg" class="show_on_mobile" alt="">
      <div id="frame-grid-wrapper">
        <div id="frame-grid">
          <div class="emergency_panel clearfix">
            <label>緊急情報</label>
            <a href="#">弾道ミサイル落下時の行動等について</a>
          </div>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img1.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame double">
            <a href="#">
              <figure><img src="./img/front/grid/img2.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img3.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img4.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame double">
            <a href="#">
              <figure><img src="./img/front/grid/img5.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame double">
            <a href="#">
              <figure><img src="./img/front/grid/img6.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img7.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame logo_center">
            <a href="#">
              <span class="light">&nbsp;</span>
              <figure><img src="./img/front/grid/logo_center.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img8.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img9.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img10.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img11.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame double">
            <a href="#">
              <figure><img src="./img/front/grid/img12.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img13.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img14.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img15.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img16.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img17.jpg" alt=""></figure>
            </a>
          </article>
        </div>
      </div>
    </div>
    <div class="link_primary">
      <a href="#" class="link_cr">
        <span class="icons_people">&nbsp;</span>
        <span class="txt">県民向け<br/>
        情報</span>
      </a>
      <a href="#" class="link_cr">
        <span class="icons_build">&nbsp;</span>
        <span class="txt">事業者<br/>
        情報</span>
      </a>
      <a href="#" class="link_cr">
        <span class="icons_camera">&nbsp;</span>
        <span class="txt">魅力・観光<br/>
        情報</span>
      </a>
    </div>
    <div class="menu_primary">
      <div class="list">
        <a href="#"><span>復興のその先へ</span></a>
        <a href="#"><span>移住定住応援</span></a>
        <a href="#"><span>仕事・就職応援</span></a>
      </div>
    </div>
    <div class="action_control">
        <button class="button_slider button_play">PLAY</button>
        <button class="button_slider button_pause">STOP</button>
    </div>
    <img src="./img/front/footer_bottom.png" class="show_on_mobile bottom" alt="">
  </main>
  <!--end main-->
  <footer id="footer">
    <div class="footer_container">
      <div class="footer_top">
        <div class="container">
          <h2 class="logo_footer">岩手県庁</h2>
          <address class="address_footer">
            <span>法人番号：4000020030007</span>
            <span>〒020-8570 岩手県盛岡市内丸10番1号</span>
            <span>電話番号：019-651-3111（総合案内）</span>
          </address>
        </div>
      </div>
      <div class="footer_copyright">
        <div class="container"><p>Copyright © Iwate Prefecture Government All Rights Reserved.</p></div>
      </div>
    </div>
  </footer>
  <!--end footer-->
</div>
```

**>Demo 3**

>JavaScript Code:
```javascript
var page = 0;
var photo_default_size = 18;
var max_w_photos, max_h_photos;
var gallery = $('#frame-grid');
var win = $(window);
var frame_item = document.querySelectorAll('#frame-grid .frame');
var Gallery = {
  Selector: {
    loading: '.loading',
    loading_wrap: '.loading-logo',
    loading_outline: '.logo-outline'
  },
  init: function() {
    Gallery.loadingScreen();
  },
  loadingScreen: function() {
    $(window).on("resize", function() {
      if ($(window).width() > 480) {
        $(Gallery.Selector.loading_outline).removeAttr('style');
        TweenLite.to($(".logo-outline"), 2, {
          height: 0,
          ease: Power1.easeInOut,
          onComplete: function() {
            TweenLite.to($(Gallery.Selector.loading), 1, {
              yPercent: -100,
              ease: Power2.easeInOut,
              delay: 0.1,
              onComplete: function() {
                TweenLite.set($(Gallery.Selector.loading), { autoAlpha: 0, yPercent: 100 });
                Gallery.header();
                Gallery.footer();
                setTimeout(function() {
                  Gallery.showPhotos();
                  $('.frame').eq(17).on('transitionend webkitTransitionEnd oTransitionEnd', Gallery.showEmergency);

                  $('.frame').eq(17).on('transitionend webkitTransitionEnd oTransitionEnd', Gallery.showMoutain);

                  $('.frame').eq(17).on('transitionend webkitTransitionEnd oTransitionEnd', Gallery.showCricle);

                  $('.menu_primary')[0].addEventListener('webkitAnimationEnd', Gallery.showPrimary);
                  $('.menu_primary')[0].addEventListener('animationend', Gallery.showPrimary);

                }, 350);
              }
            });
          }
        });
      }
    }).resize();
    if ($(window).width() < 480) {
      Gallery.header();
      Gallery.footer();
    }
  },
  header: function() {
    $('#header').addClass('fadeInDown');
  },
  footer: function() {
    $('#footer').addClass('fadeInUp');
  },
  logo: function() {

  },
  showPhotos: function() {
    win.on('resize', function(e) {
      var width = win.width(),
        height = win.height();
      // How many photos can we fit on one line?
      max_w_photos = Math.ceil(width / photo_default_size);
      // Let's do the same with the height:
      max_h_photos = Math.ceil(height / photo_default_size);
    }).resize();
    // Animate the images from the top-left
    var photos = gallery.find('.frame a img');
    for (var i = 0; i < max_w_photos + max_h_photos; i++) {
      var j = i;
      // Loop through all the lines
      for (var l = 0; l < max_h_photos; l++) {
        // If the photo is not of the current line, stop.
        if (j < l * max_w_photos) break;
        // Schedule a timeout. It is wrapped in an anonymous
        // function to preserve the value of the j variable
        (function(j) {
          setTimeout(function() {
            photos.eq(j).addClass('show');
            $(this).on('transitionend webkitTransitionEnd oTransitionEnd', Gallery.sknewLine);
          }, i * 50);
          if (l == max_w_photos - 1) {
            $(this).on('transitionend webkitTransitionEnd oTransitionEnd', Gallery.showEmergency);
          }
        })(j);
        // Increment the counter so it points to the photo
        // to the left on the line below
        j += max_w_photos - 1;
      }
    }
  },
  showPrimary: function() {
    $('.menu_primary .list').addClass('fadeInUpSmall');
  },
  showEmergency: function() {
    $('.emergency_panel').addClass('fadeInDownSmall');
  },
  showMoutain: function() {
    $('.menu_primary').addClass('showMoutain');
  },
  showCricle: function() {
    $('.link_primary').addClass('active');
    $('.link_cr').addClass('bounceIn');
  },
  sknewLine: function() {
    setTimeout(function() {
      $('.line_sknew').addClass('logo_center');
    }, 500)
  }
}

$(document).ready(function() {
  Gallery.init();
});
```
>CSS Code:
```javascript
@font-face {
  font-family: 'a-otf_jomin_stdl';
  src: url('/fonts/jominstd-light.woff2') format('woff2'),
  url('/fonts/jominstd-light.woff') format('woff');
  font-weight: normal;
  font-style: normal;
}

#header,
#footer {
  position: relative;
  z-index: 50;
  opacity: 0;
  -webkit-animation-duration: 1s;
  animation-duration: 1s;
  -webkit-animation-fill-mode: both;
  animation-fill-mode: both;
}

#header .logo {
  background-color: #ffffff;
}

.loading {
  position: fixed;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  background: #fff;
  z-index: 101;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.loading img {
  max-width: inherit;
}

.loading .loader {
  position: absolute;
  width: 100px;
  height: 100px;
  left: 50%;
  top: 50%;
  transform: translateX(-50%) translateY(-50%) rotate(-90deg);
  -webkit-transform: translateX(-50%) translateY(-50%) rotate(-90deg);
}

.loading-logo {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -70%);
  -webkit-transform: translate(-50%, -70%);
}

.logo-outline {
  position: absolute;
  width: 230px;
  height: 412px;
  top: 0;
  left: 0;
  z-index: 2;
  background: #fff;
}

.loadingtitle {
  position: fixed;
  font-family: 'a-otf_jomin_stdl';
  font-size: 43px;
  line-height: 45px;
  width: 100%;
  text-align: center;
  top: 65vh;
  transform: translateY(50%);
  -webkit-transform: translateY(50%);
  color: #a7811a;
  z-index: 105;

  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.loadingtitle span {
  display: inline-block;
  transform: translateY(24px);
  -webkit-transform: translateY(24px);
  /* opacity: 0;
  visibility: hidden; */
}

.frame img {
  /* opacity: 0;
  -webkit-animation-duration: 1s;
  animation-duration: 1s;
  -webkit-animation-fill-mode: both;
  animation-fill-mode: both;
  -webkit-transform: translate3d(0, 0, 0);
  transform: translate3d(0, 0, 0); */
  opacity: 0;
  float: left;
  background-size: cover;
  background-position: center center;

  -webkit-transform: scale(0.8);
  -moz-transform: scale(0.8);
  transform: scale(0.8);

  -webkit-transition: 0.4s;
  -moz-transition: 0.4s;
  transition: 0.4s;
}

.frame a img.show:hover {
  opacity: 0.9 !important;
}

.frame a img.show {
  opacity: 1;
  -webkit-transform: scale(1);
  -moz-transform: scale(1);
  transform: scale(1);
}

@-webkit-keyframes fadeInDown {
  from {
    opacity: 0;
    -webkit-transform: translate3d(0, -100%, 0);
    transform: translate3d(0, -100%, 0);
  }

  to {
    opacity: 1;
    -webkit-transform: translate3d(0, 0, 0);
    transform: translate3d(0, 0, 0);
  }
}

@keyframes fadeInDown {
  from {
    opacity: 0;
    -webkit-transform: translate3d(0, -100%, 0);
    transform: translate3d(0, -100%, 0);
  }

  to {
    opacity: 1;
    -webkit-transform: translate3d(0, 0, 0);
    transform: translate3d(0, 0, 0);
  }
}

@-webkit-keyframes fadeInUp {
  from {
    opacity: 0;
    -webkit-transform: translate3d(0, 100%, 0);
    transform: translate3d(0, 100%, 0);
  }

  to {
    opacity: 1;
    -webkit-transform: translate3d(0, 0, 0);
    transform: translate3d(0, 0, 0);
  }
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    -webkit-transform: translate3d(0, 100%, 0);
    transform: translate3d(0, 100%, 0);
  }

  to {
    opacity: 1;
    -webkit-transform: translate3d(0, 0, 0);
    transform: translate3d(0, 0, 0);
  }
}

.animated {
  -webkit-animation-duration: 1s;
  animation-duration: 1s;
  -webkit-animation-fill-mode: both;
  animation-fill-mode: both;
}

.fadeInDown {
  -webkit-animation-name: fadeInDown;
  animation-name: fadeInDown;
}

.fadeInUp {
  -webkit-animation-name: fadeInUp;
  animation-name: fadeInUp;
}

@media(max-width: 480px) {
  .loading {
    display: none;
    visibility: hidden;
    opacity: 0;
  }
}
```

>HTML Code:
```javascript
<div id="wrapper">
  <div class="loading">
    <div class="loading-logo">
      <img src="img/front/loading.png" width="230" height="412" alt="ひと・まち・しあわせ輝く">
      <div class="logo-outline">
        <img src="img/front/loading-outline.png" width="230" height="412" alt="ひと・まち・しあわせ輝く">
      </div>
    </div>
  </div>
  <header id="header">
    <div class="container">
      <h1 class="logo">
        <a href="#">
          <picture>
            <source media="(max-width: 650px)" srcset="./img/front/sp_logo.png" width="152" height="88">
            <img src="./img/front/logo.png" alt="logo" width="200" height="200">
          </picture>
        </a>
      </h1>
      <ul class="navigation_sp">
        <li>
          <a href="#">
            <span class="symbol">
              <i class="icons_marker">&nbsp;</i>
            </span>
            <span class="nav_text">アクセス</span>
          </a>
        </li>
        <li>
          <a href="#">
            <span class="symbol">
              <i class="icons_phone">&nbsp;</i>
            </span>
            <span class="nav_text">直通電話</span>
          </a>
        </li>
        <li>
          <a href="#">
            <span class="symbol">
              <i class="icons_nav">&nbsp;</i>
            </span>
            <span class="nav_text">メニュー</span>
          </a>
        </li>
      </ul>
      <div class="top_header">
        <div class="search_panel">
          <label>サイト内検索</label>
          <div class="search_action">
            <form class="search_form" action="" method="">
              <input type="text" placeholder="Google カスタム検索">
              <button type="submit" class="btn_search">Search</button>
            </form>
          </div>
        </div>
        <div class="setting">
          <ul class="clearfix">
            <li><a href="#">文字サイズ・色合い変更</a></li>
            <li><a href="#">音声読み上げ</a></li>
            <li><a href="#">Foreign Language</a></li>
          </ul>
        </div>
      </div>
    </div>
  </header>
  <!--end header-->
  <main id="main-content">
    <div class="container">
      <img src="./img/front/grid/mobile.jpg" class="show_on_mobile" alt="">
      <div id="frame-grid-wrapper">
        <div id="frame-grid">
          <div class="emergency_panel clearfix">
            <label>緊急情報</label>
            <a href="#">弾道ミサイル落下時の行動等について</a>
          </div>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img1.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img2.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img3.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img4.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img5.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img6.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img7.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame line_sknew">
            <a href="#">
              <figure><img src="./img/front/grid/logo_center.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img8.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img9.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img10.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img11.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img12.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img13.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img17.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img14.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img15.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img16.jpg" alt=""></figure>
            </a>
          </article>
        </div>
      </div>
      <div class="link_primary">
        <a href="#" class="link_cr">
          <span class="icons_people">&nbsp;</span>
          <span class="txt">県民向け<br/>
          情報</span>
        </a>
        <a href="#" class="link_cr">
          <span class="icons_build">&nbsp;</span>
          <span class="txt">事業者<br/>
          情報</span>
        </a>
        <a href="#" class="link_cr">
          <span class="icons_camera">&nbsp;</span>
          <span class="txt">魅力・観光<br/>
          情報</span>
        </a>
      </div>
      <div class="menu_primary">
        <div class="list">
          <a href="#"><span>復興のその先へ</span></a>
          <a href="#"><span>移住定住応援</span></a>
          <a href="#"><span>仕事・就職応援</span></a>
        </div>
      </div>
      <div class="action_control">
        <button class="button_slider button_play">PLAY</button>
        <button class="button_slider button_pause">STOP</button>
      </div>
      <img src="./img/front/footer_bottom.png" class="show_on_mobile bottom" alt="">
    </div>
  </main>
  <!--end main-->
  <footer id="footer">
    <div class="footer_top">
      <div class="container">
        <h2 class="logo_footer">岩手県庁</h2>
        <address class="address_footer">
          <span>法人番号：4000020030007</span>
          <span>〒020-8570 岩手県盛岡市内丸10番1号</span>
          <span>電話番号：019-651-3111（総合案内）</span>
        </address>
      </div>
    </div>
    <div class="footer_copyright">
      <div class="container">
        <p>Copyright © Iwate Prefecture Government All Rights Reserved.</p>
      </div>
    </div>
  </footer>
  <!--end footer-->
</div>
```

**Scale Wrapper**

```javascript
var ScaleIsotope = {
	wrapper : $('#frame-grid-wrapper'),
	child : $('#frame-grid'),
	keep_width: 1624,
	calculate : function () {
		if ($(window).width() > 480){
			if (ScaleIsotope.wrapper.width() < ScaleIsotope.keep_width){
				var scale = ScaleIsotope.wrapper.width() / ScaleIsotope.keep_width,
					height = ScaleIsotope.child.height() * scale;
				console.log(scale);
				console.log(ScaleIsotope.child.height());
				ScaleIsotope.child.css({
					'transform' : 'scale(' + scale + ')'
				});
				ScaleIsotope.wrapper.css({
					'height' : height + 1
				})
			}else{
				ScaleIsotope.child.css({
					'transform' : 'scale(1)'
				});
				ScaleIsotope.wrapper.css({
					'height' : 'auto'
				})
			}
		}else{
			ScaleIsotope.child.css({
				'transform' : 'scale(1)'
			});
			ScaleIsotope.wrapper.css({
				'height' : 'auto'
			})
		}
	}
}

$(window).on('load',function () {
	var grid = $('#frame-grid').isotope({
		itemSelector: '.frame',
	})
	ScaleIsotope.calculate();
});

$(window).on('resize',function() {
	ScaleIsotope.calculate();
})
```

#### Version 2

**>Demo 1**

>JavaScript Code:
```javascript
var tw = new TimelineMax(),
  tw2 = new TimelineMax(),
  control = $('#btn_animation_control'),
  Animation = {
    handle: {
      main: new TimelineMax(),
      two: new TimelineMax(),
      dot: new TimelineMax(),
      image: new Array(),
    },
    control: $('#btn_animation_control'),
    init: function() {
      Animation.show_header_and_footer();
      Animation.logo_center();
      Animation.control.on('click', Animation.control_handle);
    },
    //Show logo
    logo_center: function() {
      Animation.handle.main.to('.logo_center', 1.5, {
        opacity: 1,
        ease: Power2.easeIn,
        onComplete: function() {
          Animation.grid();
        }
      });
    },
    // Show grid
    grid: function() {
      var arr = [];
      for (var i = 0; i < $('.frame').length - 1; i++) {
        arr[i] = i;
      }
      shuffle(arr);
      for (var j = 0; j < arr.length; j++) {
        Animation.handle.image[j] = new TimelineMax();
        Animation.show_image(Animation.handle.image[j], $('.frame').not('.logo_center').eq(arr[j]).find('img'), j);
      }
    },
    show_image: function(tw, selector, index) {
      var position = {
        time: 0,
      }
      tw.delay(index * 0.2).to(position, 0.4, {
        time: 1,
        ease: Power2.easeIn,
        onUpdate: function() {
          selector.css({
            'opacity': position.time,
          })
        },
        onComplete: function() {
          if (index == $('.frame').length - 2) {
            Animation.show_inside_content();
          }
        }
      });
    },
    show_inside_content: function() {
      var position = {
        height: 0,
        emergency_y: -30,
        emergency_opacity: 0,
      };
      Animation.handle.main.to(position, 0.6, {
        height: 145,
        emergency_y: 0,
        emergency_opacity: 1,
        ease: Power2.easeOut,
        onUpdate: function() {
          $('.menu_primary').css({
            'height': position.height,
          });
          $('.emergency_panel').css({
            '-webkit-transform': 'translate3d(0,' + position.emergency_y + '%,0)',
            'transform': 'translate3d(0,' + position.emergency_y + '%,0)',
            'opacity': position.emergency_opacity
          });
        },
        onStart: function() {
          $('.link_primary').css({
            'opacity': 1
          });
          Animation.bounce(Animation.handle.dot, $('.link_primary .link_cr'));
        }
      });
      Animation.show_three_btn();
    },
    show_three_btn: function() {
      var position = {
        y: 40,
        opacity: 0
      };
      Animation.handle.main.to(position, 0.4, {
        y: 0,
        opacity: 1,
        onUpdate: function() {
          $('.menu_primary .list').css({
            '-webkit-transform': 'translate3d(0,' + position.y + '%,0)',
            'transform': 'translate3d(0,' + position.y + '%,0)',
            'opacity': position.opacity
          });
        },
        onComplete: function() {
          $('#btn_animation_control').attr('disabled', true);
        }
      });
    },
    show_header_and_footer: function() {
      var position = {
        y: 101,
        opacity: 0
      };
      Animation.handle.main.to(position, 0.5, {
        y: 0,
        opacity: 1,
        onUpdate: function() {
          $('#footer').css({
            '-webkit-transform': 'translate3d(0,' + position.y + '%,0)',
            'transform': 'translate3d(0,' + position.y + '%,0)',
            'opacity': position.opacity
          });
          $('#header').css({
            '-webkit-transform': 'translate3d(0,-' + position.y + '%,0)',
            'transform': 'translate3d(0,-' + position.y + '%,0)',
            'opacity': position.opacity
          });
        }
      });
    },
    show_logo: function() {
      var position = {
          x: -50,
          opacity: 0
        },
        img_pos = {
          scale: 1.2,
          opacity: 0
        };
      Animation.handle.main.to(position, 0.5, {
        x: 0,
        opacity: 1,
        onUpdate: function() {
          $('#header .logo').css({
            '-webkit-transform': 'translate3d(' + position.x + '%,0,0)',
            'transform': 'translate3d(' + position.x + '%,0,0)',
            'opacity': position.opacity
          });
        }
      });
      Animation.handle.main.to(img_pos, 0.5, {
        scale: 1,
        opacity: 1,
        onUpdate: function() {
          $('#header .logo img').css({
            '-webkit-transform': 'scale3d(' + img_pos.scale + ',' + img_pos.scale + ',' + img_pos.scale + ')',
            'transform': 'scale3d(' + img_pos.scale + ',' + img_pos.scale + ',' + img_pos.scale + ')',
            'opacity': img_pos.opacity
          });
        }
      });
    },
    // Handle control
    bounce: function(tw, selector) {

      tw.to(selector, 0.01, {
        scale: 0.5,
        ease: Elastic.easeOut.config(1, 0.3),
        onUpdate: function() {
          selector.css({
            'opacity': 1
          })
        }
      });
      tw.to(selector, 0.02, { scale: 1.8, delay: 0.02, ease: Elastic.easeOut.config(1, 0.3) });
      tw.to(selector, 0.04, { scale: 1.2, delay: 0.02, ease: Elastic.easeOut.config(1, 0.3) });
      tw.to(selector, 0.02, { scale: 2.8, delay: 0.03, ease: Elastic.easeOut.config(1, 0.3) });
      tw.to(selector, 0.04, { scale: 1.6, delay: 0.01, ease: Elastic.easeOut.config(1, 0.3) });
      tw.to(selector, 0.02, { scale: 1, delay: 0.01, ease: Elastic.easeOut.config(1, 0.3) });
    },
    control_handle: function() {
      Animation.handle.main.paused(!Animation.handle.main.paused());
      Animation.handle.two.paused(!Animation.handle.two.paused());
      Animation.handle.dot.paused(!Animation.handle.dot.paused());
      for (var i = 0; i < Animation.handle.image.length; i++) {
        Animation.handle.image[i].paused(!Animation.handle.image[i].paused());
      }
      Animation.control.text(Animation.handle.main.paused() ? "PLAY" : "STOP");
      Animation.control.toggleClass('button_pause');
      Animation.control.toggleClass('button_play');
    },
  };

$(window).on('load', function() {
  Animation.init();
});

function getCurrentPositionByTime(start, end, start_time, end_time, current_time) {
  return start + (end - start) * current_time / (end_time - start_time);
}

function shuffle(a) {
  var j, x, i;
  for (i = a.length - 1; i > 0; i--) {
    j = Math.floor(Math.random() * (i + 1));
    x = a[i];
    a[i] = a[j];
    a[j] = x;
  }
}
```

>CSS Code:
```javascript
@media (min-width: 376px) {
  #header {
    position: relative;
    z-index: 1;
    transform: translate(0, -101%);
    -moz-transform: translate(0, -101%);
    -webkit-transform: translate(0, -101%);
    opacity: 0;
  }
  #footer {
    opacity: 0;
    transform: translate3d(0, 101%, 0);
    -webkit-transform: translate3d(0, 101%, 0);
  }
  .logo {
    background-color: #ffffff;
  }
  .logo_center {
    opacity: 0;
  }
  @keyframes logo {
    0% {
      opacity: 0;
      transform: scale(1.2);
      -moz-transform: scale(1.2);
      -webkit-transform: scale(1.2);
    }
    100% {
      transform: scale(1);
      -moz-transform: scale(1);
      -webkit-transform: scale(1);
      opacity: 1;
    }
  }
  .logo_center.active {
    -webkit-animation-name: logo;
    animation-name: logo;
    -webkit-animation-duration: 0.7s;
    animation-duration: 0.7s;
    -webkit-animation-fill-mode: both;
    animation-fill-mode: both;
  }
  #frame-grid .logo_center a:before,
  #frame-grid .logo_center a:after {
    -webkit-transition: 0.2s ease all;
    -o-transition: 0.2s ease all;
    transition: 0.2s ease all;
  }
  .frame:not(.logo_center) img {
    opacity: 0;
  }
  .frame.start img {
    animation-fill-mode: forwards;
    animation-timing-function: cubic-bezier(.7, 0, .3, 1);
    animation-duration: .9s;
  }
  .logo_center figure:before {
    /* content: ''; */
    position: absolute;
    bottom: 15px;
    width: 40px;
    height: 375px;
    left: 135px;
    z-index: 9;
    background-color: #ffffff;
  }

  .show_logo img {
    opacity: 1;
  }
  .show_logo figure:before {
    /*animation: show_text 2.4s 1;
    -webkit-animation: show_text 2.4s 1;
    -moz-animation: show_text 2.4s 1;
    animation-fill-mode: forwards;*/
  }

  @keyframes show_text {
    0% {
      height: 375px;
    }
    50% {
      height: 375px;
    }
    100% {
      height: 0px;
    }
  }

  @-webkit-keyframes pulse {
    from {
      -webkit-transform: scale3d(1, 1, 1);
      transform: scale3d(1, 1, 1);
    }

    50% {
      -webkit-transform: scale3d(1.05, 1.05, 1.05);
      transform: scale3d(1.05, 1.05, 1.05);
    }

    to {
      -webkit-transform: scale3d(1, 1, 1);
      transform: scale3d(1, 1, 1);
    }
  }

  @keyframes pulse {
    from {
      -webkit-transform: scale3d(1, 1, 1);
      transform: scale3d(1, 1, 1);
    }

    50% {
      -webkit-transform: scale3d(1.05, 1.05, 1.05);
      transform: scale3d(1.05, 1.05, 1.05);
    }

    to {
      -webkit-transform: scale3d(1, 1, 1);
      transform: scale3d(1, 1, 1);
    }
  }

  .pulse {
    -webkit-animation-name: pulse;
    animation-name: pulse;
  }

  @-webkit-keyframes fadeIn {
    from {
      opacity: 0;
    }

    to {
      opacity: 1;
    }
  }

  @keyframes fadeIn {
    from {
      opacity: 0;
    }
    to {
      opacity: 1;
    }
  }

  .fadeIn {
    -webkit-animation-name: fadeIn;
    animation-name: fadeIn;
    animation-fill-mode: forwards;
  }
}
```

>HTML Code:
```javascript
<div id="wrapper">
  <header id="header">
    <div class="container">
      <h1 class="logo">
        <a href="#">
          <picture>
            <source media="(max-width: 650px)" srcset="./img/front/sp_logo.png" width="152" height="88">
            <img src="./img/front/logo.png" alt="logo" width="200" height="200">
          </picture>
        </a>
      </h1>
      <ul class="navigation_sp">
        <li>
          <a href="#">
            <span class="symbol">
              <i class="icons_marker">&nbsp;</i>
            </span>
            <span class="nav_text">アクセス</span>
          </a>
        </li>
        <li>
          <a href="#">
            <span class="symbol">
              <i class="icons_phone">&nbsp;</i>
            </span>
            <span class="nav_text">直通電話</span>
          </a>
        </li>
        <li>
          <a href="#">
            <span class="symbol">
              <i class="icons_nav">&nbsp;</i>
            </span>
            <span class="nav_text">メニュー</span>
          </a>
        </li>
      </ul>
      <div class="top_header">
        <div class="search_panel">
          <label>サイト内検索</label>
          <div class="search_action">
            <form class="search_form" action="" method="">
              <input type="text" placeholder="Google カスタム検索">
              <button type="submit" class="btn_search">Search</button>
            </form>
          </div>
        </div>
        <div class="setting">
          <ul class="clearfix">
            <li><a href="#">文字サイズ・色合い変更</a></li>
            <li><a href="#">音声読み上げ</a></li>
            <li><a href="#">Foreign Language</a></li>
          </ul>
        </div>
      </div>
    </div>
  </header>
  <!--end header-->
  <main id="main-content">
    <div class="container">
      <img src="./img/front/grid/mobile.jpg" class="show_on_mobile" alt="">
      <div id="frame-grid-wrapper">
        <div id="frame-grid">
          <div class="emergency_panel clearfix">
            <label>緊急情報</label>
            <a href="#">弾道ミサイル落下時の行動等について</a>
          </div>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img1.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img2.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img3.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img4.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img5.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img6.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img7.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame logo_center">
            <a href="#">
              <figure><img src="./img/front/grid/logo_center.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img8.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img9.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img10.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img11.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img12.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img13.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img14.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img15.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img16.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img17.jpg" alt=""></figure>
            </a>
          </article>
        </div>
      </div>
      <div class="link_primary">
          <a href="#" class="link_cr">
            <span class="icons_people">&nbsp;</span>
            <span class="txt">県民向け<br/>
            情報</span>
          </a>
          <a href="#" class="link_cr">
            <span class="icons_build">&nbsp;</span>
            <span class="txt">事業者<br/>
            情報</span>
          </a>
          <a href="#" class="link_cr">
            <span class="icons_camera">&nbsp;</span>
            <span class="txt">魅力・観光<br/>
            情報</span>
          </a>
        </div>
        <div class="menu_primary">
          <div class="list">
            <a href="#"><span>復興のその先へ</span></a>
            <a href="#"><span>移住定住応援</span></a>
            <a href="#"><span>仕事・就職応援</span></a>
          </div>
        </div>
        <div class="action_control">
            <button id="btn_animation_control" class="button_slider button_pause">STOP</button>
        </div>
        <img src="./img/front/footer_bottom.png" class="show_on_mobile bottom" alt="">
    </div>
  </main>
  <!--end main-->
  <footer id="footer">
    <div class="footer_top">
      <div class="container">
        <h2 class="logo_footer">岩手県庁</h2>
        <address class="address_footer">
          <span>法人番号：4000020030007</span>
          <span>〒020-8570 岩手県盛岡市内丸10番1号</span>
          <span>電話番号：019-651-3111（総合案内）</span>
        </address>
      </div>
    </div>
    <div class="footer_copyright">
      <div class="container"><p>Copyright © Iwate Prefecture Government All Rights Reserved.</p></div>
    </div>
  </footer>
  <!--end footer-->
</div>
```

**>Demo 2**

>JavaScript Code:
```javascript
var tw = new TimelineMax(),
  tw2 = new TimelineMax(),
  control = $('#btn_animation_control'),
  Animation = {
    handle: {
      main: new TimelineMax(),
      two: new TimelineMax(),
      dot: new TimelineMax(),
      image: new Array(),
    },
    control: $('#btn_animation_control'),
    init: function() {
      Animation.start();
      Animation.control.on('click', Animation.control_handle);
    },
    //Show logo
    start: function() {
      Animation.handle.main.to('.logo_center', 1.5, {
        opacity: 1,
        ease: Power2.easeIn,
        onComplete: function() {
          Animation.grid();
        }
      });
    },
    // Show grid
    grid: function() {
      var arr = [];
      for (var i = 0; i < $('.frame').length - 1; i++) {
        arr[i] = i;
      }
      shuffle(arr);
      for (var j = 0; j < arr.length; j++) {
        Animation.handle.image[j] = new TimelineMax();
        Animation.show_image(Animation.handle.image[j], $('.frame').not('.logo_center').eq(arr[j]).find('img'), j);
      }
    },
    show_image: function(tw, selector, index) {
      var position = {
        time: 0,
        zoom: 0.3
      }
      tw.delay(index * 0.2).to(position, 0.4, {
        time: 1,
        zoom: 1,
        ease: Power2.easeOut,
        onUpdate: function() {
          selector.css({
            'opacity': position.time,
            '-webkit-transform': 'scale3d(' + position.zoom + ',' + position.zoom + ',' + position.zoom + ')',
            'transform': 'scale3d(' + position.zoom + ',' + position.zoom + ',' + position.zoom + ')',
          })
        },
        onComplete: function() {
          if (index == $('.frame').length - 2) {
            Animation.pulse_logo();
          }
        }
      });
    },
    pulse_logo: function() {
      var position = {
        zoom: 100
      }
      Animation.handle.main.to(position, 0.4, {
        zoom: 105,
        ease: Power2.easeOut,
        onStart: function() {
          Animation.handle.two.to(".logo_center .skew", 0.8, {
            width: 58,
            ease: Power2.easeOut
          })
        },
        onUpdate: function() {
          var zoom = position.zoom / 100;
          $('.logo_center').css({
            '-webkit-transform': 'scale3d(' + zoom + ',' + zoom + ',' + zoom + ')',
            'transform': 'scale3d(' + zoom + ',' + zoom + ',' + zoom + ')',
          });
        }
      });
      Animation.handle.main.to(position, 0.4, {
        zoom: 100,
        ease: Power2.easeOut,
        onUpdate: function() {
          var zoom = position.zoom / 100;
          $('.logo_center').css({
            '-webkit-transform': 'scale3d(' + zoom + ',' + zoom + ',' + zoom + ')',
            'transform': 'scale3d(' + zoom + ',' + zoom + ',' + zoom + ')',
          });
        }
      });
      Animation.show_inside_content();
    },
    show_inside_content: function() {
      var position = {
        height: 0,
        emergency_y: -30,
        emergency_opacity: 0,
      };
      Animation.handle.main.to(position, 0.6, {
        height: 145,
        emergency_y: 0,
        emergency_opacity: 1,
        ease: Power2.easeOut,
        onUpdate: function() {
          $('.menu_primary').css({
            'height': position.height,
          });
          $('.emergency_panel').css({
            '-webkit-transform': 'translate3d(0,' + position.emergency_y + '%,0)',
            'transform': 'translate3d(0,' + position.emergency_y + '%,0)',
            'opacity': position.emergency_opacity
          });
        },
        onStart: function() {
          $('.link_primary').css({
            'opacity': 1
          });
          Animation.bounce(Animation.handle.dot, $('.link_primary .link_cr'));
        }
      });
      Animation.show_three_btn();
    },
    show_three_btn: function() {
      var position = {
        y: 40,
        opacity: 0
      };
      Animation.handle.main.to(position, 0.4, {
        y: 0,
        opacity: 1,
        onUpdate: function() {
          $('.menu_primary .list').css({
            '-webkit-transform': 'translate3d(0,' + position.y + '%,0)',
            'transform': 'translate3d(0,' + position.y + '%,0)',
            'opacity': position.opacity
          });
        }
      });
      Animation.show_header_and_footer();
    },
    show_header_and_footer: function() {
      var position = {
        y: 101,
        opacity: 0
      };
      Animation.handle.main.to(position, 0.5, {
        y: 0,
        opacity: 1,
        onUpdate: function() {
          $('#footer').css({
            '-webkit-transform': 'translate3d(0,' + position.y + '%,0)',
            'transform': 'translate3d(0,' + position.y + '%,0)',
            'opacity': position.opacity
          });
          $('#header').css({
            '-webkit-transform': 'translate3d(0,-' + position.y + '%,0)',
            'transform': 'translate3d(0,-' + position.y + '%,0)',
          });
        }
      });
      Animation.show_logo();
    },
    show_logo: function() {
      var position = {
          x: -50,
          opacity: 0
        },
        img_pos = {
          scale: 1.2,
          opacity: 0
        };
      Animation.handle.main.to(position, 0.5, {
        x: 0,
        opacity: 1,
        onUpdate: function() {
          $('#header .logo').css({
            '-webkit-transform': 'translate3d(' + position.x + '%,0,0)',
            'transform': 'translate3d(' + position.x + '%,0,0)',
            'opacity': position.opacity
          });
        }
      });
      Animation.handle.main.to(img_pos, 0.5, {
        scale: 1,
        opacity: 1,
        onUpdate: function() {
          $('#header .logo img').css({
            '-webkit-transform': 'scale3d(' + img_pos.scale + ',' + img_pos.scale + ',' + img_pos.scale + ')',
            'transform': 'scale3d(' + img_pos.scale + ',' + img_pos.scale + ',' + img_pos.scale + ')',
            'opacity': img_pos.opacity
          });
        },
        onComplete: function() {
          $('#btn_animation_control').attr('disabled', true);
        }
      });
    },
    // Handle control
    bounce: function(tw, selector) {
      var position = {
        percent: 0
      }
      // tw.to(position,0.3,{
      // 	percent: 100,
      // 	onUpdate: function(){
      // 		var scale = 1,
      // 			opacity = 1;
      // 		if (position.percent <= 20){
      // 			scale = getCurrentPositionByTime(0.3,1.1,0,20,position.percent);
      // 		}else if (position.percent <= 40){
      // 			scale = getCurrentPositionByTime(1.1,0.9,20,40,position.percent);
      // 		}else if (position.percent <= 60){
      // 			scale = getCurrentPositionByTime(0.9,1.03,40,60,position.percent);
      // 		}else if (position.percent <= 80){
      // 			scale = getCurrentPositionByTime(1.03,0.97,60,80,position.percent);
      // 		}else if (position.percent < 100){
      // 			scale = getCurrentPositionByTime(0.97,1,80,100,position.percent);
      // 		}
      // 		if (position.percent < 60){
      // 			opacity = getCurrentPositionByTime(0,1,0,60,position.percent);
      // 		}
      // 		selector.css({
      // 			'-webkit-transform': 'scale3d('+scale+','+scale+','+scale+')',
      // 			'transform': 'scale3d('+scale+','+scale+','+scale+')',
      // 			'opacity': opacity
      // 		})
      // 	}
      // })
      tw.to(selector, 0.01, {
        scale: 0.5,
        ease: Elastic.easeOut.config(1, 0.3),
        onUpdate: function() {
          selector.css({
            'opacity': 1
          })
        }
      });
      tw.to(selector, 0.02, { scale: 1.8, delay: 0.02, ease: Elastic.easeOut.config(1, 0.3) });
      tw.to(selector, 0.04, { scale: 1.2, delay: 0.02, ease: Elastic.easeOut.config(1, 0.3) });
      tw.to(selector, 0.02, { scale: 2.8, delay: 0.03, ease: Elastic.easeOut.config(1, 0.3) });
      tw.to(selector, 0.04, { scale: 1.6, delay: 0.01, ease: Elastic.easeOut.config(1, 0.3) });
      tw.to(selector, 0.02, { scale: 1, delay: 0.01, ease: Elastic.easeOut.config(1, 0.3) });
    },
    control_handle: function() {
      Animation.handle.main.paused(!Animation.handle.main.paused());
      Animation.handle.two.paused(!Animation.handle.two.paused());
      Animation.handle.dot.paused(!Animation.handle.dot.paused());
      for (var i = 0; i < Animation.handle.image.length; i++) {
        Animation.handle.image[i].paused(!Animation.handle.image[i].paused());
      }
      Animation.control.text(Animation.handle.main.paused() ? "PLAY" : "STOP");
      Animation.control.toggleClass('button_pause');
      Animation.control.toggleClass('button_play');
    },
  };

$(window).on('load', function() {
  Animation.init();
});

function getCurrentPositionByTime(start, end, start_time, end_time, current_time) {
  return start + (end - start) * current_time / (end_time - start_time);
}

function shuffle(a) {
  var j, x, i;
  for (i = a.length - 1; i > 0; i--) {
    j = Math.floor(Math.random() * (i + 1));
    x = a[i];
    a[i] = a[j];
    a[j] = x;
  }
}
```

>CSS Code:
```javascript
@media(min-width: 376px) {
  /* Ready state */
  #wrapper.ready #header {
    transition: 0.6s ease all;
    -webkit-transition: 0.6s ease all;
    -moz-transition: 0.6s ease all;
  }
  #wrapper.ready #header .logo {
    transition: 0.5s ease all;
    -webkit-transition: 0.5s ease all;
    -moz-transition: 0.5s ease all;
    /*     transition-delay: 1s;
    -webkit-transition-delay: 1s;
    -o-transition-delay: 1s; */
  }
  #wrapper.ready #header .logo img {
    transition: opacity 0.3s ease-in-out 0.5s, transform 0.3s ease-in-out 0.5s;
    -moz-transition: opacity 0.3s ease-in-out 0.5s, transform 0.3s ease-in-out 0.5s;
    -webkit-transition: opacity 0.3s ease-in-out 0.5s, transform 0.3s ease-in-out 0.5s;
    /*     transition-delay: 2s;
    -webkit-transition-delay: 1.8s;
    -o-transition-delay: 2s; */
  }
  #wrapper.ready #footer .footer_container {
    transition: 0.6s ease all;
    -webkit-transition: 0.6s ease all;
    -moz-transition: 0.6s ease all;
  }
  #wrapper.ready .logo_center img {
    -webkit-transition: 1s ease opacity;
    -o-transition: 1s ease opacity;
    transition: 1s ease opacity;
  }
  /* Header */
  #header {
    transform: translate(0, -101%);
    -moz-transform: translate(0, -101%);
    -webkit-transform: translate(0, -101%);
    position: relative;
    z-index: 99;
  }
  #header.active {
    transform: none;
    -webkit-transform: none;
    -moz-transform: none;
  }
  #header .logo {
    background-color: #ffffff;
    transform: translate(-50%, 0);
    -moz-transform: translate(-5%, 0);
    -webkit-transform: translate(-50%, 0);
    opacity: 0;
  }
  #header .logo img {
    -ms-filter: "progid:DXImageTransform.Microsoft.Alpha(Opacity=0)";
    filter: alpha(opacity=0);
    -moz-opacity: 0;
    -khtml-opacity: 0;
    opacity: 0;
    transform: scale(1.2);
    -moz-transform: scale(1.2);
    -webkit-transform: scale(1.2);
  }
  #header.active .logo {
    transform: translate(0, 0);
    -moz-transform: translate(0, 0);
    -webkit-transform: translate(0, 0);
    opacity: 1;
  }
  #header.active .logo img {
    -ms-filter: "progid:DXImageTransform.Microsoft.Alpha(Opacity=100)";
    filter: alpha(opacity=100);
    -moz-opacity: 1;
    -khtml-opacity: 1;
    opacity: 1;
    transform: scale(1);
    -moz-transform: scale(1);
    -webkit-transform: scale(1);
  }
  /* Footer */
  #footer {
    position: relative;
    z-index: 99;
    overflow: hidden;
    opacity: 0;
    transform: translate3d(0, 101%, 0);
    -webkit-transform: translate3d(0, 101%, 0);
  }
  /* Grid */
  #frame-grid .logo_center .top_skew,
  #frame-grid .logo_center a:before {
    background-position: right bottom;
  }
  #frame-grid .logo_center .bottom_skew,
  #frame-grid .logo_center a:after {
    background-position: left top;
  }
  #frame-grid .logo_center .skew {
    width: 0;
  }
  #frame-grid .logo_center a:before,
  #frame-grid .logo_center a:after {
    width: 0;
    -webkit-transition: 0.8s ease all;
    -o-transition: 0.8s ease all;
    transition: 0.8s ease all;
  }
  #frame-grid .logo_center.pulse a:before,
  #frame-grid .logo_center.pulse a:after {
    width: 58px;
  }
  #frame-grid .logo_center {
    opacity: 0;
  }
  #frame-grid .frame:not(.logo_center) img {
    opacity: 0;
  }
  .frame.start img {
    animation-fill-mode: forwards;
    animation-timing-function: ease-out;
    animation-duration: 500ms;
  }
  .show_logo img {
    opacity: 1;
  }
  .show_logo .light {
    animation: show_text 2.4s 1;
    -webkit-animation: show_text 2.4s 1;
    -moz-animation: show_text 2.4s 1;
    animation-fill-mode: forwards;
  }

  @keyframes show_text {
    0% {
      height: 375px;
    }
    50% {
      height: 375px;
    }
    100% {
      height: 0px;
    }
  }

  @-webkit-keyframes pulse {
    from {
      -webkit-transform: scale3d(1, 1, 1);
      transform: scale3d(1, 1, 1);
    }

    50% {
      -webkit-transform: scale3d(1.05, 1.05, 1.05);
      transform: scale3d(1.05, 1.05, 1.05);
    }

    to {
      -webkit-transform: scale3d(1, 1, 1);
      transform: scale3d(1, 1, 1);
    }
  }

  @keyframes pulse {
    from {
      -webkit-transform: scale3d(1, 1, 1);
      transform: scale3d(1, 1, 1);
    }

    50% {
      -webkit-transform: scale3d(1.05, 1.05, 1.05);
      transform: scale3d(1.05, 1.05, 1.05);
    }

    to {
      -webkit-transform: scale3d(1, 1, 1);
      transform: scale3d(1, 1, 1);
    }
  }

  .pulse {
    -webkit-animation-name: pulse;
    animation-name: pulse;
  }

  @-webkit-keyframes zoomIn {
    from {
      opacity: 0;
      -webkit-transform: scale3d(0.3, 0.3, 0.3);
      transform: scale3d(0.3, 0.3, 0.3);
    }

    50% {
      opacity: 1;
    }
    to {
      opacity: 1;
    }
  }

  @keyframes zoomIn {
    from {
      opacity: 0;
      -webkit-transform: scale3d(0.3, 0.3, 0.3);
      transform: scale3d(0.3, 0.3, 0.3);
    }

    50% {
      opacity: 1;
    }

    to {
      opacity: 1;
    }
  }

  .zoomIn {
    -webkit-animation-name: zoomIn;
    animation-name: zoomIn;
  }
}
```

>HTML Code:
```javascript
<div id="wrapper">
  <header id="header">
    <div class="container">
      <h1 class="logo">
        <a href="#">
          <picture>
            <source media="(max-width: 650px)" srcset="./img/front/sp_logo.png" width="152" height="88">
            <img src="./img/front/logo.png" alt="logo" width="200" height="200">
          </picture>
        </a>
      </h1>
      <ul class="navigation_sp">
        <li>
          <a href="#">
            <span class="symbol">
              <i class="icons_marker">&nbsp;</i>
            </span>
            <span class="nav_text">アクセス</span>
          </a>
        </li>
        <li>
          <a href="#">
            <span class="symbol">
              <i class="icons_phone">&nbsp;</i>
            </span>
            <span class="nav_text">直通電話</span>
          </a>
        </li>
        <li>
          <a href="#">
            <span class="symbol">
              <i class="icons_nav">&nbsp;</i>
            </span>
            <span class="nav_text">メニュー</span>
          </a>
        </li>
      </ul>
      <div class="top_header">
        <div class="search_panel">
          <label>サイト内検索</label>
          <div class="search_action">
            <form class="search_form" action="" method="">
              <input type="text" placeholder="Google カスタム検索">
              <button type="submit" class="btn_search">Search</button>
            </form>
          </div>
        </div>
        <div class="setting">
          <ul class="clearfix">
            <li><a href="#">文字サイズ・色合い変更</a></li>
            <li><a href="#">音声読み上げ</a></li>
            <li><a href="#">Foreign Language</a></li>
          </ul>
        </div>
      </div>
    </div>
  </header>
  <!--end header-->
  <main id="main-content">
    <div class="container">
      <img src="./img/front/grid/mobile.jpg" class="show_on_mobile" alt="">
      <div id="frame-grid-wrapper">
        <div id="frame-grid">
          <div class="emergency_panel clearfix">
            <label>緊急情報</label>
            <a href="#">弾道ミサイル落下時の行動等について</a>
          </div>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img1.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame double">
            <a href="#">
              <figure><img src="./img/front/grid/img2.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img3.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img4.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame double">
            <a href="#">
              <figure><img src="./img/front/grid/img5.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame double">
            <a href="#">
              <figure><img src="./img/front/grid/img6.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img7.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame logo_center">
            <a href="#">
              <span class="skew top_skew"></span>
              <figure><img src="./img/front/grid/logo_center.jpg" alt=""></figure>
              <span class="skew bottom_skew"></span>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img8.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img9.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img10.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img11.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame double">
            <a href="#">
              <figure><img src="./img/front/grid/img12.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img13.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img14.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img15.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img16.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img17.jpg" alt=""></figure>
            </a>
          </article>
        </div>
      </div>
    </div>
    <div class="link_primary">
      <a href="#" class="link_cr">
        <span class="icons_people">&nbsp;</span>
        <span class="txt">県民向け<br/>
        情報</span>
      </a>
      <a href="#" class="link_cr">
        <span class="icons_build">&nbsp;</span>
        <span class="txt">事業者<br/>
        情報</span>
      </a>
      <a href="#" class="link_cr">
        <span class="icons_camera">&nbsp;</span>
        <span class="txt">魅力・観光<br/>
        情報</span>
      </a>
    </div>
    <div class="menu_primary">
      <div class="list">
        <a href="#"><span>復興のその先へ</span></a>
        <a href="#"><span>移住定住応援</span></a>
        <a href="#"><span>仕事・就職応援</span></a>
      </div>
    </div>
    <div class="action_control">
      <button id="btn_animation_control" class="button_slider button_pause">STOP</button>
    </div>
    <img src="./img/front/footer_bottom.png" class="show_on_mobile bottom" alt="">
  </main>
  <!--end main-->
  <footer id="footer">
    <div class="footer_container">
      <div class="footer_top">
        <div class="container">
          <h2 class="logo_footer">岩手県庁</h2>
          <address class="address_footer">
            <span>法人番号：4000020030007</span>
            <span>〒020-8570 岩手県盛岡市内丸10番1号</span>
            <span>電話番号：019-651-3111（総合案内）</span>
          </address>
        </div>
      </div>
      <div class="footer_copyright">
        <div class="container">
          <p>Copyright © Iwate Prefecture Government All Rights Reserved.</p>
        </div>
      </div>
    </div>
  </footer>
  <!--end footer-->
</div>
```

**>Demo 3**

>JavaScript Code:
```javascript
var page = 0;
var gallery = $('#frame-grid');
var frame_item = document.querySelectorAll('#frame-grid .frame');
var Gallery = {
  Selector: {
    loading: '.loading',
    loading_wrap: '.loading-logo',
    loading_outline: '.logo-outline'
  },
  init: function() {
    Gallery.loadingScreen();
  },
  loadingScreen: function() {
    if ($(window).width() > 480) {
      $(Gallery.Selector.loading_outline).removeAttr('style');
      TweenLite.to($(".logo-outline"), 1.5, {
        height: 0,
        ease: Power1.easeInOut,
        onComplete: function() {
          TweenLite.to($(Gallery.Selector.loading), 0.3, {
            yPercent: -100,
            ease: Power1.easeInOut,
            delay: 0.05,
            onComplete: function() {
              TweenLite.set($(Gallery.Selector.loading), { autoAlpha: 0, yPercent: 100 });
              setTimeout(function() {
                Gallery.execute();
              }, 200);
            }
          });
        }
      });
    } else {
      Gallery.execute();
    }
  },
  header: function() {
    $('#header').addClass('fadeInDown');
  },
  footer: function() {
    $('#footer').addClass('fadeInUp');
  },
  logo: function() {

  },
  showPhotos: function() {
    // Animate the images from the top-left
    var photos = gallery.find('.frame a');
    console.log($('.frame').length);
    for (var j = 0; j < $('.frame').length; j++) {
      (function(j) {
        setTimeout(function() {
          photos.eq(j).addClass('show');
        }, j * 40);
      })(j);
    }
  },
  showPrimary: function() {
    $('.menu_primary .list').addClass('fadeInUpSmall');
  },
  showEmergency: function() {
    $('.emergency_panel').addClass('fadeInDownSmall');
  },
  showMoutain: function() {
    $('.menu_primary').addClass('showMoutain');
  },
  showCricle: function() {
    $('.link_primary').addClass('active');
    $('.link_cr').addClass('bounceIn');
  },
  execute: function() {
    Gallery.showPhotos();
    Gallery.header();
    Gallery.footer();
    $('.frame').eq(17).on('transitionend webkitTransitionEnd oTransitionEnd', Gallery.showEmergency);

    $('.frame').eq(17).on('transitionend webkitTransitionEnd oTransitionEnd', Gallery.showMoutain);

    $('.frame').eq(17).on('transitionend webkitTransitionEnd oTransitionEnd', Gallery.showCricle);

    $('.menu_primary')[0].addEventListener('webkitAnimationEnd', Gallery.showPrimary);
    $('.menu_primary')[0].addEventListener('animationend', Gallery.showPrimary);
  }
}

$(document).ready(function() {
  Gallery.init();
});
```

>CSS Code:
```javascript
@font-face {
  font-family: 'a-otf_jomin_stdl';
  src: url('/fonts/jominstd-light.woff2') format('woff2'),
  url('/fonts/jominstd-light.woff') format('woff');
  font-weight: normal;
  font-style: normal;
}

#header,
#footer {
  position: relative;
  z-index: 50;
  opacity: 0;
  -webkit-animation-duration: 1s;
  animation-duration: 1s;
  -webkit-animation-fill-mode: both;
  animation-fill-mode: both;
}

#header .logo {
  background-color: #ffffff;
}

.loading {
  position: fixed;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  background: #fff;
  z-index: 101;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.loading img {
  max-width: inherit;
}

.loading .loader {
  position: absolute;
  width: 100px;
  height: 100px;
  left: 50%;
  top: 50%;
  transform: translateX(-50%) translateY(-50%) rotate(-90deg);
  -webkit-transform: translateX(-50%) translateY(-50%) rotate(-90deg);
}

.loading-logo {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -70%);
  -webkit-transform: translate(-50%, -70%);
}

.logo-outline {
  position: absolute;
  width: 230px;
  height: 412px;
  top: 0;
  left: 0;
  z-index: 2;
  background: #fff;
}

.loadingtitle {
  position: fixed;
  font-family: 'a-otf_jomin_stdl';
  font-size: 43px;
  line-height: 45px;
  width: 100%;
  text-align: center;
  top: 65vh;
  transform: translateY(50%);
  -webkit-transform: translateY(50%);
  color: #a7811a;
  z-index: 105;

  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.loadingtitle span {
  display: inline-block;
  transform: translateY(24px);
  -webkit-transform: translateY(24px);
  /* opacity: 0;
  visibility: hidden; */
}

.frame a {
  opacity: 0;
  float: left;
  background-size: cover;
  background-position: center center;

  -webkit-transform: scale(0.8);
  -moz-transform: scale(0.8);
  transform: scale(0.8);

  -webkit-transition: 0.4s;
  -moz-transition: 0.4s;
  transition: 0.4s;
}

.frame a.show:hover {
  opacity: 0.9 !important;
}

.frame a.show {
  opacity: 1;
  -webkit-transform: scale(1);
  -moz-transform: scale(1);
  transform: scale(1);
}

@-webkit-keyframes fadeInDown {
  from {
    opacity: 0;
    -webkit-transform: translate3d(0, -100%, 0);
    transform: translate3d(0, -100%, 0);
  }

  to {
    opacity: 1;
    -webkit-transform: translate3d(0, 0, 0);
    transform: translate3d(0, 0, 0);
  }
}

@keyframes fadeInDown {
  from {
    opacity: 0;
    -webkit-transform: translate3d(0, -100%, 0);
    transform: translate3d(0, -100%, 0);
  }

  to {
    opacity: 1;
    -webkit-transform: translate3d(0, 0, 0);
    transform: translate3d(0, 0, 0);
  }
}

@-webkit-keyframes fadeInUp {
  from {
    opacity: 0;
    -webkit-transform: translate3d(0, 100%, 0);
    transform: translate3d(0, 100%, 0);
  }

  to {
    opacity: 1;
    -webkit-transform: translate3d(0, 0, 0);
    transform: translate3d(0, 0, 0);
  }
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    -webkit-transform: translate3d(0, 100%, 0);
    transform: translate3d(0, 100%, 0);
  }

  to {
    opacity: 1;
    -webkit-transform: translate3d(0, 0, 0);
    transform: translate3d(0, 0, 0);
  }
}

.animated {
  -webkit-animation-duration: 1s;
  animation-duration: 1s;
  -webkit-animation-fill-mode: both;
  animation-fill-mode: both;
}

.fadeInDown {
  -webkit-animation-name: fadeInDown;
  animation-name: fadeInDown;
}

.fadeInUp {
  -webkit-animation-name: fadeInUp;
  animation-name: fadeInUp;
}

@media(max-width: 480px) {
  .loading {
    display: none;
    visibility: hidden;
    opacity: 0;
  }
}
```

>HTML Code:
```javascript
<div id="wrapper">
<div class="loading">
  <div class="loading-logo">
    <img src="img/front/loading.png" width="230" height="412" alt="ひと・まち・しあわせ輝く">
    <div class="logo-outline">
      <img src="img/front/loading-outline.png" width="230" height="412" alt="ひと・まち・しあわせ輝く">
    </div>
  </div>
</div>
<header id="header">
  <div class="container">
    <h1 class="logo">
              <a href="#">
                <picture>
                  <source media="(max-width: 650px)" srcset="./img/front/sp_logo.png" width="152" height="88">
                  <img src="./img/front/logo.png" alt="logo" width="200" height="200">
                </picture>
              </a>
            </h1>
    <ul class="navigation_sp">
      <li>
        <a href="#">
                  <span class="symbol">
                    <i class="icons_marker">&nbsp;</i>
                  </span>
                  <span class="nav_text">アクセス</span>
                </a>
      </li>
      <li>
        <a href="#">
                  <span class="symbol">
                    <i class="icons_phone">&nbsp;</i>
                  </span>
                  <span class="nav_text">直通電話</span>
                </a>
      </li>
      <li>
        <a href="#">
                  <span class="symbol">
                    <i class="icons_nav">&nbsp;</i>
                  </span>
                  <span class="nav_text">メニュー</span>
                </a>
      </li>
    </ul>
    <div class="top_header">
      <div class="search_panel">
        <label>サイト内検索</label>
        <div class="search_action">
          <form class="search_form" action="" method="">
            <input type="text" placeholder="Google カスタム検索">
            <button type="submit" class="btn_search">Search</button>
          </form>
        </div>
      </div>
      <div class="setting">
        <ul class="clearfix">
          <li><a href="#">文字サイズ・色合い変更</a></li>
          <li><a href="#">音声読み上げ</a></li>
          <li><a href="#">Foreign Language</a></li>
        </ul>
      </div>
    </div>
  </div>
</header>
<!--end header-->
<main id="main-content">
  <div class="container">
    <img src="./img/front/grid/mobile.jpg" class="show_on_mobile" alt="">
    <div id="frame-grid-wrapper">
      <div id="frame-grid">
        <div class="emergency_panel clearfix">
          <label>緊急情報</label>
          <a href="#">弾道ミサイル落下時の行動等について</a>
        </div>
        <article class="frame">
          <a href="#">
            <figure><img src="./img/front/grid/img1.jpg" alt=""></figure>
          </a>
        </article>
        <article class="frame">
          <a href="#">
            <figure><img src="./img/front/grid/img2.jpg" alt=""></figure>
          </a>
        </article>
        <article class="frame">
          <a href="#">
            <figure><img src="./img/front/grid/img3.jpg" alt=""></figure>
          </a>
        </article>
        <article class="frame">
          <a href="#">
            <figure><img src="./img/front/grid/img4.jpg" alt=""></figure>
          </a>
        </article>
        <article class="frame">
          <a href="#">
            <figure><img src="./img/front/grid/img5.jpg" alt=""></figure>
          </a>
        </article>
        <article class="frame">
          <a href="#">
            <figure><img src="./img/front/grid/img6.jpg" alt=""></figure>
          </a>
        </article>
        <article class="frame">
          <a href="#">
            <figure><img src="./img/front/grid/img7.jpg" alt=""></figure>
          </a>
        </article>
        <article class="frame logo_center">
          <a href="#">
            <figure><img src="./img/front/grid/logo_center.jpg" alt=""></figure>
          </a>
        </article>
        <article class="frame">
          <a href="#">
            <figure><img src="./img/front/grid/img8.jpg" alt=""></figure>
          </a>
        </article>
        <article class="frame">
          <a href="#">
            <figure><img src="./img/front/grid/img9.jpg" alt=""></figure>
          </a>
        </article>
        <article class="frame">
          <a href="#">
            <figure><img src="./img/front/grid/img10.jpg" alt=""></figure>
          </a>
        </article>
        <article class="frame">
          <a href="#">
            <figure><img src="./img/front/grid/img11.jpg" alt=""></figure>
          </a>
        </article>
        <article class="frame">
          <a href="#">
            <figure><img src="./img/front/grid/img12.jpg" alt=""></figure>
          </a>
        </article>
        <article class="frame">
          <a href="#">
            <figure><img src="./img/front/grid/img13.jpg" alt=""></figure>
          </a>
        </article>
        <article class="frame">
          <a href="#">
            <figure><img src="./img/front/grid/img14.jpg" alt=""></figure>
          </a>
        </article>
        <article class="frame">
          <a href="#">
            <figure><img src="./img/front/grid/img15.jpg" alt=""></figure>
          </a>
        </article>
        <article class="frame">
          <a href="#">
            <figure><img src="./img/front/grid/img16.jpg" alt=""></figure>
          </a>
        </article>
        <article class="frame">
          <a href="#">
            <figure><img src="./img/front/grid/img17.jpg" alt=""></figure>
          </a>
        </article>
      </div>
    </div>
    <div class="link_primary">
      <a href="#" class="link_cr">
                  <span class="icons_people">&nbsp;</span>
                  <span class="txt">県民向け<br/>
                  情報</span>
                </a>
      <a href="#" class="link_cr">
                  <span class="icons_build">&nbsp;</span>
                  <span class="txt">事業者<br/>
                  情報</span>
                </a>
      <a href="#" class="link_cr">
                  <span class="icons_camera">&nbsp;</span>
                  <span class="txt">魅力・観光<br/>
                  情報</span>
                </a>
    </div>
    <div class="menu_primary">
      <div class="list">
        <a href="#"><span>復興のその先へ</span></a>
        <a href="#"><span>移住定住応援</span></a>
        <a href="#"><span>仕事・就職応援</span></a>
      </div>
    </div>
    <img src="./img/front/footer_bottom.png" class="show_on_mobile bottom" alt="">
  </div>
</main>
<!--end main-->
<footer id="footer">
  <div class="footer_top">
    <div class="container">
      <h2 class="logo_footer">岩手県庁</h2>
      <address class="address_footer">
        <span>法人番号：4000020030007</span>
        <span>〒020-8570 岩手県盛岡市内丸10番1号</span>
        <span>電話番号：019-651-3111（総合案内）</span>
      </address>
    </div>
  </div>
  <div class="footer_copyright">
    <div class="container">
      <p>Copyright © Iwate Prefecture Government All Rights Reserved.</p>
    </div>
  </div>
</footer>
<!--end footer-->
</div>
```

**>Demo 4**

>JavaScript Code:
```javascript
var tw = new TimelineMax(),
  tw2 = new TimelineMax(),
  control = $('#btn_animation_control'),
  Animation = {
    handle: {
      main: new TimelineMax(),
      two: new TimelineMax(),
      dot: new TimelineMax(),
      image: new Array(),
    },
    control: $('#btn_animation_control'),
    init: function() {
      Animation.show_header_and_footer();
      Animation.logo_center();
      Animation.control.on('click', Animation.control_handle);
    },
    //Show logo
    logo_center: function() {
      Animation.handle.main.to('.logo_center', 1.5, {
        opacity: 1,
        ease: Power2.easeIn,
        onComplete: function() {
          Animation.grid();
        }
      });
    },
    // Show grid
    grid: function() {
      var arr = [];
      for (var i = 0; i < $('.frame').length - 1; i++) {
        arr[i] = i;
      }
      shuffle(arr);
      for (var j = 0; j < arr.length; j++) {
        Animation.handle.image[j] = new TimelineMax();
        Animation.show_image(Animation.handle.image[j], $('.frame').not('.logo_center').eq(arr[j]).find('img'), j);
      }
    },
    show_image: function(tw, selector, index) {
      var position = {
        time: 0,
      }
      tw.delay(index * 0.2).to(position, 0.4, {
        time: 1,
        ease: Power2.easeIn,
        onUpdate: function() {
          selector.css({
            'opacity': position.time,
          })
        },
        onComplete: function() {
          if (index == $('.frame').length - 2) {
            Animation.show_inside_content();
          }
        }
      });
    },
    show_inside_content: function() {
      var position = {
        height: 0,
        emergency_y: -30,
        emergency_opacity: 0,
      };
      Animation.handle.main.to(position, 0.6, {
        height: 145,
        emergency_y: 0,
        emergency_opacity: 1,
        ease: Power2.easeOut,
        onUpdate: function() {
          $('.menu_primary').css({
            'height': position.height,
          });
          $('.emergency_panel').css({
            '-webkit-transform': 'translate3d(0,' + position.emergency_y + '%,0)',
            'transform': 'translate3d(0,' + position.emergency_y + '%,0)',
            'opacity': position.emergency_opacity
          });
        },
        onStart: function() {
          $('.link_primary').css({
            'opacity': 1
          });
          Animation.bounce(Animation.handle.dot, $('.link_primary .link_cr'));
        }
      });
      Animation.show_three_btn();
    },
    show_three_btn: function() {
      var position = {
        y: 40,
        opacity: 0
      };
      Animation.handle.main.to(position, 0.4, {
        y: 0,
        opacity: 1,
        onUpdate: function() {
          $('.menu_primary .list').css({
            '-webkit-transform': 'translate3d(0,' + position.y + '%,0)',
            'transform': 'translate3d(0,' + position.y + '%,0)',
            'opacity': position.opacity
          });
        },
        onComplete: function() {
          $('#btn_animation_control').attr('disabled', true);
        }
      });
    },
    show_header_and_footer: function() {
      var position = {
        y: 101,
        opacity: 0
      };
      Animation.handle.main.to(position, 0.5, {
        y: 0,
        opacity: 1,
        onUpdate: function() {
          $('#footer').css({
            '-webkit-transform': 'translate3d(0,' + position.y + '%,0)',
            'transform': 'translate3d(0,' + position.y + '%,0)',
            'opacity': position.opacity
          });
          $('#header').css({
            '-webkit-transform': 'translate3d(0,-' + position.y + '%,0)',
            'transform': 'translate3d(0,-' + position.y + '%,0)',
            'opacity': position.opacity
          });
        }
      });
    },
    show_logo: function() {
      var position = {
          x: -50,
          opacity: 0
        },
        img_pos = {
          scale: 1.2,
          opacity: 0
        };
      Animation.handle.main.to(position, 0.5, {
        x: 0,
        opacity: 1,
        onUpdate: function() {
          $('#header .logo').css({
            '-webkit-transform': 'translate3d(' + position.x + '%,0,0)',
            'transform': 'translate3d(' + position.x + '%,0,0)',
            'opacity': position.opacity
          });
        }
      });
      Animation.handle.main.to(img_pos, 0.5, {
        scale: 1,
        opacity: 1,
        onUpdate: function() {
          $('#header .logo img').css({
            '-webkit-transform': 'scale3d(' + img_pos.scale + ',' + img_pos.scale + ',' + img_pos.scale + ')',
            'transform': 'scale3d(' + img_pos.scale + ',' + img_pos.scale + ',' + img_pos.scale + ')',
            'opacity': img_pos.opacity
          });
        }
      });
    },
    // Handle control
    bounce: function(tw, selector) {

      var position = {
        opacity: 0,
      }
      tw.to(position, 0.4, {
        opacity: 1,
        ease: Power2.easeIn,
        onUpdate: function() {
          selector.css({
            'opacity': position.opacity,
          })
        },
      });
    },
    control_handle: function() {
      Animation.handle.main.paused(!Animation.handle.main.paused());
      Animation.handle.two.paused(!Animation.handle.two.paused());
      Animation.handle.dot.paused(!Animation.handle.dot.paused());
      for (var i = 0; i < Animation.handle.image.length; i++) {
        Animation.handle.image[i].paused(!Animation.handle.image[i].paused());
      }
      Animation.control.text(Animation.handle.main.paused() ? "PLAY" : "STOP");
      Animation.control.toggleClass('button_pause');
      Animation.control.toggleClass('button_play');
    },
  };

$(window).on('load', function() {
  Animation.init();
});

function getCurrentPositionByTime(start, end, start_time, end_time, current_time) {
  return start + (end - start) * current_time / (end_time - start_time);
}

function shuffle(a) {
  var j, x, i;
  for (i = a.length - 1; i > 0; i--) {
    j = Math.floor(Math.random() * (i + 1));
    x = a[i];
    a[i] = a[j];
    a[j] = x;
  }
}
```

>CSS Code:
```javascript
@media (min-width: 376px) {
  #header {
    position: relative;
    z-index: 1;
    transform: translate(0, -101%);
    -moz-transform: translate(0, -101%);
    -webkit-transform: translate(0, -101%);
    opacity: 0;
  }
  #footer {
    opacity: 0;
    transform: translate3d(0, 101%, 0);
    -webkit-transform: translate3d(0, 101%, 0);
  }
  .logo {
    background-color: #ffffff;
  }
  .logo_center {
    opacity: 0;
  }
  @keyframes logo {
    0% {
      opacity: 0;
      transform: scale(1.2);
      -moz-transform: scale(1.2);
      -webkit-transform: scale(1.2);
    }
    100% {
      transform: scale(1);
      -moz-transform: scale(1);
      -webkit-transform: scale(1);
      opacity: 1;
    }
  }
  .logo_center.active {
    -webkit-animation-name: logo;
    animation-name: logo;
    -webkit-animation-duration: 0.7s;
    animation-duration: 0.7s;
    -webkit-animation-fill-mode: both;
    animation-fill-mode: both;
  }
  #frame-grid .logo_center a:before,
  #frame-grid .logo_center a:after {
    -webkit-transition: 0.2s ease all;
    -o-transition: 0.2s ease all;
    transition: 0.2s ease all;
  }
  .frame:not(.logo_center) img {
    opacity: 0;
  }
  .frame.start img {
    animation-fill-mode: forwards;
    animation-timing-function: cubic-bezier(.7, 0, .3, 1);
    animation-duration: .9s;
  }
  .logo_center figure:before {
    /* content: ''; */
    position: absolute;
    bottom: 15px;
    width: 40px;
    height: 375px;
    left: 135px;
    z-index: 9;
    background-color: #ffffff;
  }

  .show_logo img {
    opacity: 1;
  }
  .show_logo figure:before {
    /*animation: show_text 2.4s 1;
    -webkit-animation: show_text 2.4s 1;
    -moz-animation: show_text 2.4s 1;
    animation-fill-mode: forwards;*/
  }

  @keyframes show_text {
    0% {
      height: 375px;
    }
    50% {
      height: 375px;
    }
    100% {
      height: 0px;
    }
  }

  @-webkit-keyframes pulse {
    from {
      -webkit-transform: scale3d(1, 1, 1);
      transform: scale3d(1, 1, 1);
    }

    50% {
      -webkit-transform: scale3d(1.05, 1.05, 1.05);
      transform: scale3d(1.05, 1.05, 1.05);
    }

    to {
      -webkit-transform: scale3d(1, 1, 1);
      transform: scale3d(1, 1, 1);
    }
  }

  @keyframes pulse {
    from {
      -webkit-transform: scale3d(1, 1, 1);
      transform: scale3d(1, 1, 1);
    }

    50% {
      -webkit-transform: scale3d(1.05, 1.05, 1.05);
      transform: scale3d(1.05, 1.05, 1.05);
    }

    to {
      -webkit-transform: scale3d(1, 1, 1);
      transform: scale3d(1, 1, 1);
    }
  }

  .pulse {
    -webkit-animation-name: pulse;
    animation-name: pulse;
  }

  @-webkit-keyframes fadeIn {
    from {
      opacity: 0;
    }


    to {
      opacity: 1;
    }
  }

  @keyframes fadeIn {
    from {
      opacity: 0;
    }



    to {
      opacity: 1;
    }
  }

  .fadeIn {
    -webkit-animation-name: fadeIn;
    animation-name: fadeIn;
    animation-fill-mode: forwards;
  }
}
```

>HTML Code:
```javascript
<div id="wrapper">
  <header id="header">
    <div class="container">
      <h1 class="logo">
        <a href="#">
          <picture>
            <source media="(max-width: 650px)" srcset="./img/front/sp_logo.png" width="152" height="88">
            <img src="./img/front/logo.png" alt="logo" width="200" height="200">
          </picture>
        </a>
      </h1>
      <ul class="navigation_sp">
        <li>
          <a href="#">
            <span class="symbol">
              <i class="icons_marker">&nbsp;</i>
            </span>
            <span class="nav_text">アクセス</span>
          </a>
        </li>
        <li>
          <a href="#">
            <span class="symbol">
              <i class="icons_phone">&nbsp;</i>
            </span>
            <span class="nav_text">直通電話</span>
          </a>
        </li>
        <li>
          <a href="#">
            <span class="symbol">
              <i class="icons_nav">&nbsp;</i>
            </span>
            <span class="nav_text">メニュー</span>
          </a>
        </li>
      </ul>
      <div class="top_header">
        <div class="search_panel">
          <label>サイト内検索</label>
          <div class="search_action">
            <form class="search_form" action="" method="">
              <input type="text" placeholder="Google カスタム検索">
              <button type="submit" class="btn_search">Search</button>
            </form>
          </div>
        </div>
        <div class="setting">
          <ul class="clearfix">
            <li><a href="#">文字サイズ・色合い変更</a></li>
            <li><a href="#">音声読み上げ</a></li>
            <li><a href="#">Foreign Language</a></li>
          </ul>
        </div>
      </div>
    </div>
  </header>
  <!--end header-->
  <main id="main-content">
    <div class="container">
      <img src="./img/front/grid/mobile.jpg" class="show_on_mobile" alt="">
      <div id="frame-grid-wrapper">
        <div id="frame-grid">
          <div class="emergency_panel clearfix">
            <label>緊急情報</label>
            <a href="#">弾道ミサイル落下時の行動等について</a>
          </div>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img1.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img2.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img3.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img4.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img5.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img6.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img7.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame logo_center">
            <a href="#">
              <figure><img src="./img/front/grid/logo_center.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img8.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img9.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img10.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img11.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img12.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img13.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img14.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img15.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img16.jpg" alt=""></figure>
            </a>
          </article>
          <article class="frame">
            <a href="#">
              <figure><img src="./img/front/grid/img17.jpg" alt=""></figure>
            </a>
          </article>
        </div>
      </div>
      <div class="link_primary">
        <a href="#" class="link_cr">
            <span class="icons_people">&nbsp;</span>
            <span class="txt">県民向け<br/>
            情報</span>
          </a>
        <a href="#" class="link_cr">
            <span class="icons_build">&nbsp;</span>
            <span class="txt">事業者<br/>
            情報</span>
          </a>
        <a href="#" class="link_cr">
            <span class="icons_camera">&nbsp;</span>
            <span class="txt">魅力・観光<br/>
            情報</span>
          </a>
      </div>
      <div class="menu_primary">
        <div class="list">
          <a href="#"><span>復興のその先へ</span></a>
          <a href="#"><span>移住定住応援</span></a>
          <a href="#"><span>仕事・就職応援</span></a>
        </div>
      </div>
      <div class="action_control">
        <button id="btn_animation_control" class="button_slider button_pause">STOP</button>
      </div>
      <img src="./img/front/footer_bottom.png" class="show_on_mobile bottom" alt="">
    </div>
  </main>
  <!--end main-->
  <footer id="footer">
    <div class="footer_top">
      <div class="container">
        <h2 class="logo_footer">岩手県庁</h2>
        <address class="address_footer">
          <span>法人番号：4000020030007</span>
          <span>〒020-8570 岩手県盛岡市内丸10番1号</span>
          <span>電話番号：019-651-3111（総合案内）</span>
        </address>
      </div>
    </div>
    <div class="footer_copyright">
      <div class="container">
        <p>Copyright © Iwate Prefecture Government All Rights Reserved.</p>
      </div>
    </div>
  </footer>
  <!--end footer-->
</div>
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

- abc

>JavaScript Code:
```javascript

```

**9. 20180509 Plugin SmartPhone**

**Nội dung**
- Xác định breakpoint
- Chuyển đổi màn hình PC và Smartphone
- Di chuyển element ứng với breakpoint
- Về hoạt động thì Oita city là dự án được cho là có chất lượng tốt nhất cho đến hiện tại phía bên GD.
- Oita city: https://www.city.oita.oita.jp/
- Nguyện vọng là tạo được chất lượng sản phẩm bằng hoặc cao hơn Oita city này.


>JavaScript Code:
```javascript
(function($) {
  $.gd.switchViewSP = function(options) {
    var defaults = {
        wrapper_width: 1280, //Wrapper width on PC Mode
        breakpoint: [640],
        pc_layout: [],
        map: [
          []
        ],
        button_pc: '#tmp_switch_pc_style',
        button_sp: '#tmp_switch_sp_style',
      },
      st = $.extend(defaults, options),
      t = this,
      viewport_backup = '',
      cookie = $.cookie('pcviewport'),
      realView = -1,
      currentView = -1 //pc is default
    ;

    if (cookie == 'pc') currentView = -2;

    //Init
    init();
    $(window).on('resize', function() {
      handleLayout();
    });
    $(st.button_pc).on('click', function() {
      if (currentView > -1) {
        currentView = -2;
        $('html').addClass('pc_view');
        // PC Simulator Mode
        renderLayout(currentView);
        changeViewport(currentView);
        $.cookie('pcviewport', 'pc');
        window.location.reload();
      }
    });
    $(st.button_sp).on('click', function() {
      if (currentView == -2) {
        currentView = realView;
        $('html').removeClass('pc_view');
        //Roll back to normal mode
        renderLayout(currentView);
        changeViewport(currentView);
        $.cookie('pcviewport', '');
      }
    })

    //Method
    function init() {
      handleLayout();
      // Lauch all script in pc layout if in PC Mode when first loaded
      if (currentView == -1 || (currentView == -2 && realView == -1)) {
        st.pc_layout.forEach(function(e) {
          if (typeof e.callback == 'function') {
            e.callback();
          }
        })
      }
    }

    function handleLayout() {
      var temp = getRealView();
      if (realView != temp) {
        realView = temp;
        if (currentView != -2) {
          currentView = realView; // If not in PC view simulator set current base on real view
          renderLayout(currentView); // Make change layout only if not in simulator
        }
        if (realView == -1) {
          $('html').removeClass('pc_view');
          //Roll back viewport meta
          if (currentView == -2) {
            renderLayout(realView);
            changeViewport(realView);
          }
        } else if (currentView == -2) {
          $('html').addClass('pc_view');
          //Roll back to pc view simulator
          renderLayout(currentView);
          changeViewport(currentView);
        }
      }
    }

    function changeViewport(layout) {
      var viewport = document.querySelector('meta[name="viewport"]');
      if (layout == -2) {
        var scale = screen.width / st.wrapper_width;
        if (viewport_backup == '') viewport_backup = viewport.content;
        viewport.content = "width=" + (st.breakpoint[0] + 1) + ",initial-scale=" + scale + ", maximum-scale=3.0";
      } else {
        if (viewport_backup == '') {
          viewport.content = "width=device-width, maximum-scale=3.0";
        } else {
          viewport.content = viewport_backup;
        }
      }

    }

    function getRealView() {
      var ww, counter;
      if (window.innerWidth > window.innerHeight) {
        ww = Math.max(screen.width, screen.height);
      } else {
        ww = Math.min(screen.width, screen.height);
      }
      for (counter = 0; counter < st.breakpoint.length; counter++) {
        if (ww > st.breakpoint[counter]) {
          break;
        }
      }
      return (counter - 1);
    }

    function renderLayout(index) {
      var map;
      if (index > -1) {
        map = st.map[index];
      } else {
        map = st.pc_layout;
      }
      if (map.length) {
        map.forEach(function(e, i) {
          if (e.from) {
            e.element = moveElement(e.from, e.method, e.to);
          }
          if (typeof e.callback == 'function') {
            e.callback();
          }
        });
      }
    }

    function moveElement(from, method, to) {
      var el;
      switch (method) {
        case 'append':
          el = from.appendTo($(to));
          break;
        case 'prepend':
          el = from.prependTo($(to));
          break;
        case 'before':
          el = from.insertBefore($(to));
          break;
        case 'after':
          el = from.insertAfter($(to));
          break;
        case 'remove':
          el = from.detach();
          break;
        case 'addClass':
          el = from.addClass(to);
          break;
        case 'removeClass':
          el = from.removeClass(to);
          break;
      }
      return el;
    }
  }
})(jQuery);
```

**10. Zoomer_Plugin**
**10.1. Yêu cầu**: Khi hiển thị SP, tạo style, JS có thể phóng to image trong phần content bằng tab.
- **Tham khảo**
  + http://migo-media.com/zoomer-mobile/
  + http://migo-media.com/demo/zoomer/demo.html
- Là chức năng dùng cho người không sử dụng Pinch in pinch out 
- **Phạm vi, đối tượng**
  + Trong img trong phần DIV#tmp_contents, chỉ lấy img có naturalWidth (kích thước thực tế) lớn hơn độ rộng của viewport làm đối tượng.

- **Chức năng mong muốn có**
  + Khi tap vào image thì được hiển thị như là modal window, và vùng xung quanh image sẽ thành màu đen bán trong suốt.
  + Button ”拡大/phóng to”, ”縮小/thu nhỏ”
  + Button “閉じる/Close” để có thể xóa

- **Nguyện vọng về sản phẩm tạo**
  + Hoạt động ở jQuery 1.7.1 trở lên
  + Cho dù là ở dự án như thế nào thì cũng có thể hoạt động được bằng việc bổ sung vào JS, bổ sung vào stylesheet
**10.2. Tài liệu hướng dẫn sử dụng plugin Zoomer**: 
  **Mô tả:** Tự động thêm chức năng zoom hình ảnh bằng popup cho images nằm trong khu vực ```#tmp_contents```
  
  - ![Image](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/zoom-1.jpg)
  - ![Image](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/zoom-2.jpg)
  
  **Sử dụng:**
    + Include file zoomer.css và zoomer.js vào trong document
    + Thêm script js:
    
  **Cấu hình:**
  
  | Tên thuộc tính | Loại | Mặc định | Chức năng |
  | --- | --- | --- | --- |
  | breakpoint | int | 640 | Điểm breakpoint chuyển đổi qua sp. Với trường hợp muốn sử dụng plugin trên PC thì có thể setting thành 1 số giá trị lớn như 10,000,…  |
  | selector | css selector | '#tmp_contents img' | Selector chỉ trực tiếp đến các img nhận chức năng zoomer 
  | zoomerTemplate | html | '<div id="tmp_zoomer">…</div>' | Template html popup của zoomer. Trong trường hợp thay đổi template cần giữ nguyên các id #tmp_zoomer, #tmp_zoomer_close, #tmp_zoomer_cnt, #tmp_zoomer_holder, #tmp_zoomer_plus, #tmp_zoomer_minus |
  | increaseRate | float < 1 | 0.1 | Tỷ lệ zoom với mỗi lần click. Bắt buộc phải lớn hơn 0  và bé hơn 1. |
  | timing | int | 200 | Thời gian animation khi được zoom. Với trường hợp muốn tắt hẳn animation thì setting thông số này bằng 0. |
  
1.	$.gd.zoomer();  

III/ Cấu hình:

>JavaScript Code:
```javascript
(function($) {
    $.gd.zooming = function(options){
        var defaults = {
                breakpoint : 640,
                selector: '#tmp_contents img',
                zoomingTemplate : '<div id="tmp_zooming"><div id="tmp_zooming_close">X</div><div id="tmp_zooming_cnt"><div id="tmp_zooming_holder"></div></div><div id="tmp_zooming_controls"><div id="tmp_zooming_minus">-</div><div id="tmp_zooming_plus">+</div></div></div>',
                increaseRate : 0.1,
                timing : 200//set 0 for no animation
            },
            st = $.extend(defaults,options),
            t = this,
            zooming = {
                wrap : '#tmp_zooming',
                close : '#tmp_zooming_close',
                cnt : '#tmp_zooming_cnt',
                holder : '#tmp_zooming_holder',
                img : '#tmp_zooming_holder img',
                zoomIn : '#tmp_zooming_plus',
                zoomOut : '#tmp_zooming_minus',
            };
        //Init
        $(window).on('load',function(){
            init();
            checkZoomingAvailable();
        });
        $(window).on('resize',function(){
            checkZoomingAvailable();
        })

        //Method
        function init(){
            if($(st.selector).length){
                $(st.selector).on('click',function(){
                    var imgObj = getImageData($(this));
                    imgObj.addEventListener('load',function(){
                        if (imgObj.width > $(window).width() && $(window).width() <= st.breakpoint){
                            // start init zooming
                            initZoomimg(imgObj);
                        }
                    })
                });
            }
        }
        function getImageData(selector){
            var imgObj = document.createElement('img');
            imgObj.src = selector.attr('src');
            return imgObj;
        }
        function initZoomimg(imgObj){
            var initScale = Math.min(($(window).width() - 40) / imgObj.width,($(window).height() - 40) / imgObj.height),
                newScale = initScale,
                currentScale = initScale,
                position = {
                    x : 0,
                    y : 0
                };
            console.log(initScale);
            //append raw html into view
            appendHtml(imgObj,initScale);
            //init control event
            $(zooming.zoomIn).on('click',function(){
                newScale += st.increaseRate;
                $(zooming.zoomOut).removeClass('deactive');
                if (newScale > 1 - (st.increaseRate / 2)){
                    newScale = 1;
                    $(zooming.zoomIn).addClass('deactive');
                }
                setScale(newScale);
            });
            $(zooming.zoomOut).addClass('deactive');
            $(zooming.zoomOut).on('click',function(){
                newScale -= st.increaseRate;
                $(zooming.zoomIn).removeClass('deactive');
                if (newScale < initScale + (st.increaseRate / 2)){
                    newScale = initScale;
                    $(zooming.zoomOut).addClass('deactive');
                }else{
                    $(zooming.zoomOut).removeClass('deactive');
                }
                setScale(newScale);
            });
            $(zooming.close).on('click',function(){
                $(zooming.wrap).remove();
                $('body').removeClass('zooming_active');
            })
            //init swipe event
            var origin = {
                x : 0,
                y : 0,
                temp: {
                    x: 0,
                    y: 0
                },
                limit: {
                    x: 0,
                    y: 0
                }
            }
            $(zooming.wrap).on('touchmove',function(e){
                e.preventDefault();
            })
            $(zooming.img).on('touchstart',function(e){
                origin.x = e.originalEvent.touches[0].clientX;
                origin.y = e.originalEvent.touches[0].clientY;
                origin.limit.x = ((imgObj.width * currentScale + 40) - $(window).width()) / 2;
                origin.limit.y = ((imgObj.height * currentScale + 40) - $(window).height()) / 2;
            });
            $(zooming.img).on('touchmove',function(e){
                e.preventDefault();
                $(zooming.wrap).addClass('control_deactive');
                $(zooming.wrap).addClass('moving_mode');
                var new_position ={
                    x : e.originalEvent.touches[0].clientX - origin.x,
                    y : e.originalEvent.touches[0].clientY - origin.y
                }
                new_position.x += position.x;
                new_position.y += position.y;
                //Check limit
                new_position = reCheckWithLimit(origin.limit,new_position,position);
                $(zooming.cnt).css({
                    'transform' : 'translate(' + new_position.x + 'px,' + new_position.y + 'px)',
                    '-webkit-transform' : 'translate(' + new_position.x + 'px,' + new_position.y + 'px)'
                });
                origin.temp.x = new_position.x;
                origin.temp.y = new_position.y;
                return false;
            });
            $(zooming.img).on('touchend',function(e){
                if ($(zooming.wrap).hasClass('moving_mode')){ //Only reset position if it already moved
                    $(zooming.wrap).removeClass('moving_mode');
                    $(zooming.wrap).removeClass('control_deactive');
                    position.x = origin.temp.x;
                    position.y = origin.temp.y;
                    origin.x = 0;
                    origin.y = 0;
                    origin.temp.x = 0;
                    origin.temp.y = 0;
                }
            });
            //UX
            $(zooming.img).on('click',function(){
                $(zooming.wrap).toggleClass('control_deactive');
            })

            //Private function
            function setScale(scale){
                var limit = {
                    x : ((imgObj.width * scale + 40) - $(window).width()) / 2,
                    y : ((imgObj.height * scale + 40) - $(window).height()) / 2
                }
                //Reposition with new scale
                var new_position = {
                    x: position.x,
                    y: position.y
                }
                new_position.x = (new_position.x / (imgObj.width * currentScale)) * imgObj.width * scale;
                new_position.y = (new_position.y / (imgObj.height * currentScale)) * imgObj.height * scale;
                //Check limit
                new_position = reCheckWithLimit(limit,new_position,{x:0,y:0});
                setPosition(new_position);

                if (st.timing > 0){
                    doAnimation($(zooming.img),currentScale,scale,'scale',st.timing);
                }else{
                    $(zooming.img).css({
                        'transform' : 'scale(' + scale + ')',
                        '-webkit-transform' : 'scale(' + scale + ')'
                    });
                }
                currentScale = scale;
            }
            function setPosition(new_position){
                if (st.timing > 0){
                    doAnimation($(zooming.cnt),[position.x,position.y],[new_position.x,new_position.y],'translate',200);
                }else{
                    $(zooming.cnt).css({
                        'transform' : 'translate(' + new_position.x + 'px,' + new_position.y + 'px)',
                        '-webkit-transform' : 'translate(' + new_position.x + 'px,' + new_position.y + 'px)'
                    });
                }
                position.x = new_position.x;
                position.y = new_position.y;
            }
        }
        function appendHtml(imgObj,initScale){
            $('body').append(st.zoomingTemplate);
            $('body').addClass('zooming_active');
            $(zooming.holder).append(imgObj);
            $(zooming.holder).css({
                'width' : imgObj.width,
                'height' : imgObj.height,
            });
            $(zooming.img).css({
                'transform': 'scale(' + initScale + ')',
                '-webkit-transform': 'scale(' + initScale + ')',
                'transform-origin' : '50% 50%',
                '-webkit-transform-origin' : '50% 50%'
            });
        }
        function reCheckWithLimit(limit,current,old){
            var new_position = current;
            if(limit.x > 0){
                if (new_position.x < - limit.x) new_position.x = - limit.x;
                if (new_position.x > limit.x) new_position.x = limit.x;
            }else{
                new_position.x = old.x;
            }
            if(limit.y > 0){
                if (new_position.y < - limit.y) new_position.y = - limit.y;
                if (new_position.y > limit.y) new_position.y = limit.y;
            }else{
                new_position.y = old.y;
            }
            return new_position;
        }
        function doAnimation(selector,start,end,css,timing){
            var startTimes = 0;
            window.requestAnimationFrame(step);
            function step(timestamp){
                if (!startTimes) startTimes = timestamp;
                var progressTimes = timestamp - startTimes;
                var progress;
                if (progressTimes >= timing) progressTimes = timing;
                if (Array.isArray(start)){
                    progress = new Array();
                    start.forEach(function(e,i){
                        progress[i] = e + (progressTimes * (end[i] - e) / timing)
                    });
                }else{
                    progress = start + (progressTimes * (end - start) / timing);
                }
                switch(css){
                    case 'scale' : 
                        selector.css({
                            'transform': 'scale(' + progress + ')',
                            '-webkit-transform': 'scale(' + progress + ')'
                        });
                        break;
                    case 'translate': 
                        selector.css({
                            'transform': 'translate(' + progress[0] + 'px,' + progress[1] + 'px)',
                            '-webkit-transform': 'translate(' + progress[0] + 'px,' + progress[1] + 'px)'
                        });
                        break;
                    default:
                        selector.css({
                            css : progress + 'px'
                        })
                }
                if (progressTimes < timing) window.requestAnimationFrame(step);
            }
        }
        function checkZoomingAvailable(){
            var ww = $(window).width();
            if (ww <= st.breakpoint){
                $(st.selector).each(function(){
                    var _t = $(this),
                        imgObj = getImageData(_t);
                    imgObj.addEventListener('load',function(){
                        if (imgObj.width > ww){
                            if (!(_t.parent('.zooming_available').length))
                                _t.wrap('<span class="zooming_available"></span>');
                        }else{
                            if (_t.parent('.zooming_available').length) _t.unwrap();
                        }
                    })
                });
            }else{
                $(st.selector).each(function(){
                    if ($(this).parent('.zooming_available').length) $(this).unwrap();
                })
            }
        }
    }
})(jQuery);
```

**11. 20170718 Koufu**

  - ![Image](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/koufu_1.jpg)
    + Về độ rộng hiển thì đang giả định giá trị tối thiểu là ```1280px×800px```
    + Điểm khác biệt khi hiển thị smartphone
  - ![Image](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/koufu_2.jpg)
    + Hãy chú ý đến cách thức hiển thị. Hơn nữa, hoạt động click, wheel, vv.. sẽ mất đi. 
  - ![Image](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/koufu_3.jpg)
    + Di chuyển tự động trong khoảng 2~3 giây. ※Có khả năng sẽ thay đổi thành chuyển bằng click
    + Khi xem top page một lần nữa từ end page chẳng hạn thì sẽ mất đi phần đã apply và hiển thị ở trạng thái này từ khởi tạo.
    + Lưu cookie ở timing đã xem top page rồi phán đoán có/không có cookie. 
    + Open và Close bằng thao tác click và mouse wheel
    + Open và Close, Nội dung sẽ được chuyển đổi bằng tab.
  - ![Image](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/koufu_4.jpg)
    + 
  - ![Image](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/koufu_5.jpg)
  - ![Image](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/koufu_6.jpg)
  

>JavaScript Code:
```javascript

```

**12. 20180612 Your Life in Hyogo**

**Request :**
- Bản đồ thế giới & đồng hồ thế giới
- HTML sẽ tạo: world_clock.html
- Về đồng hồ thì nhờ các bạn tạo theo hình thức là sử dụng JavaScript, và dựa vào thời gian tiêu chuẩn để hiển thị đồng hồ của các quốc gia.
- ```getTime()```: Trả về số mili giây kể từ 1970/01/01.
- ```setTime()```: Thêm số mili giây vào ngày 1 tháng 1 năm 1970 và hiển thị ngày và giờ mới
 ![Your Life in Hyogo](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/world_clock.jpg)
 
**Hướng dẫn :**

>**Case 2:**

**Step 1**
- Thứ tự đầu tiên của doanh nghiệp là để có được thời gian địa phương hiện tại. Trong JavaScript, điều này có thể dễ dàng thực hiện bằng cách khởi tạo một đối tượng ```Date()``` mà không có bất kỳ đối số nào:

```javascript
// tạo đối tượng Date cho vị trí hiện tại 
d = new Date();
```

- Thể hiện thời gian ```local``` này là số ```mili giây``` kể từ ngày 1 tháng 1 năm 1970, bằng cách gọi phương thức ```getTime()``` của đối tượng ```Date()```:

```javascript
// Chuyển đổi sang millisecond kể từ ngày 1 tháng 1 năm 1970 
localTime = d.getTime();
```

**Step 2**

- Tiếp theo, tìm múi giờ địa phương bù đắp(offset) với ```Date()``` của đối tượng ```getTimezoneOffset()``` phương pháp. Theo mặc định, phương thức này trả về chênh lệch múi giờ theo phút, do đó, chuyển đổi giá trị này thành mili giây để thao tác dễ dàng hơn:

```javascript
// lấy giá trị UTC cục bộ và chuyển thành msec 
localOffset = d.getTimezoneOffset () * 60000;
```

- Lưu ý rằng giá trị trả về âm từ hàm ```getTimezoneOffset()``` cho biết vị trí hiện tại nằm trước UTC, trong khi giá trị dương cho biết vị trí nằm sau UTC.
- **Note**: 1000 mili giây = 1 giây, và 1 phút = 60 giây. Do đó, chuyển đổi phút thành mili giây liên quan đến nhân với 60 * 1000 = 60000.

**Step 3**
- Có được thời gian UTC hiện tại, bằng cách thêm chênh lệch múi giờ local(địa phương) vào giờ local(địa phương).

```javascript
// lấy thời gian tính theo giờ UTC trong mili giây 
utc = localTime + localOffset;
```

- Tại thời điểm này, biến utc chứa thời gian UTC hiện tại. Tuy nhiên, giá trị thời gian này được biểu thị bằng số mili giây kể từ ngày 1 tháng 1 năm 1970. Giữ nguyên giá trị này trong thời điểm này bởi vì vẫn còn một vài tính toán để thực hiện.

**Step 4**
- Một khi bạn đã có được thời gian UTC, có được điểm đến UTC của thành phố đích trong giờ, chuyển đổi nó thành mili giây và thêm nó vào thời gian UTC.

```javascript
// lấy và thêm thời gian bù giờ UTC của điểm đến 
// ví dụ, Bombay 
// là UTC + 5,5 giờ
offset = 5.5;   
bombay = utc + (3600000*offset);
```

- **Note**: Trong trường hợp bạn đang tự hỏi làm thế nào tôi đến 3600000 như nhân tố nhân, nhớ rằng 1000 millseconds = 1 giây, và 1 giờ = 3600 giây. Do đó, chuyển đổi giờ thành mili giây liên quan đến nhân với 3600 * 1000 = 3600000.

**Step 5**
- Thay đổi giá trị thời gian được tính trong bước trước thành chuỗi ```date/time``` có thể đọc được bằng cách khởi tạo đối tượng ```new Date()``` object với nó và gọi phương thức ```toLocaleString()``` của đối tượng.

```javascript
// chuyển đổi giá trị msec thành chuỗi ngày
nd = new Date(bombay); 
document.writeln("Bombay time is " + nd.toLocaleString() + "<br>");
And you're done!
```

```javascript
// function to calculate local time
// in a different city
// given the city's UTC offset
function calcTime(city, offset) {

    // create Date object for current location
    d = new Date();
    
    // convert to msec
    // add local time zone offset 
    // get UTC time in msec
    utc = d.getTime() + (d.getTimezoneOffset() * 60000);
    
    // create new Date object for different city
    // using supplied offset
    nd = new Date(utc + (3600000*offset));
    
    // return time as a string
    return "The local time in " + city + " is " + nd.toLocaleString();

}

// get Bombay time
alert(calcTime('Bombay', '+5.5'));

// get Singapore time
alert(calcTime('Singapore', '+8'));

// get London time
alert(calcTime('London', '+1'));
```

>**Case 2:**
```javascript
// TimeZone
$.fn.timeZoneClock = function(utc_offset) {

  clock = this;

  function getTime() {
    var date = new Date();
    // convert to millisecond
    // add local time zone offset
    // get UTC time in millisecond
    // getTimezoneOffset() method returns the time difference between UTC time and local time, in minutes
    var nowUTC = date.getTime() + date.getTimezoneOffset() * 60 * 1000;
    date.setTime(nowUTC + (utc_offset * 60 * 60 * 1000));
    var hour = date.getHours();
    return {
      hour: appendZero(hour),
      minute: appendZero(date.getMinutes()),
      second: appendZero(date.getSeconds())
    }
  }

  function appendZero(num) {
    if (num < 10) { return "0" + num }
    return num
  }

  function updateTime(clock_id) {
    var now = getTime();
    clock = $.find('#' + clock_id);
    $(clock).find('.reality_time').html("<span class='hour'>" + now.hour + "</span>:<span class='minute'>" + now.minute + "</span>:<span class='second'>" + now.second + "</span>");
  }

  var clock_id = $(this).attr('id');

  updateTime(clock_id);

  setInterval(
    function() {
        updateTime(clock_id)
    },1000
  );
}

var timeZoneUTC = {
  paris: '2',
  hong_kong: '8',
  australia: '8',
  washington: '-4',
  brazil: '-3',
  hyogo: '9'
};

// Clock Area
$('#clock_1').timeZoneClock(timeZoneUTC.paris);
$('#clock_2').timeZoneClock(timeZoneUTC.hong_kong);
$('#clock_3').timeZoneClock(timeZoneUTC.australia);
$('#clock_4').timeZoneClock(timeZoneUTC.washington);
$('#clock_5').timeZoneClock(timeZoneUTC.brazil);
$('#clock_6').timeZoneClock(timeZoneUTC.hyogo);
```
>HTML
```javascript
<div class="clock_list">
  <div class="clock_item">
    <div class="clock_inner time_zome" id="clock_1">
      <p class="country_name">パリ</p>
      <p class="reality_time" id="paris_time">
        <span class="hour"></span>:
        <span class="minute"></span>:
        <span class="second"></span>
      </p>
    </div>
  </div>
  <div class="clock_item">
    <div class="clock_inner time_zome" id="clock_2">
      <p class="country_name">香港</p>
      <p class="reality_time" id="hong_kong_time">
        <span class="hour"></span>:
        <span class="minute"></span>:
        <span class="second"></span>
      </p>
    </div>
  </div>
  <div class="clock_item">
    <div class="clock_inner time_zome" id="clock_3">
      <p class="country_name">西オーストラリア州</p>
      <p class="reality_time" id="australia_time">
        <span class="hour"></span>:
        <span class="minute"></span>:
        <span class="second"></span>
      </p>
    </div>
  </div>
  <div class="clock_item">
    <div class="clock_inner time_zome" id="clock_4">
      <p class="country_name">ワシントン州</p>
      <p class="reality_time" id="washington_time">
        <span class="hour"></span>:
        <span class="minute"></span>:
        <span class="second"></span>
      </p>
    </div>
  </div>
  <div class="clock_item">
    <div class="clock_inner time_zome" id="clock_5">
      <p class="country_name">ブラジルパラナ州</p>
      <p class="reality_time" id="brazil_time">
        <span class="hour"></span>:
        <span class="minute"></span>:
        <span class="second"></span>
      </p>
    </div>
  </div>
  <div class="clock_item">
    <div class="clock_inner time_zome" id="clock_6">
      <p class="country_name">兵庫</p>
      <p class="reality_time" id="hyogo_time">
        <span class="hour"></span>:
        <span class="minute"></span>:
        <span class="second"></span>
      </p>
    </div>
  </div>
</div>
```

>**Case 3:**

```javascript
(function($) {
  $.fn.showClock = function() {
    offset = $(this).attr('rel');
    $(this).simpleClock(offset)
  }
})(jQuery);

(function($) {
  $.fn.simpleClock = function(utc_offset) {
    var language = $('html').attr('lang');
    switch (language) {
      case "de":
        var weekdays = ["So.", "Mo.", "Di.", "Mi.", "Do.", "Fr.", "Sa."];
        var months = ["Jan.", "Feb.", "Mär.", "Apr.", "Mai", "Juni", "Juli", "Aug.", "Sep.", "Okt.", "Nov.", "Dez."];
        break;
      case "es":
        var weekdays = ["Dom", "Lun", "Mar", "Mié", "Jue", "Vie", "Sáb"];
        var months = ["Ene", "Feb", "Mar", "Abr", "Mayo", "Jun", "Jul", "Ago", "Sept", "Oct", "Nov", "Dic"];
        break;
      case "fr":
        var weekdays = ["Dim", "Lun", "Mar", "Mer", "Jeu", "Ven", "Sam"];
        var months = ["Jan", "Fév", "Mars", "Avr", "Mai", "Juin", "Juil", "Août", "Sept", "Oct", "Nov", "Déc"];
        break;
      case "cn":
        var weekdays = ["星期日", "星期一", "星期二", "星期三", "星期四", "星期五", "星期六"];
        var months = ["一月", "二月", "三月", "四月", "五月", "六月", "七月", "八月", "九月", "十月", "十一月", "十二月"];
        break;
      case "in":
        var weekdays = ["रविवार", "सोमवार", "मंगलवार", "बुधवार", "गुरूवार", "शुक्रवार", "शनिवार"];
        var months = ["जनवरी", "फरवरी", "मार्च", "अप्रैल", "मई", "जून", "जुलाई", "अगस्त", "सितंबर", "अक्टूबर", "नवंबर", "दिसंबर"];
        break;
      default:
        var weekdays = ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"];
        var months = ["Jan", "Feb", "Mar", "Apr", "May", "June", "July", "Aug", "Sept", "Oct", "Nov", "Dec"];
        break
    }
    clock = this;

    function getTime() {
      var date = new Date();
      var nowUTC = date.getTime() + date.getTimezoneOffset() * 60 * 1000;
      date.setTime(nowUTC + (utc_offset * 60 * 60 * 1000));
      var hour = date.getHours();
      if (language == "en") {
        suffix = (hour >= 12) ? 'p.m.' : 'a.m.';
        hour = (hour > 12) ? hour - 12 : hour;
        hour = (hour == '00') ? 12 : hour
      }
      return {
        day: weekdays[date.getDay()],
        date: date.getDate(),
        month: months[date.getMonth()],
        year: date.getFullYear(),
        hour: appendZero(hour),
        minute: appendZero(date.getMinutes()),
        second: appendZero(date.getSeconds())
      }
    }

    function appendZero(num) {
      if (num < 10) { return "0" + num }
      return num
    }

    function refreshTime(clock_id) {
      var now = getTime();
      clock = $.find('#' + clock_id);
      $(clock).find('.date').html(now.day + ', ' + now.date + '. ' + now.month + ' ' + now.year);
      $(clock).find('.time').html("<span class='hour'>" + now.hour + "</span>:<span class='minute'>" + now.minute + "</span>:<span class='second'>" + now.second + "</span>");
      if (typeof(suffix) != "undefined") {
        $(clock).find('.time').append('<strong>' + suffix + '</strong>')
      }
    }
    var clock_id = $(this).attr('id');
    refreshTime(clock_id);
    setInterval(function() { refreshTime(clock_id) }, 1000)
  }
})(jQuery);

$(document).ready(function() {
  $('.clock.big').each(function() { 
    $(this).showClock() 
  });
}
```
>HTML
```javascript
<div class="clock big" id="abc" rel="9"> 
  <h2>Current local time in<br><span class="text-muted">Japan, Asia/Tokyo</span></h2> 
  <div class="date"></div> 
  <div class="time">
      <span class="hour"></span>:
      <span class="minute"></span>:
      <span class="second"></span>
      <strong>AM</strong>
  </div> 
</div>
```

**13. 20180719_Gotokyo ```localStorage()```**
**Request :**
■ Nội dung tác nghiệp
- Muốn thiết đặt button đồng ý cho phép get cookie ở phía trên phần header của site tham khảo nên hãy tạo function để có thể coding bằng JS
https://www.gotokyo.org/en/index.html

■ Dự định về JS
- HTML thì generate bằng JS (Không thay đổi template)
- Generating destination (đích generate) thì sử dụng ```prependTo()```, giá trị khởi tạo thì lấy ```#tmp_wrapper```
- Khi nhấn button 同意/đồng ý thì nó bị mất đi
- Sử dụng Local Storage chứ không phải cookie

■ Điều kiện
- Hãy tạo theo hình thức là function hóa

 ![Your Life in Hyogo](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/img_localStorage.jpg)
 
**Web Storage**
- Web Storage ứng dụng web có thể lưu trữ dữ liệu cục bộ trong trình duyệt của người dùng.
- ```window.localStorage```: Lưu trữ dữ liệu không có ngày hết hạn.
**Đoạn này có tác dụng kiểm tra trình duyệt có hỗ trợ không.
```javascript
if (typeof(Storage) !== "undefined") {
    // Code for localStorage/sessionStorage.
} else {
    // Sorry! No Web Storage support..
}
```

```javascript
(function($) {

   $.gd.localCookie = function(options) {
     var defaults = {
         selector: '#tmp_local_button',
         template: '<div id="tmp_local_bar"><div class="container"><p class="txt">このサイトのクッキーを使用してユーザー体験を向上させています。引き続き閲覧する場合は、当サイトでクッキー使用のアクセプトをお願いします。 詳細については、<a href="/ja/cookie-policy/" class="cookies_link">クッキーポリシー</a>をご覧ください。</p><a href="javascript:void(0);" id="tmp_local_button">同意</a></div></div>',
         target: '#tmp_wrapper'
       },
       st = $.extend(defaults, options),
       t = this,
       userExperience = localStorage.getItem('user_experience');

     //Init
     $(window).on('load', function() {
       init();
       bind();
     });

     function init() {
       if (userExperience == null) {
         $(st.template).prependTo(st.target);
         $('body').addClass('format_local_active');
       }
     }

     function bind() {
       $(document).on('click', st.selector, function() {
         action();
       });
     }

     function action() {
       if (userExperience == null) {
         localStorage.setItem('user_experience', true);
         var template = $(st.template)[0].id;
         $('#' + template).hide();
         $('body').removeClass('format_local_active');
       }
     }

   }
 })(jQuery);
```

**13. 20170215 Hyogo**

1. Output text data và file image đang được setting ở JSON.

 ![Hyogo](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/hyogo_gallery_1.JPG)
 
 - Nội dung thì làm theo sample cũng được. Cấu tạo thì hãy tham chiếu sheet 「JSON」
 ※Data dùng để chạy thực tế thì phía GD sẽ chèn vào nên nhờ các bạn tạo trước bằng image thích hợp.
2. Hiển thị những phần bên dưới khi click vào image (youtube) 

![Hyogo](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/hyogo_gallery_2.JPG)

3. Hiển thị youtube
  - Chỉ trường hợp đang mô tả URL vào node 「youtube_url」 của file JSON, thì hãy set để hiển thị Player của Youtube ở phần đã triển khai sau khi click vào image và có thể replay trong trường hợp đó.
4. Trường hợp chèn youtube thì sẽ hiển thị icon ở nơi hiển thị image thumbnail 

![Hyogo](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/hyogo_gallery_3.JPG)

5. Hiển thị image khởi tạo thì đến 20 cái
 - Hãy sử dụng HTML đã gửi
※Trường hợp data dưới 20 cái thì không hiển thị button More, Khung hiển thị thì cũng chỉ hiển thị số lượng cần thiết
6. Hiển thị 20 cái tiếp theo bằng cách click vào nút More

 ![Hyogo](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/hyogo_gallery_4.JPG)
 
7. Trình tự hiển thị image thì hiển thị theo random
 - Hiển thị theo random ở mỗi lần load
8. Setting radom thì cố gắng set để có thể setting bằng đối số khi tham chiếu file javascript (Tham chiếu sheet「JS」)
 - ```<script type="text/javascript" src="/cms8341/shared/js/setting_gallery.js?random=1"></script>```
 
  ![Hyogo](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/hyogo_gallery_5.JPG)
  
9. Phương pháp hiển thị từng image-video
 - Dự định hiển thị list sẽ chia ra trên dưới, space hiển thị title-Summary statement và image được zoom out sẽ được chèn vào
 - Size image
 + Ngang : 400 px
 + Dọc : Không giới hạn (Điều chỉnh tự động cho phù hợp với chiều ngang)
 
 ![Hyogo](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/hyogo_gallery_6.JPG)
 
10. Trường hợp video
 - Button replay được hiển thị trên image được zoom out, nên có thể replay video youtube trên page. Hơn nữa, khi nhấn button hiển thị zoom out của toolbar bên dưới thì sẽ link đến page video tương ứng của youtube.
 
 ![Hyogo](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/hyogo_gallery_7.JPG)
 
 - Trường hợp JS OFF thì không thể nhìn thấy được. Hiển thị message thông báo việc không được hiển thị trongg trường hợp JS OFF, và liệt kê link của image
 
11. Title
 - Khi Mouse on vào image thì Title sẽ được hiển thị
 - Size image: Khi hiển thị list, image đã đăng ký sẽ được trimming theo hình vuông
 - Trường hợp video: Dự định sẽ hiển thị "Icon video" ở trên thumbnail
 - Số lượng hiển thị: Dự định là trên Top page 20 image sẽ được hiển thị, khi nhấn nút "More" thì sẽ hiển thị 20 image tiếp theo.
 
 ![Hyogo](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/hyogo_gallery_7.JPG)

>JavaScript Code:
```javascript
//CMS-8341用JS

(function($) {

  $(function() {
    /*init*/
    init();
  });

  var gallery = $('.js_render_gallery');
  var galleryList = $('.js_render_gallery_list');
  var photo = '.js_photo';
  var photoTarget = '.js_photo_target';
  var photoRender = '.js_photo_render';
  var photoClose = '.js_photo_close';
  var loadMore = $('.js_loadmore');
  var loadDing = $('.js_loading');
  var javascript = $("#settingGallery");
  var count = 0;
  var items = [];
  var players = [];
  var random = javascript.attr('src').split('?')[1];
  random = parseInt(random.replace(/^\D+/g, ''));
  var limit = javascript.attr('src').split('?')[2];
  limit = parseInt(limit.replace(/^\D+/g, ''));
  var _start = 0;
  var _end = limit;

  /* Initialize */
  var init = function() {
    loadDing.show();
    loadMore.hide();
    _fetchData(_start, limit);
    _bind();
  };

  /* Fetch data from JSON */
  var _fetchData = function(_start, _end, _callback) {
    $.getJSON('/cms8341/shared/gallery/js/gallery.json', function(data) {
      loadDing.hide();
      items = _getData(random, data['items']);
      _renderData(_start, _end, items);
    });
  };

  var _renderData = function(_start, _end, _items) {
    if (count > _items.length) {
      return false;
    } else {
      if (_items.length > _end) {
        loadMore.show();
      } else {
        _end = _items.length;
        loadMore.hide();
      }
      if (_items.length >= _end) {
        for (var i = _start; i < _end; i++) {
          galleryList.append(_fetchItem(_items[i]));
        }
      }
    }
  };

  /* Bind Event */
  var _bind = function() {
    /* Show Preview detail */
    gallery.on('click', photoTarget, function() {
      var _this = $(this);
      _fetchDetail(_this);
      _renderPreview(_this);
      return false;
    });

    /* Close Preview detail */
    gallery.on('click', photoClose, function() {
      _closePreview($(this));
      return false;
    });

    /* Show more gallery items */
    loadMore.on('click', function() {
      _start += limit;
      _end = _start + limit;
      count += limit;
      _scrollTop(loadMore.offset().top, 1000);
      _renderData(_start, _end, items);
    });

  };

  /* Fetch Detail from @data */
  var _fetchDetail = function(_this, _callback) {
    var _id = _this.data('id');
    var _title = _this.data('title');
    var _imageUrl = _this.data('image');
    var _summary = _this.data('summary');
    var _movie = _this.data('movie');
    var _youtubeUrl = _this.data('youtube');
    var _photoAppend = _this.closest(photo).find(photoRender);
    var _typeMedia = '';
    if (_movie == 'movie') {
      _typeMedia = '<iframe class="js_media" width="400" height="225" id="' + _id + '" src="' + _youtubeUrl + '" frameborder="0" allowfullscreen=""></iframe>';
    } else {
      _typeMedia = '<img class="js_media" src="/cms8341/' + _imageUrl + '" width="400" height="300">';
    }
    var _tmp = '<div class="img_gallery_cnt">';
    _tmp += '<p class="img">';
    _tmp += '<span class="js_loading_item load">';
    _tmp += '<span class="loader_image"></span>';
    _tmp += '</span>';
    _tmp += _typeMedia;
    _tmp += '</p>';
    _tmp += '<div class="cnt">';
    _tmp += '<p class="ttl">' + _title + '</p>';
    _tmp += '<p class="txt">' + _summary + '</p>';
    _tmp += '</div>';
    _tmp += '<p class="close js_photo_close">';
    _tmp += '<a href="#"><img src="/cms8341/shared/templates/free/images/contents/img_gallery_close_btn.png" width="40" height="40" alt="close"></a>';
    _tmp += '</p>';
    _tmp += '</div>';

    if (!_photoAppend.hasClass('append')) {
      _photoAppend.addClass('append').html(_tmp);
    }

  };

  /* Fetch item from JSON */
  var _fetchItem = function(_item) {
    var _titleItem = _item['title'];
    var _detail = _item['detail'];
    var _thumb_image_path = _item['thumb_image_path'];
    _movie = _item['isyoutube'] ? 'movie' : '';

    var _tmpItem = '<li class="photo js_photo ' + _movie + '">';
    _tmpItem += '<p class="thumb">';
    _tmpItem += '<a class="js_photo_target" data-id="' + _item['id'] + '" data-title="' + _detail['title'] + '" data-image="' + _detail['image_path'] + '" data-summary="' + _detail['summary'] + '" data-movie="' + _movie + '" data-youtube="' + _detail['youtube_url'] + '" href="#">';
    _tmpItem += '<img src="' + _item['thumb_image_path'] + '" width="239" height="239" />';
    _tmpItem += '<span>' + _titleItem + '</span>';
    _tmpItem += '</a>';
    _tmpItem += '</p>';
    _tmpItem += '<div class="photo_render js_photo_render">';
    _tmpItem += '</div>';
    _tmpItem += '</li>';
    return _tmpItem;
  };

  /*Show preview Detail */
  var _renderPreview = function(_this) {
    var _photoAppend = _this.closest(photo).find(photoRender);
    var _media = _photoAppend.find('.js_media');

    if (!_this.closest(photo).hasClass('active')) {
      var _loadingInItem = _photoAppend.find('.js_loading_item');
      var _height = _photoAppend.outerHeight();

      $(photo).removeClass('active');
      /* Reset Height for animate */
      _photoAppend.css('height', 0);
      /* Set New Height */
      _photoAppend.animate({ height: _height }, 500);
      /* First loading */
      if (typeof(_media.attr('style')) == 'undefined') {
        _loadingInItem.show();
        _media.on("load", function() {
          setTimeout(function() {
            _loadingInItem.hide();
            _media.css('opacity', 1);
            _scrollTop(_this.offset().top - (_height / 2 + 80), 300);
          }, 200);
        });
      } else {
        /* Second loading */
        _scrollTop(_this.offset().top - (_height / 2 + 80), 300);
      }
      _this.closest(photo).addClass('active');
      if (_media[0]['localName'] == 'iframe') {
        _onYouTubePlayerAPIReady(_media);
      }
      _onPlayerStateChange(_this);
    }

  };

  /*Close preview Detail */
  var _closePreview = function(_this) {
    _this.closest(photo).find(photoRender).animate({ height: 0 }, 500);
    setTimeout(function() {
      /* Reset Height for auto */
      _this.closest(photo).find(photoRender).css('height', 'auto');
      _this.closest(photo).removeClass('active');
    }, 510);
    _onPlayerStateChange(_this);
  };

  /*Get DATA @default or @random */
  var _getData = function(_type, _data) {
    if (_type == 1) {
      // Is random
      var newItems = _data;
      var tmp, current, top = newItems.length;
      if (top) {
        while (--top) {
          current = Math.floor(Math.random() * (top + 1));
          tmp = newItems[current];
          newItems[current] = newItems[top];
          newItems[top] = tmp;
        }
        _data = newItems;
      }
    } else {
      _data = _data;
    }
    return _data;
  };

  var _scrollTop = function(_offset, _time) {
    $('html, body').animate({
      scrollTop: _offset
    }, _time);
  };

  var _onYouTubePlayerAPIReady = function(_video) {
    if (!_video.hasClass('active')) {
      for (var i = 0; i < _video.length; i++) {
        var t = new YT.Player($(_video[i]).attr('id'), {});
        players.push(t);
      }
      _video.addClass('active');
    }
  };

  var _onPlayerStateChange = function(_this) {
    var temp = _this.data('youtube');
    for (var i = 0; i < players.length; i++) {
      if (players[i].a.src != temp) players[i].stopVideo();
    }
  }

})(jQuery);
```

>HTML Code:
```javascript
<div id="tmp_gallery_container">
  <ul class="img_gallery_list js_render_gallery_list">
                    
  </ul>
  <p class="more_btn2 js_loadmore"><a href="javascript:void(0)">More</a></p>
</div>
```

>Json data:
```javascript
{
  "items": [
  {
    "id": 0,
    "title": "Title 1",
    "thumb_image_path": "/cms8341/shared/gallery/images/1.jpg",
    "isyoutube": false,
    "detail":
    {
      "title": "Title 1",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/1.jpg",
      "youtube_url": ""

    }
  },
  {
    "id": 1,
    "title": "Title 2",
    "thumb_image_path": "/cms8341/shared/gallery/images/2.jpg",
    "isyoutube": true,
    "detail":
    {
      "title": "Title 2",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/2.jpg",
      "youtube_url": "https://www.youtube.com/embed/pUAe9qpuAMA?enablejsapi=1"
    }
  },
  {
    "id": 2,
    "title": "Title 3",
    "thumb_image_path": "/cms8341/shared/gallery/images/3.jpg",
    "isyoutube": true,
    "detail":
    {
      "title": "Title 3",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/3.jpg",
      "youtube_url": "https://www.youtube.com/embed/i_yLpCLMaKk?enablejsapi=1"
    }
  },
  {
    "id": 3,
    "title": "Title 4",
    "thumb_image_path": "/cms8341/shared/gallery/images/4.jpg",
    "isyoutube": false,
    "detail":
    {
      "title": "Title 4",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/4.jpg",
      "youtube_url": ""
    }
  },
  {
    "id": 4,
    "title": "Title 5",
    "thumb_image_path": "/cms8341/shared/gallery/images/5.jpg",
    "isyoutube": false,
    "detail":
    {
      "title": "Title 5",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/5.jpg",
      "youtube_url": ""
    }
  },
  {
    "id": 5,
    "title": "Title 6",
    "thumb_image_path": "/cms8341/shared/gallery/images/6.jpg",
    "isyoutube": true,
    "detail":
    {
      "title": "Title 6",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/6.jpg",
      "youtube_url": "https://www.youtube.com/embed/qrV0DhHnMzs?enablejsapi=1"
    }
  },
  {
    "id": 6,
    "title": "Title 7",
    "thumb_image_path": "/cms8341/shared/gallery/images/7.jpg",
    "isyoutube": false,
    "detail":
    {
      "title": "Title 7",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/7.jpg",
      "youtube_url": ""
    }
  },
  {
    "id": 7,
    "title": "Title 8",
    "thumb_image_path": "/cms8341/shared/gallery/images/8.jpg",
    "isyoutube": false,
    "detail":
    {
      "title": "Title 8",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/8.jpg",
      "youtube_url": ""
    }
  },
  {
    "id": 8,
    "title": "Title 9",
    "thumb_image_path": "/cms8341/shared/gallery/images/9.jpg",
    "isyoutube": false,
    "detail":
    {
      "title": "Title 9",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/9.jpg",
      "youtube_url": ""
    }
  },
  {
    "id": 9,
    "title": "Title 10",
    "thumb_image_path": "/cms8341/shared/gallery/images/10.jpg",
    "isyoutube": false,
    "detail":
    {
      "title": "Title 10",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/10.jpg",
      "youtube_url": ""
    }
  },
  {
    "id": 10,
    "title": "Title 11",
    "thumb_image_path": "/cms8341/shared/gallery/images/11.jpg",
    "isyoutube": false,
    "detail":
    {
      "title": "Title 11",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/11.jpg",
      "youtube_url": ""
    }
  },
  {
    "id": 11,
    "title": "Title 12",
    "thumb_image_path": "/cms8341/shared/gallery/images/12.jpg",
    "isyoutube": false,
    "detail":
    {
      "title": "Title 12",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/12.jpg",
      "youtube_url": ""
    }
  },
  {
    "id": 12,
    "title": "Title 13",
    "thumb_image_path": "/cms8341/shared/gallery/images/13.jpg",
    "isyoutube": false,
    "detail":
    {
      "title": "Title 13",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/13.jpg",
      "youtube_url": ""
    }
  },
  {
    "id": 13,
    "title": "Title 14",
    "thumb_image_path": "/cms8341/shared/gallery/images/14.jpg",
    "isyoutube": false,
    "detail":
    {
      "title": "Title 14",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/14.jpg",
      "youtube_url": ""
    }
  },
  {
    "id": 14,
    "title": "Title 15",
    "thumb_image_path": "/cms8341/shared/gallery/images/15.jpg",
    "isyoutube": false,
    "detail":
    {
      "title": "Title 15",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/15.jpg",
      "youtube_url": ""
    }
  },
  {
    "id": 15,
    "title": "Title 16",
    "thumb_image_path": "/cms8341/shared/gallery/images/16.jpg",
    "isyoutube": false,
    "detail":
    {
      "title": "Title 16",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/16.jpg",
      "youtube_url": ""
    }
  },
  {
    "id": 16,
    "title": "Title 17",
    "thumb_image_path": "/cms8341/shared/gallery/images/17.jpg",
    "isyoutube": false,
    "detail":
    {
      "title": "Title 17",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/17.jpg",
      "youtube_url": ""
    }
  },
  {
    "id": 17,
    "title": "Title 18",
    "thumb_image_path": "/cms8341/shared/gallery/images/18.jpg",
    "isyoutube": false,
    "detail":
    {
      "title": "Title 18",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/18.jpg",
      "youtube_url": ""
    }
  },
  {
    "id": 18,
    "title": "Title 19",
    "thumb_image_path": "/cms8341/shared/gallery/images/19.jpg",
    "isyoutube": true,
    "detail":
    {
      "title": "Title 19",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/19.jpg",
      "youtube_url": "https://www.youtube.com/embed/pUAe9qpuAMA?enablejsapi=1"
    }
  },
  {
    "id": 19,
    "title": "Title 20",
    "thumb_image_path": "/cms8341/shared/gallery/images/20.jpg",
    "isyoutube": false,
    "detail":
    {
      "title": "Title 20",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/20.jpg",
      "youtube_url": ""
    }
  },
  {
    "id": 20,
    "title": "Title 21",
    "thumb_image_path": "/cms8341/shared/gallery/images/21.jpg",
    "isyoutube": true,
    "detail":
    {
      "title": "Title 21",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/21.jpg",
      "youtube_url": "https://www.youtube.com/embed/1UgKvfYy5hE?enablejsapi=1"
    }
  },
  {
    "id": 21,
    "title": "Title 22",
    "thumb_image_path": "/cms8341/shared/gallery/images/22.jpg",
    "isyoutube": false,
    "detail":
    {
      "title": "Title 22",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/22.jpg",
      "youtube_url": ""
    }
  },
  {
    "id": 22,
    "title": "Title 23",
    "thumb_image_path": "/cms8341/shared/gallery/images/23.jpg",
    "isyoutube": true,
    "detail":
    {
      "title": "Title 23",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/23.jpg",
      "youtube_url": "https://www.youtube.com/embed/Eqx90_j2moc?enablejsapi=1"
    }
  },
  {
    "id": 23,
    "title": "Title 24",
    "thumb_image_path": "/cms8341/shared/gallery/images/24.jpg",
    "isyoutube": false,
    "detail":
    {
      "title": "Title 24",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/24.jpg",
      "youtube_url": ""
    }
  },
  {
    "id": 24,
    "title": "Title 25",
    "thumb_image_path": "/cms8341/shared/gallery/images/25.jpg",
    "isyoutube": true,
    "detail":
    {
      "title": "Title 25",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/25.jpg",
      "youtube_url": "https://www.youtube.com/embed/hZ1wvuqUBMU?enablejsapi=1"
    }
  },
  {
    "id": 25,
    "title": "Title 26",
    "thumb_image_path": "/cms8341/shared/gallery/images/26.jpg",
    "isyoutube": false,
    "detail":
    {
      "title": "Title 26",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/26.jpg",
      "youtube_url": ""
    }
  },
  {
    "id": 26,
    "title": "Title 27",
    "thumb_image_path": "/cms8341/shared/gallery/images/27.jpg",
    "isyoutube": true,
    "detail":
    {
      "title": "Title 27",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/27.jpg",
      "youtube_url": "https://www.youtube.com/embed/ES7WDcrlkek?enablejsapi=1"
    }
  },
  {
    "id": 27,
    "title": "Title 28",
    "thumb_image_path": "/cms8341/shared/gallery/images/28.jpg",
    "isyoutube": true,
    "detail":
    {
      "title": "Title 28",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/28.jpg",
      "youtube_url": "https://www.youtube.com/embed/Co1XkCJhAp8?enablejsapi=1"
    }
  },
  {
    "id": 28,
    "title": "Title 29",
    "thumb_image_path": "/cms8341/shared/gallery/images/29.jpg",
    "isyoutube": false,
    "detail":
    {
      "title": "Title 29",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/29.jpg",
      "youtube_url": ""
    }
  },
  {
    "id": 29,
    "title": "Title 30",
    "thumb_image_path": "/cms8341/shared/gallery/images/30.jpg",
    "isyoutube": true,
    "detail":
    {
      "title": "Title 30",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/30.jpg",
      "youtube_url": "https://www.youtube.com/embed/lLO2-XaO9Xc?enablejsapi=1"
    }
  },
  {
    "id": 30,
    "title": "Title 31",
    "thumb_image_path": "/cms8341/shared/gallery/images/31.jpg",
    "isyoutube": false,
    "detail":
    {
      "title": "Title 31",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/31.jpg",
      "youtube_url": ""

    }
  },
  {
    "id": 31,
    "title": "Title 32",
    "thumb_image_path": "/cms8341/shared/gallery/images/32.jpg",
    "isyoutube": true,
    "detail":
    {
      "title": "Title 32",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/32.jpg",
      "youtube_url": "https://www.youtube.com/embed/4H6PeCmmabo?enablejsapi=1"
    }
  },
  {
    "id": 32,
    "title": "Title 33",
    "thumb_image_path": "/cms8341/shared/gallery/images/33.jpg",
    "isyoutube": false,
    "detail":
    {
      "title": "Title 33",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/33.jpg",
      "youtube_url": ""
    }
  },
  {
    "id": 33,
    "title": "Title 34",
    "thumb_image_path": "/cms8341/shared/gallery/images/34.jpg",
    "isyoutube": false,
    "detail":
    {
      "title": "Title 34",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/34.jpg",
      "youtube_url": ""
    }
  },
  {
    "id": 34,
    "title": "Title 35",
    "thumb_image_path": "/cms8341/shared/gallery/images/35.jpg",
    "isyoutube": false,
    "detail":
    {
      "title": "Title 35",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/35.jpg",
      "youtube_url": ""
    }
  },
  {
    "id": 35,
    "title": "Title 36",
    "thumb_image_path": "/cms8341/shared/gallery/images/36.jpg",
    "isyoutube": false,
    "detail":
    {
      "title": "Title 36",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/36.jpg",
      "youtube_url": ""
    }
  },
  {
    "id": 36,
    "title": "Title 37",
    "thumb_image_path": "/cms8341/shared/gallery/images/37.jpg",
    "isyoutube": false,
    "detail":
    {
      "title": "Title 37",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/37.jpg",
      "youtube_url": ""
    }
  },
  {
    "id": 37,
    "title": "Title 38",
    "thumb_image_path": "/cms8341/shared/gallery/images/38.jpg",
    "isyoutube": false,
    "detail":
    {
      "title": "Title 38",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/38.jpg",
      "youtube_url": ""
    }
  },
  {
    "id": 38,
    "title": "Title 39",
    "thumb_image_path": "/cms8341/shared/gallery/images/39.jpg",
    "isyoutube": false,
    "detail":
    {
      "title": "Title 39",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/39.jpg",
      "youtube_url": ""
    }
  },
  {
    "id": 39,
    "title": "Title 40",
    "thumb_image_path": "/cms8341/shared/gallery/images/40.jpg",
    "isyoutube": false,
    "detail":
    {
      "title": "Title 40",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/40.jpg",
      "youtube_url": ""
    }
  },
  {
    "id": 40,
    "title": "Title 41",
    "thumb_image_path": "/cms8341/shared/gallery/images/41.jpg",
    "isyoutube": false,
    "detail":
    {
      "title": "Title 41",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/41.jpg",
      "youtube_url": ""
    }
  },
  {
    "id": 41,
    "title": "Title 42",
    "thumb_image_path": "/cms8341/shared/gallery/images/42.jpg",
    "isyoutube": false,
    "detail":
    {
      "title": "Title 42",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/42.jpg",
      "youtube_url": ""
    }
  },
  {
    "id": 42,
    "title": "Title 43",
    "thumb_image_path": "/cms8341/shared/gallery/images/43.jpg",
    "isyoutube": false,
    "detail":
    {
      "title": "Title 43",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/43.jpg",
      "youtube_url": ""
    }
  },
  {
    "id": 43,
    "title": "Title 44",
    "thumb_image_path": "/cms8341/shared/gallery/images/44.jpg",
    "isyoutube": false,
    "detail":
    {
      "title": "Title 44",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/44.jpg",
      "youtube_url": ""
    }
  },
  {
    "id": 44,
    "title": "Title 45",
    "thumb_image_path": "/cms8341/shared/gallery/images/45.jpg",
    "isyoutube": false,
    "detail":
    {
      "title": "Title 45",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/45.jpg",
      "youtube_url": ""
    }
  },
  {
    "id": 45,
    "title": "Title 46",
    "thumb_image_path": "/cms8341/shared/gallery/images/46.jpg",
    "isyoutube": false,
    "detail":
    {
      "title": "Title 46",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/46.jpg",
      "youtube_url": ""
    }
  },
  {
    "id": 46,
    "title": "Title 47",
    "thumb_image_path": "/cms8341/shared/gallery/images/47.jpg",
    "isyoutube": false,
    "detail":
    {
      "title": "Title 47",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/47.jpg",
      "youtube_url": ""
    }
  },
  {
    "id": 47,
    "title": "Title 48",
    "thumb_image_path": "/cms8341/shared/gallery/images/48.jpg",
    "isyoutube": false,
    "detail":
    {
      "title": "Title 48",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/48.jpg",
      "youtube_url": ""
    }
  },
  {
    "id": 48,
    "title": "Title 49",
    "thumb_image_path": "/cms8341/shared/gallery/images/49.jpg",
    "isyoutube": true,
    "detail":
    {
      "title": "Title 49",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/49.jpg",
      "youtube_url": "https://www.youtube.com/embed/9ctLe3h_x6o?enablejsapi=1"
    }
  },
  {
    "id": 49,
    "title": "Title 50",
    "thumb_image_path": "/cms8341/shared/gallery/images/50.jpg",
    "isyoutube": false,
    "detail":
    {
      "title": "Title 50",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/50.jpg",
      "youtube_url": ""
    }
  },
  {
    "id": 50,
    "title": "Title 51",
    "thumb_image_path": "/cms8341/shared/gallery/images/51.jpg",
    "isyoutube": true,
    "detail":
    {
      "title": "Title 51",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/51.jpg",
      "youtube_url": "https://www.youtube.com/embed/Df6Sqo1HeB0?enablejsapi=1"
    }
  },
  {
    "id": 51,
    "title": "Title 52",
    "thumb_image_path": "/cms8341/shared/gallery/images/52.jpg",
    "isyoutube": false,
    "detail":
    {
      "title": "Title 52",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/52.jpg",
      "youtube_url": ""
    }
  },
  {
    "id": 52,
    "title": "Title 53",
    "thumb_image_path": "/cms8341/shared/gallery/images/53.jpg",
    "isyoutube": true,
    "detail":
    {
      "title": "Title 53",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/53.jpg",
      "youtube_url": "https://www.youtube.com/embed/mff3eE7uTOM?enablejsapi=1"
    }
  },
  {
    "id": 53,
    "title": "Title 54",
    "thumb_image_path": "/cms8341/shared/gallery/images/54.jpg",
    "isyoutube": false,
    "detail":
    {
      "title": "Title 54",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/54.jpg",
      "youtube_url": ""
    }
  },
  {
    "id": 54,
    "title": "Title 55",
    "thumb_image_path": "/cms8341/shared/gallery/images/55.jpg",
    "isyoutube": true,
    "detail":
    {
      "title": "Title 55",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/55.jpg",
      "youtube_url": "https://www.youtube.com/embed/Timy8PIuO8s?enablejsapi=1"
    }
  },
  {
    "id": 55,
    "title": "Title 56",
    "thumb_image_path": "/cms8341/shared/gallery/images/56.jpg",
    "isyoutube": false,
    "detail":
    {
      "title": "Title 56",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/56.jpg",
      "youtube_url": ""
    }
  },
  {
    "id": 56,
    "title": "Title 57",
    "thumb_image_path": "/cms8341/shared/gallery/images/57.jpg",
    "isyoutube": true,
    "detail":
    {
      "title": "Title 57",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/57.jpg",
      "youtube_url": "https://www.youtube.com/embed/c2RV-2dAX98?enablejsapi=1"
    }
  },
  {
    "id": 57,
    "title": "Title 58",
    "thumb_image_path": "/cms8341/shared/gallery/images/58.jpg",
    "isyoutube": false,
    "detail":
    {
      "title": "Title 58",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/58.jpg",
      "youtube_url": ""
    }
  },
  {
    "id": 58,
    "title": "Title 59",
    "thumb_image_path": "/cms8341/shared/gallery/images/59.jpg",
    "isyoutube": false,
    "detail":
    {
      "title": "Title 59",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/59.jpg",
      "youtube_url": ""
    }
  },
  {
    "id": 59,
    "title": "Title 60",
    "thumb_image_path": "/cms8341/shared/gallery/images/60.jpg",
    "isyoutube": false,
    "detail":
    {
      "title": "Title 60",
      "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
      "image_path": "/shared/gallery/images/60.jpg",
      "youtube_url": ""
    }
  }]
}
```

**14. 20180511 Foreign Language Tokyo**
- Text.

>JavaScript Code:
```javascript

```

**15. 20171211 Chiba Kun’s Hiroba FE**
- Text.

>JavaScript Code:
```javascript

```

**16. 20180508 ChartJS**
- Text.

>JavaScript Code:
```javascript

```

**17. 20180917 Shizuoka Tourist**

- Sử dụng **e.target** ```(!($(e.target).hasClass('accordion_checked') || $(e.target).parents('.accordion_checked').length))``` để loại trừ các phần tử này khỏi ```click```.

![HTML5 Landing Page](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/img_accordion.jpg)

>JavaScript Code:
```javascript
(function($) {
    $(function() {
        $('.accordion .accordion_heading').click(function(e) {
            if (!($(e.target).hasClass('accordion_checked') || $(e.target).parents('.accordion_checked').length)) {
                var dropDown = $(this).closest('.accordion_item').find('.accordion_sub');

                $(this).closest('.accordion').find('.accordion_sub').not(dropDown).slideUp();

                if ($(this).hasClass('active')) {
                    $(this).removeClass('active');
                } else {
                    $(this).closest('.accordion').find('.accordion_heading.active').removeClass('active');
                    $(this).addClass('active');
                }

                dropDown.stop(false, true).slideToggle();

                e.preventDefault();
            }
        });
    });
})(jQuery);
```

**18. 20180926 Tokyo Form Search 1st request**
- Nhờ các bạn tạo JS liên quan đến form search của Tokyo. Tokyo thì có thay đổi spec chỗ Search nên sẽ chỉnh sửa phần Search đã có. Nhờ các bạn dựa vào file để tạo JS để có được nội dung như bên dưới

▼Nội dung request
Tại phần「ファイル形式の指定/chỉ định format file」hãy chỉnh sửa giống như bên dưới

---------
Trường hợp lấy Microsoft Word (.doc)　làm đối tượng tìm kiếm
<input type="hidden" name="filetype" value="doc">

Trường hợp loại trừ Microsoft Word (.doc) 　ra khỏi đối tượng tìm kiếm
<input type="hidden" name="filetype" value="-doc">

※pdf, xls cũng tương tự, trường hợp loại bỏ thì gắn - ở value
---------

※Khi set làm đối tượng search và loại bỏ khỏi đối tượng search thì từng value được setting vào, nhưng hãy làm thế nào đó để những giá trị đó không truyền vào Search.
Về chỉnh sửa HTML thì hãy cho chúng tôi biết chỗ đã chỉnh sửa

■ URL tương ứng
http://www.metro.tokyo.jp/search/index.html
http://www.metro.tokyo.jp/tosei/hodohappyo/press/index.html

>HTML Code:
```javascript
<p>
    <input type="hidden" id="filetype_val" name="filetype" value="">
    <select id="label_as_filetype" name="as_filetype">
        <option selected="selected" value="">すべての形式</option>
        <option value="doc">Microsoft Word (.doc)</option>
        <option value="xls">Microsoft Excel (.xls)</option>
        <option value="pdf">Adobe Acrobat PDF (.pdf)</option>
    </select> を
    <select id="scope_search" title="検索対象範囲" name="as_ft">
        <option selected="selected" value="i">検索対象にする</option>
        <option value="e">検索対象から除く</option>
    </select>
</p>
```

>JavaScript Code:
```javascript
//Search target
$('#label_as_filetype').on('change', function() {
    var value = $(this).find('option:selected').val();
    var type_search = $('#scope_search').find('option:selected').val();
    if (value != '') {
        if (type_search == 'e') {
            $('#filetype_val').val('-' + value);
        } else if (type_search == 'i') {
            $('#filetype_val').val(value);
        }
    } else {
        $('#filetype_val').val('');
    }
});
$('#scope_search').on('change', function() {
    var value_scope = $(this).find('option:selected').val();
    var type_file = $('#label_as_filetype').find('option:selected').val();
    if (type_file != '') {
        if (value_scope == 'e') {
            $('#filetype_val').val('-' + type_file);
        } else if (value_scope == 'i') {
            $('#filetype_val').val(type_file);
        }
    } else {
        $('#filetype_val').val('');
    }
});
```
**19. 20180926 Tokyo Form Search 2nd request**
- Nhờ các bạn set để khi nhấn checkbox「分野」thì「ファイル形式の指定/Chỉ định format file (Selectbox file type và 検索対象にする(Set thành đối tượng search)＆除く(loại trừ khỏi đối tượng search)」được disabled
- Khi set「ファイル形式の指定/Chỉ định format file (Selectbox file type」là những mục khác「すべての形式」thì các checkbox của「分野」trở thành disabled
- Ngoài ra, khi bị disabled hãy thay đổi từng area thành màu xám

- ![Check, Select, Search](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/img_search_tko_1.jpg)
- ![Check, Select, Search](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/img_search_tko_2.jpg)
- ![Check, Select, Search](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/img_search_tko_3.jpg)

>JavaScript Code:
```javascript
(function($) {
  $(function() {
    //FileType Disable 
    var categoryType = [];
    $('input[name="CATEGORY_press_category"]').change(function() {
      if ($(this).prop('checked') == true) {
        categoryType.push($(this).attr('id'));
      } else {
        categoryType.splice(categoryType.indexOf($(this).attr('id')), 1);
      }
      disableFieldType();
    });

    function disableFieldType() {
      var select = $('select[name="as_filetype"]');
      if (categoryType.length > 0) {
        select.parents('tr').first().children().addClass('disable');
        select.prop('disabled', 'disabled');
        $('select[name="as_ft"]').prop('disabled', 'disabled');
      } else {
        select.parents('tr').first().children().removeClass('disable');
        select.prop('disabled', false);
        $('select[name="as_ft"]').prop('disabled', false);
      }
    }

    $('select[name="as_filetype"]').change(function() {
      var txt = $(this).find('option:selected').text(),
        input = $('input[name="CATEGORY_press_category"]');
      if (txt != 'すべての形式') {
        input.parents('tr').first().children().addClass('disable');
        input.attr("disabled", true);
      } else {
        input.parents('tr').first().children().removeClass('disable');
        input.attr("disabled", false);
      }
    });
  });
})(jQuery);
```

>HTML Code:
```javascript
<div id="tmp_press_enquete">
  <form id="tmp_press_search2" action="https://search.metro.tokyo.lg.jp/" method="get">
    <input type="hidden" value="JP" name="temp">
    <input type="hidden" value="u" name="ie">
    <input type="hidden" value="t" name="ord">
    <input type="hidden" value="www.metro.tokyo.jp/tosei/hodohappyo/press" name="sitesearch">
    <input id="tmp_gsa_required2" type="hidden" value="" name="requiredfields">
    <table>
      <tbody>
        <tr>
          <th>
            <label for="label_keyword">キーワード</label>
            <br class="sp_none">
            <span class="txt_red">（必須）</span></th>
          <td>
            <p>検索方法を選んで、検索するキーワードを入力して下さい。</p>
            <p class="press_textbox">
              <input id="label_keyword" maxlength="512" name="kw">
            </p>
            <div id="tmp_press_keyword_check" class="ujs">
              <fieldset>
                <legend>検索範囲</legend>
                <label for="tmp_pm_flg"><span class="press_keywordbox"><input id="tmp_pm_flg" type="radio" value="完全一致" name="pm_flg">完全一致</span></label>
                <label for="tmp_am_flg"><span class="press_keywordbox"><input id="tmp_am_flg" type="radio" checked="checked" value="あいまい" name="pm_flg">あいまい</span></label>
              </fieldset>
            </div>
          </td>
        </tr>
        <tr class="ujs">
          <th>分野</th>
          <td>
            <p>検索したい分野を選んで下さい。</p>
            <fieldset>
              <legend>分野</legend>
              <label for="label_press_category1"><span class="press_checkbox">                 <input id="label_press_category1" type="checkbox" value="イベント" name="CATEGORY_press_category">イベント</span></label>
              <label for="label_press_category2"><span class="press_checkbox">                 <input id="label_press_category2" type="checkbox" value="募集" name="CATEGORY_press_category">募集</span></label>
              <label for="label_press_category3"><span class="press_checkbox">                 <input id="label_press_category3" type="checkbox" value="お知らせ" name="CATEGORY_press_category">お知らせ</span></label>
              <label for="label_press_category4"><span class="press_checkbox">                 <input id="label_press_category4" type="checkbox" value="計画・財政" name="CATEGORY_press_category">計画・財政</span></label>
              <label for="label_press_category5"><span class="press_checkbox">                 <input id="label_press_category5" type="checkbox" value="審議会等の動き" name="CATEGORY_press_category">審議会等の動き</span></label>
              <label for="label_press_category6"><span class="press_checkbox">                 <input id="label_press_category6" type="checkbox" value="調査結果" name="CATEGORY_press_category">調査結果</span></label>
            </fieldset>
          </td>
        </tr>
        <tr class="ujs">
          <th>掲載年月日</th>
          <td>
            <p>検索したい年月日を指定して下さい。</p>
            <div class="form_select_box">
              <select title="掲載開始年" name="start_year" class="form_year">
                <option selected="selected" value="">年</option>
                <option value="2018">平成30(2018)年</option>
                <option value="2017">平成29(2017)年</option>
                <option value="2016">平成28(2016)年</option>
                <option value="2015">平成27(2015)年</option>
                <option value="2014">平成26(2014)年</option>
                <option value="2013">平成25(2013)年</option>
              </select>
              <select title="掲載開始月" name="start_month" class="form_month">
                <option selected="selected" value="">月</option>
                <option value="01">1月</option>
                <option value="02">2月</option>
                <option value="03">3月</option>
                <option value="04">4月</option>
                <option value="05">5月</option>
                <option value="06">6月</option>
                <option value="07">7月</option>
                <option value="08">8月</option>
                <option value="09">9月</option>
                <option value="10">10月</option>
                <option value="11">11月</option>
                <option value="12">12月</option>
              </select>
            </div>
            <span class="form_select_txt"><img alt="から" src="http://www.metro.tokyo.jp/shared/templates/press/images/form_txt_img.jpg"></span>
            <div class="form_select_box">
              <select title="掲載終了年" name="end_year" class="form_year last">
                <option selected="selected" value="">年</option>
                <option value="2018">平成30(2018)年</option>
                <option value="2017">平成29(2017)年</option>
                <option value="2016">平成28(2016)年</option>
                <option value="2015">平成27(2015)年</option>
                <option value="2014">平成26(2014)年</option>
                <option value="2013">平成25(2013)年</option>
              </select>
              <select title="掲載終了月" name="end_month" class="form_month last">
                <option selected="selected" value="">月</option>
                <option value="01">1月</option>
                <option value="02">2月</option>
                <option value="03">3月</option>
                <option value="04">4月</option>
                <option value="05">5月</option>
                <option value="06">6月</option>
                <option value="07">7月</option>
                <option value="08">8月</option>
                <option value="09">9月</option>
                <option value="10">10月</option>
                <option value="11">11月</option>
                <option value="12">12月</option>
              </select>
            </div>
          </td>
        </tr>
        <tr class="ujs">
          <th>
            <label for="label_as_filetype2">ファイル形式の指定</label>
          </th>
          <td>
            <p>
              <input id="filetype_val2" type="hidden" value="" name="filetype">
              <select title="ファイル形式の指定" id="label_as_filetype2" name="as_filetype">
                <option selected="selected" value="">すべての形式</option>
                <option value="doc">Microsoft Word (.doc)</option>
                <option value="docx">Microsoft Word (.docx)</option>
                <option value="xls">Microsoft Excel (.xls)</option>
                <option value="xlsx">Microsoft Excel (.xlsx)</option>
                <option value="pdf">Adobe Acrobat PDF (.pdf)</option>
                <option value="ppt">Microsoft PowerPoint (.ppt)</option>
                <option value="pptx">Microsoft PowerPoint (.pptx)</option>
              </select> を
              <select title="検索対象範囲" id="scope_search2" name="as_ft">
                <option selected="selected" value="i">検索対象にする</option>
                <option value="e">検索対象から除く</option>
              </select>
            </p>
            <p><span class="txt_small"><span class="txt_red"><strong>※</strong></span>「すべての形式」を「検索対象から除く」ことはできません。</span>
              <br>
              <span class="txt_small"><span class="txt_red"><strong>※</strong></span>「分野」と「ファイル形式の指定」を同時に絞り込むことはできません。</span>
            </p>
          </td>
        </tr>
      </tbody>
    </table>
    <div class="press_key_center">
      <div id="tmp_search_btn">
        <label>
          <input type="submit" value="検索">
        </label>
      </div>
      <input id="tmp_clear_btn" type="reset" value="クリア">
    </div>
  </form>
  <script type="text/javascript">
  (function($) {
    $(function() {
      $('#tmp_press_search2').submit(function() {
        if ($('#tmp_press_search2 input[name="kw"]').val() == '') {
          alert("キーワードを入力してください");
          return false;
        } else {
          //データ取得　変数設定
          var error = Array(); //エラー
          var pressCategory = '';
          var pressCategoryTmp = $('#tmp_press_search2 input[name="press_category"]:checked');
          var start = '';
          var startYear = $('select[name="start_year"]').val();
          var startMonth = $('select[name="start_month"]').val();
          var end = '';
          var endYear = $('select[name="end_year"]').val();
          var endMonth = $('select[name="end_month"]').val();
          var requiredField = '';

          //初期化
          if ($("#tmp_gsa_date1").length) $("#tmp_gsa_date1").remove();
          if ($("#tmp_gsa_date2").length) $("#tmp_gsa_date2").remove();
          //完全一致 or あいまい
          if ($('input[name="pm_flg"]:checked').val() == '完全一致') {
            var qVal = '"' + $('#tmp_press_search2 input[name="kw"]').val() + '"';
            qVal = qVal.replace(/^""/, '"').replace(/""$/, '"'); //「""」の付与
          } else {
            var qVal = $('#tmp_press_search2 input[name="kw"]').val().replace(/"/g, ''); //完全一致用の「"」削除
          }

          //キーワード入れ込み
          $('#tmp_press_search2 input[name="kw"]').val(qVal);
          //分野
          if (pressCategoryTmp.length) {
            $(pressCategoryTmp).each(function() {
              pressCategory += 'press_category:' + $(this).val() + '|';
            });
            pressCategory = pressCategory.replace(/\|$/, "");
          }
          //掲載年月日
          if (startYear != '' || startMonth != '' || endYear != '' || endMonth != '') {
            error['date'] = '';
            //開始年月日
            if (startYear != '' && startMonth != '') {
              start = startYear + '' + startMonth + '01';
            } else if (startYear == '' && startMonth == '') {} else {
              error['date'] += '開始年月は両方指定してください\n';
            }
            //終了年月日
            if (endYear != '' && endMonth != '') {
              var endDt = new Date(endYear, endMonth, 0);
              var endDay = endDt.getDate();
              end = endYear + '' + endMonth + '' + endDay;
            } else if (endYear == '' && endMonth == '') {} else {
              error['date'] += '終了年月は両方指定してください\n';
            }
            //エラーが無ければデータ入れ込み
            if (error['date'] == '') {
              $('#tmp_press_search2').append('<input type="hidden" name="start_dt" value="' + start + '" id="tmp_gsa_date1">').append('<input type="hidden" name="end_dt" value="' + end + '" id="tmp_gsa_date2">');
            } else {
              alert(error['date']);
              return false;
            }
          }
          //requiredfieldまとめ
          if (pressCategory != '') {
            if (requiredField != '') requiredField += '.';
            requiredField += '(' + pressCategory + ')';
          }
          $('#tmp_press_search2').find('input[name="requiredfields"]').val(requiredField);
        }
        //Search target
        var value = $('#label_as_filetype2').find('option:selected').val();
        var type_search = $('#scope_search2').find('option:selected').val();
        if (value != '') {
          if (type_search == 'e') {
            $('#filetype_val2').val('-' + value);
          } else if (type_search == 'i') {
            $('#filetype_val2').val(value);
          }
        } else {
          $('#filetype_val2').val('');
        }
        var value_scope = $('#scope_search2').find('option:selected').val();
        var type_file = $('#label_as_filetype2').find('option:selected').val();
        if (type_file != '') {
          if (value_scope == 'e') {
            $('#filetype_val2').val('-' + type_file);
          } else if (value_scope == 'i') {
            $('#filetype_val2').val(type_file);
          }
        } else {
          $('#filetype_val2').val('');
        }
      });
    });
  })(jQuery);
  </script>
</div>
```

**20. 20181025 KDDI**
- **Xử lý sự kiên click khi switch từ window sang smartphone mà ko bị lỗi**
- Có sử dụng hàm ```off()``` để tắt sự kiện click. Sau đó bật lên lại.
- Về hàm ```resize``` thì gọi lại function, hàm này có tác dụng như sau.
- ![slide 1, 2](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/clear_click.png)

>JavaScript Code:
```javascript
function dropdown_sp(){
    var interview_list = $('.interview_article_list');
    var tmp_drop = '<div class="dropdown_menu"></div>';
    var interview_item = $('.interview_article_list .interview_article_item').eq(4);
    if ($(window).width() < 480) {
        interview_item.after(tmp_drop);
        $('.interview_article_list .interview_article_item').each(function() {
            $(this).find('a').off('click');
            $(this).find('a').on('click', function(e){
                if(!$(this).hasClass('active')){
                    $('.interview_article_list .interview_article_item a').removeClass('active');
                    $(this).addClass('active');
                    $('.dropdown_menu').empty();
                    var item_list = $(this).parent().find('.interview_sub').html();
                    var interview_sub = $(this).parent().find('.interview_sub').clone().html(item_list);
                    $('.dropdown_menu').prepend(interview_sub).slideDown(300);
                } else {
                    $('.dropdown_menu').slideUp(300);
                    $(this).removeClass('active');
                }
                e.preventDefault();
            });
        });
    }
    else{
        $('.dropdown_menu').remove();
    }
}
dropdown_sp();
var timer = false;
$(window).resize(function(){
    if (timer !== false) {
        clearTimeout(timer);
    }
    timer = setTimeout(function() {
        dropdown_sp();
    }, 200);
});
```

**21. Progress Bar Start/Stop**
- Text.

>HTML Code:
```javascript
<div class="progress">
  <div class="progress-bar" role="progressbar" aria-valuenow="60" aria-valuemin="0" aria-valuemax="100" style="width: 5%;">
    <span class="sr-only">60% Complete</span>
  </div>
</div>
```

>JavaScript Code:
```javascript
function progressBar(){
  var width = 5;
  var slide_interval;
  var elem = $('.progress-bar');
  function next_slide() {
    if (width >= 100) {
      clearInterval(slide_interval);
    } else {
      width++; 
      elem.animate({width: width + '%'}, 100); 
    }
  }
  function pause_slide(){
    clearInterval(slide_interval);
  }
  function play_slide(){
    slide_interval = setInterval(next_slide, 100);
  }

  $('.time-ctrl').on('click', function(e){
    if(!$(this).hasClass('pause')){
      $(this).addClass('pause');
      play_slide();
    }
    else{
      $(this).removeClass('pause');
      pause_slide();
    }
    e.preventDefault();
  });
}
```

**22. 20181204_Advertisement_Xd**
- Text.

>JavaScript Code:
```javascript

```

**22. 20181109_Go_Tokyo_Convert_English**
- **Về scroll ở footer khi ở SP**: Về navigation được hiển thị ở footer khi về SP, vì có trường hợp menu trình duyệt chẳng hạn như Safari cản trở, không thể tap được nên「trường hợp scroll xuống dưới」thì không cho hiển thị, 「Trường hợp scroll lên trên」thì hiển thị. Tôi gửi các bạn sample, nhưng nhờ các bạn bổ sung cơ chế giống như mô tả bên dưới (dự án khác)
- ![slide 1, 2](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/scroll-up-down.jpg)
>JavaScript Code:
```javascript
var old_position = 0;
$(window).on('scroll', function() {
var current = (window.scrollY) ? window.scrollY : window.pageYOffset;
  if (current > 100 && current > old_position && current < $('#tmp_wrapper').outerHeight()- $(window).height()) {
    $('#tmp_navi_sticky').addClass('hidden');
  } else {
    $('#tmp_navi_sticky').removeClass('hidden');
  }
  old_position = current;
});
```

**23. 20181218_Kanagawa**
  - ![Image](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/koutou_data.jpg)
- Chúng tôi còn 1 request muốn nhờ các bạn tạo về JS, không biết có thể nhờ các bạn tạo theo spec bên dưới được không?
▼Khái quát
Lưu sẵn nhiều data (mã tổ chức, path image, text data) vào XML, và dựa vào data thống nhất với mã tổ chức được mô tả ở tag meta trong HTML, ghi đè lên nơi tương ứng của HTML (Về cơ bản, chúng tôi muốn lưu sẵn data của trường học vào XML, rồi lấy mã tổ chức làm key, sau đó get và hiển thị image chẳng hạn)

▼Ví dụ XML
Đính kèm
※Về inq_flg, sau khi xác định spec thì bên chúng tôi sẽ tạo nên các bạn không cần đối ứng

▼Ví dụ tag meta trong HTML
```javascript
<meta name="department" content="010010010" />
```
※Chứa data giống với department_code của XML

▼Nơi ghi đè trong HTML
\000100_GD_神奈川県教育委員会_テンプレート\cms8341\upload\top\top_a.html
```javascript
1. #tmp_hlogo .logo img / logo_path
2. #tmp_hlogo .en_name text / department_en
```
**koutou_data.xml: ** /cms8341/shared/xml/koutou_data.xml

>XML Code:
```javascript
<?xml version="1.0" encoding="utf-8"?>
<school_data>
    <item>
        <department_code>010010010</department_code>
        <department_en>sample school</department_en>
        <logo_path>/cms8341/shared/images/logo.png</logo_path>
        <inq_flg>1</inq_flg><!-- true=1, false=0 -->
    </item>
    <item>
        <department_code>010010020</department_code>
        <department_en>sample2 school</department_en>
        <logo_path>/cms8341/shared/images/logo.png</logo_path>
        <inq_flg>1</inq_flg><!-- true=1, false=0 -->
    </item>
</school_data>
```

>HTML Code:
```javascript
<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" lang="ja" xml:lang="ja">
<head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
    <meta http-equiv="Content-Style-Type" content="text/css" />
    <meta http-equiv="Content-Script-Type" content="text/javascript" />
    <title>ページタイトル</title>
    <meta name="department" content="010010020" />
</head>
<body class="format_top no_javascript">
    <div id="tmp_wrapper">
        <div id="tmp_header">
            <div class="container">
                <div id="tmp_hlogo">
                    <h1>
                        <span class="logo"><img src="/cms8341/shared/images/logo.png" alt="" /></span>
                        <span class="text">
                            <span class="prefecture">神奈川県立</span>
                            <span class="name">〇〇高等学校</span>
                            <span class="en_name" lang="en" xml:lang="en">〇〇〇〇〇〇 HIGH SCHOOL</span>
                        </span>
                    </h1>
                </div>
                <div class="right_cnt">
                    <div id="tmp_means">
                        <ul id="tmp_setting">
                            <li><a href="/cms8341/#" class="setting_link">文字サイズ・色合い変更</a></li>
                            <li><a href="/cms8341/#" class="setting_map">アクセス</a></li>
                        </ul>
                    </div>
                    <div id="tmp_search">
                        <form action="/cms8341/#" id="tmp_gsearch">
                            <label class="query_label" for="tmp_query">ページ内検索</label>
                            <div id="tmp_wrap_query">
                                <input id="tmp_query" class="query_area" size="31" name="q" />
                            </div>
                            <p class="query_submit"><input id="tmp_func_sch_btn" type="submit" name="sa" value="検索" /> </p>
                        </form>
                    </div>
                </div>
                <div id="tmp_sma_menu">
                    <a href="javacript:void(0);" class="sma_menu_open"><span>メニュー</span></a>
                    <a href="javacript:void(0);" class="close_btn">閉じる</a>
                </div>
            </div>
        </div>
    </div>
    <script type="text/javascript" src="/cms8341/shared/js/main.js"></script>
</body>
</html>
```
>JavaScript Code:
```javascript
(function($){
    if ($('meta[name="department"]').length){
        var cnt = $('meta[name="department"]').attr('content');
        $.ajax({
            'url' : '/cms8341/shared/xml/koutou_data.xml',
            'success': function(results){
                var dom = $(results);
                dom.find('item').each(function(){
                    if (cnt == $(this).find('department_code').text().trim()){
                        $('#tmp_hlogo .logo img').attr('src',$(this).find('logo_path').text());
                        $('#tmp_hlogo .en_name').text($(this).find('department_en').text());
                    }
                })
            }
        })
    }
})(jQuery);
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


