
### I. JS MATH
---
- The JavaScript Math object allows you to perform mathematical tasks on numbers.

### 1. Math.PI
---

```javascript
Math.PI; // returns 3.141592653589793
```

### 2. Math.round()
---
- Math.round(x) returns the value of x rounded to its nearest integer:

```javascript
Math.round(4.7);    // returns 5
Math.round(4.4);    // returns 4
```

### 2. Math.pow()
---
- Math.pow(x, y) returns the value of x to the power of y:

```javascript
Math.pow(3, 2);      // returns 9
Math.pow(3, 3);      // returns 27
```

### 3. Math.sqrt()
---
- Math.sqrt(x) returns the square root of x:

```javascript
Math.sqrt(64);      // returns 8
```

### 4. Math.abs()
---
- Math.abs(x) returns the absolute (positive) value of x:

```javascript
Math.abs(-4.7);     // returns 4.7
```

### 5. Math.ceil()
---
- Math.ceil(x) returns the value of x rounded up to its nearest integer:

```javascript
Math.ceil(4.4);     // returns 5
```

### 6. Math.floor()
---
- Math.floor(x) returns the value of x rounded down to its nearest integer:

```javascript
Math.floor(4.7);    // returns 4
```

### 7. Math.sin()
---
- Math.sin(x) returns the sine (a value between -1 and 1) of the angle x (given in radians).
- If you want to use degrees instead of radians, you have to convert degrees to radians:
- Angle in radians = Angle in degrees x PI / 180.

```javascript
Math.sin(90 * Math.PI / 180);     // returns 1 (the sine of 90 degrees)
```

### 8. Math.cos()
---
- Math.cos(x) returns the cosine (a value between -1 and 1) of the angle x (given in radians).
- If you want to use degrees instead of radians, you have to convert degrees to radians:
- Angle in radians = Angle in degrees x PI / 180.

```javascript
Math.cos(0 * Math.PI / 180);     // returns 1 (the cos of 0 degrees)
```

### 9. Math.min() and Math.max()
---
- Math.min() and Math.max() can be used to find the lowest or highest value in a list of arguments:

```javascript
Math.min(0, 150, 30, 20, -8, -200);  // returns -200
```

```javascript
Math.max(0, 150, 30, 20, -8, -200);  // returns 150
```

### 10. Math.cos()
---
- Math.random() returns a random number between 0 (inclusive),  and 1 (exclusive):

```javascript
Math.random();     // returns a random number
```