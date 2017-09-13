# Coding Convention

## I. HTML :
**1. Default structure HTML:**
```
<!DOCTYPE html>
<html>
<head>
  <title>[:. Title .:]</title>
  <meta http-equiv="Content-type" content="text/html;charset=UTF-8">
  <meta name="description" content="Website description">
  <meta name="keywords" content="The keywords of your website">
  <meta name="author" content="daodc">
  <meta name="robots" content="index,follow">
  <meta name="SKYPE_TOOLBAR" content="SKYPE_TOOLBAR_PARSER_COMPATIBLE">
  <meta name="format-detection" content="telephone=no">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <!-- HTML5 Shim and Respond.js IE8 support of HTML5 elements and media queries -->
     <!-- WARNING: Respond.js doesn't work if you view the page via file:// -->
      <!--[if lt IE 9]>
        <script src="https://oss.maxcdn.com/libs/html5shiv/3.7.0/html5shiv.js"></script>
        <script src="https://oss.maxcdn.com/libs/respond.js/1.4.2/respond.min.js"></script>
      <![endif]-->
  <link rel="icon" href="../images/front/favicon.ico" type="image/x-icon">
  <link rel="apple-touch-icon" href="../images/front/webclip.png" />
  <link rel="apple-touch-icon-precomposed" href="../images/front/webclip.png" />
  <link rel="stylesheet" href="../css/common.css" type="text/css" media="screen">
</head>
<body>
  <div id="wrapper">    
    <header id="head">
      <div class="container">
        <p>Header</p>
      </div>    
    </header>   
    <div id="page-content">
      <div class="container">   
        <p> content </p>      
      </div>
    </div>
  </div>
  <div id="footer">
    <div class="container">   
      p>Copyright © Site name, 20XX</p>
    </div>    
  </div>
  </footer>
  <script src="./js/jquery-2.1.3.min.js"></script>
  <script src="./js/bootstrap.min.js"></script>
  <script src="./js/common.js"></script>
</body>
</html>
```
  * Css is always placed above and in the ```<header>```.
  * Js are always placed at the bottom and in the ```<body>```.

**2. Use Correct Document Type :**

* Always declare the document type as the first line in your document:
```
<!DOCTYPE html>
```
**3. Elements :**

 * Add closing tags to elements that aren't self-closing.
 * Don't add the forward slash for self-closing elements.
 * Avoid unnecessary markup, such as surrounding a block element in a ```<div>```.
 * Use lowercase, not uppercase for File Names, Attribute Names, Element Names.

```
<!--Bad-->
<DIV>
  <UL>
    <LI>Item 1
    <LI>Item 2
  </UL>
</DIV>
<INPUT type="text" />

<!--Good-->
<ul>
  <li>Item 1</li>
  <li>Item 2</li>
</ul>
<input type="text">
```

```
<!-- Bad -->
<div CLASS="menu">

<!-- Good -->
<div class="menu">
```

```
image.jpg cannot be accessed as Image.jpg.
```
**4. Attributes :**

 * Surround values for attributes in double quotes.
 * Boolean attributes, such as required, do not need a value.
 * Follow this order for attributes:
    * class
    * id, name
    * data-*
    * src, for, type, href, value
    * title, alt
    * role, aria-*
```
<!--Bad-->
<input type='radio' class="input" required='true'>

<!--Good-->
<input class="input" type="radio" required>

<a class="..." id="..." data-toggle="modal" href="#">
  Example link
</a>

<input class="form-control" type="text">

<img src="..." alt="...">
```
**5. Courtesies:**

 * Put a single line break between blocks/components.
 * Avoid adding comments. An exception would be a closing comment for large blocks.
```
<div class="video-player">
  ...
</div>

<div class="comment-list">
  ...
</div> <!--end comment-list-->
```

**6. SEO HTML :**

 * Mỗi trang html có 1 thẻ H1, thường thì bọc Logo  
   * https://css-tricks.com/css-image-replacement/
   * http://luigimontanez.com/2010/stop-using-text-indent-css-trick/
 * Có tag meta keywork và description.
   * http://usabilitygeek.com/7-html-guidelines-for-website-usability-seo/

**7. Semantic Elements in HTML5:**

```
 - <article>
 - <aside>
 - <details>
 - <figcaption>
 - <figure>
 - <footer>
 - <header>
 - <main>
 - <mark>
 - <nav>
 - <section>
 - <summary>
 - <time>
```
**8. Images Attribute :**

   * For images whose alt attributes would introduce redundancy, and for images whose purpose is purely decorative which you cannot immediately use CSS for, use no alternative text, as in alt=""
 
