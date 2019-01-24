- [TouchSwipe JQuery Plugin](https://github.com/daodc/TouchSwipe-Jquery-Plugin)
- [Pan, Pinch, Press, Rotate, Swipe, Tap: Hammerjs](http://hammerjs.github.io/)

### Swipper viết theo kiểu object

#### HTML:

```javascript
<section id="tmp_wrap_gallery">
    <div class="swiper-container">
        <div class="swiper-wrapper">
            <div class="swiper-slide">
                <div class="cut l-cover">
                    <img class="l-cover__item" src="/cms8341/shared/templates/top/images/gallery/slider_1.jpg" alt="" width="1600" height="485">
                </div>
            </div>
            <div class="swiper-slide">
                <div class="cut l-cover">
                    <img class="l-cover__item" src="/cms8341/shared/templates/top/images/gallery/slider_2.jpg" alt="" width="1600" height="485">
                </div>
            </div>
            <div class="swiper-slide">
                <div class="cut l-cover">
                    <img class="l-cover__item" src="/cms8341/shared/templates/top/images/gallery/slider_3.jpg" alt="" width="1600" height="485">
                </div>
            </div>
            <div class="swiper-slide">
                <div class="cut l-cover">
                    <img class="l-cover__item" src="/cms8341/shared/templates/top/images/gallery/slider_2.jpg" alt="" width="1600" height="485">
                </div>
            </div>
        </div>
    </div>
</section>
```

#### CSS:

```javascript
#tmp_wrap_gallery .swiper-container {
    height: 100%;
    margin-left: auto;
    margin-right: auto;
    overflow: hidden;
    position: relative
}
#tmp_wrap_gallery .swiper-container::before {
  display: block;
  content: '';
  z-index: 2;
  width: 100%;
  height: 100%;
  position: absolute;
  top: 0;
  left: 0;
  transition: opacity 0.8s cubic-bezier(0, 0.28, 0, 1);
  -webkit-transform: scaleY(1);
  transform: scaleY(1);
  -webkit-transform-origin: left bottom;
  transform-origin: left bottom;
  opacity: 1
}
#tmp_wrap_gallery .swiper-wrapper {
    background: #282828;
}

#tmp_wrap_gallery .swiper-slide {
    height: 100vh;
    width: 100vw;
    text-align: center;
    font-size: 18px;
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    -webkit-box-pack: center;
    -ms-flex-pack: center;
    justify-content: center;
    -webkit-box-align: center;
    -ms-flex-align: center;
    align-items: center;
    overflow: hidden
}
.l-cover {
    position: relative;
    width: 100%;
    height: 100%;
    overflow: hidden
}

.l-cover .l-cover__item {
    display: block;
    position: absolute;
    top: 50%;
    left: 50%;
    -webkit-transform: translate(-50%, -50%);
    transform: translate(-50%, -50%);
    min-width: 100.5%;
    min-height: 100.5%;
    max-width: inherit;
    width: auto;
    height: auto;
    -o-object-fit: cover;
    object-fit: cover
}
#tmp_wrap_gallery .swiper-slide .cut {
    position: absolute;
    left: 0;
    top: 0
}

#tmp_wrap_gallery .swiper-wrapper,
#tmp_wrap_gallery .swiper-slide,
#tmp_wrap_gallery .swiper-slide .cut {
    -webkit-transition-timing-function: cubic-bezier(0.88, -0.02, 0, 1);
    transition-timing-function: cubic-bezier(0.79, 0.03, 0, 1)
}

#tmp_wrap_gallery .swiper-slide-active img {
    -webkit-animation-name: slideWipe;
    animation-name: slideWipe;
    -webkit-animation-duration: 5.4s;
    animation-duration: 5.4s;
    -webkit-animation-timing-function: cubic-bezier(0, 0, 0.51, 0.99);
    animation-timing-function: cubic-bezier(0, 0, 0.51, 0.99);
    -webkit-transform-origin: 0 -25%;
    transform-origin: 0 -25%
}

@-webkit-keyframes slideWipe {
    from {
        -webkit-transform: scale(1.07, 1.07) translate3d(-50%, -50%, 0);
        transform: scale(1.07, 1.07) translate3d(-50%, -50%, 0)
    }
    to {
        -webkit-transform: scale(1, 1) translate3d(-50%, -50%, 100px);
        transform: scale(1, 1) translate3d(-50%, -50%, 100px)
    }
}

@keyframes slideWipe {
    from {
        -webkit-transform: scale(1.07, 1.07) translate3d(-50%, -50%, 0);
        transform: scale(1.07, 1.07) translate3d(-50%, -50%, 0)
    }
    to {
        -webkit-transform: scale(1, 1) translate3d(-50%, -50%, 100px);
        transform: scale(1, 1) translate3d(-50%, -50%, 100px)
    }
}
```

#### JS:

```javascript
var View = {
    ScrollMagicController: null,
    needRefreshScrollMagicScene: [],
    swiperAry: [],
    isHomeVisualInView: true,
    runHomeIntro: function() {
        var owner = this;
        $('body').addClass('is-intro-end');
        for (var i in owner.swiperAry) {
            var swiper = owner.swiperAry[i];
            var activeSlide = swiper.slides[swiper.activeIndex];
            TweenMax.fromTo(activeSlide, 3.5, { css: { scale: 1.05 } }, { css: { scale: 1 }, ease: Linear.ease, delay: 0 });
            if (owner.isHomeVisualInView) { 
                swiper.startAutoplay(); 
            }
        }
    },
    initHomeVisual: function(_target_class) {
        var owner = this;
        var w = window;
        var swiper;
        var swiperChangeCount = 0;
        var interleaveOffset = -.5;
        var interleaveEffect = {
            onProgress: function(swiper, progress) {
                for (var i = 0; i < swiper.slides.length; i++) {
                    var slide = swiper.slides[i];
                    var translate, innerTranslate, scale = 1;
                    progress = slide.progress;
                    if (progress > 0) {
                        translate = progress * swiper.width;
                        innerTranslate = translate * interleaveOffset;
                        innerTranslate *= .5;
                        innerTranslate = 0;
                        scale = 1;
                    } else {
                        innerTranslate = Math.abs(progress * swiper.width) * interleaveOffset;
                        translate = 0;
                    }
                    $(slide).css({ transform: 'translate3d(' + translate + 'px,0,0) scale3d(' + scale + ',' + scale + ',1)' });
                    $(slide).find('.cut').css({ transform: 'translate3d(' + innerTranslate + 'px,0,0) scale3d(' + scale + ',' + scale + ',1)' });
                }
            },
            onTouchStart: function(swiper) { 
                for (var i = 0; i < swiper.slides.length; i++) { 
                    $(swiper.slides[i]).css({ transitionDuration: '' }); 
                } 
            },
            onSetTransition: function(swiper, speed) { 
                for (var i = 0; i < swiper.slides.length; i++) { 
                    $(swiper.slides[i]).find('.cut').addBack().css({ transitionDuration: speed + 'ms' });
                } 
            }
        };
        var swiperOptions = {
            initialSlide: Math.floor(Math.random() * 4),
            pagination: '.swiper-pagination',
            paginationClickable: true,
            speed: 1200,
            autoplay: 4000,
            autoplayDisableOnInteraction: false,
            freeMode: false,
            resistanceRatio: 0.95,
            preloadImages: true,
            loop: true,
            slidesPerView: 1,
            watchSlidesProgress: true,
            nextButton: '',
            prevButton: '',
            onInit: function(swiper) {
                owner.swiperAry.push(swiper);
                swiper.onResize();
                //swiper.stopAutoplay();
            },
            onImagesReady: function(swiper) {
                swiper.onResize();
                TweenMax.killTweensOf(_target_class);
                TweenMax.to(_target_class, 0.6, {
                    css: { opacity: 1 },
                    ease: Linear.ease,
                    delay: 0,
                    onStart: function() {
                        swiper.update();
                        swiper.onResize();
                    },
                    onComplete: function() {
                        swiper.update();
                        swiper.onResize();
                    }
                });
            },
            onDestroy: function(swiper) { 
                $(_target_class).addClass('is-destroy');
            }
        };
        swiperOptions = $.extend(swiperOptions, interleaveEffect);
        swiper = new Swiper(_target_class, swiperOptions);
        owner.swiperAry.push(swiper);
        var sceneSwiper = new ScrollMagic.Scene({ 
            triggerElement: _target_class, 
            triggerHook: 'onLeave', 
            offset: $(w).height() 
        }).addTo(owner.ScrollMagicController);
        sceneSwiper.on('enter', function(e) {
            swiper.stopAutoplay();
            owner.isHomeVisualInView = false;
        });
        sceneSwiper.on('leave', function(e) {
            swiper.startAutoplay();
            owner.isHomeVisualInView = true;
        });
        sceneSwiper.on('shift', function(e) { 
            sceneSwiper.offset($(w).height()); 
        });
    },
    setHomeIntro: function() {
        var owner = this;
        owner.initHomeVisual('.swiper-container');
    },
    init: function() {
        runHomeIntro();
        initHomeVisual();
        setHomeIntro();
    }
};
View.runHomeIntro();
View.initHomeVisual();
View.setHomeIntro();
```
