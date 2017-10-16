## Jquery gallery photo json

1. Requirement
---

- Output text data và file image đang được setting ở JSON: 
  + Data dùng để chạy thực tế thì phía GD sẽ chèn vào nên nhờ các bạn tạo trước bằng image thích hợp.
- Hiển thị những phần bên dưới khi click vào image 
  + Hiển thị nội dung, image đại diện, title, button close.
  + Nếu là image đại diện là youtube: 
    + Trường hợp chèn youtube thì sẽ hiển thị icon ở nơi hiển thị image thumbnail 
    + Chỉ trường hợp đang mô tả URL vào node 「youtube_url」 của file JSON, thì hãy set để hiển thị Player của Youtube ở phần đã triển khai sau khi click vào image và có thể replay trong trường hợp đó.
- Hiển thị image khởi tạo thì đến 20 cái
  + Trường hợp data dưới 20 cái thì không hiển thị button More
  + Khung hiển thị thì cũng chỉ hiển thị số lượng cần thiết
  + Hiển thị 20 cái tiếp theo bằng cách click vào nút More
  + Trình tự hiển thị image thì hiển thị theo random: Hiển thị theo random ở mỗi lần load
  + Setting radom thì cố gắng set để có thể setting bằng đối số khi tham chiếu file javascript (Tham chiếu sheet「JS」): ```<script type="text/javascript" src="/cms8341/shared/js/setting_gallery.js?random=1"></script>```

### Code

**HTML**

```javascript
<div class="idx2_area">
  <div class="img_gallery js_render_gallery">
    <div class="js_loading load">
      <div class="loader_container">
        <div class="loader_image"></div>
      </div>
    </div>
    <div id="tmp_gallery_container">
      <ul class="img_gallery_list js_render_gallery_list">
                        
      </ul>
      <p class="more_btn2 js_loadmore"><a href="javascript:void(0)">More</a></p>
    </div>
  </div>
</div>
```

**JS**

