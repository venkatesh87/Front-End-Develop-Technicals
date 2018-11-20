#### JQuery Technical Writing
---

## 1. Code JavaScript Flag :

**- Case 1:**

```javascript
  window.DEBUG = true;

  function log(a, b, c, d) {
       if(DEBUG) {
           console.log(a, b, c, d);
       }
  } 

  if(DEBUG) {
      // Do dev stuff
  } else {
     // Do produection stuff
  }

  log("foobar") // Does not need to be wrapper, as log() itself is functional only in debug mode    
```

```javascript
var isClicked = false;
$(this).on('click', '.ic-rating', function() {
    isClicked = true;
    $(this).addClass('selected');
});
$(this).on('click', '.ic-rating.selected', function() {
    if (isClicked) {
        $(this).removeClass('selected');
    }
});
```

**- Case 2:** 

```javascript
var is_playing = true;
if (is_playing) {
  player.pauseVideo();
  playButton.className += " disable";
} else {
  player.playVideo();
  playButton.className = playButton.className.replace('disable', '');
}
```

**- Case 3:** 

```javascript
stopBodyScrolling(true);

stopBodyScrolling(false);

function stopBodyScrolling (bool) {
    if (bool === true) {
        document.body.addEventListener("touchmove", freezeVp, false);
    } else {
        document.body.removeEventListener("touchmove", freezeVp, false);
    }
}

var freezeVp = function(e) {
    e.preventDefault();
};
```

**- Case 4:**

```javascript
#container {width: 400px;height: 400px;position: relative;background: yellow;}
#animate {width: 50px;height: 50px;position: absolute; background-color: red;}
<button onclick="myMove()">Click Me</button>
<div id ="container">
<div id ="animate"></div>
```

```javascript
function myMove() {
  var elem = document.getElementById("animate");   
  var pos = 0;
  var id = setInterval(frame, 5);
  function frame() {
    if (pos == 350) {
      clearInterval(id);
    } else {
      pos++; 
      elem.style.top = pos + 'px'; 
      elem.style.left = pos + 'px'; 
    }
  }
}
```
**- Case 5:**

```javascript
function checkCookies() {
    var text = "";
    if (navigator.cookieEnabled == true) {
      text = "Cookies are enabled.";
    } else {
      text = "Cookies are not enabled.";
    }
    document.getElementById("demo").innerHTML = text;
}
```

**- Case 6:** Khi gọi một function trong function thì hãy bỏ cặp dấu ngoặc này () đi, ```displayDate```, ```frame```.

```javascript
document.getElementById("myBtn").addEventListener("click", displayDate);
function displayDate(){
  document.getElementById('demo').innerHTML = Date();
}
```

**2. Funtion parameters**

>JavaScript Code:
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

**2. Funtion switch**

>JavaScript Code:
```javascript
$('.address-table .js-dropdown-target').on('change', function() {
  var _this = $(this);
  var _dataId = _this.data('id');
  var _value = _this.val();
  
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

**3. Funtion switch**

>JavaScript Code:
```javascript
$('.container-sortable .table > tbody > tr').on('click', '.action-edit', function() {
  var userId = parseInt($(this).parents("tr").attr("id"));
  var groupList = ["総務部", "人事部", "海外事業部", "営業部", "マーケティング部", "キャリアサポート部"];
  var cbs = {
    "1": [1, 1, 1, 1, 0, 0],
    "2": [0, 1, 1, 1, 0, 0],
    "3": [0, 1, 1, 1, 0, 0],
    "4": [0, 1, 1, 1, 0, 0],
    "5": [0, 1, 1, 1, 0, 0],
    "6": [0, 1, 1, 1, 0, 0],
    "7": [0, 0, 1, 1, 0, 0],
    "8": [0, 0, 1, 1, 0, 0],
    "9": [0, 0, 1, 1, 0, 0],
  };
  showGroupList(userId, groupList, cbs);
});
```

```javascript
function showGroupList(userId, groupList, cbs) {
  var editModal = $(".modal-edit");
  var isSelected = "";
  var list;
  editModal.on('show.bs.modal', function() {
    list = '<ul class="radio-list">';
    var box = $(".modal-edit .scroll-checkbox");
    $.each(groupList, function(idx) {
      if (cbs[userId + 1 + ""][parseInt(idx)] == 1) {
        isSelected = "checked";
      } else {
        isSelected = "";
      }
      list += '<li><div class="checkbox-regular"><input id="checkbox-edit-' + (idx + 1) + '" class= "cus-cb" value="' + (idx + 1) + '" data-id="' + (idx + 1) + '" type="checkbox" ' + isSelected + '><label class= "cus-cb-label" for="checkbox-edit-' + (idx + 1) + '"><span class= "push-number">' + (idx + 1) + '</span>：' + groupList[idx] + ' </label></div></li>';
    });
    list += '</ul>';
    box.html(list);
  });
}
```

**4. Funtion combined function**

>JavaScript Code:
```javascript

