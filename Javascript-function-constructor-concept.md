## I. Javascript function declare and constructor :

**- Case 1:**

```javascript
var fnName1 = function(){
  
};
fnName1();
```

```javascript
var fnName1 = function(){
  
};
fnName1();
```

**- Case 2:**

```javascript
var myIIFE = function() {
  // write your js code here
};
//==> Boc () toan bo function
(function(){
  // write your js code here
});
// ==> Them 1 cap ngoac don sau function, Day la bieu thuc IIFE, ham nay sau khi khai bao se chay luon chu ko phai doi call nua.
(function(){
  // write your js code here
})();
```

**- Case 3: function for jQuery**

```javascript
(function($) {
  

  $(function() {

  });

})(jQuery);
```
