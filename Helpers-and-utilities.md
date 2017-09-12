### A collection of useful generic helper functions.

#### I. Parsing a JSON string

- Takes a well-formed JSON string and returns the resulting JavaScript value.

- Use this fast and reliable method that is available in all modern browsers, including IE 8 to replace jQuery's ```$.parseJSON```:

```javascript
var json = '{ "foo": true, "bar": 1 }',
    obj = JSON.parse(json);

console.log(obj);
```

#### II. Strip leading and trailing white-space from string

- Remove white-space characters from the beginning and end of a string.

- Modern browsers have a ```String.trim()``` method included. Therefore, we only extend the prototype-object for IE 8, which has no native support for it:

```javascript
// IE 8
if (!String.prototype.trim) {
  String.prototype.trim = function() { return this.replace(/^\s+|\s+$/g, ''); };
}

// example
var s = '  Hello World!  ';
s = s.trim();
console.log(s);
// "Hello World!"
```

- All browsers except IE 8 and below make use of the optimized internal stripping method, which is much faster. This is generally recommended when extending native objects.

#### III. Test if a certain value exists in an array

- Search for a specified value within an array and return its index (or -1 if not found).

- A fast and simple helper function for testing if a certain value is contained in another array:

```javascript
function inArray(needle, haystack) {
  var length = haystack.length;
  for (var i = 0; i < length; i++) {
    if (haystack[i] == needle) return i;
  }
  return -1;
}
```

- If you don't need to support IE8, it's recommended to use the array method ```indexOf()```. It return the index of a matching value, and "-1" if the looked up value does not exist in the array.

```javascript
  var a = [1, 2, 'abc', true];

console.log(a.indexOf('abc'));
// >> 2

console.log(a.indexOf('y'));
// >> -1
```

#### IV. Merge two JavaScript objects

- Extend a JavaScript object with the key/value pairs of another.

- With the following helper, you can merge two objects into one new object:

```javascript
function extend(obj, src) {
  for (var key in src) {
    if (src.hasOwnProperty(key)) obj[key] = src[key];
  }
  return obj;
}

// example
var a = { foo: true },
  b = { bar: false };
var c = extend(a, b);

console.log(c);
// { foo: true, bar: false }
```

- This is typically useful when merging an options dict with the default settings in a function or a plugin.

- If support for IE 8 is not required, you may use Object.keys for the same functionality instead:

```javascript
function extend(obj, src) {
    Object.keys(src).forEach(function(key) { obj[key] = src[key]; });
    return obj;
}
```

- This involves slightly less code and is a bit faster.

#### V. Set cookie, get cookie and delete cookie

- Size optimized functions for creating, reading and erasing cookies in JavaScript.

- Use the following three functions for working with cookies.

```javascript
function getCookie(name) {
  var v = document.cookie.match('(^|;) ?' + name + '=([^;]*)(;|$)');
  return v ? v[2] : null;
}
```

```javascript
function setCookie(name, value, days) {
  var d = new Date;
  d.setTime(d.getTime() + 24 * 60 * 60 * 1000 * days);
  document.cookie = name + "=" + value + ";path=/;expires=" + d.toGMTString();
}
```

```javascript
function deleteCookie(name) { setCookie(name, '', -1); }
```

- All three functions are optimized on size. You may squeeze out some more bytes by minification.