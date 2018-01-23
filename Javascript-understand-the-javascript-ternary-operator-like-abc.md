### Understand The JavaScript Ternary Operator like the ABCs

**1. Operators in JavaScript**
---
- In the JavaScript theatre, various operations require operators, which are basically denoted with symbols ```+ - / = * %```. For the various operations like arithmetic and assignment operations, various symbols are used. These operators in their usage are split into 3 types:
  + **Unary Operators** - Requires one operand either before or after the operator.
  + **Binary Operators** - Requires two operands on either side of the operator.
  + **Ternary Operator** - Requires three operands and is a conditional operator.

```javascript
time++ //Unary operator (increment)
2 + 3 //Binary Operator (addition)
a ? 'hello' : 'world' //Ternary/Conditional operator
```
- We will focus on the ternary operator as earlier stated.

**2. Ternary Operator**
---
- The ternary operator has been around for a while now, but isn’t widely used, maybe because of the syntax or some form of ambiguity I’m unaware of. The ternary operator is a conditional operator and can effectively and efficiently replace several lines of IF statements. It simply verifies if a condition is true or false and returns an expression or carry out an operation based on the state of the condition, in probably one line of code. Using an IF statement we have:

```javascript
var day = true;
if(day){
  alert('It is day-time')
} else{
  alert('It is night-time')
}
// It is day-time
```

- Using the ternary operator:

```javascript
var day = true; //condition
alert(day ? 'It is day-time' : 'It is night-time') // It is day-time
```

- This reduced the syntax of the IF statement to:

```
- ? - means IF 
- : - means Else
```

- So, if day is true, alert It is daylight, else alert It is nighttime. Simple!

- Let’s get to more details.

**3. Variable Assignment**
---

```javascript

```


**4. Usage in Functions**
---

```javascript

```


**5. Multiple Conditions**
---

```javascript

```

**6. Multiple Operations per Condition**
---

```javascript

```


