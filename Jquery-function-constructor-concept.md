#### 1. Window onload
---
```javascript
$( window ).load(function() {
  // code here
});
```

#### 2. Document ready
---
```javascript
$(document).ready(function(){
  // code here
});
```

#### 3. function($)
---
```javascript
(function($) {
  $(function() {
    // Function
    var handleFunction = function() {
      
    };
    // Call function
    handleFunction();

  });
})(jQuery);
```

#### 4. App function
---
```javascript
var App = function() {
  function handleFunction() {
		// code here   
  }
  return {
    init: function() {
      handleFunction();
    }
  };
}();
$(document).ready(function() {
  App.init();
});
```

#### 5. Function ```window```
---
- Scroll down header slide up, Scroll Up header slide down.
- Kiểm tra xem thử ```window``` có hàm ```tt_sticky``` hay chưa. Nếu chưa có thì gán ```function``` cho nó.

```javascript
var jc = jQuery;
jc.noConflict();
'use strict';
jc(document).ready(function() {
  tt_sticky();
});

if ('function' !== typeof(window['tt_sticky'])) {
  window.tt_sticky = function() {
    var isMobile = jc('body').hasClass('touch') ? true : false;
    if (jc('.tt_sticky').length) {
      var menuposition;
      var menu_content_offset = jc('#header_container').outerHeight() - jc('.tt_sticky').outerHeight();
      jc('#header_container').css('min-height', jc('#header_container').outerHeight());
      if (jc('.admin-bar').length && !window.matchMedia('(max-width: 600px)').matches) {
        menuposition = jc('#header_container').offset().top - jc('#wpadminbar').outerHeight() + menu_content_offset;
      } else {
        menuposition = jc('#header_container').offset().top + menu_content_offset;
      }
      jc(window).resize(function() {
        setTimeout(function() {
          jc('#header_container').css('min-height', jc('.tt_sticky').outerHeight());
        }, 500);
        if (jc('.admin-bar').length && !window.matchMedia('(max-width: 600px)').matches) {
          menuposition = jc('#header_container').offset().top - jc('#wpadminbar').outerHeight() + menu_content_offset;
        } else {
          menuposition = jc('#header_container').offset().top + menu_content_offset;
        }
      });
      jc(window).scroll(function(event) {
        if (jc(window).scrollTop() > menuposition) {
          jc('.tt_sticky').addClass('tt_stuck');
        } else {
          jc('.tt_sticky').removeClass('tt_stuck');
        }
      });
    }
    if (jc('.tt_header_hiding').length && isMobile == false) {
      var didScroll;
      var delta = 5;
      var navbarHeight = jc('#header_container').outerHeight() + jc('.tt_header_hiding').outerHeight();
      var lastScrollTop = jc('#header_container').offset().top + jc('.tt_header_hiding').outerHeight();
      var firstTop = jc('#header_container').offset().top + jc('.tt_sticky').outerHeight();
      jc(window).scroll(function(event) {
        if (jc(window).scrollTop() > menuposition) {
          didScroll = true;
          hasScrolled();
        }
      });

      function hasScrolled() {
        var st = jc(window).scrollTop();
        if (Math.abs(lastScrollTop - st) <= delta) { return; }
        if (st > lastScrollTop && st > navbarHeight) {
          jc('.tt_header_hiding').css('margin-top', -jc('.tt_header_hiding').outerHeight());
          jc('.tt_header_hiding').addClass('.tt_header_hidden');
        } else {
          if (st + jc(window).height() < jc(document).height()) {
            jc('.tt_header_hiding').removeClass('.tt_header_hidden');
            jc('.tt_header_hiding').css('margin-top', '0');
          }
        }
        if (st > firstTop) {
          lastScrollTop = st;
        } else {
          lastScrollTop = firstTop;
        }
      }
    }
  };
}
```
#### 6. function for jQuery**
---
```javascript
//function to fix height of iframe!
  var calcHeight = function() {
    var headerDimensions = $('#mainlivedemo').height();
    var selector = ($('.stretched').length > 0) ? '#iframelive' : '#iframelive iframe';
    $(selector).height($(window).height() - headerDimensions);
  }
  $(document).ready(function() {
    calcHeight();
  });
  $(window).resize(function() {
    calcHeight();
  }).load(function() {
    calcHeight();
  });
  ```

