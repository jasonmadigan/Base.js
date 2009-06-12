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