```

**5. Funtion Render Data**

>JavaScript Code:
```javascript
function renderData() {
  $('.Data .listItem').each(function(index) {
    var tmpList = $('.slidersList');
    var Image = $(this).find('.Image img').attr('src');
    var Heading = $(this).find('.Heading').text();
    var Title = $(this).find('.Title').text();
    var Time = $(this).find('.Time').text();
    var Summary = $(this).find('.Summary').text();
    var tmpItem = '<div class="slideItem slideItem' + (index + 1) + '">' +
      '<h2 class="slideTitle"><a href="#" class="highLight">' + Heading + '</span></h2>' +
      '<div class="balloonsImage">' +
      '<div class="imageRepresentInner">' +
      '<img src="' + Image + '" alt="Represent" width="896" height="896">' +
      '</div>' +
      '</div>' +
      '<div class="balloonsDetail">' +
      '<div class="articleInner">' +
      '<h3 class="balloonTitle"><a href="#">' + Title + '</a></h3>' +
      '<p class="dateTime">' + Time + '</p>' +
      '<p class="balloonsCaption"><span>' + Summary + '<span></p>' +
      '</div>' +
      '</div>' +
      '</div>'
    tmpList.append(tmpItem);
  });
}
```

**6. Chú ý về $(window).width() > 640)**
- ```$(window).width() > 640)```: Phải để ngoài ```$(window).scroll()```
>JavaScript Code:
```javascript
$(window).scroll(function() {
  if ($(window).width() > 640) {
    if ($(window).scrollTop() > offset.top) {
      menuFollow.selector.sideBar.stop().animate({
          marginTop: $(window).scrollTop() - offset.top + topPadding
      }, 650);
    } else {
      menuFollow.selector.sideBar.stop().animate({
          marginTop: 0
      });
    }
  }
});
```

**7. Phán quyết vị trí được nhấp**
- Ẩn khi focus ngoài vùng dropdown được hiển thị.
>JavaScript Code:
```javascript
$('#headerCorporateLogo').on("click", function() {
  $('.userMenu').stop(true, true).slideToggle();
});
$(document).on('click', function(e) {
  // ２．クリックされた場所の判定
  // console.log($(e.target).closest('#headerCorporateLogo').length );
  // console.log($(e.target).closest('.userMenu').length);
  // console.log(!$(e.target).closest('#headerCorporateLogo').length && !$(e.target).closest('.userMenu').length);

  if(!$(e.target).closest('#headerCorporateLogo').length && !$(e.target).closest('.userMenu').length){
      $('.userMenu').fadeOut();
  }
});

```

**8. **

>JavaScript Code:
```javascript

```

**9. **

>JavaScript Code:
```javascript

```

**10. **

>JavaScript Code:
```javascript

```

**11. **

>JavaScript Code:
```javascript

```

**12. **

>JavaScript Code:
```javascript

```

**13. **

>JavaScript Code:
```javascript

```

**14. **

>JavaScript Code:
```javascript

```

**15. **

>JavaScript Code:
```javascript

```

**16. **

>JavaScript Code:
```javascript

```

**17. **

>JavaScript Code:
```javascript

```

**18. **

>JavaScript Code:
```javascript

```

**19. **

>JavaScript Code:
```javascript

```

**20. **

>JavaScript Code:
```javascript

```

**21. **

>JavaScript Code:
```javascript

```

**22. **

>JavaScript Code:
```javascript

```

**23. **

>JavaScript Code:
```javascript

```

**24. **

>JavaScript Code:
```javascript

```

**25. **

>JavaScript Code:
```javascript

```

**26. **

>JavaScript Code:
```javascript

```

**27. **

>JavaScript Code:
```javascript

```

**28. **

>JavaScript Code:
```javascript

```

**29. **

>JavaScript Code:
```javascript

```

**30. **

>JavaScript Code:
```javascript

```

**31. **

>JavaScript Code:
```javascript

```
**32. **

>JavaScript Code:
```javascript

```

**33. **

>JavaScript Code:
```javascript

```

**34. **

>JavaScript Code:
```javascript

```

**35. **

>JavaScript Code:
```javascript

```

