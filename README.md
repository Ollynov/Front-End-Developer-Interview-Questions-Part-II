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
# ES6

# React
### Give an overview of component based design

### How would you design a nav bar with React? 

### Describe React Lifecycles and how they mix into the app workflow? 


### Why should the render() function of a component be 'pure', and what does that mean?

For starters, the render() function doesn't necessarily need to be 'pure', but it _should be_ so it does not produce any tricky errors, and so that your entire app can have a structure that is easier to reason about. A pure function must return the same result each time that it is invoked. For render(), this means that it should not modify component state. The lifecycle functions, such as componentWillMount() and componentDidMount() should be used for state change. 

### When would it be unnecessary to include a constructor() in your component?

If your react component has no props being passed down to it, has no state, and has no function bindings, then you do not need a contructor function. 

### What is super(props)? 

Super() allows you to access the constructor of the parent class. Inside of a components constructor method, you need to include super(props) if you are having props passed down, before any other statements. If you don't include it, then 'this.props' will be undefined. The following code will work just as well:
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

React has built-in lifecycle methods that are automatically invoked at the appropriate 'lifecycle hooks.' When a component is passed to ReactDOM.render(), first that component's constructor is called, and then that component's render() method is invoked. Immediately after, the actual DOM is updated with this render output. Right _after_ the render() output is inserted into the DOM, React automatically calls componentDidMount(). The "mount" is the actual DOM updating. 

### Why does React have 'unidirectional' data flow? 

State is local, and specific to a particular component, it is 'encapsulated.' This state is only accessible to the ONE component that initializes it and stores it. This state can only affect the components that are structured below it in the hierarchy. State can only be passed to child components through props, from top-down, hence- 'unidirectional.'

### Difference between Angular and React? 
Angular is a much more extensive framework, it is full MVC. While React is only views focused
Data binding is different, Angular has two way data binding, in the sense that when a user provides input, not only the view will be updated, but the Model as well. React on the other hand updates the view, but it is not a standalone app, you need to combine it with something else. 

React is quicker. Angular’s two way data binding and dirty checking is quite costly. (see below). React on the other hand has a virtual DOM, which is just a lightweight js object. When there is a change, first the virtual DOM is changed, and then there is comparison of the virtual to the real DOM, and only the necessary components are altered, there is no need for a full O(n^3) tree traversal. 
Angular has directives, which are a blend of JS, CSS, and HTML, while react uses JSX which is javascript XML, you can essentially mimic html inside of your javascript code. Not necessary, but way easier. 


### What is dirty checking with angular, and what is the React equivalent?
Another word for the digest loop of Angular, in which a loop watches for any changes in any of the variables watched by the $scope.  If $scope.myVar is marked to be watched, then it will fall into Angular’s dirty digest loop. It scans the scope for changes. 

Whenever you call setState on a component, the state is changed and the component is marked as ‘dirty.’ Then the React event loop happens, and looks at all dirty components and re-renders them. The important factor to note here is that the DOM is modified with the updated components all at once. This batching is incredibly important for performance, and would be tough to do with vanilla javascript.

### What is event delegation in React? 
Attaching event listeners to the DOM is slow and memory consuming (like many alterations with the DOM). Instead, React implements it’s own event delegation. The event listeners are stored in a hash map, rather than on the virtual DOM. 

A single event listener is attached to the root of the document. When an event is fired, the browser gives us the target DOM node. Now, React actually doesn’t even need to iterate through the virtual DOM in order to propagate the event through the DOM hierarchy (misconception). Since every React component has a unique ID, we can use string manipulation to get the ID of all the parents for the event propagation. 

### How do you include a click handler in React? 
Similar to how you would in HTML, but the events are named in camel case (rather than lowercase), and you pass a function as the actual event handler (rather than a string). 

### Explain the 'diffing' algorithm
The point of the “diffing” algorithm is to make component updates predictable, but still super fast. 
It’s one of the factors that makes React so fast. Altering the DOM is relatively expensive, especially if you are making alterations that don’t need to happen. When you batch together write and read operations, then event delegation is faster. The beautiful thing is that React does this all automatically. 

When a virtual DOM is created (lightweight javascript object), it is going to compare that to the actual DOM to make the minimal amount of changes necessary. It’s a O(n^3) (n represents the number of elements in the tree) problem in general to find the minimal modifications between two trees. However, this is still to slow, it’s like a billion comparisons for a thousand elements. React tries to only find differences between trees, level by level. Super rare to have a component moved to a different level in a tree, only horizontally. 


### What happens when you call setState in React? 
The state is updated, and your component is marked as dirty, and then the render() method is called on every child element, and the virtual DOM is rebuilt for all of them. In other words, if you call setState on the root node, then the entire app is re-rendered. Every component will render() even if it’s state has not changed. This is not so bad because we’re still not touching the DOM. Furthermore, you have the option to customize and prevent a particular component from updating with the shouldComponentUpdate. 

Then all at once it will take the dirty components and update the DOM. 


### In react how would you communicate from child to child without redux or the parent
^ you can share a file that is sharing elements. But the real answer is that all other children simply need to be notified. 

### How can you prevent a large tree from re-rendering unnecessarily? 
Use shouldComponentUpdate().


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
