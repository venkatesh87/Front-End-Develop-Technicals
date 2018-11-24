##### 1. Code JavaScript Flag :
---

>**Case 1:**
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

>**Case 2:** 

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

##### 2. Check active:
---

>**Switch class active:**

>**Case 1**
```javascript

```

>**Case 5:** Loop active Javascript

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

##### 3. Check length element :
---
>**Case 1: length-of-a-javascript-string**
```javascript
var str = "Hello World!";
var n = str.length;
```

>**Case 2: length-of-a-javascript-object** 

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

##### 4. Object :
---
>**Length of a JavaScript object (or associative array)**

>**The most robust answer:**
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
>**- Here's an update as of 2016 and widespread deployment of ES5 and beyond. For IE9+ and all other modern ES5+ capable browsers, you can use Object.keys() so the above code just becomes:**

```javascript
var size = Object.keys(myObj).length;
```
>**- If you know you don't have to worry about hasOwnProperty checks, you can do this very simply:**

```javascript
Object.keys(myArray).length
```

>**Use something as simple as:**

```javascript
Object.keys(obj).length
```
##### 5. Keyboard
---

>**Disable F12 Key in a Page**

```javascript
document.onkeypress = function (event) {  
  event = (event || window.event);  
  if (event.keyCode == 123) {  
    return false;  
  }                                                           
}  
document.onkeydown = function (event) {  
  event = (event || window.event);  
  if (event.keyCode == 123) {  
    return false;  
  }  
}
```

>**Disable Ctrl+U Key in a Page**

```javascript
document.onkeydown = function(e) {
  if (e.ctrlKey &&
    (e.keyCode === 67 ||
      e.keyCode === 86 ||
      e.keyCode === 85 ||
      e.keyCode === 117)) {
    alert('not allowed');
    return false;
  } else {
    return true;
  }
};
```

>**Disable View Page Source Key in a Page Right Click Mouse**

```javascript
<body oncontextmenu="return false">
```

>**Disable keyboard Ctrl+S:**

```javascript
document.onkeydown = function (e) {
    e = e || window.event;//Get event
    if (e.ctrlKey) {
        var c = e.which || e.keyCode;//Get key code
        switch (c) {
            case 83://Block Ctrl+S
                e.preventDefault();     
                e.stopPropagation();
            break;
        }
    }
};
```

>**Rendering a simple list of products with jQuery:**

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

##### 5. Scroll
---
>**Case 1: ```document.body.scrollTop > 20 || document.documentElement.scrollTop```**
```javascript
window.onscroll = function() {
    if ($(window).width() < 700) {
        navSticky();
    }
};
function navSticky() {
  if (document.body.scrollTop > 20 || document.documentElement.scrollTop > 20) {
    $('.navigation_top').addClass('sticky');
  } else {
    $('.navigation_top').removeClass('sticky');
  }
}
```
>**Case 2:** Scroll Indicator
```javascript
// When the user scrolls the page, execute myFunction 
window.onscroll = function() {myFunction()};

function myFunction() {
  var winScroll = document.body.scrollTop || document.documentElement.scrollTop;
  var height = document.documentElement.scrollHeight - document.documentElement.clientHeight;
  var scrolled = (winScroll / height) * 100;
  document.getElementById("myBar").style.width = scrolled + "%";
}
```

>**```window.pageYOffset```**
```javascript

```

##### 6. Keyboard
---
>**```window.pageYOffset```**
```javascript

```
