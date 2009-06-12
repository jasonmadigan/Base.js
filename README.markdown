From http://dean.edwards.name/weblog/2006/03/base/

The Base Class
==============

I’ve created a JavaScript class (Base.js) that I hope eases the pain of JavaScript OO. It’s a simple class and extends the Object object by adding two instance methods and one class method.

The Base class defines two instance methods:

extend
------
Call this method to extend an object with another interface:

    var object = new Base;
    object.extend({
      value: "some data",
      method: function() {
        alert("Hello World!");
      }
    });
    object.method();
    // ==> Hello World!
    
base
----
If a method has been overridden then the base method provides access to the overridden method:

    var object = new Base;
    object.method = function() {
      alert("Hello World!");
    };
    object.extend({
      method: function() {
        // call the "super" method
        this.base();
        // add some code
        alert("Hello again!");
      }
    });
    object.method();
    // ==> Hello World!
    // ==> Hello again!
    
You can also call the base method from within a constructor function.

Creating Classes
================
Classes are created by calling the extend method on the Base class:

    var Animal = Base.extend({
      constructor: function(name) {
        this.name = name;
      },
  
      name: "",
  
      eat: function() {
        this.say("Yum!");
      },
  
      say: function(message) {
        alert(this.name + ": " + message);
      }
    });
    
All classes created in this manner will inherit the extend method so we can easily subclass the Animal class:

    var Cat = Animal.extend({
      eat: function(food) {
        if (food instanceof Mouse) this.base();
        else this.say("Yuk! I only eat mice.");
      }
    });
  
    var Mouse = Animal.extend();
    
Class Properties and Methods
============================
A second parameter passed to the extend method of a class defines the class interface:

    var Circle = Shape.extend({ // instance interface
      constructor: function(x, y, radius) {
        this.base(x, y);
        this.radius = radius;
      },
  
      radius: 0,
  
      getCircumference: function() {
        return 2 * Circle.PI * this.radius;
      }
    }, { // class interface
      PI: 3.14
    });
    
Note the use of the base method in the constructor. This ensures that the Shape constructor is also called. Some other things to note:

  * If you define a class method (not an instance method) called init it will be automatically called when the class is created
  * Constructor functions are never called during the prototyping phase (subclassing)
