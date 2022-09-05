# JavaVM.js
A Java Virtual Machine written entirely in JavaScript allowing Java bytecode to be executed in a browser.

## Why
Browsers used to come equipped with JVM's back when Java Applets were a thing, but now that is a thing of the past. Now there are many resources out there to let you transpile your Java code to JavaScript allowing you to run your Java program in a JavaScript environment such as a browser. But that wasn't good enough for me because I didn't want to lose any of the behaviors of Java. I needed the Java to be executed with the same rules as if it were being run natively. I searched for an already existing solution and the two things I found were: https://github.com/Jivings/jsJVM and https://github.com/plasma-umass/doppio . jsJVM hadn't been updated in 10 years meaning that it is extremely outdated and doesn't use any of the modern JavaScript features which would allow improved perfomrance. Not only that, but all its links led to websites that don't exist anymore; leaving with me no documentation about how to even use it. Doppio is less outdated than jsJVM and runs Java 8, but still is quite old compared to the latest stable version of Java is version 17. But the bigger issue for me was that it's not so much just a JVM, rather it is more like an entire OS simulator written in JS and as a result using it requires downloading 40 MB (not exactly lightweight) of source code every time you want to use it. So I decided to try and create my own JVM in JS with the goal of it being as lightweight, fast, and easy to use as possible. Plus I really just thought it would be a cool project to create my own JVM.

## Usage
1) Import the JavaVM.js script (https://cdn.jsdelivr.net/gh/vExcess/JavaVM.js/JavaVM.js)
2) Follow the code below:
```javascript
// create a new JVM
var myJVM = createJVM();

// attach any native handlers you would like. These allow input/output from JavaScript
// the println handler should expect (String value)
myJVM.attachHandler("println", println);
// the debug handler should expect (String value, String scope)
myJVM.attachHandler("debug", debug);
// the throwError handler should expect (String value, String scope, String code)
myJVM.attachHandler("throwError", throwError);

// load a string of bytecode into the JVM. The bytecode should be in the format returned by calling `javap -c -p -v Example.class`
myJVM.loadByteCode(bytecode);

// execute the loaded bytecode (invokes the loaded classes' main method)
myJVM.init();
```

## Future Improvements
Since my goal is for this to be a lightweight and fast as possible, once I get a production worthy version of this written in JavaScript I will rewrite my JVM in Web Assembly. This will allow for the JVM to be more compact allowing for significantly faster loading speeds. Not only that, but being written in WASM will allow the JVM run only 1.5x slower than native Java; much faster than it could run being written in JavaScript (Doppio is written in 100% JS).

## Status
I just started this project very recently so there is still a lot to come.
Currently it has very limited support for Java. 
Less than 20% of Java's opcodes are supported.
And there is next to no support for standard Java libraries.

## Contribute
There is bound to be a gazillion bugs in with my JVM.
If you find any bugs please report an issue.
Also if you have and code contributions that would be helpful.
