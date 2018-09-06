# I. Memorize the company Project Outsite

**1. 20180328_I_DESIGN**
- Switch screen with smartphone.

>JavaScript Code:
```javascript
function myResizeFunction() {
  if($(window).width() <= 1100){
    // do something
  }
}
$(myResizeFunction); // Do on DOM ready
$(window).on("load resize", myResizeFunction); 
```

```javascript
$(window).resize(function() {
  calcHeight();
}).load(function() {
  calcHeight();
});
```

>JavaScript Code hiệu quả: Cái này có 1 cái hại là mỗi khi resize nó thực thi lại hành động
```javascript
// Bind to the resize event of the window object
$(window).on("resize", function () {
  // Set .right's width to the window width minus 480 pixels
  $(".content .right").width( $(this).width() - 480 );
// Invoke the resize event immediately
}).resize();
```

>JavaScript Code hiệu quả: 
```javascript
$('.nav-icons').click(function(e) {
  if($(window).width()<=1000){
    $(this).toggleClass('open');
  }
});
```

>JavaScript Code EventListener sẽ không hiểu:
```javascript
if($(window).width()<=1000){
  $('.nav-icons').click(function(e) {
    $(this).toggleClass('open');
  });
}
```

**ForEach**: item sẽ hiểu từng thẻ ```<li>```.
>JavaScript Code:
```javascript
var Navigation = {
  selector: {
    nav_item: document.querySelectorAll('.navigation ul li')  
  },
  init: function(){
    Navigation.nav_reset();
  },
  nav_reset: function(){
    if ($(window).width() > 1000) {
      Navigation.selector.nav_item.forEach(function(item) {
        item.style.WebkitOpacity = "1";
        item.style.msOpacity = "1";
        item.style.opacity = "1";
        item.style.WebkitTransform = "translate3d(0, 0, 0)";
        item.style.msTransform = "translate3d(0, 0, 0)";
        item.style.transform = "translate3d(0, 0, 0)";
      });
    } else if ($(window).width() <= 1000) {
      Navigation.selector.nav_item.forEach(function(userItem) {
        item.style.WebkitOpacity = "0";
        item.style.msOpacity = "0";
        item.style.opacity = "0";
        item.style.WebkitTransform = "translate3d(0, 40px, 0)";
        item.style.msTransform = "translate3d(0, 40px, 0)";
        item.style.transform = "translate3d(0, 40px, 0)";
      });
    }
  }
}
```

**TweenMax:** Thuộc tính ```autoAlpha: 0``` tương đương với ```opacity: 0```.

