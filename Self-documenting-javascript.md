# Overview of Techniques

- We can split the techniques for self-documenting code into three broad categories:
  + structural, where the structure of code or directories is used to clarify the purpose
  + naming related, such as function or variable naming
  + syntax related, where we make use of (or avoid using) features of the language to clarify code.

# I.Structural

- First, let’s look at the structural category. Structural changes refer to shifting code around for enhanced clarity.

### 1.Move code into a function
- This is the same as the “extract function” refactoring — meaning that we take existing code and move it into a new function: we “extract” the code out into a new function.
- For example, try to guess what the following line does:

  ```javascript
  var width = (value - 0.5) * 16;
  ```

- Not very clear; a comment here could be quite useful. Or, we could extract a function to make it self documenting:

  ```javascript
  var width = emToPixels(value);

  function emToPixels(ems) {
      return (ems - 0.5) * 16;
  }

```
### 2.Replace conditional expression with function:

- If clauses with multiple operands can often be hard to understand without a comment. We can apply a similar method as above to clarify them:

  ```javascript
  if(!el.offsetWidth || !el.offsetHeight) {
  }
  ```

- What is the purpose of the above condition?

  ```javascript
  function isVisible(el) {
      return el.offsetWidth && el.offsetHeight;
  }

  if(!isVisible(el)) {
  }
  ```

- Again, we moved the code into a function and the code is immediately much easier to understand.

### 3.Replace expression with variable

- Replacing something with a variable is similar to moving code into a function, but instead of a function, we simply use a variable.
- Let’s take a look at the example with if clauses again:

  ```javascript
  if(!el.offsetWidth || !el.offsetHeight) {
  }
  ```
- Instead of extracting a function, we can also clarify this by introducing a variable:

  ```javascript
  var isVisible = el.offsetWidth && el.offsetHeight;
    if(!isVisible) {
  }
  ```
- This can be a better choice than extracting a function — for example, when the logic you want to clarify is very specific to a certain algorithm used only in one place.
- The most common use for this method is mathematical expressions:

  ```javascript
  return a * b + (c / d);
  ```

- We can clarify the above by splitting the calculation:

  ```javascript
  var multiplier = a * b;
  var divisor = c / d;
  return multiplier + divisor;
  ```
- Because I’m terrible at math, imagine the above example has some meaningful algorithm. In any case, the point is that you can move complex expressions into variables that add meaning to otherwise hard-to-understand code.

### 4.Class and module interfaces

- The interface — that is, the public methods and properties — of a class or module can act as documentation on its usage.
- Let’s look at an example:

  ```javascript
  class Box {
      setState(state) {
          this.state = state;
      }

      getState() {
          return this.state;
      }
  }
  ```

- What if we changed it to something like this:

  ```javascript
  class Box {
      open() {
          this.state = 'open';
      }

      close() {
          this.state = 'closed';
      }

      isOpen() {
          return this.state === 'open';
      }
  }
  ```

- Much easier to see the usage, don’t you think? Notice that we only changed the public interface; the internal representation is still the same with the this.state property.
- Now you can tell at a glance how the Box class is used. This shows that even though the first version had good names in the functions, the complete package was still confusing, and how, with simple decisions like this, you can have a very big impact. You always have to think of the big picture.

### 5.Code grouping

- Consider the following example:

  ```javascript
  var foo = 1;

  blah()
  xyz();

  bar(foo);
  baz(1337);
  quux(foo);
  ```

- Can you see at a glance how many times foo was used? Compare it to this:

  ```javascript
  var foo = 1;
  bar(foo);
  quux(foo);

  blah()
  xyz();

  baz(1337);
  ```
### 6.Use pure functions

