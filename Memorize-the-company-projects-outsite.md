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

**2. ForEach**: item sẽ hiểu từng thẻ ```<li>```.
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

**3. TweenMax:** Thuộc tính ```autoAlpha: 0``` tương đương với ```opacity: 0```.

- Text.
```javascript
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
```

>JavaScript Code:
```javascript

```

**4. Hệ Thống Cảnh Báo Thiên Tai**
- https://www.windy.com/?2018-11-07-09,17.811,109.863,5

>JavaScript Code:
```javascript
$(document).ready(function() {
  //Handle no javascript
  $('body').removeClass('no_javascript');
  // Handle Suggest Search
  var data = [
    "Albania",
    "Andorra",
    "Armenia",
    "Austria",
    "Azerbaijan",
    "Belarus",
    "Belgium",
    "Bosnia & Herzegovina",
    "Bulgaria",
    "Croatia",
    "Cyprus",
    "Czech Republic",
    "Denmark",
    "Estonia",
    "Finland",
    "France",
    "Georgia",
    "Germany",
    "Greece",
    "Hungary",
    "Iceland",
    "Ireland",
    "Italy",
    "Kosovo",
    "Latvia",
    "Liechtenstein",
    "Lithuania",
    "Luxembourg",
    "Macedonia",
    "Malta",
    "Moldova",
    "Monaco",
    "Montenegro",
    "Netherlands",
    "Norway",
    "Poland",
    "Portugal",
    "Romania",
    "Russia",
    "San Marino",
    "Serbia",
    "Slovakia",
    "Slovenia",
    "Spain",
    "Sweden",
    "Switzerland",
    "Turkey",
    "Ukraine",
    "United Kingdom",
    "Vatican City"
  ];

  //create AutoComplete UI component
  $("#search-top").kendoAutoComplete({
      dataSource: data,
      filter: "startswith",
      separator: ", "
  }).keypress(function(e) {
    if (event.keyCode === 13) {
      $('.page-content').addClass('loading');
      function doneLoading(){
        $('.page-content').removeClass('loading');
      }
      setTimeout(function() {
        doneLoading();
      }, 2500);
      return false;
      //$(this).closest('form').trigger('submit');
    }
  });
  // Handle Tooltip
  function handleToolTip() {
    $('.control-right .tooltip').tooltipster({
      side: 'left',
      animation: 'fade',
      //trigger: 'click',
      theme: 'tooltipster-borderless'
    });
    $('.control-left .tooltip').tooltipster({
      side: 'right',
      animation: 'fade',
      //trigger: 'click',
      theme: 'tooltipster-borderless'
    });
  };
  // handleFullscreen
  var handleFullscreen = function(){
    var wrapper = $('#wrapper');
    var header = $('.header');
    var footer = $('.footer');
    var main_content = $('.page-container');
    var resetDefault = $(window).height() - ($('.header').height() + $('.footer').outerHeight()) + 'px';
    var is_check = true;
    
    $('.fullscreen-event').on('click', function(e){
      e.preventDefault();
      if($(this).hasClass('fullscreen')){
        $('.tool-map .tool-map-item a').removeClass('fullscreen');
        header.fadeOut(100);
        footer.fadeOut(100);
        wrapper.css({'margin-bottom':'0','padding-bottom':'0'});
        main_content.css({'height':'100%'});
        $('.page-content #map').css('height', $(window).height());
      } else {
        $(this).addClass('fullscreen');
        header.fadeIn(300);
        footer.fadeIn(300);
        wrapper.css({'margin-bottom':'-60px','padding-bottom':'60px'});
        main_content.css({'height':'100%'});
        $('.page-content #map').css('height', resetDefault);
      }
    });
  }
  // handleSearchSP
  var handleSearchSP = function(){
    if ($(window).width() < 870) {
      $('.js-search-sp').off('click')
      $('.js-search-sp').on('click', function(e){
        e.preventDefault();
        if($('.form-search-top').is(':visible')){
          $('.form-search-top').fadeOut(250);
        }
        else{
          $('.form-search-top').slideDown(200);
        }
      });
    }
  }

  // Handle sidebar menu
  var handleSidebarMenu = function() {
    jQuery('.js-page-sidebar').on('click', 'li > a', function(e) {
      if ($(this).next().hasClass('sub-menu') == false) {
        if ($('.btn-navbar').hasClass('collapsed') == false) {
          $('.btn-navbar').click();
        }
        return;
      }

      if ($(this).next().hasClass('sub-menu always-open')) {
        return;
      }
      var iscurrent = $(this).parent().hasClass('active');
      var parent = $(this).parent().parent();
      var the = $(this);
      var menu = $('.js-page-sidebar-menu');
      var sub = $(this).next();

      var slideSpeed = menu.data("slide-speed") ? parseInt(menu.data("slide-speed")) : 200;

      parent.children('li.is-open').children('a').children('.arrow').removeClass('is-open');
      parent.children('li.is-open').children('.sub-menu:not(.always-open)').slideUp(200);
      parent.children('li.is-open').removeClass('is-open');

      var slideOffeset = -200;

      if (sub.is(":visible")) {
        $('.arrow', $(this)).removeClass("is-open");
        $(this).parent().removeClass("is-open");
        sub.slideUp(slideSpeed);
      } else {
        $('.arrow', $(this)).addClass("is-open");
        $(this).parent().addClass("is-open");
        sub.slideDown(slideSpeed);
      }

      e.preventDefault();
    });
  };

  // Handle Scrollbar
  function handleScrollbar() {
    $(".tbody-scroll").mCustomScrollbar({
      theme: "minimal-dark",
      advanced: {
        updateOnBrowserResize: true,
        updateOnContentResize: true
      }
    });
    $(".road-panel .road-body").mCustomScrollbar({
      theme: "minimal-dark",
      advanced: {
        updateOnBrowserResize: true,
        updateOnContentResize: true
      }
    });
    $(".js-storm-scroll").mCustomScrollbar({
      theme: "minimal-dark",
      advanced: {
        updateOnBrowserResize: true,
        updateOnContentResize: true
      }
    });
    $(".sub-menu-scroll").mCustomScrollbar({
      theme: "minimal-dark",
      advanced: {
        updateOnBrowserResize: true,
        updateOnContentResize: true
      }
    });
  };

  // Handle OnResize
  var handleOnResizeScrollbar = function() {
    $(window).resize(function() {
      handleScrollbar();
    }).load(function() {
      handleScrollbar();
    });
  };

  // Handle Height Element
  var handleHeightElement = function() {
    var hgtWindow = $(window).height();
    var hgtHeader = $('.header').height();
    var hgtFooter = $('.footer').outerHeight();
    var distanceTop = hgtHeader + hgtFooter;
    var rest = hgtWindow - distanceTop + 'px';
    $('.page-sidebar').css('height', rest);
    $('#scroll-content').css('height', rest);
    $('.page-content .iframe-map').css('height', rest);
    $('.page-content #map').css('height', rest);
  };

  // only top
  var handleOnlyTop = function() {
    var topFlg = $('body').hasClass('format-top');
    if (topFlg) {
      $(window).resize(function() {
        handleHeightElement();
      }).load(function() {
        handleHeightElement();
      });
    }
  };

  function handleImageFile(input) {
    if (input.files && input.files[0]) {
      var reader = new FileReader();
      reader.onload = function(e) {
        $('#avatar-logo').attr('src', e.target.result);
        $('#avatar-logo').hide();
        $('#avatar-logo').fadeIn(550);
      }
      reader.readAsDataURL(input.files[0]);
    }
  }

  // Handle RangeSlider
  function handleRangeSlider() {
    if($('.js-range-slider').length){
      var min = +moment().format("X");
      var max = +moment().add(7, 'days').format("X");
      var from = +moment().subtract(1, "hours").format("X");
      var step = 4500;
      var $range2 = $('.js-range-slider');
      var instance2;
      $range2.ionRangeSlider({
        type: "single",
        min: min,
        max: max,
        from: from, 
        step: step,
        grid: true,
        force_edges: true,
        prettify: function (num) {
            var m = moment(num, "X").locale("vi");
            return m.format("Do ddd, HH:mm");
        },
        onStart: function (data) {
          console.log("onStart");
        },
        onChange: function (data) {
          console.log("onChange");
        },
        onFinish: function (data) {
          console.log("onFinish");
        },
        onUpdate: function (data) {
          console.log("onUpdate");
        }
      });
      instance2 = $range2.data("ionRangeSlider");
      function update(data) {
        instance2.update(data);
      }
      var updateRange = function(direction) {
        from += step * direction;
        if (from < min) {
            from = min;
        } else if (from > max) {
            from = max;
        }
        update({
            from: from
        });
      };
      var playTimer;
      function play() {
        playTimer = setTimeout(function(){
          if ( from == max ) {
            pause();
          } else {
            updateRange(1);
            play();
          }
        }, 250 ); // Timer
      }

      function pause() {
        clearTimeout(playTimer);
      }

      $('.time-ctrl').on('click', function(e){
        if(!$(this).hasClass('pause')){
          $(this).addClass('pause');
          play();
        }
        else{
          $(this).removeClass('pause');
          pause();
        }
        e.preventDefault();
      });
    }
  }
  // Function callback
  handleToolTip();
  handleFullscreen();
  handleSearchSP();
  handleSidebarMenu();
  handleScrollbar();
  handleOnResizeScrollbar();
  handleOnlyTop();
  handleRangeSlider();
  
  // Change image input file
  $("#logo-name").change(function() {
    handleImageFile(this);
  });
  // Event Click
  // action left
  $('.control-left .action-system .action-item').each(function(){
    $(this).find('a').on('click', function(e){
      e.preventDefault();
      var attrHref = $(this).attr('href');

      if(!$(this).hasClass('active')){
        $('.control-left .action-system .action-item a').removeClass('active');
        $(this).addClass('active');
        $('.portlet-pos-left').addClass('portlet-expend-left');
        $(attrHref).removeClass('portlet-expend-left');
      }
      else{
        $(this).removeClass('active');
        $('.portlet-pos-left').addClass('portlet-expend-left');
        $(attrHref).addClass('portlet-expend-left');
      }
    });
  });
  // action right
  $('.control-right .action-system .action-item').each(function(){
    $(this).find('a').on('click', function(e){
      e.preventDefault();
      var attrHref = $(this).attr('href');

      if(!$(this).hasClass('active')){
        $('.control-right .action-system .action-item a').removeClass('active');
        $(this).addClass('active');
        $('.portlet-pos-right').addClass('portlet-expend-right');
        $(attrHref).removeClass('portlet-expend-right');
      }
      else{
        $(this).removeClass('active');
        $('.portlet-pos-right').addClass('portlet-expend-right');
        $(attrHref).addClass('portlet-expend-right');
      }
    });
  });
  // close portlet
  $('.portlet-close-left').on('click', function(e){
    e.preventDefault();
    $('.control-left .action-system .action-item a').removeClass('active');
    $(this).parents().find('.portlet-box').addClass('portlet-expend-left');
  });
  $('.portlet-close-right').on('click', function(e){
    e.preventDefault();
    $('.control-right .action-system .action-item a').removeClass('active');
    $(this).parents().find('.portlet-box').addClass('portlet-expend-right');
  });
  // close alert
  $('.panel-alert-close').on('click', function(e){
    e.preventDefault();
    $('.panel-alert').fadeOut(500);
  });
  // Action loading popup login, registry
  $('#form-login').submit(function(e){
      $('.modal-login .login-inner').addClass('loading');
      function popLoading(){
        $('.modal-login .login-inner').removeClass('loading');
      }
      setTimeout(function() {
        popLoading();
      }, 2500);
      //$('#form-login').submit();
      e.preventDefault();
  });
  $('#form-registry').submit(function(e){
      $('.modal-login .login-inner').addClass('loading');
      function popLoading(){
        $('.modal-login .login-inner').removeClass('loading');
      }
      setTimeout(function() {
        popLoading();
      }, 2500);
      //$('#form-registry').submit();
      e.preventDefault();
  });
  // Function resize mobile
  var timer = false;
  $(window).resize(function(){
      if (timer !== false) {
          clearTimeout(timer);
      }
      timer = setTimeout(function() {
          handleSearchSP();
      }, 200);
  });

});

```
**Xử lý loading**
```javascript
// Action loading popup login, registry
$('#form-login').submit(function(e){
    $('.modal-login .login-inner').addClass('loading');
    function popLoading(){
      $('.modal-login .login-inner').removeClass('loading');
    }
    setTimeout(function() {
      popLoading();
    }, 2500);
    //$('#form-login').submit();
    e.preventDefault();
});
```

