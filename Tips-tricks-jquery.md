### Tips Tricks JQuery

#### Sử dụng Plugin:
- **Chú ý:** Trong trường hợp dùng nhiều thư viện ```plugin``` jQuery trên site gồm nhiều page thường hay bị báo lỗi thư viện tại trang ko được load plugin. Lý do bởi vì ```class``` or ```id``` của ```page này``` được gọi trong thư viện ```jQuery```, nhưng ```class``` or ```id``` ở ```page này``` lại không tồn tại ```page khác``` dù ```page khác``` có ```include``` thư viện của ```plugin``` đó đi chăng nữa nó vẫn bị lỗi. Để giải quyết trường hợp này có 2 cách xử lý:

>**Case 1:** Dùng kỹ thuật ```flag```
```javascript
var topFlg = $('body').hasClass('format_top');
if (topFlg) {
  var bannerSlider = $(".slider_top");
  bannerSlider.slick({
    dots: true,
    infinite: true,
    speed: 500,
    fade: true,
    autoplay: true,
    arrows: false,
    autoplaySpeed: 5000,
    cssEase: 'linear'
  });
}
```

>**Case 2:** Dùng kỹ thuật ```.length```
```javascript
var bannerSlider = $(".slider_top");
if (bannerSlider.length) {
  bannerSlider.slick({
    dots: true,
    infinite: true,
    speed: 500,
    fade: true,
    autoplay: true,
    arrows: false,
    autoplaySpeed: 5000,
    cssEase: 'linear'
  });
}
```
#### 1. Scroll:
<hr />

> **Back Top**

```javascript
////////////////////////////////
// Back Top
////////////////////////////////
$(window).scroll(function() {
  var windowWidth = $(window).width();
  var scrollBottom = $(window).scrollTop() + $(window).height();
  var height_document = $(document).height() - 110;
  if (scrollBottom > height_document) {
    $('.back_top').css('bottom', 96);
  } else {
    $('.back_top').css('bottom', 20);
  }

if (scrollBottom > height_document && windowWidth < 690 && windowWidth > 390) {
  $('.back_top').css('bottom', 115);
} else if (scrollBottom > height_document && windowWidth < 690 && windowWidth < 390) {
  $('.back_top').css('bottom', 160);
}

if ($(this).scrollTop() > 250) {
  $('.back_top').fadeIn(500);
  $('.back_top').removeClass('fadeOutDown').addClass('animated fadeInUp');
} else {
//$('.back_top').fadeOut(500);
  $('.back_top').removeClass('fadeInUp').addClass('fadeOutDown');
  }
});
$('.back_top').click(function() {
  $("html, body").animate({ scrollTop: 0 }, 1500, 'easeOutExpo');
  return false;
});
```

- ```$(window).scrollTop()``` : Tính height của scroll khi cuộn trong body

- ```$(document).height()``` : Toàn bộ height của doucument tức là tính luôn nội dung của kể cả trang web có scroll bao nhiêu đi chăng nữa. Khác với ```$(window).height()```: chỉ tính height() của window chứ ko tính height của phần scroll trong body.

- ```$(document).height()``` : thì bằng tổng $(window).scrollTop() + $(window).height().

>**Scroll/Follow Sidebar**
```javascript
$(function() {
    var $sidebar   = $("#sidebar"), 
        $window    = $(window),
        offset     = $sidebar.offset(),
        topPadding = 15;
    $window.scroll(function() {
        if ($window.scrollTop() > offset.top) {
            $sidebar.stop().animate({
                marginTop: $window.scrollTop() - offset.top + topPadding
            });
        } else {
            $sidebar.stop().animate({
                marginTop: 0
            });
        }
    });   
});
```

>**Nếu sử dụng javascript Pure thì phải kèm theo ```document.body.scrollTop``` và ```document.documentElement.scrollTop```**
```javascript
window.onscroll = function() {navSticky()};
function navSticky() {
  if (document.body.scrollTop > 20 || document.documentElement.scrollTop > 20) {
    $('.navigation_top').addClass('sticky');
  } else {
    $('.navigation_top').removeClass('sticky');
  }
}
```

