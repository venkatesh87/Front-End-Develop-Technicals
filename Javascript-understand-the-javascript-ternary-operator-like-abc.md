### Understand The JavaScript Ternary Operator like the ABCs
---
- Don’t Repeat Yourself

>**1. Operators in JavaScript**
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

>**2. Ternary Operator**
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

- So, if ```day``` is ```true```, alert ```It is daylight```, ```else``` alert ```It is nighttime```. Simple!

- Let’s get to more details.

>**3. Variable Assignment**
---
- As stated earlier, the result of the condition evaluation can be an expression or an operation, and in this case a variable assignment.

```javascript
var myName = false;
var age = false;
var message = myName ? "I have a name" : "I don't have a name, duh"
console.log(message)
```

- Notice we assigned the result of a ternary operation first to a global variable ```message```, and later on, reassigned it when the condition changed. Notice the reassignment of the global variable ```age``` in the condition of the ternary operator. Reassignment operations can occur in a ternary operation - so much done in one line yeah? The ```ELSE``` part of the operation can also be an expression or an operation on its own, just like it’s done in conventional ```IF``` statements.

>**4. Usage in Functions**
---

- Usually, the next use case for IF statements are in functions, basically ternary operations make a function ‘syntactically sweet’. Same way variables are assigned the result of ternary operations is the same way functions return the result of ternary operations. With IF statements we have:

```javascript
var dog = true;
function myPet(){
  if(dog){
    return 'How do i get it?';
  }
  else{
    'Get me a dog!'
  }
}
console.log(myPet());
```
- with a ternary operator:

```
var dog = false;
function myPet(){
  return dog ? 'How do i get it?' : 'Get me a dog!';
}
console.log(myPet()) // Get me a dog!
```

- Imagine if we had quite a number of IF statements, with a host of ```return``` expressions in them, now think of how these can be shortened using ternary operators. Next, we will see how we can chain multiple conditions together, you can have the conditions in functions as well!

>**5. Multiple Conditions**
---

- Just like in good old IF statement with IF/ELSE IF, multiple conditions can be chained in ternary operations to give one robust operation. Normally we would write:

```javascript
var myName = true;
var myAge = true;
var message = '';
if (myName){
  if(myAge){
    message = "I'll like to know your age and name"
  }else{
    message = "I'll stick with just your name then"
  }
} else {
  "Oh, I'll call you JavaScript then, cus you fine and mysterious"
}
console.log(message) //I'll like to know your age and name
```

- but with a ternary operator we have:

```
var myName = true;
var myAge = true;
var message = myName? (myAge ? "I'll like to know your age and name" : "I'll stick with just your name") : "Oh, I'll call you JavaScript then, cus you fine and mysterious"
console.log(message) // I'll like to know your age and name
```

- This is just a simple illustration of having two conditions in one IF statement. Here’s a lighter one:

```
var email = false;
var phoneNumber = true;
var message = email ? 'Thanks for reaching out to us' : phoneNumber ? 'Thanks for reaching out to us' : 'Please fill in your email or phone-number'
console.log(message) //Thanks for reaching out to us
```

- Here we simply have multiple conditions chained to one another, and if a condition doesn’t pass, another condition is put forward, and if it still doesn’t pass, (now you cannot be offered any further assistance, lol) an expression is returned.

>**6. Multiple Operations per Condition**
---

- A friend of mine would say “in code, you read A + B but later you are required to pull B from a remote server, make A a ninja, minify B, before they can be added together”. So far we have seen multiple conditions chained together, what about expressions or conditions per condition? Say we would like to make a request to an API if a condition passes as true. Just like in IF statements, here’s a simple one:

```javascript
var home = true;
if(home){
  alert('Welcome 127.0.0.1');
  var port = prompt('What port do you like?');
  alert('Serving you a cool dish on ' + port)
} else {
  alert('Check back when you get home' )
}
//serving you a cool dish on ???
```

- but with a ternary operator, simply separate each operation with a comma.

```
var home = true;
var port = '';
home ? (
  alert('Welcome 127.0.0.1'),
  port = prompt('What port do you like?'),
  alert('Serving you a cool dish on ' + port)
) : alert('Check back when you get home' )
//serving you a cool dish on ???
```

> Note: All variables used in a ternary operation should be defined before the operation is created. Also, If the operations in the condition are assignment operations, the value of the last expression or operation is used i.e

```
var home = true;
var myLocation = 'Lagos';
myLocation = home ? ('Brussels', 'london', 'Rio de Janero', 'Newark' ) : 'Kinshasha'
console.log(myLocation) // Newark
```

>**7. Multiple Conditions**

- So far, you have seen how invaluable using ternary operators to write conditional statements make code plain and effortless, from writing simple lines of conditional statements to writing large chunks of chained operations in or out of functions. Using ternary operators, keep writing better code, …and DRY(Don’t Repeat Yourself) code.