```javascript
//create AutoComplete UI component
$("#search-top").kendoAutoComplete({
    dataSource: data,
    filter: "startswith",
    separator: ", "
}).keypress(function(e) {
  if (event.keyCode === 13) {
    $('.page-content').addClass('loading');
    function doneLoading(){
      $('.page-content').removeClass('loading');
    }
    setTimeout(function() {
      doneLoading();
    }, 2500);
    return false;
    //$(this).closest('form').trigger('submit');
  }
});
```
**Xử lý ionRangeSlider play/pause**

**5. 20181114 Bukken Web**

**5.1 Chỉ click trong vùng dropdown, ngoài vùng dropdown thì ẩn**
- ```$(e.target)```: Có nghĩa là tại cái vị trí con trỏ chuột ```click```.
- ```closest()```: Phương thức trả về tổ tiên đầu tiên của phần tử được chọn.
- ```$("span").closest("ul").css({"color": "red", "border": "2px solid red"})```: Trả về phần tử ```ul```.

>JavaScript Code:
```javascript
$('#headerCorporateLogo').on("click", function() {
  $('.userMenu').slideToggle();
  var $this = $(this);
  if ($this.hasClass('active')){
    $('#headerCorporateLogo').parents('.header-aside').find('div.userMenu').slideUp();
    $('#headerCorporateLogo').removeClass('active');
  }
  else{
    $('#headerCorporateLogo').parents('.header-aside').find('div.userMenu').slideDown();
    $('#headerCorporateLogo').removeClass('active');
    $('div.userMenu').slideDown();
    $this.addClass('active');
  }
});
$(document).on('click', function(e) {
  //2. Xác định vị trí nhấp
  console.log($(e.target).closest('#headerCorporateLogo').length );
  console.log($(e.target).closest('.userMenu').length);
  console.log(!$(e.target).closest('#headerCorporateLogo').length && !$(e.target).closest('.userMenu').length);

  if(!$(e.target).closest('#headerCorporateLogo').length && !$(e.target).closest('.userMenu').length){
      $('.userMenu').fadeOut();
  }
});
```