>**Cách tính ```scrollBottom```**
- ```scrollBottom``` thì bằng ```$(window).scrollTop() + $(window).height();```
```javascript
$(window).scroll(function() {
  var scrollBottom = $(window).scrollTop() + $(window).height();
  var height_document = $(document).height();
  if (scrollBottom > height_document) {
    $('.navigation_top').addClass('sticky');
  } else {
    $('.navigation_top').removeClass('sticky');
  }
});
```
#### 2. Function jQuery:
<hr />
> siblings(): Lấy thành phần con cùng cấp của mỗi thành phần trong một bộ chọn phù hợp(Tức là tất cả các thành phần anh chị em cùng cấp với ```<li>``` có class="second" đều đã được chọn, riêng chính nó thì không.) 

#### 3. Check active:
<hr />

> **Case 1:** 
      
```javascript
$('ul.page-sidebar-menu > li').find('a').click(function(e) {
  e.preventDefault();
  var iscurrent = $(this).parent().hasClass('active');
  if (iscurrent == false) {
    $(this).parent().addClass('active').siblings().each(function() {
    $(this).removeClass('active');
  });
  }
});
```

> **Case 2:** 
      
```javascript
$('ul.page-sidebar-menu > li').find('a').click(function(e) {
  e.preventDefault();
  $('ul.page-sidebar-menu > li').removeClass('active');
  $(this).addClass('active');
});
```

> **Case 3:** 
      
```javascript
function removeClassFromElem(classSelect, classToRemove){
  $(classSelect).each(function(){
    var currElem=$(this);
    if(currElem.hasClass(classToRemove)){
      currElem.removeClass(classToRemove);
    }
  });
}
//usage
removeClassFromElem('.someclass', 'active');
```

> **Case 4:** 

```javascript
$('ul.wd-information li a').click(function(){
  $('ul.wd-information li a').removeClass('current');
  $(this).addClass('current');
});
```

> **Case 5:** 

- Get index of tag ```<a>```.
  ```this_index = selectors.navigation.find('a').index(this);```
  
- Assign the variable to the ```<a>``` tag containing the active class.
  ```var active_selector = selectors.navigation.find('.active');```
  
- Get index of active class.
  ```active_index = selectors.navigation.find('a').index(active_selector);```
  
- Từ ```index``` của ```this_index``` và ```index``` của ```active```, chúng ta có thể lấy nó và gán lên ```function()``` xử lý tab để ẩn hiện ```eachItem(this_index)```
  
```javascript
var this_index = '';
var active_index = '';
var selectors = {
  navigation: $('.nav-tabs'),
  content: $('.tab_panel')
}
var tabs = {
  showContent: function(index) {
    selectors.content.eq(active_index).hide();
    selectors.content.eq(index).show();
  }
}
var eachItem = function(this_index) {
  if ($('.tab_panel').hasClass('active')) {
    tabs.showContent(this_index);
  }
};
$(document).ready(function() {
  selectors.navigation.on('click', 'a', function(e) {
    e.preventDefault();
    this_index = selectors.navigation.find('a').index(this);
    var active_selector = selectors.navigation.find('.active');
    active_index = selectors.navigation.find('a').index(active_selector);

    active_selector.removeClass('active');
    $(this).addClass('active');
    
    // If the element is not found, index() will return -1.
    eachItem(this_index);
  });
});
```

> **Case 6:** Loop active jQuery

```javascript
var toggleSlide = function(){
    $("h1 .words span.active").removeClass().next().add("h1 .words span:first").last().addClass("active");
  }
  setInterval(toggleSlide, 1500);
```

```javascript
toggleSlide = function() {
  var active = $("#slider ul li.active");
  var next = active.next();
  if (next.length === 0) {
    next = $('#slider ul li:first');
  }

  active.removeClass('active');
  next.addClass('active');
}
setInterval(toggleSlide, 1000);
```

>**Case 7: ** Loop active Javascript

**HTML**
```javascript
<ul>
  <li class="panel active">Item 1</li>
  <li class="panel">Item 2</li>
  <li class="panel">Item 3</li>
</ul>
```

**JS**
```javascript
$(function() {
  var lis_count = $('li.panel').length;
  var active_li_index = 0;

  setInterval(function() {
    if ($('li.panel.active').index() == lis_count - 1)
      active_li_index = 0;
    else
      active_li_index++;

    $('li.panel.active').removeClass('active');
    $('li.panel').eq(active_li_index).addClass('active');
  }, 1000);
})
```

