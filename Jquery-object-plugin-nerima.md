## Cách viêt plugin jquery theo kiểu object dự án Nerima.

1. Tham số
---

- Mỗi parameter trong một function thì có một nhiệm vụ riêng tại function đó.

- Nếu trong function cha trực tiếp có funtion con và function con này được gọi từ một function khác thì đừng nhầm tưởng về parameter của function trực tiếp co map với function con.

```javascript
slide: function(direction, index, url){
  if(direction == 'left'){
    Animation.wrapper.slide('right', 1, 0)
  }
  else{
    Animation.wrapper.slide('left', 1, 0)
  }
  Animation.wrapper.reset(1.1);
  Animation.loader.show(1, url, 1);
}
```

**JS**

```javascript
//CMS-8341用JS

(function($) {
  var this_index = '';
  var active_index = '';
  var Selector = {
    header: $('#tmp_header'),
    navigation: $('#footerArea'),
    wrapper: $('.tmp_step'),
    wrap_main: $('#tmp_wrap_inside'),
    content: $('.tmp_step_container'),
    loader: $('#tmp_loading')
  };
  $(function() {
    var Animation = {
      core:{
        slide: function(direction, index, url){
          if(direction == 'left'){
            Animation.wrapper.slide('right', 1, 0)
          }
          else{
            Animation.wrapper.slide('left', 1, 0)
          }
          Animation.wrapper.reset(1.1);
          Animation.loader.show(1, url, 1);
        },
        showContent: function(index, delay){
          Selector.wrapper.eq(active_index).hide();
          Selector.wrapper.eq(index).show();
        }
      },

      loader: {
        show: function(delay, url, callback){
          Animation.func.set_state(Selector.loader, 'show', delay, callback, url);
        },
        hide: function(delay, callback){
          Animation.func.set_state(Selector.loader, 'hide', delay, callback, '');
        }
      },

      wrapper: {
        slide: function(direction, duration, delay){
          if(direction == 'left'){
            Animation.func.translate_from_to_per(Selector.wrap_main, [0, 0], [100, 0], duration, delay);
          }else if(direction == 'right'){
            Animation.func.translate_from_to_per(Selector.wrap_main, [0, 0], [-100, 0], duration, delay);
          }
        },
        reset: function(delay) {
          var position = { y: 0 };
          console.log(position.y);
          var this_animate = TweenLite.to(position, 0.1, {
            y: 1,
            ease: Power2.easeIn,
            onComplete: function() {
              console.log(position.y);
              Selector.wrap_main.css({
                'transform': 'none'
              });
            }
          });
          this_animate.delay(delay);
        }
      },
      func:{
        translate_from_to_per: function(selector, start, end, duration, delay){
          selector.css({'transform': 'translate(' + start[0] + '%,' + start[1] + '%)'});
          var position = {x: start[0], y: start[1]};
          var this_animate = TweenLite.to(position, duration, {
            x: end[0],
            y: end[1],
            ease: Power2.easeIn,
            onUpdate: function(){
              selector.css({'transform': 'translate('+ position.x + '%,' + position.y + '%)'});
            },
            onComplete: function(){

            }
          });
          this_animate.delay(delay).play();
        },
        set_state: function(target, state, delay, callback, url){
          var position = {y:0};
          var this_animate = TweenLite.to(position, 0.1, {
            y: 1,
            ease:Power2.easeIn,
            onComplete: function(){
              switch (state){
                case 'hide':
                  target.hide();
                  break;
                case 'show':
                  target.show();
                  break;
              }
              if(callback == 1){
                if(!$('#tmp_step_'+this_index).hasClass('active')){
                  if(!$('#tmp_step_'+this_index + '.tmp_step_container').html()){
                    getAjax(url, function(data){
                      var content = $(data).contents().filter(function() {
                        return this.nodeType == 1;
                      }).remove();
                      renderHtml(content);
                      Animation.loader.hide(0, 0.5);
                      Animation.core.showContent(this_index, 0.5);
                    });
                    $('#tmp_step_'+active_index).removeClass('active');
                    $('#tmp_step_'+this_index).addClass('active');
                    if(window.history.pushState){
                      window.history.pushState({url:url}, '', url);
                    }
                  }
                  else{
                    Animation.loader.hide(0, 0.5);
                    Animation.core.showContent(this_index, 0.5);
                    if(window.history.pushState){
                      window.history.pushState({url:url}, '', url);
                    }
                  }
                }
              }
            }
          });
          this_animate.delay(delay).play();
        }
      }
    }
    var urlHash = function(url){
      var trend = this_index > active_index  ? 'left' : 'right';
      Animation.core.slide(trend, this_index, url);
    };

    var renderHtml = function(content){
      var tmp_html = content.find('#tmp_step_'+this_index).find('.tmp_step_container');
      $('#tmp_step_'+this_index).find('.tmp_step_container').html(tmp_html)
    };

    var getAjax = function(url, _callback){
      $.ajax({
        url: url,
        type: 'GET',
        dateType: 'html',
        success: function(data){
          if(typeof _callback == 'function'){
            _callback(data);
          }
        },
        error: function(xhr){
          alert("Sorry, Can't load page, <br />"+xhr.status);
        }
      });
    };

    var bind = function(){
      Selector.navigation.on('click', 'a', function(e){
        e.preventDefault();
        if(!$(this).hasClass('active')){
          this_index = Selector.navigation.find('a').index(this);
          var active_selector = Selector.navigation.find('.active');
          active_index = Selector.navigation.find('a').index(active_selector);
          Selector.navigation.find('a').removeClass('active');
          $(this).addClass('active');
          var url = $(this).attr('href');
          urlHash(url);
        }
      });
    };

    $(document).ready(function() {
      Animation.loader.hide(0, 0.5);
      Animation.core.showContent(this_index, 0.5)
      bind();
    });
  });

})(jQuery);
```

