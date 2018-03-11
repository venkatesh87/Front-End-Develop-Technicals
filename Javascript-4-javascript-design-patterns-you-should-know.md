#### JavaScript basic - Exercises, Practice, Solution
---
- Every developer strives to write maintainable, readable, and reusable code. Code structuring becomes more important as applications become larger. Design patterns prove crucial to solving this challenge - providing an organization structure for common issues in a particular circumstance.
- JavaScript web developers frequently interact with design patterns, even unknowingly, when creating applications.
>****
>**Table of Contents**
   1. Module Design Pattern
   2. Prototype Design Pattern
   3. Observer Design Pattern
   4. Singleton
   5. Conclusion
   6. Scotchmas Day 2 Giveaway
   
- Although there is a diverse list of design patterns used in certain circumstances, JavaScript developers tend to use some patterns customarily more than others.
- In this post, I want to discuss these common patterns to expose ways to improve your programming repertoire and dive deeper into the JavaScript internals.
- The design patterns in question include the following:
  + **Module**
  + **Prototype**
  + **Observer**
  + **Singleton**

- Each pattern consists of many properties, though, I will emphasize the following key points:
  1. **Context:** Where/under what circumstances is the pattern used?
  1. **Problem:** What are we trying to solve?
  1. **Solution:** How does using this pattern solve our proposed problem?
  1. **Implementation:** What does the implementation look like?
  
#### Module Design Pattern
---
- JavaScript modules are the most prevalently used design patterns for keeping particular pieces of code independent of other components. This provides loose coupling to support well-structured code.
- For those that are familiar with object-oriented languages, modules are JavaScript "classes". One of the many advantages of classes is encapsulation - protecting states and behaviors from being accessed from other classes. The module pattern allows for public and private (plus the lesser-know protected and privileged) access levels.
- Modules should be Immediately-Invoked-Function-Expressions (IIFE) to allow for private scopes - that is, a closure that protect variables and methods (however, it will return an object instead of a function). This is what it looks like:

>JavaScript Code:
```javascript
(function() {

    // declare private variables and/or functions

    return {
      // declare public variables and/or functions
    }

})();
```
- Here we instantiate the private variables and/or functions before returning our object that we want to return. Code outside of our closure is unable to access these private variables since it is not in the same scope. Let's take a more concrete implementation:

```
var HTMLChanger = (function() {
  var contents = 'contents'

  var changeHTML = function() {
    var element = document.getElementById('attribute-to-change');
    element.innerHTML = contents;
  }

  return {
    callChangeHTML: function() {
      changeHTML();
      console.log(contents);
    }
  };

})();

HTMLChanger.callChangeHTML();       // Outputs: 'contents'
console.log(HTMLChanger.contents);  // undefined
```
- Notice that ```callChangeHTML``` binds to the returned object and can be referenced within the ```HTMLChanger``` namespace. However, when outside the module, contents are unable to be referenced.

#### Revealing Module Pattern
---
- A variation of the module pattern is called the **Revealing Module Pattern**. The purpose is to maintain encapsulation and reveal certain variables and methods returned in an object literal. The direct implementation looks like this:

>JavaScript Code:
```javascript
var Exposer = (function() {
  var privateVariable = 10;

  var privateMethod = function() {
    console.log('Inside a private method!');
    privateVariable++;
  }

  var methodToExpose = function() {
    console.log('This is a method I want to expose!');
  }

  var otherMethodIWantToExpose = function() {
    privateMethod();
  }

  return {
      first: methodToExpose,
      second: otherMethodIWantToExpose
  };
})();

Exposer.first();        // Output: This is a method I want to expose!
Exposer.second();       // Output: Inside a private method!
Exposer.methodToExpose; // undefined
```
- Although this looks much cleaner, an obvious disadvantage is unable to reference the private methods. This can pose unit testing challenges. Similarly, the public behaviors are non-overridable.

#### Prototype Design Pattern

- Any JavaScript developer has either seen the keyword prototype, confused by the prototypical inheritance, or implemented prototypes in their code. The Prototype design pattern relies on the [JavaScript prototypical inheritance](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain). The prototype model is used mainly for creating objects in performance-intensive situations.

- The objects created are clones (shallow clones) of the original object that are passed around. One use case of the prototype pattern is performing an extensive database operation to create an object used for other parts of the application. If another process needs to use this object, instead of having to perform this substantial database operation, it would be advantageous to clone the previously created object.
![Prototype Design Pattern on Wikipedia](https://upload.wikimedia.org/wikipedia/commons/1/14/Prototype_UML.svg)

>JavaScript Code:
```javascript

```

**4..**

>JavaScript Code:
```javascript

```

**5..**

>JavaScript Code:
```javascript

```

**6..**

>JavaScript Code:
```javascript

```
