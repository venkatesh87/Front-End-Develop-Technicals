### Media Queries in HTML

> **Case 1:**

```javascript
<link rel="stylesheet" media="all" href="cssbasic.css" />
<link rel="stylesheet" media="(min-width: 500px)" href="csswide.css" />
```
> **Case 2:**

```javascript
<link href="/cms8341/shared/style/smartphone.css" rel="stylesheet" media="only screen and (max-width : 480px)" type="text/css" id="tmp_smartphone_css" />
<link href="/cms8341/shared/templates/top/style/edit_sp.css" rel="stylesheet" media="only screen and (max-width : 480px)" type="text/css" id="tmp_smartphone_editcss" />
```

### Media Queries in CSS

> **Case 1:**

```javascript
@media screen and (max-width : 640px) {}
```

> **Case 2:**

```javascript
@media(max-width: 640px) {}
```

> **Case 3:**

```javascript
@media screen and (max-width: 1000px) and (min-width: 700px) {}
```

### Media Queries in JavaScript

> **How to Write Media Queries with JavaScript Code**

```javascript
const mq = window.matchMedia( "(min-width: 500px)" );
if (mq.matches) {
  // window width is at least 500px
} else {
  // window width is less than 500px
}
```

> **You can also add an event listener which fires when a change is detected:**

```javascript
// media query event handler
if (matchMedia) {
  const mq = window.matchMedia("(min-width: 500px)");
  mq.addListener(WidthChange);
  WidthChange(mq);
}

// media query change
function WidthChange(mq) {
  if (mq.matches) {
    // window width is at least 500px
  } else {
    // window width is less than 500px
  }

}
```

#### Demo:

> **HTML**

```javascript
<div id="page">
  <h1>JavaScript Media Queries</h1>
  <p>Current design: <strong id="current">unknown</strong></p>
  <section>
    <div class="element">element one</div>
    <div class="element">element two</div>
    <div class="element">element three</div>
  </section>
</div>
```
> **CSS**

```javascript
body {
  font-family: arial, sans-serif;
  font-size: 100%;
  margin: 10px;
  color: #222;
  background-color: #dfd;
}

#page {
  min-width: 200px;
  height: 100%;
  padding: 20px 30px;
  margin: 0 auto;
  background-color: #fff;
  border: 1px solid #999;
}

section {
  width: 100%;
  margin-bottom: 3em;
}

div.element {
  text-align: center;
  padding: 10px 0;
  margin: 4px;
  background-color: #dfd;
  border: 2px solid #666;
}

h1 {
  font-weight: normal;
  margin: 0 0 1em 0;
}

strong {
  color: #c00;
}

@media all and (min-width: 500px) {
  body {
    background-color: #ddf;
  }

  #page {
    max-width: 600px;
  }

  section:after {
    content: "";
    display: table;
    clear: both;
  }

  div.element {
    float: left;
    width: 30%;
    padding: 30px 0;
    background-color: #ddf;
  }
}
```
> **JS**

```javascript
/* JavaScript Media Queries */
if (matchMedia) {
  const mq = window.matchMedia("(min-width: 500px)");
  mq.addListener(WidthChange);
  WidthChange(mq);
}

// media query change
function WidthChange(mq) {

  const msg = (mq.matches ? "more" : "less") + " than 500 pixels";
  document.getElementById("current").firstChild.nodeValue = msg;

}
```
