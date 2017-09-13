**Disable F12 Key in a Page**

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

**Disable Ctrl+U Key in a Page**

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

**Disable View Page Source Key in a Page Right Click Mouse**

```javascript
<body oncontextmenu="return false">
```

**Disable keyboard Ctrl+S:**

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

** Rendering a simple list of products with jQuery:**

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