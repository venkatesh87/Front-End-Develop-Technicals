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
  
### 7. Function Declarations
---
```javascript
function functionName(parameters) {
  code to be executed
}
```

### 8. Function Expression
---
```javascript
var x = function (a, b) {
  return a * b
};
document.getElementById("demo").innerHTML = x(4,5);
```

### 9. Build pattern more function for project step 1
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

### 10. Build pattern more function for project step 2
---
```javascript
/**
 * CyberAgent
 *
 * @date 2017-08-16
 */

(function($) {
  var CA = window.CA || {};

  CA.Top = function() {
    // Initialize
    var _init = function _init() {
      _heroUI();
      _contentsNavUI();
    };

    var _heroUI = function _heroUI() {
      var $hero_carousel = $('#hero_carousel');
      var $hero_carousel_item = $hero_carousel.find('.hero_carousel_item');
      var carouse_item_length = $hero_carousel_item.length;
      var carousel_change_speed = 1000;
      var carousel_change_interval = 4500;
      var $hero_carousel_toggleSwitch = $('#hero_carousel_toggleSwitch');
      var $hero_carousel_pager = $('#hero_carousel_pager');
      var $hero_carousel_pager_item = $hero_carousel_pager.find('.hero_carousel_pager_item');
      var $hero_carousel_pager_thumb = $('#hero_carousel_pager_thumb');
      var $hero_carousel_pager_thumb_list = $('#hero_carousel_pager_thumb_list');
      var hero_carousel_pager_thumb_width = $hero_carousel_pager_thumb.width();
      var currentCarouselIndex = 0;
      var timer = void 0;
      var autoplayIsEnabled = true;
      var carouselIsAnimated = false;

      $(window).on('resize', function() {
        hero_carousel_pager_thumb_width = $hero_carousel_pager_thumb.width();
      });

      // スワイプ操作
      $hero_carousel.hammer().on('swipe', function(event) {
        if (event.gesture.deltaX < 0) {
          changeCarousel(currentCarouselIndex + 1);
        }
        if (event.gesture.deltaX > 0) {
          changeCarousel(currentCarouselIndex - 1);
        }
      });

      $hero_carousel_item.eq(currentCarouselIndex).removeClass('is-ready').addClass('is-current');
      $hero_carousel_pager_item.eq(currentCarouselIndex).addClass('is-current');

      $hero_carousel_pager_thumb_list.css({ width: hero_carousel_pager_thumb_width * carouse_item_length });

      $hero_carousel_pager.find('li').each(function(i) {
        $(this).on('click', function() {
          changeCarousel(i, true);
        });

        $(this).on('mouseenter', function() {
          TweenMax.to($hero_carousel_pager_thumb_list, 0.4, {
            x: hero_carousel_pager_thumb_width * i * -1,
            ease: Power4.easeOut
          });

          TweenMax.to($hero_carousel_pager_thumb, 0.4, {
            x: $hero_carousel_pager.width() / carouse_item_length * i - hero_carousel_pager_thumb_width / 2 + 6,
            opacity: 1,
            ease: Power4.easeOut
          });
        });

        $(this).on('mouseleave', function() {
          TweenMax.to($hero_carousel_pager_thumb, 0.3, {
            opacity: 0,
            ease: Power4.easeOut
          });
        });
      });

      var mark_play = 'M14.510,14.638 C16.428,13.139 16.428,10.687 14.510,9.188 L3.481,0.571 C1.286,-0.709 0.009,0.111 0.009,3.225 L0.009,20.601 C0.009,24.637 1.896,24.482 3.481,23.254 L14.510,14.638 Z';
      var mark_pause = 'M17.000,24.000 C15.343,24.000 14.000,22.657 14.000,21.000 L14.000,3.000 C14.000,1.343 15.343,-0.000 17.000,-0.000 C18.657,-0.000 20.000,1.343 20.000,3.000 L20.000,21.000 C20.000,22.657 18.657,24.000 17.000,24.000 ZM3.000,24.000 C1.343,24.000 0.000,22.657 0.000,21.000 L0.000,3.000 C0.000,1.343 1.343,-0.000 3.000,-0.000 C4.657,-0.000 6.000,1.343 6.000,3.000 L6.000,21.000 C6.000,22.657 4.657,24.000 3.000,24.000 Z';
      var duration = 300;
      var s = Snap('#hero_carousel_toggleSwitch_svg');
      var path = s.path(mark_pause).attr({ fill: '#fff' });

      $hero_carousel_toggleSwitch.on('click', function() {
        if (autoplayIsEnabled) {
          autoplayIsEnabled = false;
          controlProgress.reset(currentCarouselIndex);
          path.animate({ path: mark_play }, duration, mina.backout);
          stopCarousel();
        } else {
          autoplayIsEnabled = true;
          path.animate({ path: mark_pause }, duration, mina.backout);
          playCarousel();
        }
      });

      // プログレスバー
      var controlProgress = function() {
        var _increment = function _increment(index) {
          var $target = $hero_carousel_pager_item.eq(index).find('.hero_carousel_pager_item_progress');
          TweenMax.to($target, carousel_change_interval / 1000, {
            scaleX: 1,
            ease: Linear.easeNone
          });
        };

        var _reset = function _reset(target) {
          var $target = void 0;

          if (target === 'all') {
            $target = $('.hero_carousel_pager_item_progress');
          } else {
            $target = $hero_carousel_pager_item.eq(target).find('.hero_carousel_pager_item_progress');
          }

          TweenMax.to($target, 0.4, {
            scaleX: 0,
            ease: Power4.easeOut
          });
        };

        var _finish = function _finish(index) {
          var $target = $hero_carousel_pager_item.eq(index).find('.hero_carousel_pager_item_progress');

          var tl = new TimelineMax();

          tl.to($target, 0.7, {
            scaleX: 1,
            ease: Power4.easeOut
          }).set($target, {
            'transform-origin': 'right'
          }).to($target, 1.1, {
            scaleX: 0,
            ease: Power4.easeOut
          }).set($target, {
            'transform-origin': 'left'
          });
        };

        return {
          increment: _increment,
          reset: _reset,
          finish: _finish
        };
      }();

      // 再生処理
      var playCarousel = function playCarousel() {
        controlProgress.increment(currentCarouselIndex);

        timer = setInterval(function() {
          var nextCarouselIndex = void 0;

          if (currentCarouselIndex === carouse_item_length - 1) {
            nextCarouselIndex = 0;
          } else {
            nextCarouselIndex = currentCarouselIndex + 1;
          }

          changeCarousel(nextCarouselIndex);
        }, carousel_change_interval);
      };

      // 停止処理
      var stopCarousel = function stopCarousel() {
        clearInterval(timer);
      };

      // 切り替え処理
      var changeCarousel = function changeCarousel(newCarouselIndex, usePager) {
        var transitionTime = window.innerWidth < 768 ? 1800 : 2200;

        if (newCarouselIndex === currentCarouselIndex || carouselIsAnimated) {
          return;
        }

        if (newCarouselIndex >= carouse_item_length) {
          newCarouselIndex = 0;
        }

        if (newCarouselIndex < 0) {
          newCarouselIndex = carouse_item_length - 1;
        }

        if (currentCarouselIndex === carouse_item_length - 1 && newCarouselIndex === 0) {
          controlProgress.finish(currentCarouselIndex);

          var tl = new TimelineMax();

          tl.to($('#hero_carousel_pager_progress'), 0.4, {
            scaleX: 1,
            ease: Power4.easeOut
          }).set($('#hero_carousel_pager_progress'), {
            'transform-origin': 'right'
          }).to($('#hero_carousel_pager_progress'), 1.1, {
            delay: 0.7,
            scaleX: 0,
            ease: Power4.easeOut
          }).set($('#hero_carousel_pager_progress'), {
            'transform-origin': 'left'
          });
        } else {
          if (newCarouselIndex > currentCarouselIndex) {
            controlProgress.finish(currentCarouselIndex);
          } else {
            controlProgress.reset(currentCarouselIndex);
          }

          TweenMax.to($('#hero_carousel_pager_progress'), 0.4, {
            scaleX: newCarouselIndex / carouse_item_length,
            ease: Power4.easeOut
          });
        }

        carouselIsAnimated = true;

        var oldCarouselIndex = currentCarouselIndex;

        $hero_carousel_pager_item.eq(oldCarouselIndex).removeClass('is-current');
        $hero_carousel_pager_item.eq(newCarouselIndex).addClass('is-current');

        var direction = void 0;

        if (currentCarouselIndex === carouse_item_length - 1 && newCarouselIndex === 0 && !usePager) {
          direction = 'next';
        } else if (newCarouselIndex > oldCarouselIndex) {
          direction = 'next';
        } else {
          direction = 'prev';
        }

        stopCarousel();

        if (direction === 'next') {
          $hero_carousel_item.eq(oldCarouselIndex).removeClass('is-current').addClass('is-prev');
          $hero_carousel_item.eq(newCarouselIndex).addClass('is-ready-next');

          setTimeout(function() {
            $hero_carousel_item.eq(newCarouselIndex).removeClass(function(index, className) {
              return (className.match(/\bis-\S*/g) || []).join(' ');
            }).addClass('is-current');
          }, 100);
        } else if (direction === 'prev') {
          $hero_carousel_item.eq(oldCarouselIndex).removeClass('is-current').addClass('is-next');
          $hero_carousel_item.eq(newCarouselIndex).addClass('is-ready-prev');

          setTimeout(function() {
            $hero_carousel_item.eq(newCarouselIndex).removeClass(function(index, className) {
              return (className.match(/\bis-\S*/g) || []).join(' ');
            }).addClass('is-current');
          }, 100);
        }

        // WAI-ARIA
        $hero_carousel_item.eq(oldCarouselIndex).attr({ 'aria-hidden': true });
        $hero_carousel_item.eq(newCarouselIndex).attr({ 'aria-hidden': false });
        $hero_carousel_pager_item.eq(oldCarouselIndex).attr({ 'aria-selected': false });
        $hero_carousel_pager_item.eq(newCarouselIndex).attr({ 'aria-selected': true });

        currentCarouselIndex = newCarouselIndex;

        setTimeout(function() {
          carouselIsAnimated = false;

          if (autoplayIsEnabled) {
            playCarousel();
          }
        }, transitionTime);
      };

      playCarousel();
    };

    var _contentsNavUI = function _contentsNavUI() {
      var $contentsNav_section = $('.contentsNav_section');

      $contentsNav_section.each(function() {
        var $this = $(this);
        var $contentsNav_item = $this.find('.contentsNav_item');
        var $contentsNav_section_bg = $this.find('.contentsNav_section_bg');

        $contentsNav_item.each(function() {
          var categoryLabel = $(this).data('category');
          var $relatedBg = $contentsNav_section_bg.filter('.contentsNav_section_bg-' + categoryLabel);
          var $relatedVideo = $relatedBg.find('video');

          $(this).on({
            'mouseenter touchstart': function mouseenterTouchstart() {
              $this.addClass('is-hovered-' + categoryLabel);
              $relatedBg.addClass('is-active');
              playVideo($relatedVideo.get(0));
            },
            'mouseleave touchend': function mouseleaveTouchend() {
              $this.removeClass(function(index, className) {
                return (className.match(/\bis-hovered-\S+/g) || []).join(' ');
              });
              $contentsNav_section_bg.removeClass('is-active');
              pauseVideo($relatedVideo.get(0));
            }
          });
        });
      });

      var playVideo = function playVideo(videoElement) {
        if (!videoElement || !videoElement.paused) {
          return;
        }
        videoElement.play();
      };

      var pauseVideo = function pauseVideo(videoElement) {
        if (!videoElement || videoElement.paused) {
          return;
        }
        videoElement.pause();
      };
    };

    return {
      init: _init
    };
  }();

  CA.Top.init();
})(jQuery);
```
