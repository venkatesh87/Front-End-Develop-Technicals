#### I. Rule image use with CSS or HTML
---

**1. ```<picture>```**

>HTML Code:
```javascript
<picture>
  <source media="(min-width: 650px)" srcset="img_pink_flowers.jpg">
  <source media="(min-width: 465px)" srcset="img_white_flower.jpg">
  <img src="img_orange_flowers.jpg" alt="Flowers" style="width:auto;">
</picture>
```

```javascript
<picture>
 <source srcset="mdn-logo-wide.png" media="(min-width: 600px)">
 <img src="mdn-logo-narrow.png" alt="MDN">
</picture>
```

```javascript
​<picture>
 <source srcset="mdn-logo.svg" type="image/svg+xml">
 <img src="mdn-logo.png" alt="MDN">
</picture>
```

**2. Img object-fit CSS**: fill | contain | cover | none | scale-down

>CSS Code:
```javascript
object-fit: fill;
object-fit: contain;
object-fit: cover;
object-fit: none;
object-fit: scale-down;
```

**3. Img CSS object-position**

>CSS Code:
```javascript
object-position: 50% 50%;
object-position: right top;
object-position: left bottom;
object-position: 250px 125px;
```

**4. <img>**

>JavaScript Code:
```javascript

```

**5. <img>**

>JavaScript Code:
```javascript

```

**6. <img>**

>JavaScript Code:
```javascript

```

**7. <img>**

>JavaScript Code:
```javascript

```