**HTML**

```javascript
<?xml version="1.0" encoding="utf-8" ?>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" lang="ja" xml:lang="ja" class="html_theme html_theme_1">

<head>
  <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
  <meta http-equiv="Content-Style-Type" content="text/css" />
  <meta http-equiv="Content-Script-Type" content="text/javascript" />
  <title>ページタイトル</title>
  <meta name="author" content="#" />
  <meta name="viewport" content="width=device-width, maximum-scale=3.0" />
  <meta name="format-detection" content="telephone=no" />
  <link href="./css/default.css" rel="stylesheet" type="text/css" media="all" />
  <link href="./css/shared.css" rel="stylesheet" type="text/css" media="all" />
  <link href="./css/color/color0.css" rel="stylesheet" type="text/css" media="all" id="tmp_color" class="tmp_color" title="default" />
  <link href="./css/color/color1.css" rel="alternate stylesheet" type="text/css" media="all" class="tmp_color" title="darkblue" />
  <link href="./css/color/color2.css" rel="alternate stylesheet" type="text/css" media="all" class="tmp_color" title="yellow" />
  <link href="./css/color/color3.css" rel="alternate stylesheet" type="text/css" media="all" class="tmp_color" title="black" />
  <link href="./css/font/normal.css" rel="stylesheet" type="text/css" id="tmp_font" media="all" title="default" class="tmp_font" />
  <link href="./css/font/small.css" rel="alternate stylesheet" type="text/css" media="all" title="small" class="tmp_font" />
  <link href="./css/font/big.css" rel="alternate stylesheet" type="text/css" media="all" title="big" class="tmp_font" />
  <link href="./css/font/big2.css" rel="alternate stylesheet" type="text/css" media="all" title="big2" class="tmp_font" />
  <link href="./css/edit_top.css" rel="stylesheet" type="text/css" media="all" />
  <link href="./css/tablet.css" rel="stylesheet" media="only screen and (min-width : 481px) and (max-width : 768px)" type="text/css" id="tmp_tablet_css" />
  <link href="./css/smartphone.css" rel="stylesheet" media="only screen and (max-width : 480px)" type="text/css" id="tmp_smartphone_css" />
  <link href="#" rel="alternate" type="application/rss+xml" title="#" />
  <script type="text/javascript" src="./js/jquery.js"></script>
  <script type="text/javascript" src="./js/gd.js"></script>
  <script type="text/javascript" src="./js/setting_head.js"></script>
</head>

<body class="format_top body_theme body_theme_1 no_javascript">
  <script type="text/javascript" src="./js/setting_body.js"></script>
  <div id="tmp_wrapper">
    <div id="tmp_wrap_inside">
      <noscript>
        <p>このサイトではJavaScriptを使用したコンテンツ・機能を提供しています。JavaScriptを有効にするとご利用いただけます。</p>
      </noscript>
      <p><a href="#tmp_honbun" class="skip">本文へスキップします。</a>
      </p>
      <div id="tmp_header">
        <div class="image-header">
          <img src="/img/header/image-header.png" alt="" width="1600" height="91" />
        </div>
        <div class="header_top">
          <img src="/img/header/breadcumb.png" alt="" width="1600" height="40" />
        </div>
        <div class="header_main">
          <img src="/img/gnavi/gnavi_1.jpg" alt="The ALT here is not included" width="1600" height="70" />
        </div>
      </div>
      <div id="tmp_wrap_main">
        <div id="tmp_main">
          <div id="tmp_contents">
            <div id="tmp_step_0" class="tmp_step contentsArea active">
              <div class="tmp_step_container">
                <img src="/img/top/contentA.png" alt="The ALT here is not included" width="1240" height="1646" />
              </div>
            </div>
            <div id="tmp_step_1" class="tmp_step contentsArea">
              <div class="tmp_step_container"></div>
            </div>
            <div id="tmp_step_2" class="tmp_step contentsArea">
              <div class="tmp_step_container"></div>
            </div>
            <div id="tmp_step_3" class="tmp_step contentsArea">
              <div class="tmp_step_container"></div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div id="tmp_footer">
      <img src="/img/free/img_footer.png" width="1600" height="209" />
    </div>
    <div class="Arrow_L" style="display: none;"><img src="/img/gnavi/Arrow_L.png" alt="" border="0"></div>
    <div class="Arrow_R"><img src="/img/gnavi/Arrow_R.png" alt="" border="0"></div>
    <div id="footerArea" class="menuA">
      <ul class="navi_control">
        <li><a href="/index/benri.html" class="active"><img src="/img/gnavi/navi_ctrl_1.jpg" alt="The ALT here is not included" width="175" height="50"></a></li>
        <li><a href="/index/chiiki.html"><img src="/img/gnavi/navi_ctrl_2.jpg" alt="The ALT here is not included" width="175" height="50"></a></li>
        <li><a href="/index/jigyosha.html"><img src="/img/gnavi/navi_ctrl_3.jpg" alt="The ALT here is not included" width="175" height="50"></a></li>
        <li><a href="/index/tetsuzuki.html"><img src="/img/gnavi/navi_ctrl_4.jpg" alt="The ALT here is not included" width="175" height="50"></a></li>
      </ul>
    </div>
  </div>
  <div id="tmp_loading" class="loading js_loading">
    <div class="loading_inner">
      <div class="content js_loading_content">&nbsp;</div>
    </div>
  </div>
  <div id="tmp_overlay_0" class="tmp_overlay theme_0">
    <div class="tmp_overlay_inside"></div>
  </div>
  <div id="tmp_overlay_1" class="tmp_overlay theme_1">
    <div class="tmp_overlay_inside"></div>
  </div>
  <div id="tmp_overlay_2" class="tmp_overlay theme_2">
    <div class="tmp_overlay_inside"></div>
  </div>
  <div id="tmp_overlay_3" class="tmp_overlay theme_3">
    <div class="tmp_overlay_inside"></div>
  </div>
  <script type="text/javascript" src="./js/setting_responsive.js"></script>
  <script type="text/javascript" src="./js/tweenMax.js"></script>
  <script type="text/javascript" src="./js/setting_onload.js"></script>
</body>

</html>
```

**CSS**

```javascript


```

