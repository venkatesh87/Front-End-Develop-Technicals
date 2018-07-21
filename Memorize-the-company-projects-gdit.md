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

 ![Your Life in Hyogo](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/world_clock.jpg)
 
**Hướng dẫn :**
>Case 1:
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

>Case 2:

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

```javascript

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

```javascript

```

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
**13. 20180508 ChartJS**
- Text.

>JavaScript Code:
```javascript

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


