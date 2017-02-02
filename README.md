# Front-End-Developer-Interview-Questions-Part-II
An extension to the ever famous front-end-developer-interview-questions github repo. 

# Modules
### Describe the require function. 
### Describe in detail the readFile function

Javascript environments (browser, Node) each have a built in readFile function, which first takes the path of a file, and returns the contents as a large string. The next step is to actually take this data (in string format), and evaluate it as code. The most simple way is with the built-in eval operator: 
```
function returnAfterEval(data) {
  eval(data);
  return x;
}

console.log(returnAfterEval("var x = 'hello world'"));
// hello world
```

Another method of evaluating a piece of data (string) as code is to pass in the data directly into the Function constructor. 
```
var evaluated = new Function("x, y", "return x + y");
console.log(evaluated(2, 3))
// 5
```

The constructor takes two arguments, the first being a string with comma separated argument names, and the second argument being a string with the body of the function. 






# Non- Categorized for now
### What is 'use strict' mode?

You can type in 'use strict' (just a string) at the top of your javascript code (you can also just place in a function to contain to only that scope) and 'opt in' to a more strict interpretation of the code- much of the reason for this has to do with the fact that javascript has some quirks and flaws, and strict mode helps you avoid them. For example, in strict mode you are forbidden to redefine the special arguments keyword: 
```
"use strict";
var arguments = 'new';
console.log(arguments)

var arguments = 'new';
    ^^^^^^^^^
SyntaxError: Unexpected eval or arguments in strict mode
```

### What is a network protocol?
A protocol describes the style of communication over a particular network. There are protocols for sending email, for fetching email, for sharing files, or even for controlling computers that happen to be infected by malicious software. The two most commone for requesting a url are HTTP and HTTPS.
