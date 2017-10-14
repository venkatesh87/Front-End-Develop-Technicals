## http://fizzy.school/

[Refer](http://fizzy.school/?utm_content=bufferc44ac&utm_medium=social&utm_source=facebook.com&utm_campaign=buffer)

1. Cache jQuery objects
---

- Making the same jQuery selections within functions and across code blocks.

#### Look out for

**JS**

```javascript
$('.photo-list').on( 'click', 'a', function( event ) {
  event.preventDefault();
  $('.gallery__image').attr( 'src', $( this ).attr('href') );
  $('.gallery__title').text( $( this ).text() );
  $('.gallery__caption').text( $( this ).attr('title') );
});

$('.reset-button').on( 'click', function() {
  $('.gallery__image').attr( 'src', 'https://dummyimage.com/240x240/AAA/fff' );
  $('.gallery__title').text( 'Photo title' );
  $('.gallery__caption').text( 'This is the photo caption' );
});
```

**HTML**

```javascript
<ul class="photo-list">
  <li><a href="https://s3-us-west-2.amazonaws.com/s.cdpn.io/82/cat-nose.jpg"
         title="Close up cat nose">Cat</a></li>
  <li><a href="https://s3-us-west-2.amazonaws.com/s.cdpn.io/82/contrail.jpg"
         title="Passing overhead we sailed into tomorrow">Contrail</a></li>
  <li><a href="https://s3-us-west-2.amazonaws.com/s.cdpn.io/82/drizzle.jpg"
         title="I heard the rain wash the streets">Drizzle</a></li>
  <li><a href="https://s3-us-west-2.amazonaws.com/s.cdpn.io/82/grapes.jpg"
         title="Oh the grapes, they had so much WRATH">Grapes</a></li>
  <li><a href="https://s3-us-west-2.amazonaws.com/s.cdpn.io/82/orange-tree.jpg"
         title="Pluck an orange from the tree">Orange tree</a></li>
  <li><a href="https://s3-us-west-2.amazonaws.com/s.cdpn.io/82/shore.jpg"
         title="Approaching the shoreline, waiting for the tide">Shore</a></li>
  <li><a href="https://s3-us-west-2.amazonaws.com/s.cdpn.io/82/submerged.jpg"
         title="Beneath the waves he could still hear them calling">Submerged</a></li>
  <li><a href="https://s3-us-west-2.amazonaws.com/s.cdpn.io/82/tulip.jpg"
         title="A present from a dewey morning">Tulip</a></li>
  <li><a href="https://s3-us-west-2.amazonaws.com/s.cdpn.io/82/van.jpg"
         title="Get in. I'll explain when we're on the road.">Van</a></li>
</ul>

<div class="gallery">
  <h2 class="gallery__title">Orange tree</h2>
  <img class="gallery__image" src="https://s3-us-west-2.amazonaws.com/s.cdpn.io/82/orange-tree.jpg" />
  <p class="gallery__caption">Pluck an orange from the tree<p>
</div>

<p><button class="reset-button">Reset photo</button></p>
```

**CSS**

```javascript
.photo-list {
  padding-left: 0;
}

.photo-list a { color: #05D; }

.photo-list li {
  display: inline-block;
  margin: 0 0.5em;
}

.photo-list {
  padding: 0;
  display: -webkit-box;
  display: flex;
  flex-wrap: wrap;
}

.photo-list li {
  display: block;
  margin: 0 0 5px;
  margin-right: -1px;
  text-decoration: none;
  color: #08E;
}

.photo-list a {
  text-decoration: none;
  display: block;
  padding: 10px;
  border: 1px solid #DDD;
  color: #08E;
}

.photo-list a:hover {
  background: #EEE;
}

.gallery__image {
  display: block;
  height: 240px;
}

button {
  font: inherit;
  padding: 10px 20px;
}

```

#### Resolve by

- Storing jQuery objects as variables so they can be reused.

**JS**

```javascript
// get jQuery selections
var $galleryImage = $('.gallery__image');
var $galleryTitle = $('.gallery__title');
var $galleryCaption = $('.gallery__caption');

$('.photo-list').on( 'click', 'a', function( event ) {
  event.preventDefault();
  // get clicked element
  var $link = $( this );
  // set image, title, & caption from clicked link
  $galleryImage.attr( 'src', $link.attr('href') );
  $galleryTitle.text( $link.text() );
  $galleryCaption.text( $link.attr('title') );
});

$('.reset-button').on( 'click', function() {
  $galleryImage.attr( 'src', 'https://dummyimage.com/240x240' );
  $galleryTitle.text( 'Photo title' );
  $galleryCaption.text( 'This is the photo caption' );
});

```

2. State variables
---
#### Look out for

**JS**

```javascript

```

**HTML**

```javascript

```

**CSS**

```javascript

```

#### Resolve by

**JS**

```javascript

```

**HTML**

```javascript

```

**CSS**

```javascript

```

3. Un-repeat with functions
---
#### Look out for

**JS**

```javascript

```

**HTML**

```javascript

```

**CSS**

```javascript

```

#### Resolve by

**JS**

```javascript

```

**HTML**

```javascript

```

**CSS**

```javascript

```

4. Replace jQuery's this
---
#### Look out for

**JS**

```javascript

```

**HTML**

```javascript

```

**CSS**

```javascript

```

#### Resolve by

**JS**

```javascript

```

**HTML**

```javascript

```

**CSS**

```javascript

```

5. Simplify selectors
---
#### Look out for

**JS**

```javascript

```

**HTML**

```javascript

```

**CSS**

```javascript

```

#### Resolve by

**JS**

```javascript

```

**HTML**

```javascript

```

**CSS**

```javascript

```

6. Hash maps
---
#### Look out for

**JS**

```javascript

```

**HTML**

```javascript

```

**CSS**

```javascript

```

#### Resolve by

**JS**

```javascript

```

**HTML**

```javascript

```

**CSS**

```javascript

```
