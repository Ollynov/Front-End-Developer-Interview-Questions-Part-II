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


# Javascript with the Modern Browser
### Describe the global 'document' variable

Whenever a browser opens up a webpage, it pulls in the html, parses it, and builds up the Document Object Model (DOM). It is a data structure, that can be modified, and then it immediately updates the webpage. The 'document' variable refers to this DOM object. It is a tree-like data structure, where document.documentElement is the root. Every node in this DOM object may have child nodes, or 'leaves' which are properties that are either variables or values and do not have further child nodes. Each DOM node has a children property, which will log onto the console all of the child nodes. You can play around with this, open up the console (cmd + option + i), and run: 
```
console.log(document.documentElement.children)
// and you will get: 
HTMLCollection[2]
0:head
1:body.logged-in.env-production.macintosh.vis-public.page-edit-blob
length:2
__proto__:HTMLCollection
```
Every DOM node also has a nodeType property which will return a number, that represents what sort of node it is. A 1 represents a regular element. A 3 represents text. An 8 represents a comment block. 

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
