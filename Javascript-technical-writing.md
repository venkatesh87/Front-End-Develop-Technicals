## I. Code JavaScript Flag :

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

```
#container {width: 400px;height: 400px;position: relative;background: yellow;}
#animate {width: 50px;height: 50px;position: absolute; background-color: red;}
<button onclick="myMove()">Click Me</button>
<div id ="container">
<div id ="animate"></div>

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

```
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

```
document.getElementById("myBtn").addEventListener("click", displayDate);
function displayDate(){
	 document.getElementById('demo').innerHTML = Date();
}
```

## II. Check length element :

**- Case 1: length-of-a-javascript-string**
```javascript
var str = "Hello World!";
var n = str.length;
```

**- Case 2: length-of-a-javascript-object** 

```javascript
Object.size = function(obj) {
  var size = 0,
    key;
  for (key in obj) {
    if (obj.hasOwnProperty(key)) size++;
  }
  return size;
};

// Get the size of an object
var size = Object.size(myArray);

```     

```javascript
Object.keys(myObject).length
```  


## III. Object :

### Length of a JavaScript object (or associative array)

**- The most robust answer:**
```javascript
var myArray = new Object();
myArray["firstname"] = "Gareth";
myArray["lastname"] = "Simpson";
myArray["age"] = 21;

Object.size = function(obj) {
    var size = 0, key;
    for (key in obj) {
        if (obj.hasOwnProperty(key)) size++;
    }
    return size;
};
// Get the size of an object
var size = Object.size(myArray);
```
**- Here's an update as of 2016 and widespread deployment of ES5 and beyond. For IE9+ and all other modern ES5+ capable browsers, you can use Object.keys() so the above code just becomes:**

```javascript
var size = Object.keys(myObj).length;
```
**- If you know you don't have to worry about hasOwnProperty checks, you can do this very simply:**

```javascript
Object.keys(myArray).length
```

**Use something as simple as:**

```javascript
Object.keys(obj).length
```
## IV. Array :

## V. API Youtube :

### Reference : https://developers.google.com/youtube/documentation/

**- Case iframe:**

[Iframe Api Reference](https://developers.google.com/youtube/iframe_api_reference)

**HTML**

```html
<div class="video_background">
    <div class="video_foreground">
        <iframe id="video" data-autoplay src="https://www.youtube.com/embed/XklyzzH47pU?enablejsapi=1&controls=0&showinfo=0&rel=0&autoplay=1&loop=1" frameborder="0" width="100%" height="100%" allowfullscreen></iframe>
    </div>
</div>
```
**JS**

```javascript
// https://developers.google.com/youtube/iframe_api_reference
// Inject YouTube API script
var tag = document.createElement('script');
tag.src = "//www.youtube.com/player_api";
var firstScriptTag = document.getElementsByTagName('script')[0];
firstScriptTag.parentNode.insertBefore(tag, firstScriptTag);
// global variable for the player
var player;
var is_playing = true;
var height_window = window.innerHeight;

// this function gets called when API is ready to use
function onYouTubePlayerAPIReady() {
    // create the global player from the specific iframe (#video)
    player = new YT.Player('video', {
        playerVars: {
            autoplay: 1,
            controls: 0,
            rel: 0,
            iv_load_policy: 3,
            showinfo: 0
        },
        events: {
            // call this function when player is ready to use
            'onReady': onPlayerReady,
            'onStateChange': onPlayerStateChange
        }
    });
}

function onPlayerReady(event) {
    // bind events
    var playButton = document.getElementById("play_button");
    var that = this;
    /*window.onscroll = function(){
        if(document.documentElement.scrollTop > height_window || document.documentElement.scrollTop > height_window){
            player.pauseVideo();
            playButton.className += " disable";
        }
        else{
            player.playVideo();
            playButton.className = playButton.className.replace('disable', '');
        }
    }*/

    playButton.addEventListener("click", function(click_event) {
        // console.log("playButton - click");
        if (is_playing) {
            player.pauseVideo();
            playButton.className += " disable";
        } else {
            player.playVideo();
            playButton.className = playButton.className.replace('disable', '');
        }
    });
    var muteButton = document.getElementById("mute_toggle");
    muteButton.addEventListener("click", function(click_event) {
        if (!player.isMuted()) {
            muteButton.className += " disable";
            player.mute();

        } else {
            muteButton.className = muteButton.className.replace('disable', '');
            player.unMute();
        }
    });
    event.target.playVideo();
}

// 5. The API calls this function when the player's state changes.
//    The function indicates that when playing a video (state=1),
//    the player should play for six seconds and then stop.
function onPlayerStateChange(event) {
    if (event.data == YT.PlayerState.PLAYING) {
        is_playing = true;
    } else {
        is_playing = false;
    }
}

function stopVideo() {
    player.pauseVideo();
}
function startVideo() {
    player.playVideo();
}
```
**- Get Thumbnail youtube:**

Copy link youtube dán vào đây.
**https://boingboing.net/features/getthumbs.html**

## VI. API Facebook:

## VII. Character :

```javascript
// Count character base on byte.
function wc(str) {
  var bc = 0;
  for (var i = 0; i < str.length; i++) {
    if (str.charCodeAt(i) < 0x100) {
      // case: ascii character.
      bc += 1;
    } else {
      // case: double byte character.
      bc += 2;
    }
  }
  return bc;
}
```

## VIII. document.querySelector():

```javascript
var demo1 = document.querySelector('.demo1'),
    demo2 = document.querySelector('.demo2'),
    demo3 = document.querySelector('.demo3');

function popSwitcher(el, emphasis = '') {
  el.addEventListener('click', function () {
    if (this.classList.contains('pop')) {
      this.classList.remove('pop','entrance' + emphasis);
      this.classList.add('unpop','exit' + emphasis);
    } else {
      this.classList.remove('unpop','exit' + emphasis);
      this.classList.add('pop','entrance' + emphasis);
    }
  }, false);
}

popSwitcher(demo1);
popSwitcher(demo2, '-emphasis');
popSwitcher(demo3, '-emphasis');
```
### IX.Reference : https://developers.facebook.com/docs/plugins

### X. Cách get data trong file Json

```javascript
- var random = jsonContent.featured[Math.floor(Math.random() * jsonContent.featured.length)];
    console.log(random)
- var random = jsonContent["featured"][Math.floor(Math.random()*jsonContent["featured"].length)];
```

## XI. Is it correct to use JavaScript Array.sort() method for shuffling?(Nó là đúng để sử dụng phương pháp JavaScript Array.sort () cho xáo trộn không?)

[stackoverflow shuffling random](http://stackoverflow.com/questions/962802/is-it-correct-to-use-javascript-array-sort-method-for-shuffling#962890)

```javascript
function shuffle(array) {
    var tmp, current, top = array.length;

    if(top) while(--top) {
        current = Math.floor(Math.random() * (top + 1));
        tmp = array[current];
        array[current] = array[top];
        array[top] = tmp;
    }

    return array;
}
```

### XII. Code writing techniques

>**Truyền ```object``` vào ```function```**
[Demo](https://codepen.io/mrfrk/pen/WzjweX)
```javascript
var data = {
  '#box1': '5',
  '#box2': '4',
  '#box3': '3',
  '#box4': '2',
  '#box5': '1',
  '#box6': '0'
}

var zindexer = (function() {
  Object.keys(data).map(function(key, index) {
    var select = document.querySelectorAll(key);
    if (select.length > 1)
      Array.prototype.forEach.call(select, function(item) {
        item.style.zIndex = data[key];
      });
    else
      select[0].style.zIndex = data[key];
  });
});
zindexer(data);

```