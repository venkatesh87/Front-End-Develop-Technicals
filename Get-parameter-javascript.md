http://stackoverflow.com/questions/2190801/passing-parameters-to-javascript-files

- Trong html gán ?random=1:
  <script id="myScript" type="text/javascript" src="/cms8341/shared/gallery/js/setting_gallery.js?random=1"></script>
- Trong JS:
  var queryString = $("script[src*='/cms8341/shared/gallery/js/setting_gallery.js']").attr('src').split('?')[1];
  console.log(queryString);

- var myScript = document.getElementById("myScript").getAttribute("src").split('?')[1];
- console.log(myScript);

- var javascript = $("#settingGallery");
- var random = javascript.attr('src').split('?')[1];
- random = parseInt(random.replace(/^\D+/g, ''));