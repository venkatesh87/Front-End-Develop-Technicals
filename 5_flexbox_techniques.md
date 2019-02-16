## 5 Flexbox Techniques You Need to Know About

#### 1. Creating Equal Height Columns

**Reference :**
- [Css-Tricks](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)

> **HTML :**

```html
<div class="container">
    <!-- Equal height columns -->
    <div>...</div>
    <div>...</div>
    <div>...</div>
</div>
```

> **CSS :**

```javascript
.container {
        /* Initialize the flex model */
    display: flex;

        /* These are the default values but you can set them anyway */
    flex-direction: row;    /* Items inside the container will be positioned horizontally */
        align-items: stretch;   /* Items inside the container will take up it's entire height */
}
```

#### 2. Reordering Elements

> **HTML :**

```html
<div class="container">

    <!-- These items will appear in reverse order -->

    <div class="blue">...</div>
    <div class="red">...</div>
    <div class="green">...</div>
</div>
```

> **CSS:**

```javascript
.container{
    display: flex;
}

/* Reverse the order of elements */

.blue{
    order: 3;
}

.red{
    order: 2;
}

.green{
    order: 1;
}
```

#### 3. Horizontal And Vertical Centering

```html
<div class="container">
    <!-- Any element placed here will be centered
         both horizonally and vertically -->
    <div>...</div>
</div>
```

> **CSS:**

```javascript
.container{
    display: flex;

    /* Center according to the main axis */
    justify-content: center;

    /* Center according to the secondary axis */
        align-items: center;
}
```


#### 4. Creating Fully Responsive Grids

```html
<div class="container">

    <!-- This column will be 25% wide -->
    <div class="col-1">...</div>

    <!-- This column will be 50% wide -->
    <div class="col-2">...</div>

    <!-- This column will be 25% wide -->
    <div class="col-1">...</div>

</div>
```

> **CSS:**

```javascript
.container{
    display: flex;
}

/* Classes for each column size. */

.col-1{
    flex: 1;
}

.col-2{
    flex: 2;
}

@media (max-width: 800px){
    .container{
        /* Turn the horizontal layout into a vertical one. */
        flex-direction: column;     
    }
}
```


#### 5. Creating The Perfect Sticky Footer

```html
<body>

    <!-- All the page content goes here  -->

    <div class="main">...</div>

    <!-- Our sticky foooter -->

    <footer>...</footer>

</body>
```

> **CSS:**

```javascript
html{
    height: 100%;
}

body{
    display: flex;
    flex-direction: column;
    height: 100%;
}

.main{
   /* The main section will take up all the available free space
      on the page that is not taken up by the footer. */
   flex: 1 0 auto;
}

footer{
   /* The footer will take up as much vertical space as it needs and not a pixel more. */
   flex: 0 0 auto;
}
```

#### 6. Flex centering item and ziczac column

```javascript
.intro-list {
  padding: 0;
  margin: 0;
  list-style: none;
  .intro-item {
    margin: 0 -22px;
    padding: 30px 0;
    .intro-flex {
      @include flexbox();
      -webkit-flex-flow: row wrap;
      flex-flow: row wrap;
      align-items: center;
      justify-content: center;
      .intro-col{
        padding: 0 22px;
        float: left;
        width: 49.8%;
        @media (max-width: 1180px) {
          padding: 0 15px;
        }
        @media (max-width: 690px) {
          width: 100%;
          float: none;
        }
      }
    }
    &:nth-child(even) {
      .intro-flex {
        flex-direction: row-reverse;
      }
    }
    @media (max-width: 1180px) {
      margin: 0 -15px;
    }
    @media (max-width: 1050px) {
      padding: 20px 0;
    }
    @media (max-width: 690px) {
      padding: 0 0 10px;
    }
  }
}
```

#### 7. Grid with flex

```javascript

```

#### 8. ý nghĩa của flex-flow column

```javascript

```

#### 9. Equal height item with flex

```javascript

```
