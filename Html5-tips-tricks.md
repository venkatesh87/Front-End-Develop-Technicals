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

> **2.3 Nesting figure Inside Another figure
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

> **2.4 Correct Usage of figcaption
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

> **2.5 You Can Use Flow Elements in figcaption Too
```javascripts
<figure>
  <img src="dogs.jpg" alt="Group photo of dogs">
  <figcaption>
    <h2>Puppy School</h2>
    <p>Championship Class of 2016</p>
  </figcaption>
</figure>
```