**2. **
- Text.
$(document).ready(function() {
    App.init();
    var currentSlide = 0;
    var slideItem = $('.slideItem');
    var countSlide = $('.slidersList .slideItem').length;
    var hgtWin = $(window).height();

    var Animation = {
        selector: {
            openning: '.openning',
            logo: '.logo',
            heading: '.slideTitle',
            balloons: '.balloonsImage',
            balloonsInner: '.imageRepresentInner',
            ellipseOne: '.ellipseOne',
            ellipseTwo: '.ellipseTwo',
            balloonsDetail: '.balloonsDetail',
            balloonTitle: '.balloonTitle',
            dateTime: '.dateTime',
            balloonsCaption: '.balloonsCaption',

        },
        handle: {
            logoTw: new TimelineMax(),
            mainTw: new TimelineMax()

        },
        init: function() {
            setTimeout(function(){
                Animation.show_logo();
            }, 150)
            Animation.animateTitle();
            Animation.change_slide();
        },
        show_logo: function(){
          Animation.handle.logoTw.fromTo(
                $(Animation.selector.logo), 0.5, 
                {css:{y: -160,opacity: 0,ease: Circ.easeOut}},
                {css:{y: 0,opacity: 1,ease: Circ.easeOut}}
            );  
        },
        animateTitle: function(){
            var titleChars = new SplitText($(Animation.selector.balloonTitle), { type: 'lines, words, chars' });
            var titleCharsTLM = new TimelineMax({ paused: !0 });
            titleCharsTLM.staggerFrom(titleChars.chars, 1, {y: 100+'%', opacity: 0, ease: Circ.easeOut }, .05, 0);
            titleCharsTLM.duration(1.4).restart(); 
        },
        slide: function() {
            var addtition_time = "-=0";
            var typeItem = '.slideItem' + currentSlide + ' ';
            if (currentSlide != 1) addtition_time = "-=0.5";
            Animation.handle.mainTw.to($(typeItem + Animation.selector.heading), 1, {x: '0%', opacity: 1, yoyo: true, ease: Circ.easeOut},addtition_time)
            if (currentSlide != countSlide){
                Animation.handle.mainTw.fromTo($(typeItem + Animation.selector.balloonsInner), 11, {y: hgtWin, opacity: 1, yoyo: true}, {y: -hgtWin-100, scale: 1.494, opacity: 1, yoyo: true, ease: SlowMo.ease.config(0.7, 0.7, false)},addtition_time)
            }else{
                Animation.handle.mainTw.fromTo($(typeItem + Animation.selector.balloonsInner), 11, {y: hgtWin, opacity: 1, yoyo: true}, {y: 0, scale: 1.494, opacity: 1, yoyo: true, ease: SlowMo.ease.config(0.7, 0.7, false)},addtition_time)
            }
            Animation.handle.mainTw.to($(typeItem + Animation.selector.ellipseOne), 6, {y: -hgtWin, opacity: 1, yoyo: true, ease: Power2.easeOut}, "-=12")
                                   .to($(typeItem + Animation.selector.ellipseTwo), 6, {y: -hgtWin, opacity: 0.5, yoyo: true, ease: Power2.easeOut}, "-=12")
                                   .to($(typeItem + Animation.selector.dateTime), 4, { y: 0, opacity: 1, yoyo: true, ease: Circ.easeOut}, "-=12")
                                   .to($(typeItem + Animation.selector.balloonsCaption), 4, {y: 0, opacity: 1, yoyo: true, ease: Circ.easeOut}, "-=12")
                                   .to($(typeItem + Animation.selector.balloonsDetail),12, {y: '5%', opacity: 1, yoyo: true, ease: Circ.easeOut}, "-=11.5")
            if (currentSlide != countSlide){
                Animation.handle.mainTw.to($(typeItem + Animation.selector.balloonsDetail),12, {y: '-114%', opacity: 1, yoyo: true, ease: SlowMo.ease.config(0.7, 0.7, false),
                                        onComplete: function(){
                                            $(typeItem).removeClass('active');
                                        }
                                    }, "-=11.5")
                                   .to($(Animation.selector.heading), 0, {x: '-100%',opacity: 0, yoyo: true, ease: Circ.easeOut,onComplete: function(){
                                        setTimeout(Animation.change_slide, 0);
                                    }}, "-=1");
                                   Animation.animateTitle();
            }
        },
        change_slide: function() {
            var addtition_time = "-=0";
            if (currentSlide == countSlide) currentSlide = 0;
            if (currentSlide != 0) addtition_time = "-=2.0";
            var typeItem = '.slideItem' + (currentSlide + 1) + ' ';
            var position_balloon = (Math.round((Math.random() * 2) + 1) == 1) ? 'balloon_1' : 'balloon_2',
                position_eclip = (Math.round((Math.random() * 2) + 1) == 1) ? 'eclip_1' : 'eclip_2';
            $(typeItem).removeClass('balloon_1 balloon_2 eclip_1 eclip_2');
            $(typeItem).addClass(position_balloon + ' ' + position_eclip);
            Animation.handle.mainTw.to($(typeItem + Animation.selector.balloonsInner), 0, {y: hgtWin, opacity: 0, yoyo: true, scale: 1, ease: Power2.easeOut},addtition_time)
                                   .to($(typeItem + Animation.selector.ellipseOne), 0, {y: hgtWin,scale: 1, opacity: 0, yoyo: true, ease: Power2.easeOut},addtition_time)
                                   .to($(typeItem + Animation.selector.ellipseTwo), 0, {y: hgtWin, opacity: 0, yoyo: true, ease: Power2.easeOut},addtition_time)
                                   .to($(typeItem + Animation.selector.balloonsDetail), 0, {y: '114%', yoyo: true, ease: Circ.easeOut},addtition_time)
                                   .to($(typeItem + Animation.selector.dateTime), 0, {y: 70, opacity: 0, yoyo: true, ease: Circ.easeOut},addtition_time)
                                   .to($(typeItem + Animation.selector.balloonsCaption), 0, {y: 70, opacity: 0, yoyo: true, ease: Circ.easeOut,
                                        onComplete: function() {
                                            //Animation.slide();
                                            setTimeout(Animation.slide, 0)
                                        }
                                   },addtition_time);
            /*slideItem.removeClass('active');*/
            slideItem.eq(currentSlide).addClass('active');
            currentSlide++;
        }
    }
    
    Animation.init();
});
>JavaScript Code:
```javascript

```

**3. **
- Text.

>JavaScript Code:
```javascript

```

**4. **
- Text.

>JavaScript Code:
```javascript

```

**5. **
- Text.

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
