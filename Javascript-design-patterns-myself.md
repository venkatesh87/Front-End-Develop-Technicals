#### I. Javascript Design Patterns myself
---

>**Design Paterns Plugin**

```javascript
var name = document.querySelectorAll('#name');
var Gallery = {
  selector: {
    list: '.list',
    item: '.item'
  },
  init: function() {
    Gallery.show();
  },
  show: function() {
    
  }
}
$(document).ready(function() {
  Gallery.init();
});
```

```
var BackToTop = {
    selector : $('#btn_to_top'),
    appear : $(window).height() * 0.3,
    anchor : $('#tmp_footer_cnt').offset().top - $(window).height(),
    update : function(){
        BackToTop.appear = $(window).height() * 0.3;
        BackToTop.anchor = $('#tmp_footer_cnt').offset().top - $(window).height();
    },
    scroll : {
        to_top: function(){
            $('html, body').animate({scrollTop: 0}, 1000)
        },
        update_position: function(current_position){
            if (current_position <= BackToTop.appear){
                BackToTop.selector.removeClass('appear');
            }else{
                BackToTop.selector.addClass('appear');
            }
            if (current_position < BackToTop.anchor){
                BackToTop.selector.addClass('anchor');
            }else{
                BackToTop.selector.removeClass('anchor');
            }
        }
    }
}
$(document).ready(function() {
  BackToTop.update();
  BackToTop.update();
  BackToTop.scroll.update_position(window.scrollY);
  BackToTop.selector.on('click',function(e){
      e.preventDefault();
      BackToTop.scroll.to_top();
  });
});

```

>**Object**
```javascript
//Scroll Top
var scrollTop = function() {
    //scrollTop
    $(window).scroll(function() {
        var footerProducedHeght = $('#temp_footer').height();
        var footerHeght = footerProducedHeght - 33;
        if (window.innerWidth > $('#temp_wrapper').width()) {
            var posTopFooter = $('#temp_footer').offset().top;
            var scrollBottom = $(window).scrollTop() + $(window).height();
            var backTopHeight = $('.ptop').height();
            var headerProducedHeght = $('#temp_header').height();
            var height_document = $(document).height() - footerHeght;
            var sbHeight = window.innerHeight * (window.innerHeight / document.body.offsetHeight);
            var ofBottom = (document.body.offsetHeight - $(window).scrollTop() - window.innerHeight) + 60;

            if (footerProducedHeght >= ofBottom + 50) {
                $('.ptop').css({ 'bottom': footerHeght, 'position': 'absolute' });
            } else {
                $('.ptop').css({ 'bottom': 0, 'position': 'fixed' });
            }
            if ($(this).scrollTop() > $('#temp_header').outerHeight()) {
                $('.ptop').fadeIn(350);
            } else {
                $('.ptop').fadeOut(350);
            }
        } else {
            $('.ptop').css({ 'bottom': footerHeght, 'position': 'absolute' });
        }
    });

    $(".ptop a").click(function() {
        $('html, body').animate({ scrollTop: 0 }, 'slow');
        return false;
    });
};
```

>**Array**
```javascript

```

>**Function**
```javascript

```

>**Condition**
```javascript

```