```javascript
//CMS-8341用JS

(function($) {

  $(function() {
    /*init*/
    init();
  });

  var gallery = $('.js_render_gallery');
  var galleryList = $('.js_render_gallery_list');
  var photo = '.js_photo';
  var photoTarget = '.js_photo_target';
  var photoRender = '.js_photo_render';
  var photoClose = '.js_photo_close';
  var loadMore = $('.js_loadmore');
  var loadDing = $('.js_loading');
  var javascript = $("#settingGallery");
  var count = 0;
  var isRandom = false;
  var items = [];
  var random = javascript.attr('src').split('?')[1];
  random = parseInt(random.replace(/^\D+/g, ''));
  var limit = javascript.attr('src').split('?')[2];
  limit = parseInt(limit.replace(/^\D+/g, ''));
  var _start = 0;
  var _end = limit;

  /* Initialize */
  var init = function() {
    loadDing.show();
    loadMore.hide();
    _fetchData(_start, limit);
    _bind();
  };

  /* Fetch data from JSON */
  var _fetchData = function(_start, _end, _callback) {
    $.getJSON('/cms8341/shared/gallery/js/gallery.json', function(data) {
      loadDing.hide();
      items = _getData(random, data['items']);
      _renderData(_start, _end, items);
      
    });
  };

  var _renderData = function (_start, _end, _items) {
    if (count > _items.length) {
      return false;
    } else {
      if (_items.length > _end) {
        loadMore.show();
      } else {
        _end = _items.length;
        loadMore.hide();
      }
      if (_items.length >= _end) {
        for (var i = _start; i < _end; i++) {
          galleryList.append(_fetchItem(_items[i]));
        }
      }
    }
  };

  /* Bind Event */
  var _bind = function() {
    /* Show Preview detail */
    gallery.on('click', photoTarget, function() {
      var _this = $(this);
      _fetchDetail(_this);
      _renderPreview(_this);
      return false;
    });

    /* Close Preview detail */
    gallery.on('click', photoClose, function() {
      _closePreview($(this));
      return false;
    });

    /* Show more gallery items */
    loadMore.on('click', function() {
      _start += limit;
      _end = _start + limit;
      count += limit;
      _renderData(_start, _end, items);
      _scrollTop(loadMore.offset().top, 1000);
    });

  };

  /* Fetch Detail from @data */
  var _fetchDetail = function(_this, _callback) {
    var _title = _this.data('title');
    var _imageUrl = _this.data('image');
    var _summary = _this.data('summary');
    var _movie = _this.data('movie');
    var _youtubeUrl = _this.data('youtube');
    var _photoAppend = _this.closest(photo).find(photoRender);
    var _typeMedia = '';
    if (_movie == 'movie') {
      _typeMedia = '<iframe class="js_media" width="400" height="225" src="' + _youtubeUrl + '" frameborder="0" allowfullscreen=""></iframe>';
    } else {
      _typeMedia = '<img class="js_media" src="/cms8341/' + _imageUrl + '" width="400" height="300">';
    }
    var _tmp = '<div class="img_gallery_cnt">';
    _tmp += '<p class="img">';
    _tmp += '<span class="js_loading_item load">';
    _tmp += '<span class="loader_image"></span>';
    _tmp += '</span>';
    _tmp += _typeMedia;
    _tmp += '</p>';
    _tmp += '<div class="cnt">';
    _tmp += '<p class="ttl">' + _title + '</p>';
    _tmp += '<p class="txt">' + _summary + '</p>';
    _tmp += '</div>';
    _tmp += '<p class="close js_photo_close">';
    _tmp += '<a href="#"><img src="/cms8341/shared/templates/free/images/contents/img_gallery_close_btn.png" width="40" height="40" alt="close"></a>';
    _tmp += '</p>';
    _tmp += '</div>';

    if (!_photoAppend.hasClass('append')) {
      _photoAppend.addClass('append').html(_tmp);
    }

  };

  /* Fetch item from JSON */
  var _fetchItem = function(_item) {
    var _titleItem = _item['title'];
    var _detail = _item['detail'];
    var _thumb_image_path = _item['thumb_image_path'];
    _movie = _item['isyoutube'] ? 'movie' : '';
    var _tmpItem = '<li class="photo js_photo ' + _movie + '">';
    _tmpItem += '<p class="thumb">';
    _tmpItem += '<a class="js_photo_target" data-title="' + _detail['title'] + '" data-image="' + _detail['image_path'] + '" data-summary="' + _detail['summary'] + '" data-movie="' + _movie + '" data-youtube="' + _detail['youtube_url'] + '" href="#"><img src="' + _item['thumb_image_path'] + '" width="239" height="239" /><span>Kitano Ijinkan (Foreigners Residences)</span></a>';
    _tmpItem += '</p>';
    _tmpItem += '<div class="photo_render js_photo_render">';
    _tmpItem += '</div>';
    _tmpItem += '</li>';
    return _tmpItem;
  };

  /*Show preview Detail */
  var _renderPreview = function(_this) {
    if (!_this.closest(photo).hasClass('active')) {
      var _photoAppend = _this.closest(photo).find(photoRender);
      var _height = _photoAppend.outerHeight();
      $(photo).removeClass('active');
      _photoAppend.css('height', 0);
      _photoAppend.animate({ height: _height }, 500);
      if (typeof(_photoAppend.find('.js_media').attr('style')) == 'undefined') {
        _photoAppend.find('.js_loading_item').show();
        _photoAppend.find('.js_media').on("load", function() {
          setTimeout(function() {
            _photoAppend.find('.js_loading_item').hide();
            _photoAppend.find('.js_media').css('opacity', 1);
            _scrollTop(_this.offset().top - (_height / 2 + 80), 300);
          }, 200);
        });
      } else {
        _scrollTop(_this.offset().top - (_height / 2 + 80), 300);
      }
      _this.closest(photo).addClass('active');
    }
  };

  /*Close preview Detail */
  var _closePreview = function(_this) {
    _this.closest(photo).find(photoRender).animate({ height: 0 }, 500);
    setTimeout(function() {
      _this.closest(photo).find(photoRender).css('height', 'auto');
      _this.closest(photo).removeClass('active');
    }, 510);
  };

  /*Get DATA @default or @random */
  var _getData = function(_type, _data) {
    if (_type == 1) {
      var newItems = _data;
      var random = '';
      // Is random
      var max = _data.length;
      var tmp, current, top = newItems.length;
      if (top) {
        while (--top) {
          current = Math.floor(Math.random() * (top + 1));
          tmp = newItems[current];
          newItems[current] = newItems[top];
          newItems[top] = tmp;
        }
        _data = newItems;
      }
    } else {
      _data = _data;
    }
    return _data;
  };

  var randomItems = function(_items) {
    var newItems = [];

    for (var i = 0; i < ms.length; i++) {

      newItems[i]
    }
  }

  var _scrollTop = function(_offset, _time) {
    $('html, body').animate({
      scrollTop: _offset
    }, _time);
  };

})(jQuery);

```