```
<!-- Bad -->
<img src="spreadsheet.png">
```

```
<!-- Good -->
<img src="spreadsheet.png" alt="Spreadsheet screenshot." width="100" height=100"">
```
**9. No self closing tags:**

   * With HTML5 we can write things like ```<hr />``` as ```<hr>```, ```<img />``` as ```<img>``` and so on. I choose to omit the, so in my HTML you’ll see things like:

**10. Comments on closing tags :**

   * After every major chunk of HTML, for example, the end of a carousel, or the end of the content ```<div>```, I place a closing-comment, for example:
```
<div class=content>
      <div class=carousel>
     ...
      </div><!-- /carousel -->
</div><!-- /content -->
```
**11. HTML Comments :**

   * Short comments should be written on one line, with a space after <!-- and a space before -->:
```
<!-- This is a comment -->
```
   * Long comments, spanning many lines, should be written with <!-- and --> on separate lines:
```
<!-- 
  This is a long comment example. This is a long comment example. This is a long comment example.
  This is a long comment example. This is a long comment example. This is a long comment example.
-->
```

**12. Formatting :**

   All HTML documents must use two spaces for indentation and there should be no trailing whitespace. HTML5 syntax must be used and all attributes must use double quotes around attributes.
  
```
<video autoplay="autoplay" poster="poster_image.jpg">
  <source src="foo.ogg" type="video/ogg">
</video>
```

**13. Blank Lines and Indentation**

 * Do not add blank lines without a reason.
 * For readability, add blank lines to separate large or logical code blocks.
 * For readability, add 2 spaces of indentation. Do not use TAB.
 * Do not use unnecessary blank lines and indentation. It is not necessary to use blank lines between short and related items. It is not necessary to indent every element:
  
```
<!-- Bad -->
<body>

  <h1>Famous Cities</h1>

  <h2>Tokyo</h2>

  <p>
    Tokyo is the capital of Japan, the center of the Greater Tokyo Area,
    and the most populous metropolitan area in the world.
    It is the seat of the Japanese government and the Imperial Palace,
    and the home of the Japanese Imperial Family.
  </p>

</body>
```

```
<!-- Good -->
<body>

<h1>Famous Cities</h1>

<h2>Tokyo</h2>
<p>Tokyo is the capital of Japan, the center of the Greater Tokyo Area,
and the most populous metropolitan area in the world.
It is the seat of the Japanese government and the Imperial Palace,
and the home of the Japanese Imperial Family.</p>

</body>
```

  **Table Example:**

  ```
  <table>
    <tr>
      <th>Name</th>
      <th>Description</th>
    </tr>
    <tr>
      <td>A</td>
      <td>Description of A</td>
    </tr>
    <tr>
      <td>B</td>
      <td>Description of B</td>
    </tr>
  </table>
  ```
  
  **List Example:**
  
  ```
  <ol>
    <li>London</li>
    <li>Paris</li>
    <li>Tokyo</li>
  </ol>
  ```

**14. File Extensions**

 * HTML files should have a .html extension (or .htm).
 * CSS files should have a .css extension.
 * SASS files should have a .scss extension.
 * LESS files should have a .less extension.
 * JavaScript files should have a .js extension.

**15. The Difference Between ID and Class**

 * The simple difference between the two is that while a class can be used repeatedly on a page, an ID must only be used once per page. Therefore, it is appropriate to use an ID on the div element that is marking up the main content on the page, as there will only be one main content section. In contrast, you must use a class to set up alternating row colors on a table, as they are by definition going to be used more than once.

 * ID's are unique :
   - Each element can have only one ID
   - Each page can have only one element with that ID
    
 * Classes are NOT unique :
   - You can use the same class on multiple elements.
   - You can use multiple classes on the same element.
    
 * ID's have special browser functionality
    
 * Classes have no special abilities in the browser, but ID's do have one very important trick up their sleeve. This is the "hash value" in the URL. If you have a URL like http://yourdomain.com#comments, the browser will attempt to locate the element with an ID of "comments" and will automatically scroll the page to show that element. It is important to note here that the browser will scroll whatever element it needs to in order to show that element, so if you did something special like a scrollable DIV area within your regular body, that div will be scrolled too.
    
 * This is an important reason right here why having ID's be absolutely unique is important. So your browser knows where to scroll!
    
 * Elements can have BOTH
    
 * There is nothing stopping you from having both an ID and a Class on a single element. In fact, it is often a very good idea. Take for example the default markup for a WordPress comment list item:
    
  ```
  <li id="comment-27299" class="item">
  ```

**16. Do not use inline style attributes**

