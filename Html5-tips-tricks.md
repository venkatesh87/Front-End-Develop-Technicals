### I. Tips and tricks
---
> **1. Video**

- Trình duyệt Internet Explorer 9:  MP4
- Firefox 4.0: WebM, Ogg
- Google Chrome 6: MP4,WebM, Ogg
- Apple Safari 5: MP4
- Opera 10.6: WebM, Ogg

```javascripts
<div class="audio">
    <audio controls>
        <source src="http://www.w3schools.com/tags/horse.ogg" type="audio/ogg">
        <source src="http://www.w3schools.com/tags/horse.mp3" type="audio/mpeg"> Your browser does not support the audio element.
    </audio>
    <p><strong>Chú ý:</strong> Thẻ audio không hỗ trợ Internet Explorer 8 và các phiên bản cũ hơn.</p>
</div>
<div class="video">
    <video width="320" height="240" controls>
        <source src="http://www.w3schools.com/tags/movie.mp4" type="video/mp4">
        <source src="http://www.w3schools.com/tags/movie.ogg" type="video/ogg"> Your browser does not support the video tag.
    </video>
    <p><strong>Chú ý:</strong> Thẻ video không hỗ trợ Internet Explorer 8 và các phiên bản cũ hơn.</p>
</div>
<div class="video">
    <video width="320" height="240" controls>
        <source src="https://www.w3schools.com/html/mov_bbb.mp4" type="video/mp4">
        <source src="https://www.w3schools.com/html/movie.ogg" type="video/ogg"> Your browser does not support the video tag.
    </video>
    <p><strong>Chú ý:</strong> Thẻ video không hỗ trợ Internet Explorer 8 và các phiên bản cũ hơn.</p>
</div>
```

- autoplay: Xác định trạng thái tự động chạy của video.
- controls: Hiển thị bộ điều khiển của video.
- height: Xác định chiều cao của video.
- width: Xác định chiều rộng của video.
- loop: Xác định video có được lặp lại hay không.
- muted: Tắt âm thanh khi mở video.
- poster: Xác định hình đại diện cho video.
- preload: Xác định việc tải video khi tải trang.

> **2. Details/Summary**

```javascripts
<h2>I'm having a party!</h2>
<details>
  BYOB. There will be pin the tail on the donkey. The pool will be warm. Shrimp on the barbie.  
</details>
```

```javascripts
<details>
  <summary>What is the population of New Orleans?</summary>
  According to 2010 Census Bureau estimates, New Orleans' population is made up of approximately 343,829 residents.
</details>

<details>
  <summary>What's a Po' Boy?</summary>
  A po' boy (also po-boy, po boy) is a traditional sandwich from Louisiana. It almost always consists of meat, which is usually roast beef or fried seafood, often shrimp, crawfish, fish, oysters or crab.
</details>

<details>
  <summary>How do I get to New Orleans?</summary>
  Use Google Maps.
</details>
```

> **2. Figure element**

> **2.1 The figure element is commonly used for images**
```javascripts
<figure>
  <img src="dog.jpg" alt="Maltese Terrier">
</figure>
```

> **2.2 Multiple Images in figure**
```javascripts
<figure>
  <img src="dog1.jpg" alt="Maltese Terrier">
  <img src="dog2.jpg" alt="Black Labrador">
  <img src="dog3.jpg" alt="Golden Retriever">
</figure>
<figure>
  <pre>
  <code>
    p {
        color: #333;
        font-family: Helvetica, sans-serif;
        font-size: 1rem;
    }
  </code>
</pre>
</figure>
```

> **2.3 Nesting figure Inside Another figure**
```javascripts
<figure role="group">
  <figcaption>Dog breeds</figcaption>
  <figure>
    <img src="dog1.jpg" alt="Maltese Terrier">
    <figcaption>Adorable Maltese Terrier</figcaption>
  </figure>
  <figure>
    <img src="dog2.jpg" alt="Black Labrador">
    <figcaption>Cute black labrador</figcaption>
  </figure>
</figure>
```