**JSON**

```javascript
{
  "items": [
    {
      "id": 0,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/1.jpg",
      "isyoutube": false,
      "detail": {
        "title": "Title 1",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/1.jpg",
        "youtube_url": ""

      }
    },
    {
      "id": 1,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/2.jpg",
      "isyoutube": true,
      "detail": {
        "title": "Title 2",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/2.jpg",
        "youtube_url": "https://www.youtube.com/embed/pUAe9qpuAMA"
      }
    },
    {
      "id": 2,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/3.jpg",
      "isyoutube": false,
      "detail": {
        "title": "Title 3",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/3.jpg",
        "youtube_url": ""
      }
    },
    {
      "id": 3,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/4.jpg",
      "isyoutube": false,
      "detail": {
        "title": "Title 4",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/4.jpg",
        "youtube_url": ""
      }
    },
    {
      "id": 4,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/5.jpg",
      "isyoutube": false,
      "detail": {
        "title": "Title 5",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/5.jpg",
        "youtube_url": ""
      }
    },
    {
      "id": 5,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/6.jpg",
      "isyoutube": false,
      "detail": {
        "title": "Title 6",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/6.jpg",
        "youtube_url": ""
      }
    },
    {
      "id": 6,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/7.jpg",
      "isyoutube": false,
      "detail": {
        "title": "Title 7",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/7.jpg",
        "youtube_url": ""
      }
    },
    {
      "id": 7,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/8.jpg",
      "isyoutube": false,
      "detail": {
        "title": "Title 8",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/8.jpg",
        "youtube_url": ""
      }
    },
    {
      "id": 8,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/9.jpg",
      "isyoutube": false,
      "detail": {
        "title": "Title 9",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/9.jpg",
        "youtube_url": ""
      }
    },
    {
      "id": 9,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/10.jpg",
      "isyoutube": false,
      "detail": {
        "title": "Title 10",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/10.jpg",
        "youtube_url": ""
      }
    },
    {
      "id": 10,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/11.jpg",
      "isyoutube": false,
      "detail": {
        "title": "Title 11",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/11.jpg",
        "youtube_url": ""
      }
    },
    {
      "id": 11,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/12.jpg",
      "isyoutube": false,
      "detail": {
        "title": "Title 12",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/12.jpg",
        "youtube_url": ""
      }
    },
    {
      "id": 12,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/13.jpg",
      "isyoutube": false,
      "detail": {
        "title": "Title 13",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/13.jpg",
        "youtube_url": ""
      }
    },
    {
      "id": 13,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/14.jpg",
      "isyoutube": false,
      "detail": {
        "title": "Title 14",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/14.jpg",
        "youtube_url": ""
      }
    },
    {
      "id": 14,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/15.jpg",
      "isyoutube": false,
      "detail": {
        "title": "Title 15",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/15.jpg",
        "youtube_url": ""
      }
    },
    {
      "id": 15,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/16.jpg",
      "isyoutube": false,
      "detail": {
        "title": "Title 16",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/16.jpg",
        "youtube_url": ""
      }
    },
    {
      "id": 16,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/17.jpg",
      "isyoutube": false,
      "detail": {
        "title": "Title 17",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/17.jpg",
        "youtube_url": ""
      }
    },
    {
      "id": 17,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/18.jpg",
      "isyoutube": false,
      "detail": {
        "title": "Title 18",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/18.jpg",
        "youtube_url": ""
      }
    },
    {
      "id": 18,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/19.jpg",
      "isyoutube": true,
      "detail": {
        "title": "Title 19",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/19.jpg",
        "youtube_url": "https://www.youtube.com/embed/pUAe9qpuAMA"
      }
    },
    {
      "id": 19,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/20.jpg",
      "isyoutube": false,
      "detail": {
        "title": "Title 20",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/20.jpg",
        "youtube_url": ""
      }
    },
    {
      "id": 20,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/21.jpg",
      "isyoutube": true,
      "detail": {
        "title": "Title 21",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/21.jpg",
        "youtube_url": "https://www.youtube.com/embed/pUAe9qpuAMA"
      }
    },
    {
      "id": 21,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/22.jpg",
      "isyoutube": false,
      "detail": {
        "title": "Title 22",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/22.jpg",
        "youtube_url": ""
      }
    },
    {
      "id": 22,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/23.jpg",
      "isyoutube": true,
      "detail": {
        "title": "Title 23",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/23.jpg",
        "youtube_url": "https://www.youtube.com/embed/pUAe9qpuAMA"
      }
    },
    {
      "id": 23,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/24.jpg",
      "isyoutube": false,
      "detail": {
        "title": "Title 24",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/24.jpg",
        "youtube_url": ""
      }
    },
    {
      "id": 24,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/25.jpg",
      "isyoutube": true,
      "detail": {
        "title": "Title 25",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/25.jpg",
        "youtube_url": "https://www.youtube.com/embed/pUAe9qpuAMA"
      }
    },
    {
      "id": 25,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/26.jpg",
      "isyoutube": false,
      "detail": {
        "title": "Title 26",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/26.jpg",
        "youtube_url": ""
      }
    },
    {
      "id": 26,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/27.jpg",
      "isyoutube": true,
      "detail": {
        "title": "Title 27",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/27.jpg",
        "youtube_url": "https://www.youtube.com/embed/pUAe9qpuAMA"
      }
    },
    {
      "id": 27,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/28.jpg",
      "isyoutube": true,
      "detail": {
        "title": "Title 28",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/28.jpg",
        "youtube_url": "https://www.youtube.com/embed/pUAe9qpuAMA"
      }
    },
    {
      "id": 28,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/29.jpg",
      "isyoutube": false,
      "detail": {
        "title": "Title 29",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/29.jpg",
        "youtube_url": ""
      }
    },
    {
      "id": 29,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/30.jpg",
      "isyoutube": true,
      "detail": {
        "title": "Title 30",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/30.jpg",
        "youtube_url": "https://www.youtube.com/embed/pUAe9qpuAMA"
      }
    },
    {
      "id": 30,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/31.jpg",
      "isyoutube": false,
      "detail": {
        "title": "Title 31",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/31.jpg",
        "youtube_url": ""

      }
    },
    {
      "id": 31,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/32.jpg",
      "isyoutube": true,
      "detail": {
        "title": "Title 32",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/32.jpg",
        "youtube_url": "https://www.youtube.com/embed/pUAe9qpuAMA"
      }
    },
    {
      "id": 32,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/33.jpg",
      "isyoutube": false,
      "detail": {
        "title": "Title 33",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/33.jpg",
        "youtube_url": ""
      }
    },
    {
      "id": 33,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/34.jpg",
      "isyoutube": false,
      "detail": {
        "title": "Title 34",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/34.jpg",
        "youtube_url": ""
      }
    },
    {
      "id": 34,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/35.jpg",
      "isyoutube": false,
      "detail": {
        "title": "Title 35",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/35.jpg",
        "youtube_url": ""
      }
    },
    {
      "id": 35,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/36.jpg",
      "isyoutube": false,
      "detail": {
        "title": "Title 36",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/36.jpg",
        "youtube_url": ""
      }
    },
    {
      "id": 36,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/37.jpg",
      "isyoutube": false,
      "detail": {
        "title": "Title 37",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/37.jpg",
        "youtube_url": ""
      }
    },
    {
      "id": 37,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/38.jpg",
      "isyoutube": false,
      "detail": {
        "title": "Title 38",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/38.jpg",
        "youtube_url": ""
      }
    },
    {
      "id": 38,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/39.jpg",
      "isyoutube": false,
      "detail": {
        "title": "Title 39",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/39.jpg",
        "youtube_url": ""
      }
    },
    {
      "id": 39,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/40.jpg",
      "isyoutube": false,
      "detail": {
        "title": "Title 40",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/40.jpg",
        "youtube_url": ""
      }
    },
    {
      "id": 40,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/41.jpg",
      "isyoutube": false,
      "detail": {
        "title": "Title 41",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/41.jpg",
        "youtube_url": ""
      }
    },
    {
      "id": 41,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/42.jpg",
      "isyoutube": false,
      "detail": {
        "title": "Title 42",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/42.jpg",
        "youtube_url": ""
      }
    },
    {
      "id": 42,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/43.jpg",
      "isyoutube": false,
      "detail": {
        "title": "Title 43",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/43.jpg",
        "youtube_url": ""
      }
    },
    {
      "id": 43,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/44.jpg",
      "isyoutube": false,
      "detail": {
        "title": "Title 44",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/44.jpg",
        "youtube_url": ""
      }
    },
    {
      "id": 44,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/45.jpg",
      "isyoutube": false,
      "detail": {
        "title": "Title 45",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/45.jpg",
        "youtube_url": ""
      }
    },
    {
      "id": 45,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/46.jpg",
      "isyoutube": false,
      "detail": {
        "title": "Title 46",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/46.jpg",
        "youtube_url": ""
      }
    },
    {
      "id": 46,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/47.jpg",
      "isyoutube": false,
      "detail": {
        "title": "Title 47",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/47.jpg",
        "youtube_url": ""
      }
    },
    {
      "id": 47,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/48.jpg",
      "isyoutube": false,
      "detail": {
        "title": "Title 48",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/48.jpg",
        "youtube_url": ""
      }
    },
    {
      "id": 48,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/49.jpg",
      "isyoutube": true,
      "detail": {
        "title": "Title 49",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/49.jpg",
        "youtube_url": "https://www.youtube.com/embed/pUAe9qpuAMA"
      }
    },
    {
      "id": 49,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/50.jpg",
      "isyoutube": false,
      "detail": {
        "title": "Title 50",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/50.jpg",
        "youtube_url": ""
      }
    },
    {
      "id": 50,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/51.jpg",
      "isyoutube": true,
      "detail": {
        "title": "Title 51",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/51.jpg",
        "youtube_url": "https://www.youtube.com/embed/pUAe9qpuAMA"
      }
    },
    {
      "id": 51,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/52.jpg",
      "isyoutube": false,
      "detail": {
        "title": "Title 52",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/52.jpg",
        "youtube_url": ""
      }
    },
    {
      "id": 52,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/53.jpg",
      "isyoutube": true,
      "detail": {
        "title": "Title 53",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/53.jpg",
        "youtube_url": "https://www.youtube.com/embed/pUAe9qpuAMA"
      }
    },
    {
      "id": 53,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/54.jpg",
      "isyoutube": false,
      "detail": {
        "title": "Title 54",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/54.jpg",
        "youtube_url": ""
      }
    },
    {
      "id": 54,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/55.jpg",
      "isyoutube": true,
      "detail": {
        "title": "Title 55",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/55.jpg",
        "youtube_url": "https://www.youtube.com/embed/pUAe9qpuAMA"
      }
    },
    {
      "id": 55,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/56.jpg",
      "isyoutube": false,
      "detail": {
        "title": "Title 56",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/56.jpg",
        "youtube_url": ""
      }
    },
    {
      "id": 56,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/57.jpg",
      "isyoutube": true,
      "detail": {
        "title": "Title 57",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/57.jpg",
        "youtube_url": "https://www.youtube.com/embed/pUAe9qpuAMA"
      }
    },
    {
      "id": 57,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/58.jpg",
      "isyoutube": true,
      "detail": {
        "title": "Title 58",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/58.jpg",
        "youtube_url": "https://www.youtube.com/embed/pUAe9qpuAMA"
      }
    },
    {
      "id": 58,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/59.jpg",
      "isyoutube": false,
      "detail": {
        "title": "Title 59",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/59.jpg",
        "youtube_url": ""
      }
    },
    {
      "id": 59,
      "title": "images tittle",
      "thumb_image_path": "/cms8341/shared/gallery/images/60.jpg",
      "isyoutube": true,
      "detail": {
        "title": "Title 60",
        "summary": "images summary texttexttexttexttexttexttexttexttexttexttexttexttexttexttext",
        "image_path": "/shared/gallery/images/60.jpg",
        "youtube_url": "https://www.youtube.com/embed/pUAe9qpuAMA"
      }
    }
  ]
}
```

