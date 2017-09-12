# Purpose:
 Find all results fit for condition of Regular Expression.
# How to build a Regular Expression:
 Refer on [www.taphuan.vn](http://www.taphuan.vn/2015/05/xu-ly-chuoi-voi-regular-expression.html).
# Examples:
```
var reUserName = /(<p class="d-chat_timeline-name">)(\S\D{1,500}\:[0-9]{1,10}\D)(<\/p>)/gi;   
var reGroupName = /(<h1 class="autotrim">)(\S.{1,500})(<\/h1>)/gi;   
var reDateTime = /(<li>)(\d{4}年\d{1,2}月\d{1,2}日 \d{1,2}:\d{1,2})(<\/li>)/gi;
var reMail = /([a-zA-Z0-9._-]+@[a-zA-Z0-9._-]+\.[a-zA-Z0-9._-]+)/gi;
var rePhoneNumber = /((\+84|0)+[0-9]{9,10}(?![0-9]))|(((0|\+81)\d{1,3})-(\d{3,4})-(\d{3,4}))/gi;
```
 