**5.2 Move Element**

>JavaScript Code:
```javascript
// move status
function moveStatus(){
	$('.result-list .result-item').each(function(){
		var status_list = $(this).find('.company-information .company-above .status-list');
		var status_list_pos = $(this).find('.company-name .status-list');
		var company_name = $(this).find('.company-name');
		var company_above = $(this).find('.company-information .company-above');
		if($(window).width() < 390){
	  	company_name.append(status_list);
		}
		else{
	  	company_above.append(status_list_pos);
		}
	});
}
moveStatus();
// move search result
function moveSearch(){
	var search_result = $('.search-result');
	var result_wrap = $('.result-wrap');
	var search_sort = $('.panel-result .search-sort');
	if($(window).width() < 390){
  	result_wrap.append(search_result);
	}
	else{
		search_sort.prepend(search_result);
	}
}
moveSearch();
// Function resize mobile
var timer = false;
$(window).resize(function(){
    if (timer !== false) {
        clearTimeout(timer);
    }
    timer = setTimeout(function() {
			moveStatus();
			moveSearch();
    }, 200);
});
```
**6. 20190114_DingTea**

**Multiple modal bootstrap.**
>JavaScript Code:
```javascript
//Trigger next modal
  $('.link-login-modal').on( 'click', function() {
    $('.modal-login').modal('show');
    $('.modal-registries').modal('hide');
    $('.modal-forgot-password').modal('hide');
  });
  $('.link-registration').on( 'click', function() {
    $('.modal-login').modal('hide');
    $('.modal-registries').modal('show');
    $('.modal-forgot-password').modal('hide');
  });
  $('.forgot-password-link').on( 'click', function() {
    $('.modal-login').modal('hide');
    $('.modal-registries').modal('hide');
    $('.modal-forgot-password').modal('show');
  });
```

