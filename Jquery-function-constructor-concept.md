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

```javascript
/**
 * CyberAgent
 *
 * @date 2017-10-18
 */
var CA = function ($) {
	var $win = $(window);
	var $doc = $(document);
	var $html = $('html');
	var $body = $('body');
	var viewClass = {
		gnav: 'view-gnav',
		search: 'view-search',
		nav: 'view-nav',
		categoryTopAnimation: 'view-categoryTopAnimation'
	};
	var triggerHideHeaderOffsetTop = 500;
	var hammerTapEvent = $.ua.isTouchDevice ? 'tap' : 'click';

	// 初期化
	var _init = function _init() {
		$(function () {
			if (!$.ua.isTouchDevice) {
				$('.js-rollover').rollover();
			}
			$.scroller({
				marginTop: 30,
				easing: 'easeOutQuint',
				callback: function callback() {
					if ($win.scrollTop() <= triggerHideHeaderOffsetTop && $win.scrollTop() !== 0) {
						_headerUI.hide();
					}
				}
			});
			$('.js-matchHeight').matchHeight();

			if ($.ua.isTouchDevice) {
				_touchHover();
			}

			_headerUI.init();
			_globalNavUI();
			_searchUI();
			_sitemapUI();
			_drawerUI();
			_categoryTopUI();
			_carouselUI();
			_moduleInteraction.init();
			_utilityNavUI();

			setTimeout(function () {
				$body.addClass('is-loaded');
			}, 500);
		});
	};

	var _headerUI = function () {
		var triggerFixedOffsetTop = void 0;
		var scrollTop = 0;
		var $header = $('#header');

		function _init() {
			if (!$('.l-container').length) {
				return;
			}

			$win.on('scroll', function () {
				_scrollHandler();
			});

			$win.on('resize', function () {
				_setValue();
			});

			_setValue();
		}

		function _setValue() {
			triggerFixedOffsetTop = $('.l-container').offset().top;

			if (triggerFixedOffsetTop === 0) {
				$header.addClass('is-fixed');
			}
		}

		function _scrollHandler() {
			var _scrollTop = $win.scrollTop();

			if (_scrollTop > 100) {
				$header.addClass('has-shadow');
			} else {
				$header.removeClass('has-shadow');
			}

			_toggle(_scrollTop);
		}

		function _toggle(_scrollTop) {
			if ($html.hasClass(viewClass.nav)) {
				return;
			}

			if (triggerFixedOffsetTop !== 0) {
				if (scrollTop >= triggerFixedOffsetTop) {
					$header.addClass('is-fixed');
				} else {
					$header.removeClass('is-fixed');
				}
			}

			if (_scrollTop > scrollTop && !$html.hasClass(viewClass.gnav) && !$html.hasClass(viewClass.categoryTopAnimation)) {
				if (scrollTop > triggerHideHeaderOffsetTop && !$header.hasClass('is-hidden')) {
					_hide();
				}
			} else {
				if ($header.hasClass('is-hidden')) {
					_show();
				}
			}

			scrollTop = _scrollTop;
		}

		function _show() {
			$header.removeClass('is-hidden');
		}

		function _hide() {
			$header.addClass('is-hidden');
		}

		return {
			init: _init,
			show: _show,
			hide: _hide
		};
	}();

	var _globalNavUI = function _globalNavUI() {
		var $header = $('.l-header');
		var $gnav_inner = $('.l-globalNavInner');
		var $gnav_item = $('.l-globalNav_item');
		var currentNavIndex = null;
		var heightArw = void 0;
		var currentNavHeight = 0;

		var _init = function _init() {
			heightArw = [];

			$gnav_item.each(function () {
				var $heading = $(this).find('.l-globalNav_heading');
				var $list = $(this).find('.l-globalNav_list');

				TweenMax.set($heading, {
					y: 15,
					opacity: 0
				});
				TweenMax.set($list, {
					y: 15,
					opacity: 0
				});

				heightArw.push($(this).innerHeight() + 180);
			});
		};

		$('.l-header_nav_item').each(function (i) {
			if (location.pathname.indexOf($(this).find('a').attr('data-categoryPath')) === 0) {
				$(this).addClass('is-current');
			}

			$(this).on('mouseenter', function () {
				if (currentNavIndex === i || $html.hasClass(viewClass.categoryTopAnimation)) {
					return;
				}

				if (currentNavIndex !== null) {
					hideNav(currentNavIndex);
				}

				currentNavIndex = i;

				TweenMax.fromTo($gnav_inner, 0.4, {
					height: currentNavHeight
				}, {
					height: heightArw[i],
					ease: Back.easeOut
				});

				currentNavHeight = heightArw[i];
				showNav(i);
			});
		});

		$header.on('mouseleave', function () {
			if (currentNavIndex === null) {
				return;
			}

			TweenMax.fromTo($gnav_inner, 0.5, {
				height: heightArw[currentNavIndex]
			}, {
				height: 0,
				ease: Power4.easeInOut
			});

			hideNav(currentNavIndex);
			currentNavIndex = null;
			currentNavHeight = 0;
		});

		function showNav(i) {
			$html.addClass(viewClass.gnav);
			var $heading = $gnav_item.eq(i).find('.l-globalNav_heading');
			var $list = $gnav_item.eq(i).find('.l-globalNav_list');

			TweenMax.killTweensOf($gnav_item.eq(i));
			$gnav_item.eq(i).css({
				visibility: 'visible',
				opacity: 1
			});

			TweenMax.killTweensOf($heading);
			TweenMax.fromTo($heading, 0.75, {
				y: 25,
				opacity: 0
			}, {
				delay: 0.3,
				y: 0,
				opacity: 1,
				ease: Power4.easeOut
			});

			TweenMax.killTweensOf($list);
			TweenMax.fromTo($list, 0.75, {
				y: 25,
				opacity: 0
			}, {
				delay: 0.45,
				y: 0,
				opacity: 1,
				ease: Power4.easeOut
			});
		}

		function hideNav(i) {
			$html.removeClass(viewClass.gnav);

			TweenMax.fromTo($gnav_item.eq(i), 0.35, {
				opacity: 1
			}, {
				opacity: 0,
				ease: Power4.easeOut,
				onComplete: function onComplete() {
					$gnav_item.eq(i).css({
						visibility: 'hidden',
						opacity: 1
					});
				}
			});
		}

		$win.on('resize', function () {
			_init();
		});

		_init();
	};

	var _searchUI = function _searchUI() {
		$('#header_toggleSearch').hammer().on(hammerTapEvent, function () {
			_open();
		});

		$('#search_close').hammer().on(hammerTapEvent, function () {
			_close();
		});

		var _open = function _open() {
			$doc.on('keydown.searchUI', function (e) {
				if (e.keyCode === 27) {
					_close();
				}
			});

			$html.addClass(viewClass.search);
			setTimeout(function () {
				$('.mf_finder_searchBox_query_input').focus();
			}, 100);
		};

		var _close = function _close() {
			$doc.off('.searchUI');
			$html.removeClass(viewClass.search);
		};
	};

	var _sitemapUI = function _sitemapUI() {
		$win.on('resize', function () {
			_close();
		});

		$('#header_toggleSitemap').hammer().on(hammerTapEvent, function () {
			_open();
		});

		$('#sitemap_close').hammer().on(hammerTapEvent, function () {
			_close();
		});

		var _open = function _open() {
			setTimeout(function () {
				$('.l-sitemap_close').eq(0).find('button').focus();
			}, 100);

			$doc.on('keydown.sitemapUI', function (e) {
				if (e.keyCode === 27) {
					_close();
				}
			});

			$body.addClass('view-sitemap');
		};

		var _close = function _close() {
			$doc.off('.sitemapUI');
			$body.removeClass('view-sitemap');
		};
	};

	var _drawerUI = function _drawerUI() {
		var $toggle = $('#header_toggleDrawer_btn');
		var $directory_lv1 = $('.l-drawer_directory-lv1');
		var $directory_lv2 = $('.l-drawer_directory-lv2');
		var $directory_lv3 = $('.l-drawer_directory-lv3');
		var $directory_lv2_item = $directory_lv2.find('.l-drawer_directory_item');
		var $directory_lv3_item = $directory_lv3.find('.l-drawer_directory_item');
		var stateClass = {
			active: 'is-active'
		};
		var _easing = 'Power3.easeInOut';
		var _duration = 0.5;

		$toggle.hammer().on(hammerTapEvent, _toggle);

		function _toggle() {
			if ($html.hasClass(viewClass.nav)) {
				_close();
			} else {
				_open();
			}
		}

		function _open() {
			var $currentDirectory = $('.l-drawer_directory_item').has('.l-drawer_list a.is-current');

			$win.on('resize.drawerUI', function () {
				if (window.innerWidth >= 1032) {
					_close();
				}
			});

			$doc.on('keydown.drawerUI', function (e) {
				if (e.keyCode === 27) {
					_close();
				}
			});

			$html.addClass(viewClass.nav);

			TweenMax.to('.l-container, .l-importantNotice', _duration, {
				ease: _easing,
				left: '-275px'
			});

			TweenMax.to('#header.is-fixed', _duration, {
				ease: _easing,
				left: '-275px'
			});

			TweenMax.to('#drawer_container', _duration, {
				ease: _easing,
				x: '-275px'
			});

			// カレントディレクトリの確認
			if ($currentDirectory.length) {
				var _directory = $currentDirectory.data('directory');
				var _parentDirectory = $currentDirectory.data('parentDirectory');

				$('[data-directory="' + _directory + '"]').addClass(stateClass.active);

				TweenMax.to($directory_lv1, 0, {
					x: '-270px'
				});
				$directory_lv2.addClass(stateClass.active);

				// カレントディレクトリが3階層目の場合
				if (_parentDirectory) {
					$('[data-directory="' + _parentDirectory + '"]').addClass(stateClass.active);

					TweenMax.to($directory_lv2, 0, {
						x: '-265px'
					});
					$directory_lv3.addClass(stateClass.active);
				}
			} else {
				TweenMax.to($directory_lv1, _duration, {
					ease: _easing,
					x: '-10px'
				});

				TweenMax.to($directory_lv2, _duration, {
					ease: _easing,
					x: '-5px'
				});
			}

			setTimeout(function () {
				$('#header, .l-container').on('touchmove.drawerUI', function () {
					return false;
				});
				$('#header, .l-container').on('click.drawerUI', _close);
			}, _duration * 1000);
		}

		function _close() {
			$win.off('.drawerUI');

			$html.removeClass(viewClass.nav);
			$('#header, .l-container').off('.drawerUI');

			$('.l-drawer_directory').removeClass(stateClass.active);
			$('.l-drawer_directory .l-drawer_directory_item').removeClass(stateClass.active);

			TweenMax.to('.l-container, .l-importantNotice', _duration, {
				ease: _easing,
				left: '0'
			});

			TweenMax.to('#header.is-fixed', _duration, {
				ease: _easing,
				left: '0'
			});

			TweenMax.to('#drawer_container', _duration, {
				ease: _easing,
				x: '0'
			});

			TweenMax.to('.l-drawer_directory', 0, {
				delay: _duration,
				x: '0px'
			});

			return false;
		}

		$directory_lv1.find('.l-drawer_next').hammer().on(hammerTapEvent, function () {
			$directory_lv2_item.removeClass(stateClass.active);
			$('[data-directory="' + $(this).data('rel') + '"]').addClass(stateClass.active);

			TweenMax.to($directory_lv1, _duration, {
				ease: _easing,
				x: '-270px'
			});
			$directory_lv2.addClass(stateClass.active);
		});

		$directory_lv2.find('.l-drawer_next').hammer().on(hammerTapEvent, function () {
			$directory_lv3_item.removeClass(stateClass.active);
			$('[data-directory="' + $(this).data('rel') + '"]').addClass(stateClass.active);

			TweenMax.to($directory_lv2, _duration, {
				ease: _easing,
				x: '-265px'
			});
			$('.l-drawer_directory-lv3').addClass(stateClass.active);
		});

		$directory_lv1.find('.l-drawer_back').hammer().on(hammerTapEvent, function () {
			_close();
		});

		$directory_lv2.find('.l-drawer_back').hammer().on(hammerTapEvent, function () {
			TweenMax.to($directory_lv1, _duration, {
				ease: _easing,
				x: '-10px',
				onComplete: function onComplete() {
					$directory_lv2_item.removeClass(stateClass.active);
				}
			});
			$directory_lv2.removeClass(stateClass.active);
		});

		$directory_lv3.find('.l-drawer_back').hammer().on(hammerTapEvent, function () {
			TweenMax.to($directory_lv2, _duration, {
				ease: _easing,
				x: '-5px',
				onComplete: function onComplete() {
					$directory_lv3_item.removeClass(stateClass.active);
				}
			});
			$directory_lv3.removeClass(stateClass.active);
		});

		// スワイプ操作
		$directory_lv1.hammer().on('swipe', function (event) {
			if (event.gesture.deltaX > 0) {
				_close();
			}
		});

		$directory_lv2.hammer().on('swipe', function (event) {
			if (event.gesture.deltaX > 0) {
				TweenMax.to($directory_lv1, _duration, {
					ease: _easing,
					x: '-10px',
					onComplete: function onComplete() {
						$directory_lv2_item.removeClass(stateClass.active);
					}
				});
				$directory_lv2.removeClass(stateClass.active);
			}
		});

		$directory_lv3.hammer().on('swipe', function (event) {
			if (event.gesture.deltaX > 0) {
				TweenMax.to($directory_lv2, _duration, {
					ease: _easing,
					x: '-5px',
					onComplete: function onComplete() {
						$directory_lv3_item.removeClass(stateClass.active);
					}
				});
				$directory_lv3.removeClass(stateClass.active);
			}
		});
	};

	var _categoryTopUI = function _categoryTopUI() {
		if (!$('.l-categoryHero').length) {
			return;
		}

		$body.addClass('page-categoryTop');

		if (window.innerWidth < 768 || $('.l-categoryHero-fluid').length) {
			var _ret = function () {
				var _restore = function _restore() {
					$(document).off('.categoryTopAnimation');
					$('.l-container').off('.categoryTopAnimation');
					$html.removeClass(viewClass.categoryTopAnimation);
				};

				var _scroll = function _scroll() {
					$('html, body').stop().animate({ scrollTop: targetOffsetTop }, 1200, 'easeInOutExpo', function () {
						_restore();
						CA.headerUI.hide();
					});
				};

				if ($win.scrollTop() !== 0 || $('.l-categoryHero-noscroll').length) {
					return {
						v: void 0
					};
				}

				$html.addClass(viewClass.categoryTopAnimation);

				var scroll_event = 'onwheel' in document ? 'wheel' : 'onmousewheel' in document ? 'mousewheel' : 'DOMMouseScroll';

				$(document).on(scroll_event + '.categoryTopAnimation', function (e) {
					e.preventDefault();
				});
				$('.l-container').on('touchmove.categoryTopAnimation', function (e) {
					e.preventDefault();
				});

				var targetOffsetTop = $('.l-categoryHero').outerHeight();

				setTimeout(function () {
					if ($html.hasClass(viewClass.search) || $html.hasClass(viewClass.nav)) {
						_restore();
						return;
					}

					_scroll();
				}, 2200);
			}();

			if ((typeof _ret === 'undefined' ? 'undefined' : _typeof(_ret)) === "object") return _ret.v;
		}
	};

	var _carouselUI = function _carouselUI() {
		$('.m-carousel').each(function () {
			var $this = $(this);
			var $carousel = $this.find('.m-carousel_items');
			var $item = $carousel.find('.m-carousel_item');
			var item_length = $item.length;
			var $toggleSwitch = $this.find('.m-carousel_toggleSwitch');
			var $toggleSwitch_svg = $toggleSwitch.find('.m-carousel_toggleSwitch_svg').get(0);
			var carousel_change_speed = 700;
			var carousel_change_interval = 4500;
			var $pager_progress = $this.find('.m-carousel_pager_progress');
			var $pager = $this.find('.m-carousel_pager');
			var $pager_item = $pager.find('.m-carousel_pager_item');
			var currentCarouselIndex = 0;
			var timer = void 0;
			var autoplayIsEnabled = true;
			var carouselIsAnimated = false;

			// スワイプ操作
			$carousel.hammer().on('swipe', function (event) {
				if (event.gesture.deltaX < 0) {
					changeCarousel(currentCarouselIndex + 1);
				}
				if (event.gesture.deltaX > 0) {
					changeCarousel(currentCarouselIndex - 1);
				}
			});

			$pager.find('li').each(function (i) {
				$(this).on('click', function () {
					changeCarousel(i, true);
				});
			});

			$item.each(function (i) {
				var $this = $(this);

				$this.find('a').on('click', function () {
					if (!$this.hasClass('is-current')) {
						if (currentCarouselIndex === 0 && i === item_length - 1) {
							changeCarousel(currentCarouselIndex - 1);
						} else if (currentCarouselIndex === item_length - 1 && i === 0) {
							changeCarousel(currentCarouselIndex + 1);
						} else if (i > currentCarouselIndex) {
							changeCarousel(currentCarouselIndex + 1);
						} else {
							changeCarousel(currentCarouselIndex - 1);
						}
						return false;
					}
				});
			});

			var mark_play = 'M14.510,14.638 C16.428,13.139 16.428,10.687 14.510,9.188 L3.481,0.571 C1.286,-0.709 0.009,0.111 0.009,3.225 L0.009,20.601 C0.009,24.637 1.896,24.482 3.481,23.254 L14.510,14.638 Z';
			var mark_pause = 'M17.000,24.000 C15.343,24.000 14.000,22.657 14.000,21.000 L14.000,3.000 C14.000,1.343 15.343,-0.000 17.000,-0.000 C18.657,-0.000 20.000,1.343 20.000,3.000 L20.000,21.000 C20.000,22.657 18.657,24.000 17.000,24.000 ZM3.000,24.000 C1.343,24.000 0.000,22.657 0.000,21.000 L0.000,3.000 C0.000,1.343 1.343,-0.000 3.000,-0.000 C4.657,-0.000 6.000,1.343 6.000,3.000 L6.000,21.000 C6.000,22.657 4.657,24.000 3.000,24.000 Z';
			var duration = 300;
			var snapToggleSwitch = Snap($toggleSwitch_svg);
			var path = snapToggleSwitch.path(mark_pause).attr({ fill: '#82be28' });

			$toggleSwitch.on('click', function () {
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
			var controlProgress = function () {
				var _increment = function _increment(index) {
					var $target = $pager_item.eq(index).find('.m-carousel_pager_item_progress');
					TweenMax.to($target, carousel_change_interval / 1000, {
						scaleX: 1,
						ease: Linear.easeNone
					});
				};

				var _reset = function _reset(target) {
					var $target = void 0;

					if (target === 'all') {
						$target = $('.m-carousel_pager_item_progress');
					} else {
						$target = $pager_item.eq(target).find('.m-carousel_pager_item_progress');
					}

					TweenMax.to($target, 0.4, {
						scaleX: 0,
						ease: Power4.easeOut
					});
				};

				var _finish = function _finish(index) {
					var $target = $pager_item.eq(index).find('.m-carousel_pager_item_progress');

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

				timer = setInterval(function () {
					var nextCarouselIndex = void 0;

					if (currentCarouselIndex === item_length - 1) {
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
				var transitionTime = 1000;

				if (newCarouselIndex === currentCarouselIndex || carouselIsAnimated) {
					return;
				}

				if (newCarouselIndex >= item_length) {
					newCarouselIndex = 0;
				}

				if (newCarouselIndex < 0) {
					newCarouselIndex = item_length - 1;
				}

				if (currentCarouselIndex === item_length - 1 && newCarouselIndex === 0) {
					controlProgress.finish(currentCarouselIndex);

					var tl = new TimelineMax();

					tl.to($pager_progress, 0.4, {
						scaleX: 1,
						ease: Power4.easeOut
					}).set($pager_progress, {
						'transform-origin': 'right'
					}).to($pager_progress, 1.1, {
						delay: 0.7,
						scaleX: 0,
						ease: Power4.easeOut
					}).set($pager_progress, {
						'transform-origin': 'left'
					});
				} else {
					if (newCarouselIndex > currentCarouselIndex) {
						controlProgress.finish(currentCarouselIndex);
					} else {
						controlProgress.reset(currentCarouselIndex);
					}

					TweenMax.to($pager_progress, 0.4, {
						scaleX: newCarouselIndex / item_length,
						ease: Power4.easeOut
					});
				}

				carouselIsAnimated = true;

				var oldCarouselIndex = currentCarouselIndex;

				$item.eq(oldCarouselIndex).removeClass('is-current');
				$carousel.find('.slick-cloned').removeClass('is-current');
				$item.eq(newCarouselIndex).addClass('is-current');
				$pager_item.eq(oldCarouselIndex).removeClass('is-current');
				$pager_item.eq(newCarouselIndex).addClass('is-current');

				if (currentCarouselIndex === item_length - 1 && newCarouselIndex === 0 && !usePager) {
					_carousel.slick('slickNext');
					$item.eq(oldCarouselIndex).next().addClass('is-current');
				} else if (currentCarouselIndex === 0 && newCarouselIndex === item_length - 1 && !usePager) {
					_carousel.slick('slickPrev');
					$item.eq(oldCarouselIndex).prev().addClass('is-current');
				} else {
					_carousel.slick('slickGoTo', newCarouselIndex);
				}

				stopCarousel();

				// WAI-ARIA
				$item.eq(oldCarouselIndex).attr({ 'aria-hidden': true });
				$item.eq(newCarouselIndex).attr({ 'aria-hidden': false });
				$pager_item.eq(oldCarouselIndex).attr({ 'aria-selected': false });
				$pager_item.eq(newCarouselIndex).attr({ 'aria-selected': true });

				currentCarouselIndex = newCarouselIndex;

				setTimeout(function () {
					carouselIsAnimated = false;

					if (autoplayIsEnabled) {
						playCarousel();
					}
				}, transitionTime);
			};

			var _carousel = $this.find('.m-carousel_items');

			_carousel.on('init', function () {
				$item.eq(currentCarouselIndex).addClass('is-current');

				if (item_length > 1) {
					$pager_item.eq(currentCarouselIndex).addClass('is-current');
					playCarousel();
				} else {
					$this.addClass('is-singleImgMode');
				}

				setTimeout(function () {
					$this.addClass('is-initialized');
				}, 200);
			});

			_carousel.slick({
				mobileFirst: true,
				centerMode: false,
				centerPadding: '0px',
				speed: carousel_change_speed,
				arrows: false,
				swipe: false,
				responsive: [{
					breakpoint: 940,
					settings: {
						centerMode: true,
						slidesToShow: 1,
						variableWidth: true
					}
				}]
			});
		});
	};

	var _touchHover = function _touchHover() {
		$('.js-touchhover').on({
			'touchstart mouseenter': function touchstartMouseenter() {
				$(this).addClass('is-touched');
			},
			'touchend mouseleave': function touchendMouseleave() {
				$(this).removeClass('is-touched');
			}
		});
	};

	var _moduleInteraction = function () {
		var _init = function _init() {
			if ($.ua.isTouchDevice) {
				$('.m-card, .m-btn, .m-iconBadge, .m-iconBadgeText, .m-newsList_item a, .m-linkList_item a, .m-media a, .m-figureLink a, .m-carousel_item a, .m-pager_prev, .m-pager_next, .m-pager_item a, .l-utilityNav_item-pagetop').on({
					'touchstart mouseenter': function touchstartMouseenter() {
						$(this).addClass('is-touched');
					},
					'touchend mouseleave': function touchendMouseleave() {
						$(this).removeClass('is-touched');
					}
				});
			}

			$('.js-inview .m-card').waypoint({
				handler: function handler(direction) {
					$(this.element).addClass('is-inview');
				},
				offset: '90%'
			});

			$('.m-accordionList_item').each(function () {
				var $this = $(this);
				var $header = $this.find('.m-accordionList_header');
				var $body = $this.find('.m-accordionList_body');

				if ($header.attr('aria-expanded') === 'true') {
					_open();
				}

				$header.hammer().on(hammerTapEvent, function () {
					_toggle();
				});

				function _toggle() {
					if ($header.attr('aria-expanded') === 'true') {
						_close();
					} else {
						_open();
					}
				}

				function _open() {
					$header.attr('aria-expanded', true);
					$body.attr('aria-hidden', false);
					$body.slideDown({ duration: 500, easing: 'easeOutQuint' });
				}

				function _close() {
					$header.attr('aria-expanded', false);
					$body.attr('aria-hidden', true);
					$body.slideUp({ duration: 400, easing: 'easeOutQuint' });
				}
			});
		};

		return {
			init: _init
		};
	}();

	var _utilityNavUI = function _utilityNavUI() {
		var $utilityNav = $('#utilityNav');
		var scrollTop = void 0;

		$win.on('scroll', function () {
			scrollTop = $(this).scrollTop();

			if (scrollTop > triggerHideHeaderOffsetTop) {
				$utilityNav.addClass('is-visible');
				$('#swallow-widget-frame').addClass('is-visible');
			} else {
				$utilityNav.removeClass('is-visible');
				$('#swallow-widget-frame').removeClass('is-visible');
			}
		});
	};

	return {
		init: function init() {
			window.console = window.console || {
				log: function log() {}
			};
			_init();
		},
		headerUI: _headerUI
	};
}(jQuery);

CA.init();
```