```javascript
document.addEventListener('DOMContentLoaded', function() {
  var lis = Array.prototype.slice.call(document.querySelectorAll('li.panel'));
  var lis_count = lis.length;
  var active_li_index = 0;

  setInterval(function() {
    var active_li = document.querySelector('li.panel.active');

    if (lis.indexOf(active_li) == lis_count - 1)
      active_li_index = 0;
    else
      active_li_index++;

    active_li.classList.remove('active');
    document.querySelectorAll('li.panel')[active_li_index].classList.add('active');
  }, 1000);
}, false);
```

**CSS**
```javascript
.active {
  background - color: yellow;
}
```

#### 4. Allow show/hide, fadeIn/fadeOut, slideUp/slideDown block:

<hr />

>**Case 1:** 

```javascript
$(".click").bind('click', function(e) {
  e.preventDefault();
  if ($('.dropdown-list').is(':visible')) {
    $(this).parent().removeClass('active');
    $('.block-overlay').fadeOut(300);
  } else {
    $(this).parent().addClass('active');
    $('.block-overlay').fadeIn(300);
  }
});
```    

> **Case 2:** 
    
```javascript
$(".click").bind('click', function(e) {
  e.preventDefault();
  if ($('.dropdown-list').is(':hidden')) {
    $(this).parent().addClass('active');
    $('.block-overlay').fadeIn(300);
  } else {
    $(this).parent().removeClass('active');
    $('.block-overlay').fadeOut(300);
  }
});
```     

> **Case 3:** 
    
 ```javascript
$('.map-thumb .switch-map').click(function(e) {
   if ($('.map-thumb').css('right') == '0px') {
     $('.map-thumb').delay(500).stop(true, true).animate({ right: -153 }, 500);
     $(this).addClass('active').stop(true, true).animate({ left: -27 }, 400);
   } else {
     $('.map-thumb').stop(true, true).delay(500).animate({ right: 0 }, 400);
     $(this).removeClass('active').stop(true, true).animate({ left: 0 }, 400);
   }
   e.preventDefault();
 });
```

> **Case 4:** 
    
 ```javascript
$('.map-thumb .switch-map').click(function(e) {
  if ($('.map-thumb').css('right') == '0px') {
    $('.map-thumb').delay(500).stop(true, true).animate({ right: -153 }, 500);
    $(this).addClass('active').stop(true, true).animate({ left: -27 }, 400);
  } else {
    $('.map-thumb').stop(true, true).delay(500).animate({ right: 0 }, 400);
    $(this).removeClass('active').stop(true, true).animate({ left: 0 }, 400);
  }
  e.preventDefault();
});
      
```

#### 5. Show selected text value dropdown:
<hr />

  ```javascript
  /**
   * Show selected text value dropdown
   
   * @param string selectItem Selected item selector
   * @param string showTo   Show selected text to element selector
   * 
   * @return void
   **/
  function showSelected(selectItem, showTo) {
    $(document).on('click', selectItem, function() {
      $(showTo).text($(this).text());
    });
  };
  showSelected('.dropdown-catagory li a', '.dropdown-toggle .value-catagory');
  ```

#### 6. Detect Resize combined load:
<hr />

  ```javascript
  $(window).resize(function() {
    calcHeight();
  }).load(function() {
    calcHeight();
  });
  ```

#### 7. Call js Cufon:
<hr />

  ```javascript
Cufon.replace('#wd-nav ul.wd-dropdownMenu li a',{fontFamily: 'UTM Essendine Caps'});
Cufon.replace('.wd-left-content ul.wd-information li a.wd-link-first',{
fontFamily: 'UTM Essendine Caps',
  hover: {
    color: '#b61010'
  }
});
  ```

#### 8. Bind click document:
<hr />

```javascript
$('ul.account > li').bind('click',function(e){
  e.stopPropagation();
  $(document).bind('click',function(){
    $('ul.account > li').removeClass('open');
  });
});
```


#### 9. Scroll Effect Element:
<hr />

>**Case 1:** 
    
 ```javascript
jQuery('.to_slide_left').each(function() {
  var imagePos = jQuery(this).offset().top;
  var topOfWindow = jQuery(window).scrollTop();
  if (imagePos < topOfWindow + windowHeight - 100) {
    jQuery(this).addClass("animated fadeInLeft");
  }
});
```

