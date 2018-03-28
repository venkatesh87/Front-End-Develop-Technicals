#### 1. Code JavaScript Flag :
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

#### 2. Check active:
---

>**Switch class active:**

>**Case 1**
```javascript
$('selector').on('click', function(){
  $('selector').removeClass('active');
  $(this).addClass('active');
});
```

>**Case 2**

```javascript
$('selector').find('a').click(function() {
  var iscurrent = $(this).parent().hasClass('active');
  $('selector').find('li').removeClass('active');
  $(this).parent().addClass('active');
  return false;
});
```

>**Case 3** Index and active index

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

>**Case 4: ** Loop active jQuery

```javascript
var toggleSlide = function(){
    $("h1 .words span.active").removeClass().next().add("h1 .words span:first").last().addClass("active");
  }
  setInterval(toggleSlide, 1500);
````

>**Case 5: ** Loop active Javascript

```javascript

````

#### 2. Check length element :
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


#### 3. Object :

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
#### 4. Keyboard
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