**data-backdrop="static"**
>JavaScript Code:
```javascript
<div class="modal fade modal-general modal-form modal-forgot-password" data-backdrop="static" id="forgot-modal" tabindex="-1" role="dialog"  aria-hidden="true">
```

**Event block out scroll body when open modal**
>JavaScript Code:
```javascript

```

**Add smooth scrolling to page anchors**
>JavaScript Code:
```javascript
// Add smooth scrolling to all links
$(".click-scroll").on('click', function(event) {

  // Make sure this.hash has a value before overriding default behavior
  if (this.hash !== "") {
    // Prevent default anchor click behavior
    event.preventDefault();

    // Store hash
    var hash = this.hash;

    // Using jQuery's animate() method to add smooth page scroll
    // The optional number (800) specifies the number of milliseconds it takes to scroll to the specified area
    $('html, body').animate({
      scrollTop: $(hash).offset().top
    }, 800, function(){
 
      // Add hash (#) to URL when done scrolling (default click behavior)
      window.location.hash = hash;
    });
  } // End if
});
```

**7. Dingtea**
**hasClass**: Một chú ý khi dùng ```hasClass``` nếu điều kiện đúng nó sẽ chạy điều kiện trong lệnh ```if``` nếu điều kiện sai nó sẽ chạy điều kiện trong lệnh ```else```

