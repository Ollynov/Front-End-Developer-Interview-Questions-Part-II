# Front-End-Developer-Interview-Questions-Part-II
An extension to the ever famous front-end-developer-interview-questions github repo. 

# Modules
### Describe the require function. 
### Describe in detail the readFile function

Javascript environments (browser, Node) each have a built in readFile function, which first takes the path of a file, and returns the contents as a large string. The next step is to actually take this data (in string format), and evaluate it as code. The most simple way is with the built-in eval operator: 

function returnAfterEval(data) {
  eval(data);
  return x;
}

console.log(returnAfterEval("var x = 'hello world'"));
// hello world

Another method of evaluating a piece of data (string) as code is to pass in the data directly into the Function constructor. 
var evaluated = new Function("x, y", "return x + y");
console.log(evaluated(2, 3))
// 5

The constructor takes two arguments, the first being a string with comma separated argument names, and the second argument being a string with the body of the function. 