* As much as possible, use css classes instead of using inline style attributes. This has the advantages:
Makes it easier to change the look of the UI by changing the stylesheet
Makes it possible to reuse the css class in another place, giving a more consistent UI and making it possible to change the look by changing only one place.

```
<!-- Bad -->
<div style="width:100px;align:center;">

<!-- Good -->
<div class="message">
```

##II. CSS :

**1. Concept understand :**

- Block : Standalone entity that is meaningful on its own.
- Element : Parts of a block and have no standalone meaning. They are semantically tied to its block.
- Modifier : Flags on blocks or elements. Use them to change appearance or behavior.
- Naming : Block names may consist of Latin letters, digits, and dashes. To form a CSS class, add a short prefix for namespacing: .block .

```
<!-- Bad -->
<div style="width:100px;align:center;">

<!-- Good -->
<div class="message">
```
**2. NAMING CONVENTION :**

You don't have to follow a certain naming convention, but doing so will reduce the amount of time you spend thinking names up, give you a good code structure, and make it easy for the next developer to pick up.
  
  * Find one you like and stick to it.
  * This site was made using [BEM](http://getbem.com/). Other options include:
  
    1. [OOCSS](https://github.com/stubbornella/oocss/wiki)
    2. [SMACSS](https://smacss.com/)
    3. [Idiomatic CSS](https://github.com/necolas/idiomatic-css)
    4. [RSCSS](https://github.com/rstacruz/rscss)
    5. [Title CSS](http://www.sitepoint.com/title-css-simple-approach-css-class-naming/)
    6. [CSS Module](http://glenmaddern.com/articles/css-modules)
    7. [ITCSS](https://www.xfive.co/blog/itcss-scalable-maintainable-css-architecture/)

```

.item {
  &__number {
    ...
  }

  &--selected {
    ...
  }
}

```
**3. FORMATTING :**

These formatting defaults are the standard at many companies and also have the added benefit of making the code easier to scan.

  * Each selector in a group should be on its own line.
  * The opening brace belongs on the same line as the selector.
  * Put a space before the opening brace.
  * Each property and value pair gets its own line
  * Properties and values belong on the same line.
  * One space after the colon of a property.
  * Put a space after each comma.
  * Always end with a semicolon.
 
```
/* Bad*/
h4, h5, h6
{
  color:rgba(100,100,100,0);
  margin-bottom:0.25rem
}

/* Good */
h4,
h5,
h6 {
  color: rgba(100, 100, 100, 0);
  margin-bottom: 0.25rem;
}
```

**4. SCSS :**

  SASS has many powerful tools, but these can make your code difficult to maintain if you're not careful and confusing for the next person who touches it.
  On any decent-sized site, specificity problems can and will arise rather quickly. Extending your components later will be difficult as well.
  Defaults to help out the next developer and make the code easier to scan.

  * Stick to the basics: variables, includes, and mixins. 
  * Avoid nesting whenever possible.
  * Adhere to this order: 
  
    * @extend
    * @include
    * regular styles
    * pseudo classes
    * nested items (only if you must)
    * media queries

```
.list-item {
    @include font-size(1);
    padding: 1rem;
    
    &:hover {
      background-color: $light-gray;
    }
    
    @include respond($br-desktop) {
      padding: 2rem;
    }
}
```

**5. CSS :**
 
  Classes prefixed with js- are strictly for hooking into Javascript. Developers know this is the class to use for setting up click events and such. They are not meant to be styled.
  Properties marked with !important can make that component's reusability difficult in the future.
  
  * Hyphen - or _ delimit your class names.
  * Use lowercase, not uppercase.
  * Prefix decimals with a leading 0.
  * Don't specify units for zero values.
  * Do not style js- prefixed classes. 
  * Avoid using !important unless absolutely necessary. Restrict its use to utility classes prefixed with a u-.
  * Adhere to this property order:
    
    * Positioning (position, z-index...)
    * Box Model (display, margin...)
    * Typographic (font, color...)
    * Visual (background, opacity...)
 
```
.declaration-order {
  /* Positioning */
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 100;

  /* Box-model */
  display: block;
  float: right;
  width: 100px;
  height: 100px;

  /* Typography */
  font: normal 13px "Helvetica Neue", sans-serif;
  line-height: 1.5;
  color: #333;
  text-align: center;

  /* Visual */
  background-color: #f5f5f5;
  border: 1px solid #e5e5e5;
  border-radius: 3px;

  /* Misc */
  opacity: 1;
}
```

**6. Style Sheets**

- Use simple syntax for linking style sheets (the type attribute is not necessary):

  ```
  <link rel="stylesheet" href="styles.css">
  ```

**7. Subject :**

- Use css processor : sass, less to build project Front End.
- Obligatory sprite all the icons.
- Apply tool PerfectPixel for project.

**8. Commenting :**

 Use a title comment for sections/components. 
 
 Keep comments coupled with the component/element. Don't put comments next to individual properties. 
 
 Don't comment about what you're doing. It's more important to comment why you're doing it. 
 
* **Comment Atribute :**

```
.cf{
  *zoom :1; /*for IE6 and IE7*/
}
```
* **Comment page :**

```
/***************************
****************************
These are the styles for
the header section
****************************
***************************/
or 
/*------------------------------------*\
  CONTENTS
\*------------------------------------*/
/*
NOTES
RESET
SHARED     Share anything we can across elements.
MAIN       HTML, BODY, etc.
*/
```

```
/*----------------------------------------
  #MAIN-NAV
----------------------------------------*/

/* We're setting an opacity here because of a Safari rendering issue. */
/* The flex-direction changes to ensure nothing is oddly stacked on mobile. */

```

**9. Class names**

Please do not use excessively long class names. From my experience, it is good to use up to 3 words. Alternatively, please use the module’s interpretation.

```
/* Bad */
.catagory_list_item__link{}
.catagory_list_item__link_image{}
```

```
/* Good */
.catagory{
.catagory_list{...}
.catagory_item{...}
.catagory_link{...}
.catagory_image{...}
}
```

```
/* Good */
.catagory{
.list{...}
.item{...}
.link{...}
}
```
**10. If the value is zero “0”, please omit the unit.**

This is to ensure that JavaScript and CSS are loosely coupled, can be edited separately without one influencing the other and reduce the size of css.
```
/* Bad */
padding: 0px;
```

```
/* Good */
padding: 0;
```

**7. Abbreviate the elements in a property as much as possible**

```
/* Bad */
.hoge{
  border-top-style: none;
  font-family: palatino, georgia, serif;
  font-size: 100%;
  line-height: 1.6;
  padding-bottom: 2em;
  padding-left: 1em;
  padding-right: 1em;
  padding-top: 0;
}
```

```
/* Good */
.hoge{
  border-top: 0;
  font: 100%/1.6 palatino, georgia, serif;
  padding: 0 1em 2em;
}
```

**8. Use a semi-colon at the end of a property.**

```
/* Bad */
.test {
  display: block;
  height: 100px
}
```

```
/* Good */
.test {
  display: block;
  height: 100px;
}
```

**11. CSS nesting should go up to grandchild**

No matter how deeply the CSS is nested, please nest up to great grandchild at the maximum. Any more than this - please reconsider the HTML and CSS structure. It is likely that you will be able to fix the structure.

```
/* Bad */
.forbear{
  .parent{
    .child{
      .grandchild{

      }

    }

  }
}
```

```
/* Good */
.forbear{
  .parent{
    .child{

    }

  }
}
```

##III. JS and jQuery :

**1. Loading JavaScript in HTML:**

Use simple syntax for loading external scripts (the type attribute is not necessary):

```
<script src="./js/jquery-2.1.3.min.js"></script>
<script src="common.js">
```

**2. jQuery :**

  - Function jQuery 
     Reference : [http://api.jquery.com/](http://api.jquery.com/)

**3. All functions must be placed in common.js file :**

```
$(document).ready(function(){
  //flexslider
	$('#banner .flexslider').flexslider({
		animation: "fade",
		controlNav: false,
		directionNav: true,
		prevText: "",
		nextText: "", 
		start: function(slider){
			$('body').removeClass('loading');
		}
	});
});
```

##IV. Responsive :

* Tag meta
* images
* Retina
* Media query
* Use framework Bootstrap
* Use framework Materialize

##V. No-Responsive :

- Remove Tag meta : 

```
<meta name="viewport" content="width=device-width, initial-scale=1">
```

- Fix width container

##VI. Build project with Grunt or Gulp :

   * Grunt :
      * Reference : [http://gruntjs.com/](http://gruntjs.com/)

   * Gulp :
       * Reference : [http://gulpjs.com/](http://gulpjs.com/)


##VII. TOOLS :

Everyone uses different tools to write their code. These settings ensure that everything will display the same regardless of environment or text editor.

It also ensures you don't muddy up commits and diffs with spacing issues.

Use this file to get these defaults after downloading the EditorConfig plugin for your text editor of choice.

 * Use UTF-8 encoding.
 * Use soft tabs set to 2 spaces.
 * Give yourself an 80 character wide guide
 * Remove any trailing whitespace.
 * Put a new line at the end of files.


