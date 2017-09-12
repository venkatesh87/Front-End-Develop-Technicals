# Linting HTML using CSS

When HTML is written incorrectly, nothing much happens. Because of this, it's easy to have invalid, unsemantic, or unaccessible bits in markup without it being obvious.

There are many ways we can lint our HTML to discover and fix these issues, for example using the W3C Markup Validation Service. Another thing we can do, which can be more easily integrated into a development workflow, is to use some slightly advanced CSS selectors to highlight potential problem areas. Here are a few things we can use CSS selectors to help us catch out.

## Inline Styles

```javascript
*[style] { 
    border: 5px solid red; /* Style to make the elements noticeable */
}
```
This selector will target any element on the page that has inline styles applied to it. As a general rule, inline styles should be avoided as they are difficult to override due to their increased level of specificity. Although inline styles may be necessary in some cases, this selector will help highlight them so a decision can be made on a case-by-case basis.

With the problem elements selected, we can apply any style to make them more visibly obvious on the page, e.g. a big red border.

## Faulty or Missing Link Targets

```javascript
a:not([href])  
a[href="#"],  
a[href=""],  
a[href*="javascript:void(0)"] { … }  
```
These selectors will highlight any anchor elements that either do not have any href attribute at all, or have a meaningless one.

## Unaccessible Images

```javascript
img:not([alt]) { ... }  
```
As a blanket rule, all images should have an alt attribute. When this attribute is missing, most screenreaders will read out the value of the src attribute instead which, of course, is not useful to the user and can in fact be confusing.

It should be noted that the above selector will not select images with a null/empty alt attribute, i.e. images with alt="". This is because a null alt attribute can be an intentional way of having a screen reader skip over the image, which is useful if, for example, the image is purely decorative. It could, however, still be useful to have these highlighted, which we can do with the following selector -

```javascript
img[alt=""] { ... }  
```

## Missing Document Language

```javascript
html:not([lang]),  
html[lang=""] { ... }  
```
An important attribute that should be present on all html elements is the language attribute. This attribute is a signal to screen readers what language the page is in, which can determine how the content of the page is read aloud.

Here's an example of what can happen when the lang attribute is missing -

## Incorrect Character Set

```javascript
meta[charset]:not([charset="UTF-8"]) { ... } 
```

This selector targets any meta character set tag that is not set to UTF-8. This tag tells the browser to use the UTF-8 form of character encoding, which is presently the recommended form for HTML documents. Having this tag is therefore required for valid HTML.

Ideally, this tag should also be the first element after the opening <head> tag. We can check for this using the following selector -

```javascript
meta[charset="UTF-8"]:not(:first-child) { ... }  
```

## Unaccessible Viewport Attributes

```javascript
meta[name="viewport"][content*="user-scalable=no"],  
meta[name="viewport"][content*="maximum-scale"],  
meta[name="viewport"][content*="minimum-scale"] { ... }  
```

This selector can be used to highlight unaccessible viewport meta attributes. It is generally advised that we avoid restricting the user's ability to manipulate the viewport by shrinking and enlarging it. So, using user-scalable=no, maximum-scale, or minimum-scale should never be used.

## Unlabelled Form Elements

```javascript
input:not([id]),  
select:not([id]),  
textarea:not([id]) { ... }

label:not([for]) { ... }  
```

Form elements are perhaps the most important elements when it comes to labelling. Although there are several ways to label a form element, the most common way is by having an ID on the element that is referenced by a label element. The above selector checks for form elements that do not have an ID, and label elements that are not explicitly linked to a form element using the for attribute.

Another type of labelling that is important for form elements is via the name attribute. While the id attribute is used for labelling the element in the context of the HTML document, the name attribute is used to reference the the element when submitted with the form data.

```javascript
input:not([name]),  
select:not([name]),  
textarea:not([name]) { ... }  
```

Additionally, besides the form elements themselves, it is useful to give the form element itself a name and/or id.
```javascript
form:not([name]):not([id]) { ... }  
```
This selector will highlight any form element that is missing both ```name``` and ```id``` attributes.
## Empty Interactive Elements

```javascript
button:empty,  
a:empty { ... }  
```
Interactive elements like links or buttons are typically labelled by their content. Although it is possible to label these elements using other methods, such as an aria-label attribute, having them be empty is likely a sign of something wrong. This selector will highlight any links of buttons that have no HTML content inside them.

## Unnecessary or Deprecated Attributes

```javascript
script[type="text/javascript"],  
link[rel="stylesheet"][type="text/css"] { ... }  
```

Finally, we can use CSS selectors to highlight attributes in our HTML that are deprecated or no longer needed.