> **2.4 Correct Usage of figcaption**
```javascripts
<figure>
  <figcaption>Three different breeds of dog.</figcaption>
  <img src="dog1.jpg" alt="Maltese Terrier">
  <img src="dog2.jpg" alt="Black Labrador">
  <img src="dog3.jpg" alt="Golden Retriever">
</figure>
```
**OR:**
```javascripts
<figure>
  <img src="dog1.jpg" alt="Maltese Terrier">
  <img src="dog2.jpg" alt="Black Labrador">
  <img src="dog3.jpg" alt="Golden Retriever">
  <figcaption>Three different breeds of dog.</figcaption>
</figure>
```

> **2.5 You Can Use Flow Elements in figcaption Too**
```javascripts
<figure>
  <img src="dogs.jpg" alt="Group photo of dogs">
  <figcaption>
    <h2>Puppy School</h2>
    <p>Championship Class of 2016</p>
  </figcaption>
</figure>
```

> **3. Create a Responsive SVG**
- You should width = 100% and set attribute is preserveAspectRatio="none".

>**SVG Non-Responsive**
```javascripts
<?xml version="1.0" encoding="UTF-8" standalone="no"?>
<svg width="1440px" height="184px" viewBox="0 0 1440 184" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
    <!-- Generator: Sketch 49.3 (51167) - http://www.bohemiancoding.com/sketch -->
    <title>Banner Copy 2</title>
    <desc>Created with Sketch.</desc>
    <defs></defs>
    <g id="Page-1" stroke="none" stroke-width="1" fill="none" fill-rule="evenodd">
        <g id="Banner-Copy-2">
            <path d="M1439.90076,0 L1440,0 L1440,183 L0,183 L0,182.65625 C817.489956,174.070312 1258.10437,164.479167 1321.84325,153.882812 C1385.58213,143.286458 1424.96771,115.395833 1440,70.2109375 L1439.90076,0 Z" id="Combined-Shape" fill="#FFFFFF"></path>
            <path d="M1439.86021,1.81582461 L1440,1.81582461 L1440,70.8116742 C1424.96771,115.99657 1385.58213,143.887195 1321.84325,154.483549 C1258.10437,165.079903 817.489956,174.671049 0,183.256987 C816.891371,128.749174 1257.2065,96.1970909 1320.94537,85.6007367 C1384.68425,75.0043825 1424.32259,47.1172162 1439.86038,1.93923769 L1439.86021,1.81582461 Z" id="nam-tren" fill="#F2EAEA"></path>
        </g>
    </g>
</svg>
```

>**4. SVG Responsive**
```javascripts
<?xml version="1.0" encoding="UTF-8" standalone="no"?>
<svg width="100%" height="184px" viewBox="0 0 1440 184" preserveAspectRatio="none" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
  <!-- Generator: Sketch 49.3 (51167) - http://www.bohemiancoding.com/sketch -->
  <title>Banner Copy 2</title>
  <desc>Created with Sketch.</desc>
  <defs></defs>
  <g id="Page-1" stroke="none" stroke-width="1" fill="none" fill-rule="evenodd">
    <g id="Banner-Copy-2">
      <path d="M1439.90076,0 L1440,0 L1440,183 L0,183 L0,182.65625 C817.489956,174.070312 1258.10437,164.479167 1321.84325,153.882812 C1385.58213,143.286458 1424.96771,115.395833 1440,70.2109375 L1439.90076,0 Z" id="Combined-Shape" fill="#FFFFFF"></path>
      <path d="M1439.86021,1.81582461 L1440,1.81582461 L1440,70.8116742 C1424.96771,115.99657 1385.58213,143.887195 1321.84325,154.483549 C1258.10437,165.079903 817.489956,174.671049 0,183.256987 C816.891371,128.749174 1257.2065,96.1970909 1320.94537,85.6007367 C1384.68425,75.0043825 1424.32259,47.1172162 1439.86038,1.93923769 L1439.86021,1.81582461 Z" id="nam-tren" fill="#F2EAEA"></path>
    </g>
  </g>
</svg>
```

>**5. Hover Icons SVG**

```javascripts
.social--footer .social__item svg * {
  fill: #373f48
}
.social--footer .social__item a:hover svg * {
  fill: #ca9d81
}
.social--footer .social__item a svg * {
  -webkit-transition: fill ease .25s;
  -ms-transition: fill ease .25s;
  transition: fill ease .25s
}
```