- Pure functions are much easier to understand than functions that rely on state.
- What is a pure function? When calling a function with the same parameters, if it always produces the same output, it’s most likely a so-called “pure” function. This means the function should not have any side effects or rely on state — such as time, object properties, Ajax, etc.
- These types of functions are easier to understand, as any values affecting their output are passed in explicitly. You won’t have to dig around to figure out where something comes from, or what affects the result, as it’s all in plain sight.
- Another reason these types of functions make for more self-documenting code is you can trust their output. No matter what, the function will always return output only based on what parameters you give it. It also won’t affect anything external, so you can trust it won’t cause an unexpected side effect.
- A good example of where this goes wrong is ```document.write()```. Experienced JS developers know you shouldn’t use it, but many beginners stumble with it. Sometimes it works well — but other times, in certain circumstances, it can wipe the whole page clean. Talk about a side effect!
- For a better overview of what a pure function is, see the article [Functional Programming]: Pure Functions(https://www.sitepoint.com/functional-programming-pure-functions/).

### 7.Directory and file structure
- When naming files or directories, follow the same naming convention as used in the project. If there’s no clear convention in the project, follow the standard for your language of choice.
- For example, if you’re adding new UI-related code, find where similar functionality is in the project. If UI-related code is placed in src/ui/, you should do the same.
- This makes it easier to find the code and shows its purpose, based on what you already know about the other pieces of code in the project. All UI code is in the same place, after all, so it must be UI related.

# II.Naming

- There’s a popular quote about the two hard things in computer science:
- There are only two hard things in Computer Science: cache invalidation and naming things. — Phil Karlton
- So let’s take a look at how we can use naming things to make our code self documenting.
### 9.Rename function
- Function naming is often not too difficult, but there’s some simple rules that you can follow:
- Avoid using vague words like “handle” or “manage”: ```handleLinks(), manageObjects()```. What do either of these do?
- Use active verbs: ```cutGrass(), sendFile()``` — functions that actively perform something.
- Indicate return value: ```getMagicBullet(), readFile()```. This is not something you can always do, but it’s helpful where it makes sense.
- Languages with strong typing can use type signatures to help indicate return values as well.

### 10. Rename variable

- With variables, here are two good rules of thumb:

  + Indicate units: if you have numeric parameters, you can include the expected unit. For example, widthPx instead of width to indicate the value is in pixels instead of some other unit.
  + Don’t use shortcuts: a or b are not acceptable names, except for counters in loops.
### 11.Follow established naming conventions
- Try to follow the same naming conventions in your code. For example, if you have an object of a specific type, call it the same name:

  ```javascript
  var element = getElement();
  ```
- Don’t suddenly decide to call it a node:
  ```javascript
  var node = getElement();
  ```
- If you follow the same conventions as elsewhere in the codebase, anyone reading it can make safe assumptions about the meanings of things based on what it means elsewhere.
### 12. Use meaningful errors
- Undefined is not an object!
- Everyone’s favorite. Let’s not follow JavaScript’s example, and let’s make sure any errors our code throws have a meaningful message in them.
- What makes an error message meaningful?
  + it should describe what the problem was
  + if possible, it should include any variable values or other data which caused the error
  + key point: the error should help us find out what went wrong — therefore acting as documentation on how the function should work.
# III. Syntax
- Syntax-related methods for self-documenting code can be a little bit more language specific. For example, Ruby and Perl allow you to do all kinds of strange syntax tricks, which, in general, should be avoided.
- Let’s take a look at a few that happen with JavaScript.
### 1.Don’t use syntax tricks
- Don’t use strange tricks. Here’s a good way to confuse people:

  ```javascript
  imTricky && doMagic();
  ```
- It’s equivalent to this much more sane looking code:

  ```javascript
  if(imTricky) {
      doMagic();
  }
  ```
- Always prefer the latter form. Syntax tricks are not going to do anyone any favors.

### 2.Use named constants, avoid magic values
- If you have special values in your code — such as numbers or string values — consider using a constant instead. Even if it seems clear now, more often than not, when coming back to it in a month or two, nobody will have any idea why that particular number was put there.

  ```javascript
  const MEANING_OF_LIFE = 42;
  ```
- (If you’re not using ES6, you can use a var and it’ll work equally well.)
### 3.Avoid boolean flags
- Boolean flags can make for hard-to-understand code. Consider this:

  ```javascript
  myThing.setData({ x: 1 }, true);
  ```
- What is the meaning of true? You have absolutely no idea, unless you dig into the source for setData() and find out.
- Instead, you can add another function, or rename an existing function:

  ```javascript
  myThing.mergeData({ x: 1 });
  ```
- Now you can immediately tell what’s going on.
### 4. Use language features to your advantage
- We can even use some features of our chosen language to better communicate the intention behind some code.
- A good example of this in JavaScript are the array iteration methods:

  ```javascript
  var ids = [];
  for(var i = 0; i < things.length; i++) {
    ids.push(things[i].id);
  }
  ```
- The above code collects a list of IDs into a new array. However, in order to know that, we need to read the whole body of the loop. Compare it with using map():

  ```javascript
  var ids = things.map(function(thing) {
    return thing.id;
  });
  ```
- In this case, we immediately know that this produces a new array of something, because that’s the purpose of map(). This can be beneficial especially if you have more complicated looping logic. There’s a list of other iteration functions on MDN.
- Another example with JavaScript is the const keyword.
- Often, you declare variables where the value is supposed to never change. A very common example is when loading modules with CommonJS:

  ```javascript
  var async = require('async');
  ```
- We can make the intention of never changing this even more clear:

  ```javascript
  const async = require('async');
  ```
- As an added benefit, if someone ever accidentally tries to change this, we’ll now get an error.