>**Case 2: Through each level** 
    
 ```javascript
jQuery('.to_animate_child_blocks').each(function() {
  var imagePos = jQuery(this).offset().top;
  var topOfWindow = jQuery(window).scrollTop();
  if (imagePos < topOfWindow + windowHeight - 100) {
    jQuery(this).find('.block').each(function(index) {
      var self = jQuery(this);
      setTimeout(function() {
        self.addClass("animated fadeInRight");
      }, index * 200);
    });
  }
});
```

#### 10. Ajax:
<hr />

>**Case 1:** 

 ```javascript
var username ='';
if (username != '') {
  //add user infomation
  $.ajax({
    url: app.getBaseURL() + 'users/' + username,
    type: 'GET',
    success: function(res) {
      $('#txthoTen').val(res.data.info.displayname);
      $('#txtEmail1').val(res.data.info.email);
    },
    error: function(jqXHR, textStatus) {
      console.log(jqXHR);
    }
  });
}

```

#### 11. Process input search on header, header use position: fixed and run on device smartphone :
<hr />

![Images](https://github.com/daodc/Front-End-Develop-Technical/wiki/jQuery)

>**Case 1:** 

 ```javascript
$(document).on('focus', 'select, input, textarea', function() {
  $('#header').css({ 'position': 'absolute', 'top': '0px' });
});
$(document).on('blur', 'select, input, textarea', function() {
  $('#header').css({ 'position': 'fixed' });
});
```

#### 12. Checkbox append value to element need show.
<hr />

**HTML:** 

```javascript
<div class="dropdown dropdown-block js-dropdown-block">
  <button class="btn btn-dropdown" type="button" data-toggle="dropdown">
    <span class="label-setting">
      グループ設定 ： 
      <span class="slot-text js-dropdown-value">
      <span class="push-number"></span>
    </span>
    </span>
    <span class="icon arrow-down-tb"></span>
  </button>
  <div class="dropdown-menu">
    <p class="label-set-level">このユーザーのレベルを設定</p>
    <ul class="radio-list">
      <li>
        <div class="checkbox-regular">
          <input id="checkbox-drop-1" class="cus-cb js-dropdown-target" type="checkbox" value="" data-id="">
          <label class="cus-cb-label" for="checkbox-drop-1">グループなし</label>
        </div>
      </li>
      <li>
        <div class="checkbox-regular">
          <input id="checkbox-drop-2" class="cus-cb js-dropdown-target" type="checkbox" value="1" data-id="1">
          <label class="cus-cb-label" for="checkbox-drop-2"><span class="push-number">1</span>：総務部</label>
        </div>
      </li>
      <li>
        <div class="checkbox-regular">
          <input id="checkbox-drop-3" class="cus-cb js-dropdown-target" type="checkbox" value="2" data-id="2">
          <label class="cus-cb-label" for="checkbox-drop-3"><span class="push-number">2</span>：人事部</label>
        </div>
      </li>
      <li>
        <div class="checkbox-regular">
          <input id="checkbox-drop-4" class="cus-cb js-dropdown-target" type="checkbox" value="3" data-id="3">
          <label class="cus-cb-label" for="checkbox-drop-4"><span class="push-number">3</span>：海外事業部</label>
        </div>
      </li>
      <li>
        <div class="checkbox-regular">
          <input id="checkbox-drop-5" class="cus-cb js-dropdown-target" type="checkbox" value="4" data-id="4">
          <label class="cus-cb-label" for="checkbox-drop-5"><span class="push-number">4</span>：営業部</label>
        </div>
      </li>
    </ul>
  </div>
</div>
```

**JS:** 
<hr />

```javascript
$('.address-table .js-dropdown-target').on('change', function() {
  var _dataId = $(this).data('id');
  var _value = $(this).val();
  var _this = $(this);
  if (_dataId && _value != '') {
    if ($(this).is(':checked')) {
      _renderValueCheck(_this, _value, _dataId);
    } else {
      _removeValueCheck(_this, _dataId);
    }
  }
});

var _renderValueCheck = function(_this, _id, _value) {
  var _htmlValue = '<span class="js-value-item push-number" data-id="' + _id + '">' + _value + '&nbsp;・' + '</span>';
  _this.closest('.js-dropdown-block').find('.js-dropdown-value').append(_htmlValue);
};

var _removeValueCheck = function(_this, _id) {
  _this.closest('.js-dropdown-block').find('.js-value-item').filter('[data-id="' + _id + '"]').remove();
};
```

#### 13. Get atribute id ascending for element :
<hr />

```javascript
function getAtributeTable() {
    $('.address-table tbody tr').each(function(index) {
        $(this).attr('id', +index)
    });
}
```

#### 14. Combine event ```mouseover``` and ```click```:
<hr />

```javascript
$('.address-table tbody tr td .action-link').on('mouseover click', '.ic-rating', function(event) {
  if (event.type == "mouseover") {
    $(this).toggleClass('selected');
    mouseoverClick();
  } else if (event.type == "click") {
    $(this).toggleClass('selected');
  }
});
```

#### 15. Bootstrap dropdown list auto position (Up/Bottom):
<hr />

```javascript
$('.container-sortable .table > tbody > tr > td').on('click', '[data-toggle=dropdown]', function() {
    var dropmenu = $(this).next('.dropdown-menu');
    dropmenu.css({
        visibility: "hidden",
        display: "block"
    });
    // Necessary to remove class each time so we don't unwantedly use dropup's offset top
    dropmenu.parent().removeClass("dropup");
    // Determine whether bottom of menu will be below window at current scroll position
    if (dropmenu.offset().top + dropmenu.outerHeight() > $(window).innerHeight() + $(window).scrollTop()) {
        dropmenu.parent().addClass("dropup");
    }
    // Return dropdown menu to fully hidden state
    dropmenu.removeAttr("style");
});
```

#### 16. Remove One Row And All Row :
<hr />

```javascript
$('.address-table > thead > tr > th').on('click', '.action-delete', function() {
  var _this = $(this).parent().parent().parent().parent().find('tbody');
  $('.btn-remove-row').on('click', function() {
    _removeAllRow(_this);
  });
});
$('.address-table tbody tr td').on('click', '.action-delete', function() {
  var _this = $(this).parent().parent();
  $('.btn-remove-row').on('click', function() {
    _removeRow(_this);
  });
});

var _removeRow = function(_this) {
  _this.closest('tr').remove();
};
var _removeAllRow = function(_this) {
  _this.html('');
};
```
#### 17. Handle event click and click again:
<hr />

```javascript
$('.address-table tbody tr').each(function() {
        var isClicked = false;
        $(this).on('click', '.ic-rating', function() {
            isClicked = true;
            $(this).addClass('selected');
            $(this).parent().find('.value-stars').html("selected");
        });
        $(this).on('click', '.ic-rating.selected', function() {
            if (isClicked) {
                $(this).removeClass('selected');
                $(this).parent().find('.value-stars').html("");
            }
        });
});
```

#### 18. Use jQuery to hide a DIV when the user clicks outside of it:

> **Case 1:**

**HTML**

```
<div class="dropdown">
  <button class="btn btn-default btn-dropdown" type="button">
    Dropdown
    <span class="caret"></span>
  </button>
  <ul class="dropdown-menu">
    <li><a href="#">Action</a></li>
    <li><a href="#">Another action</a></li>
    <li><a href="#">Something else here</a></li>
    <li role="separator" class="divider"></li>
    <li><a href="#">Separated link</a></li>
  </ul>
</div>
```

```javascript
$(".btn-dropdown").click(function(e) {
  $(".dropdown1").toggleClass('open');
  e.stopPropagation();
});

$(".dropdown").click(function(e) {
  e.stopPropagation();
});

$(document).click(function() {
  $(".dropdown").removeClass('open');
});
```

> **Case 2:**

```javascript
<div class="dropdown">
  <button class="btn btn-default btn-drop-click2" type="button">
    Dropdown
    <span class="caret"></span>
  </button>
  <ul class="dropdown-menu">
    <li><a href="#">Action</a></li>
    <li><a href="#">Another action</a></li>
    <li><a href="#">Something else here</a></li>
    <li role="separator" class="divider"></li>
    <li><a href="#">Separated link</a></li>
  </ul>
</div>
```

**JS**

```javascript
$(".btn-drop-click2").click(function() {
  $(".dropdown2").toggleClass('open');
});

$(document).click(function(e) {
  if (!$(e.target).hasClass("btn-drop-click2") && $(e.target).parents(".dropdown2").length === 0) {
    $(".dropdown2").removeClass('open');
  }
});
```

#### 19. Function:
<hr />

> **prop:** 

The prop() method sets or returns properties and values of the selected elements.

> **Return the value of a property::** 

```javascript
$(selector).prop(property)
```

> **Set the property and value::** 

```javascript
$(selector).prop(property,value)
```

> **Set property and value using a function:** 

```javascript
$(selector).prop(property,function(index,currentvalue))
```

> **Set multiple properties and values:** 

```javascript
$(selector).prop({property:value, property:value,...})
```

> **Selected all input có type là checkbox trong table:** 

```javascript
$('#allcb').change(function() {
  if ($(this).prop('checked')) {
    $('tbody tr td:first-child input[type="checkbox"]').each(function() {
      $(this).prop('checked', true);
    });
  } else {
    $('tbody tr td:first-child input[type="checkbox"]').each(function() {
      $(this).prop('checked', false);
    });
  }
});
```

#### 20.Rendering a simple list of products with jQuery:

```javascript
var products = [
  {
    id: 1,
    name: 'Book',
    price: 15
  },
  {
    id: 2,
    name: 'Burrito',
    price: 8
  },
  {
    id: 3,
    name: 'Spaceship',
    price: 999999999
  },
  {
    id: 4,
    name: 'Dinosaur Bones',
    price: 5000000
  }
];

function buyProduct(productId) {
  // buy the product
}

/* -- Just jQuery -- */
function buyButtonJquery(product) {
  var button = $('<button class="buy-button">$' + product.price
    + '</button>');
  
  // handle click event
  $(button).on('click', function(event) {
    event.preventDefault();
    buyProduct(product.id);
  });

  return button;
}

function productListJustJquery(products, element) {
  var list = $('<ul class="product-list"></ul>');

  products.forEach(function(product) {
    var item = $('<li>' + product.name + '</li>');
    item.append(buyButtonJquery(product));
    list.append(item);
  });

  // replace the existing list if there is one
  var currentList = $(element).find('.product-list');
  if (currentList.length) {
    currentList.replaceWith(list);
  } else {
    $(element).append(list);
  }
}
```

#### 21.How to Dynamically Trim Text Using jQuery

```javascript
$(document).ready(function($) {
  $("p").each(function() {
    if ($(this).text().length > 40) {
      $(this).text($(this).text().substr(0, 37));
      $(this).append('...');
    }
  });
});
```

#### 22.jQuery Snippets: Getting the Current Year

> **HTML:**

```javascript
<p>© <span class=".currentyear"></span></p>
```
> **JS:**

```javascript
$(function() {
  thisyear = new Date().getFullYear();
  $('.currentyear').text(thisyear);
});
```
#### 23.jQuery Snippets: How to Conditionally Enable Submit

> **HTML:**

```javascript
<input type="submit" id="submit" value="Submit" disabled>
```
> **JS:**

```javascript
$('#name').keyup(function() {
 $('#submit').attr('disabled', !$('#name').val());
});
```

#### 24.jQuery Snippets: Using jQuery to Check All Boxes

> **HTML:**

```javascript
<a rel="50checkboxes" href="#check-all">Check All</a>
<a rel="50checkboxes" href="#uncheck-all">Uncheck All</a>
<div id="50checkboxes">
   <input type="checkbox">
   ...
   ...
</div>
```
> **JS:**

> **Check all:**
```javascript
$("A[href='#check-all']").click(function() {
 $("#" + $(this).attr('rel') + " INPUT[type='checkbox']").attr('checked', true);
 return false;
});
```

> **Uncheck:**

```javascript
$("A[href='#uncheck-all']").click(function() {
 $("#" + $(this).attr('rel') + " INPUT[type='checkbox']").attr('checked', false);
 return false;
});
```

#### 25.How to Use jQuery to Check if Cookies are Enabled

> **JS:**

```javascript
$(document).ready(function() {
    var dt = new Date();
    dt.setSeconds(dt.getSeconds() + 60);
    document.cookie = "cookietest=1; expires=" + dt.toGMTString();
    var cookiesEnabled = document.cookie.indexOf("cookietest=") != -1;
    if(!cookiesEnabled){
        //cookies are not enabled
    }
});
```

> **Here’s how you would use it:**

```javascript
var c = "Cookies enabled:" + navigator.cookieEnabled;
```

> **The result of the variable c would be:**

```javascript
Cookies enabled: true
```

> **If cookies were enabled on the browser, or:**

```javascript
Cookies enabled: false
```
#### XX.How to Use jQuery to Create a Sticky Navigation on Scroll

```javascript
$(window).scroll(function() {
 if ($(window).scrollTop() > 200 ) {
 $('.nav').css({'position' : 'fixed', 'top' : 0});
 } else {
 $('.nav').css({'position' : 'relative', 'top' : 'none'});
 }
});
```

#### 26.How to Use jQuery’s Keystroke Methods:

> **.keypress():**

```javascript
i=0
$("textbox").keypress(function(){
  console.log(i += 1);
})
```
> **.keydown():**

> **.keyup():**

```javascript
$("textarea").keyup(function(){
  ("textarea").css("color", "blue");
})
```
#### 27.How to Use jQuery’s Keystroke Methods:

```javascript
$(document).ready(function(){
 var iFrameDOM = $("iframe#frameID").contents();
 iFrameDOM.find(".main").css("color", "#333");
});
```

#### 28.How to Use jQuery to Create Blinking Text:

```javascript
function blink(selector){
 $(selector).fadeOut('slow', function(){
   $(this).fadeIn('slow', function(){
    blink(this);
   });
 });
}

$(document).ready(function(){
 blink('.blink'); 
});
```
#### 29.How to Disable Right-Click Menu Using jQuery:

```javascript
$(document).bind("contextmenu",function(e){
 return false;
 });
});
```

#### 30.How to Detect Browser Using jQuery

```javascript
function _setBrowser()
{
 var userAgent = navigator.userAgent.toLowerCase();
 // Figure out what browser is being used
 jQuery.browser = {
 version: (userAgent.match( /.+(?:rv|it|ra|ie|me|ve)[\/: ]([\d.]+)/ ) || [])[1],
 chrome: /chrome/.test( userAgent ),
 safari: /webkit/.test( userAgent ) && !/chrome/.test( userAgent ),
 opera: /opera/.test( userAgent ),
 firefox: /firefox/.test( userAgent ),
 msie: /msie/.test( userAgent ) && !/opera/.test( userAgent ),
 mozilla: /mozilla/.test( userAgent ) && !/(compatible|webkit)/.test( userAgent ),
 webkit: $.browser.webkit,
 gecko: /[^like]{4} gecko/.test( userAgent ),
 presto: /presto/.test( userAgent ),
 xoom: /xoom/.test( userAgent ),
 android: /android/.test( userAgent ),
 androidVersion: (userAgent.match( /.+(?:android)[\/: ]([\d.]+)/ ) || [0,0])[1],
 iphone: /iphone|ipod/.test( userAgent ),
 iphoneVersion: (userAgent.match( /.+(?:iphone\ os)[\/: ]([\d_]+)/ ) || [0,0])[1].toString().split('_').join('.'),
 ipad: /ipad/.test( userAgent ),
 ipadVersion: (userAgent.match( /.+(?:cpu\ os)[\/: ]([\d_]+)/ ) || [0,0])[1].toString().split('_').join('.'),
 blackberry: /blackberry/.test( userAgent ),
 winMobile: /Windows\ Phone/.test( userAgent ),
 winMobileVersion: (userAgent.match( /.+(?:windows\ phone\ os)[\/: ]([\d_]+)/ ) || [0,0])[1]
 };
 jQuery.browser.mobile = ($.browser.iphone || $.browser.ipad || $.browser.android || $.browser.blackberry );
};
```

#### 31.How to Use jQuery to Set Textarea Max Length

> **HTML:**
```javascript
<textarea id="limit-text" rows="10" cols="20">
<span id="txt-length-left">Characters Left:</span>
```
> **JS:**
```javascript
$(document).ready(function() {
  var maxLen = 50;
  $('#limit-txt').keypress(function(event) {
    var Length = $("#limit-txt").val().length;
    var AmountLeft = maxLen - Length;
    $('#txt-length-left').html(AmountLeft);
    if (Length >= maxLen) {
      if (event.which != 48) {
        return false;
      }
    }
  });
});
```

#### 32.How to Dynamically Open External Links in New Window

```javascript
$('a').each(function() {
   var a = new RegExp('/' + window.location.host + '/');
   if(!a.test(this.href)) {
      $(this).click(function(event) {
          event.preventDefault();
          event.stopPropagation();
          window.open(this.href, '_blank');
      });
   }
});
```

#### 33.jQuery Snippets: How to Add/Remove Classes After Delay

```javascript
var header = $('#header');
header.addClass('blue');
setTimeout(function() {
  header.removeClass('blue');
}, 4000);
```

#### 34.Remove all inline styles

> **Remove all inline styles from the HTML page:**
```javascript
$(document).ready(function() {
  $("* [style]").removeAttr("style");
})
```

> **Remove inline styles from the element:**
```javascript
$(document).ready(function() {
  $("div").removeAttr("style");
});
```
#### 35.How to Use jQuery to Search and Replace HTML
```javascript
$(function() {
  $(":contains(FIND)").not(":has(:contains(FIND))").each(function() {
    var that = $(this),
      html = that.html();
    html = html.replace(/(\(FIND:.*?\))/g, "REPLACE-WITH");
    that.html(html);
  });
});
```
#### 36.How to Use jQuery’s .blur() Method
> **HTML:**
```javascript
<input type=”text” class=”email”>
```
> **Remove all inline styles from the HTML page:**
```javascript
$(“.email”).blur(function() {
  $(this).fadeOut();
})
```
#### 37.Set/Get/Delete Cookies with jQuery
> **Set cookies:**
```javascript
function setCookie(name, value, expires, path, domain, secure) {
  var today = new Date();
  today.setTime(today.getTime());
  if (expires) {
    expires = expires * 1000 * 60 * 60 * 24;
  }
  var expires_date = new Date(today.getTime() + (expires));
  document.cookie = name + '=' + escape(value) +
    ((expires) ? ';expires=' + expires_date.toGMTString() : '') + //expires.toGMTString()
    ((path) ? ';path=' + path : '') +
    ((domain) ? ';domain=' + domain : '') +
    ((secure) ? ';secure' : '');
}
```
> **Get cookies:**
```javascript
function getCookie(name) {
  var start = document.cookie.indexOf(name + "=");
  var len = start + name.length + 1;
  if ((!start) && (name != document.cookie.substring(0, name.length))) {
    return null;
  }
  if (start == -1) return null;
  var end = document.cookie.indexOf(';', len);
  if (end == -1) end = document.cookie.length;
  return unescape(document.cookie.substring(len, end));
}
```
> **Delete cookies:**
```javascript
function deleteCookie(name, path, domain) {
  if (getCookie(name)) document.cookie = name + '=' +
    ((path) ? ';path=' + path : '') +
    ((domain) ? ';domain=' + domain : '') +
    ';expires=Thu, 01-Jan-1970 00:00:01 GMT';
}
```

#### 37. Change DIV background color randomly
> **Set cookies:**
```javascript
$(document).ready(function() {
  changeColor();
});

function changeColor() {
  var rndColors = ["#00FF00", "#CCCCCC", "#995499", "#FFFFFF", "#FF9900"];
  var selColor = Math.floor(Math.random() * rndColors.length);
  $('div').css("background-color", rndColors[selColor]);
  setTimeout(changeColor, 1000);
}
```

#### 38. 
> **Set cookies:**
```javascript

```

#### 39. 
> **Set cookies:**
```javascript

```

#### 40. 
> **Set cookies:**
```javascript

```

#### 41. 
> **Set cookies:**
```javascript

```

#### 42. 
> **Set cookies:**
```javascript

```

#### 43. 
> **Set cookies:**
```javascript

```

#### 44. 
> **Set cookies:**
```javascript

```

#### 45. 
> **Set cookies:**
```javascript

```

#### 46. 
> **Set cookies:**
```javascript

```

#### 47. 
> **Set cookies:**
```javascript

```

#### 48. 
> **Set cookies:**
```javascript

```

#### 49. 
> **Set cookies:**
```javascript

```

#### 50. 
> **Set cookies:**
```javascript

```

#### 51. 
> **Set cookies:**
```javascript

```

#### 52. 
> **Set cookies:**
```javascript

```

#### 53. 
> **Set cookies:**
```javascript

```

#### 54. 
> **Set cookies:**
```javascript

```

#### 55. 
> **Set cookies:**
```javascript

```