### 7. Build pattern more function for project
---
```javascript
var _ua = (function(u) {
  return {
    Tablet: u.indexOf("ipad") !== -1 || (u.indexOf("android") !== -1 && u.indexOf("mobile") === -1) || (u.indexOf("firefox") !== -1 && u.indexOf("tablet") !== -1),
    iOS: (u.indexOf("ipad") !== -1) || u.indexOf("iphone") !== -1 || u.indexOf("ipod") !== -1,
    Mobile: (u.indexOf("windows") !== -1 && u.indexOf("phone") !== -1) || u.indexOf("iphone") !== -1 || u.indexOf("ipod") !== -1 || (u.indexOf("android") !== -1 && u.indexOf("mobile") !== -1) || (u.indexOf("firefox") !== -1 && u.indexOf("mobile") !== -1)
  };
})(window.navigator.userAgent.toLowerCase());

$(function() {
  var wW, wH, headrHeight;
  var $window = $(window);
  ({
    conf: {
      breakPoint: 768,
    },
    init: function() {
      var self = this;
      self.isSP();
      self.isiOS();
      self.retina();
      self.smoothScroll();
      self.outerHashLink();
      self.loading();
      self.accordion_1();
      self.accordion_2();
      self.pageTop();
      self.gNav();
      self.gotoWorksBG();
    },
    getResize: function() {
      var self = this;
      $window.on('resize', function() {
        wW = window.innerWidth;
        wH = window.innerHeight;
      }).trigger("resize");
      if (wW <= self.conf.breakPoint) {
        $('meta[name="viewport"]').attr('content', 'width=device-width,initial-scale=1');
      } else {
        $('meta[name="viewport"]').attr('content', 'width=1140');
      }
      $window.on('orientationchange', function() {
        if (wW <= self.conf.breakPoint) {} else {}
      });
      return [wW, wH];
    },
    isSP: function() { // SP用
      if (_ua.Mobile) {
        $('.callaction').each(function() {
          var $ele = $(this),
            tel = $ele.data('tel');
          $ele.wrap('<a href="tel:' + tel + '"></a>');
        });
      }
    },
    isiOS: function() { // SP以外
      //			var self = this;
      if (_ua.iOS) {
        $('article a, a.btn01, a.btn02, form span.btn02').addClass('ios');
      }
    },
    retina: function() {
      var retinaCheck = window.devicePixelRatio;
      if (retinaCheck >= 2) {
        $('img.retina').each(function() {
          var retinaimg = $(this).attr('src').replace(/\.(?=(?:png|jpg|jpeg)$)/i, '@2x.');
          $(this).attr('srcset', retinaimg + " 2x");
        });
      }
    },
    gNav: function() {
      var start_pos = 0;
      $(window).scroll(function() {
        var current_pos = $(this).scrollTop();
        var cntH = $('body').height();
        if (current_pos < 10) {
          setTimeout(func, 100);
        } else if (current_pos > start_pos) { //下へスクロール
          //					console.log('scrollDown');
          if (current_pos < wH * 0.1) { //ウィンドウ上部
            $('body').removeClass('scrollDown').addClass('scrollUp');
          } else if (current_pos > (cntH - wH - 1)) { //ウィンドウ下部
            //					console.log('scrollDown bottom');
            $('#gNav').addClass('show');
            $('body').removeClass('scrollDown').addClass('scrollUp');
          } else { //ウィンドウ中段
            $('#gNav').addClass('show');
            $('body').removeClass('scrollUp').addClass('scrollDown');
          }
        } else if (current_pos) { //上へスクロール
          //					console.log('scrollUp');
          $('body').removeClass('scrollDown').addClass('scrollUp');
        }
        start_pos = current_pos;
      });
      $("#gNav").hover(
        function() {
          $('body').removeClass('scrollDown').addClass('scrollUp');
        },
        function() {
          $('body').removeClass('scrollUp').addClass('scrollDown');
        }
      );

      function func() {
        $('#gNav').removeClass('show');
      }
    },
    loading: function() {
      //			var self = this;
      if ($('body.loading')[0]) {
        $('body').append('<div id="loading"><span><img src="/img/common/arrow_01.svg" alt="読み込み中"></span></div>');
        $window.on('load', function() {
          var tl = new TimelineMax();
          tl
            .to($('#wrapper'), 0.3, {
              opacity: 1,
              onComplete: function() {
                $('article.wpPost > *').attr('data-aos', 'fade-up');
              }
            })
            .to('#loading img', 0.2, {
              opacity: 0,
              delay: 0.2,
              onComplete: function() {}
            })
            .to('#loading', 0.2, {
              opacity: 0,
              delay: 0.2,
              onComplete: function() {
                $('#loading').remove();
                var scrPos = $window.scrollTop();
                $window.scrollTop(scrPos + 1).scrollTop(scrPos - 1); //1pxスクロールして要素を表示
                AOS.init({
                  easing: 'ease-in-out-cubic',
                  once: true,
                  disable: 'phone'
                });
              }
            });
        });
      }
    },
    skip: function() {
      var scrPos = $window.scrollTop();
      $('#loading').fadeOut();
      $('#wrapper').css('opacity', 1);
      $window.scrollTop(scrPos + 1).scrollTop(scrPos - 1); //1pxスクロールして要素を表示
    },
    smoothScroll: function() {
      $('a[href^="#"]').click(function() {
        var speed = 1000;
        var href = $(this).attr('href');
        var target = $(href === "#" || href === "" ? 'html' : href);
        var position = target.offset().top - 15;
        $('body,html').animate({ scrollTop: position }, speed, 'easeOutQuint');
        return false;
      });
    },
    outerHashLink: function() { //別ページからのハッシュリンク
      var url = location.search;
      //			var $wpr = $('#wrapper');
      if (url.indexOf('id=') !== -1) {
        var id = url.match(/id=(.*?)(&|$)/)[1];
        $(window).on('load', function() {
          setTimeout(function() { //レンダリングを待つ
            //$wpr.fadeTo('fast',1);
            var target = $('#' + id);
            var pos = target.offset().top - headrHeight;
            $("html, body").animate({ scrollTop: pos }, 500, 'easeOutQuint');
          }, 50);
        });
      } else {
        $(window).on('load', function() {
          //$wpr.fadeTo(200,1); //
        });
      }
    },
    accordion_1: function() {
      $('.acTrigger').on('click', function() {
        $(this).next().slideToggle('slow', 'easeOutQuint');
        $(this).toggleClass('opened');
      });
    },
    accordion_2: function() {
      var $acdSet = $('.acdSet');
      $acdSet.each(function() {
        var obj = !1,
          $this = $(this),
          $btnMore = $this.find('.btnMore'),
          $wrap = $this.find('.acdWrap'),
          opend = 'opend';
        $btnMore.click(function() {
          var wrapH = $wrap.outerHeight(),
            containerH = $this.find('.acdContents').innerHeight();
          obj ?
            (TweenMax.to($wrap, 1, { height: wrapH, ease: Power3.easeInOut }), $this.removeClass(opend), obj = !1) :
            (TweenMax.to($wrap, 1, { height: containerH, ease: Power3.easeInOut }), $btnMore.fadeOut('slow'), $this.addClass(opend), obj = !0)
        });
      });
    },
    gotoWorksBG: function() {
      //			var self = this;
      var target = $('#gotoWorks');
      if (target[0]) {
        $("#scroller").simplyScroll({
          pauseOnHover: false,
          pauseOnTouch: false,
          speed: 1
        });
      }
    },
    pageTop: function() {
      var btnPagetop = $('#pageTop');
      $window.on('scroll', function() {
        if ($(this).scrollTop() > 110) {
          btnPagetop.fadeIn('slow');
        } else {
          btnPagetop.fadeOut('slow');
        }
      });
    }
  }.init());

  // easing
  $.extend($.easing, {
    easeOutQuint: function(e, f, a, h, g) {
      return -h * ((f = f / g - 1) * f * f * f - 1) + a;
    }
  });

});
```

### 8. Function Declarations
---
```javascript
function functionName(parameters) {
  code to be executed
}
```

### 9. Function Expression
---
```javascript
var x = function (a, b) {
  return a * b
};
document.getElementById("demo").innerHTML = x(4,5);
```
