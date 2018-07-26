#### I. JavaScript Design Pattern Genneral
---
**Reference**: https://addyosmani.com/resources/essentialjsdesignpatterns/book/#summarytabledesignpatterns

1. [Constructor Pattern](#constructor-pattern)
1. [Module Pattern](#module-pattern)
1. [Revealing Module Pattern](#revealing-module-pattern)
1. [Singleton Pattern](#singleton-pattern)
1. [Observer Pattern](#observer-pattern)
1. [Mediator Pattern](#mediator-pattern)
1. [Prototype Pattern](#prototype-pattern)
1. [Command Pattern](#command-pattern)
1. [Facade Pattern](#facade-pattern)
1. [Factory Pattern](#factory-pattern)
1. [Mixin Pattern](#mixin-pattern)
1. [Decorator Pattern](#decorator-pattern)
1. [Flyweight Pattern](#flyweight-pattern)

## Constructor Pattern
**1. Object Creation**
- Ba cách phổ biến để tạo các đối tượng mới trong JavaScript như sau:

```javascript
// Each of the following options will create a new empty object:
 
var newObject = {};
 
// or
var newObject = Object.create( Object.prototype );
 
// or
var newObject = new Object();
```
- Sau đó có bốn cách mà sau đó các ```key``` và ```value``` có thể được gán cho một đối tượng:

```
// ECMAScript 3 compatible approaches
 
// 1. Dot syntax
 
// Set properties
newObject.someKey = "Hello World";
 
// Get properties
var value = newObject.someKey;
 
 
 
// 2. Square bracket syntax
 
// Set properties
newObject["someKey"] = "Hello World";
 
// Get properties
var value = newObject["someKey"];
 
 
 
// ECMAScript 5 only compatible approaches
// For more information see: http://kangax.github.com/es5-compat-table/
 
// 3. Object.defineProperty
 
// Set properties
Object.defineProperty( newObject, "someKey", {
    value: "for more control of the property's behavior",
    writable: true,
    enumerable: true,
    configurable: true
});
 
// If the above feels a little difficult to read, a short-hand could
// be written as follows:
 
var defineProp = function ( obj, key, value ){
  var config = {
    value: value,
    writable: true,
    enumerable: true,
    configurable: true
  };
  Object.defineProperty( obj, key, config );
};
 
// To use, we then create a new empty "person" object
var person = Object.create( Object.prototype );
 
// Populate the object with properties
defineProp( person, "car", "Delorean" );
defineProp( person, "dateOfBirth", "1981" );
defineProp( person, "hasBeard", false );
 
console.log(person);
// Outputs: Object {car: "Delorean", dateOfBirth: "1981", hasBeard: false}
 
 
// 4. Object.defineProperties
 
// Set properties
Object.defineProperties( newObject, {
 
  "someKey": {
    value: "Hello World",
    writable: true
  },
 
  "anotherKey": {
    value: "Foo bar",
    writable: false
  }
 
});
 
// Getting properties for 3. and 4. can be done using any of the
// options in 1. and 2.
```
- Như chúng ta sẽ thấy một chút sau trong cuốn sách, các phương thức này thậm chí có thể được sử dụng để thừa kế(inheritance), như sau
```javascript

```

```javascript
// Usage:
 
// Create a race car driver that inherits from the person object
var driver = Object.create( person );
 
// Set some properties for the driver
defineProp(driver, "topSpeed", "100mph");
 
// Get an inherited property (1981)
console.log( driver.dateOfBirth );
 
// Get the property we set (100mph)
console.log( driver.topSpeed );
```
**2. Basic Constructors**

```javascript
function Car( model, year, miles ) {
 
  this.model = model;
  this.year = year;
  this.miles = miles;
 
  this.toString = function () {
    return this.model + " has done " + this.miles + " miles";
  };
}
 
// Usage:
 
// We can create new instances of the car
var civic = new Car( "Honda Civic", 2009, 20000 );
var mondeo = new Car( "Ford Mondeo", 2010, 5000 );
 
// and then open our browser console to view the
// output of the toString() method being called on
// these objects
console.log( civic.toString() );
console.log( mondeo.toString() );
```
**3. Constructors With Prototypes**

```javascript
function Car( model, year, miles ) {
 
  this.model = model;
  this.year = year;
  this.miles = miles;
 
}
 
 
// Note here that we are using Object.prototype.newMethod rather than
// Object.prototype so as to avoid redefining the prototype object
Car.prototype.toString = function () {
  return this.model + " has done " + this.miles + " miles";
};
 
// Usage:
 
var civic = new Car( "Honda Civic", 2009, 20000 );
var mondeo = new Car( "Ford Mondeo", 2010, 5000 );
 
console.log( civic.toString() );
console.log( mondeo.toString() );
```

## Module Pattern
- Trong JavaScript, có một số tùy chọn để triển khai các mô-đun. Bao gồm các:
  + The Module pattern
  + Object literal notation
  + AMD modules
  + CommonJS modules
  + ECMAScript Harmony modules

**1. Object Literals**
```javascript

```

**2. The Module Pattern**

- Chúng ta hãy bắt đầu xem xét việc thực hiện mô hình Module bằng cách tạo ra một mô-đun độc lập.

```javascript
var testModule = (function () {
 
  var counter = 0;
 
  return {
 
    incrementCounter: function () {
      return counter++;
    },
 
    resetCounter: function () {
      console.log( "counter value prior to reset: " + counter );
      counter = 0;
    }
  };
 
})();
 
// Usage:
 
// Increment our counter
testModule.incrementCounter();
 
// Check the counter value and reset
// Outputs: counter value prior to reset: 1
testModule.resetCounter();
```

- Khi làm việc với mẫu Mô-đun, chúng tôi có thể thấy hữu ích khi xác định một mẫu đơn giản mà chúng tôi sử dụng để bắt đầu với mẫu đó. Dưới đây là một trong đó bao gồm các biến không gian tên, public và private:

```javascript
var myNamespace = (function () {
 
  var myPrivateVar, myPrivateMethod;
 
  // A private counter variable
  myPrivateVar = 0;
 
  // A private function which logs any arguments
  myPrivateMethod = function( foo ) {
      console.log( foo );
  };
 
  return {
 
    // A public variable
    myPublicVar: "foo",
 
    // A public function utilizing privates
    myPublicFunction: function( bar ) {
 
      // Increment our private counter
      myPrivateVar++;
 
      // Call our private method using bar
      myPrivateMethod( bar );
 
    }
  };
 
})();
```

```javascript
var basketModule = (function () {
 
  // privates
 
  var basket = [];
 
  function doSomethingPrivate() {
    //...
  }
 
  function doSomethingElsePrivate() {
    //...
  }
 
  // Return an object exposed to the public
  return {
 
    // Add items to our basket
    addItem: function( values ) {
      basket.push(values);
    },
 
    // Get the count of items in the basket
    getItemCount: function () {
      return basket.length;
    },
 
    // Public alias to a private function
    doSomething: doSomethingPrivate,
 
    // Get the total value of items in the basket
    getTotal: function () {
 
      var q = this.getItemCount(),
          p = 0;
 
      while (q--) {
        p += basket[q].price;
      }
 
      return p;
    }
  };
})();
```
- Bên trong module, bạn có thể nhận thấy rằng chúng ta trả về một đối tượng. Điều này được tự động gán cho basketModule để chúng ta có thể tương tác với nó như sau:

```javascript
// basketModule returns an object with a public API we can use
 
basketModule.addItem({
  item: "bread",
  price: 0.5
});
 
basketModule.addItem({
  item: "butter",
  price: 0.3
});
 
// Outputs: 2
console.log( basketModule.getItemCount() );
 
// Outputs: 0.8
console.log( basketModule.getTotal() );
 
// However, the following will not work:
 
// Outputs: undefined
// This is because the basket itself is not exposed as a part of our
// public API
console.log( basketModule.basket );
 
// This also won't work as it only exists within the scope of our
// basketModule closure, but not in the returned public object
console.log( basket );
```
**2. Module Pattern Variations**

**2.1 Import mixins**

```javascript
// Global module
var myModule = (function ( jQ, _ ) {
 
    function privateMethod1(){
        jQ(".container").html("test");
    }
 
    function privateMethod2(){
      console.log( _.min([10, 5, 100, 2, 1000]) );
    }
 
    return{
        publicMethod: function(){
            privateMethod1();
        }
    };
 
// Pull in jQuery and Underscore
})( jQuery, _ );
 
myModule.publicMethod();
```

**2.2 Exports**

```javascript
// Global module
var myModule = (function () {
 
  // Module object
  var module = {},
    privateVariable = "Hello World";
 
  function privateMethod() {
    // ...
  }
 
  module.publicProperty = "Foobar";
  module.publicMethod = function () {
    console.log( privateVariable );
  };
 
  return module;
 
})();
```

**2.3 Dojo**

```javascript
var store = window.store || {};
 
if ( !store["basket"] ) {
  store.basket = {};
}
 
if ( !store.basket["core"] ) {
  store.basket.core = {};
}
 
store.basket.core = {
  // ...rest of our logic
};
```

- Hoặc như sau sử dụng Dojo 1.7 (phiên bản tương thích với AMD) trở lên:

```javascript
require(["dojo/_base/customStore"], function( store ){
 
  // using dojo.setObject()
  store.setObject( "basket.core", (function() {
 
      var basket = [];
 
      function privateMethod() {
          console.log(basket);
      }
 
      return {
          publicMethod: function(){
                  privateMethod();
          }
      };
 
  })());
 
});
```

**2.4 ExtJS**

```javascript
// create namespace
Ext.namespace("myNameSpace");
 
// create application
myNameSpace.app = function () {
 
  // do NOT access DOM from here; elements don't exist yet
 
  // private variables
  var btn1,
      privVar1 = 11;
 
  // private functions
  var btn1Handler = function ( button, event ) {
      console.log( "privVar1=" + privVar1 );
      console.log( "this.btn1Text=" + this.btn1Text );
    };
 
  // public space
  return {
    // public properties, e.g. strings to translate
    btn1Text: "Button 1",
 
    // public methods
    init: function () {
 
      if ( Ext.Ext2 ) {
 
        btn1 = new Ext.Button({
          renderTo: "btn1-ct",
          text: this.btn1Text,
          handler: btn1Handler
        });
 
      } else {
 
        btn1 = new Ext.Button( "btn1-ct", {
          text: this.btn1Text,
          handler: btn1Handler
        });
 
      }
    }
  };
}();
```

**2.5 YUI**

```javascript
Y.namespace( "store.basket" ) ;
Y.store.basket = (function () {
 
    var myPrivateVar, myPrivateMethod;
 
    // private variables:
    myPrivateVar = "I can be accessed only within Y.store.basket.";
 
    // private method:
    myPrivateMethod = function () {
        Y.log( "I can be accessed only from within YAHOO.store.basket" );
    }
 
    return {
        myPublicProperty: "I'm a public property.",
 
        myPublicMethod: function () {
            Y.log( "I'm a public method." );
 
            // Within basket, I can access "private" vars and methods:
            Y.log( myPrivateVar );
            Y.log( myPrivateMethod() );
 
            // The native scope of myPublicMethod is store so we can
            // access public members using "this":
            Y.log( this.myPublicProperty );
        }
    };
 
})();
```

**2.6 jQuery**

```javascript
function library( module ) {
 
  $( function() {
    if ( module.init ) {
      module.init();
    }
  });
 
  return module;
}
 
var myLibrary = library(function () {
 
  return {
    init: function () {
      // module implementation
    }
  };
}());
```

## Revealing Module Pattern

- Một ví dụ về cách sử dụng mô hình Revealing Module có thể được tìm thấy dưới đây:

```javascript
var myRevealingModule = (function() {

  var privateVar = "Ben Cherry",
    publicVar = "Hey there!";

  function privateFunction() {
    console.log("Name:" + privateVar);
  }

  function publicSetName(strName) {
    privateVar = strName;
  }

  function publicGetName() {
    privateFunction();
  }


  // Reveal public pointers to
  // private functions and properties

  return {
    setName: publicSetName,
    greeting: publicVar,
    getName: publicGetName
  };

})();

myRevealingModule.setName("Paul Kinlan");
```

- Mẫu này cũng có thể được sử dụng để tiết lộ các hàm và thuộc tính riêng với lược đồ đặt tên cụ thể hơn nếu chúng ta muốn:

```javascript
var myRevealingModule = (function() {

  var privateCounter = 0;

  function privateFunction() {
    privateCounter++;
  }

  function publicFunction() {
    publicIncrement();
  }

  function publicIncrement() {
    privateFunction();
  }

  function publicGetCount() {
    return privateCounter;
  }

  // Reveal public pointers to
  // private functions and properties

  return {
    start: publicFunction,
    increment: publicIncrement,
    count: publicGetCount
  };

})();

myRevealingModule.start();
```

## Singleton Pattern

**1. Chúng ta có thể thực hiện Singleton như sau:**
```javascript
var mySingleton = (function () {
 
  // Instance stores a reference to the Singleton
  var instance;
 
  function init() {
 
    // Singleton
 
    // Private methods and variables
    function privateMethod(){
        console.log( "I am private" );
    }
 
    var privateVariable = "Im also private";
 
    var privateRandomNumber = Math.random();
 
    return {
 
      // Public methods and variables
      publicMethod: function () {
        console.log( "The public can see me!" );
      },
 
      publicProperty: "I am also public",
 
      getRandomNumber: function() {
        return privateRandomNumber;
      }
 
    };
 
  };
 
  return {
 
    // Get the Singleton instance if one exists
    // or create one if it doesn't
    getInstance: function () {
 
      if ( !instance ) {
        instance = init();
      }
 
      return instance;
    }
 
  };
 
})();
 
var myBadSingleton = (function () {
 
  // Instance stores a reference to the Singleton
  var instance;
 
  function init() {
 
    // Singleton
 
    var privateRandomNumber = Math.random();
 
    return {
 
      getRandomNumber: function() {
        return privateRandomNumber;
      }
 
    };
 
  };
 
  return {
 
    // Always create a new Singleton instance
    getInstance: function () {
 
      instance = init();
 
      return instance;
    }
 
  };
 
})();
 
 
// Usage:
 
var singleA = mySingleton.getInstance();
var singleB = mySingleton.getInstance();
console.log( singleA.getRandomNumber() === singleB.getRandomNumber() ); // true
 
var badSingleA = myBadSingleton.getInstance();
var badSingleB = myBadSingleton.getInstance();
console.log( badSingleA.getRandomNumber() !== badSingleB.getRandomNumber() ); // true
 
// Note: as we are working with random numbers, there is a
// mathematical possibility both numbers will be the same,
// however unlikely. The above example should otherwise still
// be valid.
```

- Điểm thứ hai trong số này đề cập đến trường hợp chúng ta có thể cần mã như:

```javascript
mySingleton.getInstance = function(){
  if ( this._instance == null ) {
    if ( isFoo() ) {
       this._instance = new FooSingleton();
    } else {
       this._instance = new BasicSingleton();
    }
  }
  return this._instance;
};
```

- Trong thực tế, mẫu Singleton rất hữu ích khi chính xác một đối tượng là cần thiết để điều phối những người khác trên một hệ thống. Dưới đây là một ví dụ với mẫu được sử dụng trong ngữ cảnh này:

```javascript
var SingletonTester = (function () {
 
  // options: an object containing configuration options for the singleton
  // e.g var options = { name: "test", pointX: 5};
  function Singleton( options ) {
 
    // set options to the options supplied
    // or an empty object if none are provided
    options = options || {};
 
    // set some properties for our singleton
    this.name = "SingletonTester";
 
    this.pointX = options.pointX || 6;
 
    this.pointY = options.pointY || 10;
 
  }
 
  // our instance holder
  var instance;
 
  // an emulation of static variables and methods
  var _static = {
 
    name: "SingletonTester",
 
    // Method for getting an instance. It returns
    // a singleton instance of a singleton object
    getInstance: function( options ) {
      if( instance === undefined ) {
        instance = new Singleton( options );
      }
 
      return instance;
 
    }
  };
 
  return _static;
 
})();
 
var singletonTest = SingletonTester.getInstance({
  pointX: 5
});
 
// Log the output of pointX just to verify it is correct
// Outputs: 5
console.log( singletonTest.pointX );
```

## Observer Pattern

- **Subject:** duy trì danh sách các nhà ```observers```, tạo điều kiện thêm hoặc xóa người ```observers```.
- **Observer:** cung cấp một giao diện cập nhật cho các đối tượng cần được thông báo về các thay đổi trạng thái của một Subject's.
- **ConcreteSubject:** phát sóng notifications cho người quan sát về những thay đổi của state, lưu trữ state của ```ConcreteObservers```
- **ConcreteObserver:** lưu trữ một tham chiếu đến ```ConcreteSubject```, thực hiện một giao diện cập nhật cho ```Observer``` để đảm bảo trạng thái phù hợp với Subject's

**1. Trước tiên, hãy lập mô hình danh sách các nhà dependent Observers một chủ đề có thể có:**

```javascript
function ObserverList(){
  this.observerList = [];
}
 
ObserverList.prototype.add = function( obj ){
  return this.observerList.push( obj );
};
 
ObserverList.prototype.count = function(){
  return this.observerList.length;
};
 
ObserverList.prototype.get = function( index ){
  if( index > -1 && index < this.observerList.length ){
    return this.observerList[ index ];
  }
};
 
ObserverList.prototype.indexOf = function( obj, startIndex ){
  var i = startIndex;
 
  while( i < this.observerList.length ){
    if( this.observerList[i] === obj ){
      return i;
    }
    i++;
  }
 
  return -1;
};
 
ObserverList.prototype.removeAt = function( index ){
  this.observerList.splice( index, 1 );
};
```

**2.Tiếp theo, hãy mô hình hóa Chủ đề và khả năng thêm, xóa hoặc thông báo cho observer trên observer list.**

```javascript
function Subject(){
  this.observers = new ObserverList();
}
 
Subject.prototype.addObserver = function( observer ){
  this.observers.add( observer );
};
 
Subject.prototype.removeObserver = function( observer ){
  this.observers.removeAt( this.observers.indexOf( observer, 0 ) );
};
 
Subject.prototype.notify = function( context ){
  var observerCount = this.observers.count();
  for(var i=0; i < observerCount; i++){
    this.observers.get(i).update( context );
  }
};
```

**3. Sau đó, chúng tôi xác định một bộ xương để tạo Observers mới. Chức năng ```update``` ở đây sẽ được ghi đè sau bằng hành vi tùy chỉnh.**

```javascript
// The Observer
function Observer(){
  this.update = function(){
    // ...
  };
}
```

```
<button id="addNewObserver">Add New Observer checkbox</button>
<input id="mainCheckbox" type="checkbox"/>
<div id="observersContainer"></div>
```

```javascript
// Extend an object with an extension
function extend( obj, extension ){
  for ( var key in extension ){
    obj[key] = extension[key];
  }
}
 
// References to our DOM elements
 
var controlCheckbox = document.getElementById( "mainCheckbox" ),
  addBtn = document.getElementById( "addNewObserver" ),
  container = document.getElementById( "observersContainer" );
 
 
// Concrete Subject
 
// Extend the controlling checkbox with the Subject class
extend( controlCheckbox, new Subject() );
 
// Clicking the checkbox will trigger notifications to its observers
controlCheckbox.onclick = function(){
  controlCheckbox.notify( controlCheckbox.checked );
};
 
addBtn.onclick = addNewObserver;
 
// Concrete Observer
 
function addNewObserver(){
 
  // Create a new checkbox to be added
  var check = document.createElement( "input" );
  check.type = "checkbox";
 
  // Extend the checkbox with the Observer class
  extend( check, new Observer() );
 
  // Override with custom update behaviour
  check.update = function( value ){
    this.checked = value;
  };
 
  // Add the new observer to our list of observers
  // for our main subject
  controlCheckbox.addObserver( check );
 
  // Append the item to the container
  container.appendChild( check );
}
```

**4. Sự khác biệt giữa Observer và Publish / Subscribe Pattern**
```javascript

```

**1. Object Creation**
```javascript

```

**1. Object Creation**
```javascript

```

**1. Object Creation**
```javascript

```
## Mediator Pattern
**1. Object Creation**
```javascript

```

**1. Object Creation**
```javascript

```

**1. Object Creation**
```javascript

```

**1. Object Creation**
```javascript

```

**1. Object Creation**
```javascript

```

**1. Object Creation**
```javascript

```

**1. Object Creation**
```javascript

```
## Prototype Pattern
**1. Object Creation**
```javascript

```

**1. Object Creation**
```javascript

```

**1. Object Creation**
```javascript

```

**1. Object Creation**
```javascript

```

**1. Object Creation**
```javascript

```

**1. Object Creation**
```javascript

```

**1. Object Creation**
```javascript

```
## Command Pattern
**1. Object Creation**
```javascript

```

**1. Object Creation**
```javascript

```

**1. Object Creation**
```javascript

```

**1. Object Creation**
```javascript

```

**1. Object Creation**
```javascript

```

**1. Object Creation**
```javascript

```

**1. Object Creation**
```javascript

```
## Facade Pattern
**1. Object Creation**
```javascript

```

**1. Object Creation**
```javascript

```

**1. Object Creation**
```javascript

```

**1. Object Creation**
```javascript

```

**1. Object Creation**
```javascript

```

**1. Object Creation**
```javascript

```

**1. Object Creation**
```javascript

```
## Factory Pattern
**1. Object Creation**
```javascript

```

**1. Object Creation**
```javascript

```

**1. Object Creation**
```javascript

```

**1. Object Creation**
```javascript

```

**1. Object Creation**
```javascript

```

**1. Object Creation**
```javascript

```

**1. Object Creation**
```javascript

```
## Mixin Pattern
**1. Object Creation**
```javascript

```

**1. Object Creation**
```javascript

```

**1. Object Creation**
```javascript

```

**1. Object Creation**
```javascript

```

**1. Object Creation**
```javascript

```

**1. Object Creation**
```javascript

```

**1. Object Creation**
```javascript

```
## Decorator Pattern
**1. Object Creation**
```javascript

```

**1. Object Creation**
```javascript

```

**1. Object Creation**
```javascript

```

**1. Object Creation**
```javascript

```

**1. Object Creation**
```javascript

```

**1. Object Creation**
```javascript

```

**1. Object Creation**
```javascript

```
## Flyweight Pattern
**1. Object Creation**
```javascript

```

**1. Object Creation**
```javascript

```

**1. Object Creation**
```javascript

```

**1. Object Creation**
```javascript

```

**1. Object Creation**
```javascript

```

**1. Object Creation**
```javascript

```

**1. Object Creation**
```javascript

```