>**Case 1**

- ![hasClass](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/hasClass-2.jpg)

>JavaScript HTML:
```javascript
<h1>True</h1>
<p class="intro">This is a paragraph.</p>
<p>This is another paragraph.</p>
<button>Does any p element have an "intro" class?</button>
```

>JavaScript JS:
```javascript
$("button").click(function() {
  alert($("p").hasClass("intro"));
  if ($("p").hasClass("intro")) {
    $('p').css('background', '#f00');
  } else {
    $('p').css('background', '#ff0');
  }
});
```

>**Case 2**

- ![hasClass](https://github.com/daodc/Front-End-Develop-Technicals/blob/master/images/hasClass-1.jpg)

>JavaScript JS:
```javascript
$("button").click(function() {
  alert($("p").hasClass("intros"));
  if ($("p").hasClass("intros")) {
    $('p').css('background', '#f00');
  } else {
    $('p').css('background', '#ff0');
  }
});
```

**Input file image**
- Chú ý function này có kiểm tra là image thì mới dc upload.
- Về sự kiện nên chọn là sự kiện ```change()```, đừng để 3 sự kiện cùng một lúc nó sẽ tính 3 lần.
>JavaScript Code:
```javascript
/* Preview upload image avatar */
var readURL = function((input, event)) {
  if (input.files && input.files[0]) {
    var file = input.files[0];
    var fileType = file['type'];
    var validImageTypes = ['image/gif', 'image/jpeg', 'image/png'];
    var reader = new FileReader();
    var tmppath = URL.createObjectURL(event.target.files[0]);
    console.log(tmppath);
    if (!validImageTypes.includes(fileType)) {
      // invalid file type code goes here.
      alert('Invalid');
    }else{
      reader.onload = function(e) {
        $('.fileinput .thumbnail > img').attr('src', e.target.result);
      }
      reader.readAsDataURL(input.files[0]);
    }
  }
}
$('.fileinput .btn-file > input[type=file]').on('change focus click', function (e) {
  readURL(this, e);
});
```

**Khi click vào link tại trang chủ load đến page coń và scroll đến vị trí ```section``` chứa ```id``` trùng với ```href``` thẻ a khi click **

**Case 1**
---

>HTML link trang chủ:
```
<a href="http://localhost:3000/menu.html#menu-highlight-1" class="btn btn-menu-order"><span class="icons-order">&nbsp;</span> Detail</a>
```

>HTML trang con:
```
<div class="menu-trend-item js-menusub-item" id="menu-highlight-3"></div>
```

>JS Scroll:
```
var transfer_page = function(){
  var url = window.location.href;
  var id_position = url.substring(url.lastIndexOf('#'));
  if(window.location.href.indexOf("#") > -1){
    if($(id_position).length){
      $('html, body').animate({scrollTop: $(id_position).offset().top - distanceHead}, 1500);
      $(id_position).addClass('active');
    }
  }
}
```

- ```if(window.location.href.indexOf("#") > -1)```: Kiểm tra điều kiện này để loại bỏ những ```url``` không có dấu ```#``` phía sau. Kiểm tra dòng này giúp cho các page ko có dâu ```#``` phía sau không bị lỗi ```js```.
- Hàm ```indexOf``` trả về ```-1``` nếu giá trị cần tìm không bao giờ xảy ra.
**Case 2**
---

**Usage**
- Example URL: http://www.example.com/index.php?id=1&image=awesome.jpg
- Calling ```getQueryVariable("id")``` - would return "1".
- Calling ```getQueryVariable("image")``` - would return "awesome.jpg".

>JavaScript Code:
```javascript
function getQueryVariable(variable){
  var query = window.location.search.substring(1);
  var vars = query.split("&");
  for (var i=0; i<vars.length; i++) {
    var pair = vars[i].split("=");
    if(pair[0] == variable){
      return pair[1];
    }
  }
  return(false);
}
```

**Case 3**
---

- Example URL: http://papermashup.com/index.php?id=123&page=home

>JavaScript Code:
```javascript
function getUrlVars() {
  var vars = {};
  var parts = window.location.href.replace(/[?&]+([^=&]+)=([^&]*)/gi, function(m,key,value) {
    vars[key] = value;
  });
  return vars;
}
```

>JavaScript Code:
```javascript
var first = getUrlVars()["id"];
var second = getUrlVars()["page"];

alert(first);
alert(second);
```

**Case 4**
---

>JavaScript Code:
```
$.urlParam = function(name){
  var results = new RegExp('[\?&]' + name + '=([^&#]*)').exec(window.location.href);
  return results[1] || 0;
}

// example.com?param1=name&param2=&id=6
$.urlParam('param1'); // name
$.urlParam('id');        // 6
$.urlParam('param2');   // null

//example params with spaces
http://www.jquery4u.com?city=Gold Coast
console.log($.urlParam('city'));  
//output: Gold%20Coast

console.log(decodeURIComponent($.urlParam('city')));  
//output: Gold Coast
```

>JavaScript Code:
```javascript
$.urlParam = function(name){
  var results = new RegExp('[\?&]' + name + '=([^&#]*)').exec(window.location.href);
  if (results==null){
    return null;
  }
  else{
    return results[1] || 0;
  }
}
```

**Case 5**
---
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

**18. **
- Text.

>JavaScript Code:
```javascript

```
