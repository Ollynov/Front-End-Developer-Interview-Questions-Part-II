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

# React
### Why should the render() function of a component be 'pure', and what does that mean?

For starters, the render() function doesn't necessarily need to be 'pure', but it _should be_ so it does not produce any tricky errors, and so that your entire app can have a structure that is easier to reason about. A pure function must return the same result each time that it is invoked. For render(), this means that it should not modify component state. The lifecycle functions, such as componentWillMount() and componentDidMount() should be used for state change. 

### When would it be unnecessary to include a constructor() in your component?

If your react component has no props being passed down to it, has no state, and has no function bindings, then you do not need a contructor function. 

### What is super(props)? 

Inside of a components constructor method, you need to include super(props) if you are having props passed down, before any other statements. If you don't include it, then 'this.props' will be undefined. The following code will work just as well:
```
constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }
// this works just the same
constructor(props) {
    super();
    this.state = {date: new Date()};
  }
```
Both work. The only difference is that when you pass props into super, super(props), then you have access to props in the constructor as this.props as well. As of now, this is the way props is passed down in the React documentation, so we'll follow that. 

### Describe componentDidMount() and when it is precisely called

React has built-in lifecycle methods that are automatically invoked at the appropriate 'lifecycle hooks.' When a component is passed to ReactDOM.render(), first that component's constructor is called, and then that component's render() method is invoked. Immediately after, the actual DOM is updated to match the render output. Right _after_ the render() output is inserted into the DOM, React automatically calls componentDidMount(). The "mount" is the actual DOM updating. 

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
