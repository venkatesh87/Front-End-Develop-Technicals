# SCSS

**Table of Contents**

1. [How It Works](#How-It-Works)
2. [BEM is an HTML Mirror](#Hang-Up-1)
3. [When to Define a Block, an Element, and a Modifier](#Hang-Up-2)
4. [When to Redefine a Block](#Hang-Up-3)
5. [Blocks in Blocks](#Hang-Up-4)

## How-It-Works

**Syntax:** **[block]__[element]--[modifier]**

- Tên lớp BEM bao gồm tối đa ba phần.
  1. **Block**: Phần tử cha ngoài cùng của thành phần được xác định là khối.
  2. **Element**: Trong bên trong phần component có thể là một or thêm con phần các phần tử.
  3. **Modifier**: Một khối hoặc phần tử có thể có một biến thể được biểu thị bằng một sửa đổi.

#### Component With No Elements or Modifiers

```javascript
<button class="btn"></button>
<style>
  .btn {}
</style>
```

#### Component With A Modifier

```
<!-- DO THIS -->
<button class="btn btn--secondary"></button>
<style>
  .btn {
    display: inline-block;
    color: blue;
  }
  .btn--secondary {
    color: green;
  }  
</style>
```

```
<!-- DON'T DO THIS -->
<button class="btn--secondary"></button>

<style>
  .btn--secondary {
    display: inline-block;
    color: green;
  }
</style>
```

#### Component With Elements

```
<!-- DO THIS -->
<figure class="photo">
  <img class="photo__img" src="me.jpg">
  <figcaption class="photo__caption">Look at me!</figcaption>
</figure>

<style>
  .photo { } /* Specificity of 10 */
  .photo__img { } /* Specificity of 10 */
  .photo__caption { } /* Specificity of 10 */
</style>

<!-- DON'T DO THIS -->
<figure class="photo">
  <img src="me.jpg">
  <figcaption>Look at me!</figcaption>
</figure>

<style>
  .photo { } /* Specificity of 10 */
  .photo img { } /* Specificity of 11 */
  .photo figcaption { } /* Specificity of 11 */
</style>
```

```
<!-- DO THIS -->
<figure class="photo">
  <img class="photo__img" src="me.jpg">
  <figcaption class="photo__caption">
    <blockquote class="photo__quote">
      Look at me!
    </blockquote>
  </figcaption>
</figure>

<style>
  .photo { }
  .photo__img { }
  .photo__caption { }
  .photo__quote { }
</style>


<!-- DON'T DO THIS -->
<figure class="photo">
  <img class="photo__img" src="me.jpg">
  <figcaption class="photo__caption">
    <blockquote class="photo__caption__quote"> <!-- never include more than one child element in a class name -->
      Look at me!
    </blockquote>
  </figcaption>
</figure>

<style>
  .photo { }
  .photo__img { }
  .photo__caption { }
  .photo__caption__quote { }
</style>
```

#### Element With Modifier

```javascript
<figure class="photo">
  <img class="photo__img photo__img--framed" src="me.jpg">
  <figcaption class="photo__caption photo__caption--large">Look at me!</figcaption>
</figure>

<style>
  .photo__img--framed {
    /* incremental style changes */
  }
  .photo__caption--large {
    /* incremental style changes */
  }
</style>
```

#### Style Elements Based on the Component Modifier

```
<!-- DO THIS -->
<figure class="photo photo--highlighted">
  <img class="photo__img" src="me.jpg">
  <figcaption class="photo__caption">Look at me!</figcaption>
</figure>

<style>
  .photo--highlighted .photo__img { }
  .photo--highlighted .photo__caption { }
</style>

<!-- DON'T DO THIS -->
<figure class="photo">
  <img class="photo__img photo__img--highlighted" src="me.jpg">
  <figcaption class="photo__caption photo__caption--highlighted">Look at me!</figcaption>
</figure>

<style>
  .photo__img--highlighted { }
  .photo__caption--highlighted { }
</style>
```

#### Multi-word Names

```
<!-- DO THIS -->
<div class="some-thesis some-thesis--fast-read">
  <div class="some-thesis__some-element"></div>
</div>

<style>
  .some-thesis { }
  .some-thesis--fast-read { }
  .some-thesis__some-element { }
</style>

<!-- DON'T DO THIS -->
// These class names are harder to read
<div class="somethesis somethesis--fastread">
  <div class="somethesis__someelement"></div>
</div>

<style>
  .somethesis { }
  .somethesis--fastread { }
  .somethesis__someelement { }
</style>
```

---

## Hang-Up-1: BEM is an HTML Mirror

```javascript
<section class="blog-post">
  <header class="blog-post__header">
    <h1 class="blog-post__header__title">...</h1>
  </header>
  <article class="blog-post__body">
    ...
  </article>
</section>
```

```javascript
<div class="hoverstates">
  <div class="hoverstates__grace">
    <div class="hoverstates__maddie">
      <div class="hoverstates__sam">...</div>
      <div class="hoverstates__lee">...</div>
    </div> 
  </div>
  <div class="hoverstates__ed">
    <div class="hoverstates__alexis">...</div>
  </div>
</div>
```

---

## Hang-Up #2: When to Define a Block, an Element, and a Modifier

```javascript
.block {
  // styles for .block
  &__element {
    // styles for .block__element
    &--modifier {
      // styles for .block__element--modifier
    }
  }
  &--modifier {
    // styles for .block--modifier
  }
}
```

---

## Hang-Up #3: When to Redefine a Block

```javascript
<div class="block">
  <div class="block__element-one">...</div>
  <div class="block__element-two new-block">
    <div class="new-block__element">...</div>
  </div>
</div>
```

```javascript
<div class="block">
  <div class="block__element-one">...</div>
  <div class="block__new-block">
    <div class="new-block">
      <div class="new-block__element">...</div>
    </div>
  </div>
</div>
```
---

## Hang-Up #4: Blocks in Blocks

```javascript
<div class="block">
  <div class="block__element-one">...</div>
  <div class="block__element-two new-block">
    <div class="new-block__element">...</div>
  </div>
</div>
```

```javascript
<div class="block">
  <div class="block__element-one">...</div>
  <div class="block__new-block">
    <div class="new-block">
      <div class="new-block__element">...</div>
    </div>
  </div>
</div>
```

---
