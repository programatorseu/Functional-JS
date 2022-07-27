# Functional-light JS
## 1. Intro
having keyword function in programm does not function programming
### 1.1 Why Functional Programming ?
impossible to write functional programming in isolation 
- difference in way you appraoch code 

**imperative vs declarative**
imperative - code focus on how to do sth 
list of numbers - we want sum -> we will use for loop
future reader of that code must mentally execute code to understand 
human brain is not built for executing code !:) 

declarative - what and why ? - why we incremment by 

### 1.2 Functional programming Journey
we got early wins - get a little bit complex. 
then you start thinking - it was more readable before 
**we need to ship code** !!! 

functional programming promies that we can use principles of programming 
## 2. Function Purity
### 2.1 Functions vs Procedures 
Those are procudures: 
```js
function addNumbers(x = 0, y = 0, z = 0) {
  var total = x + y + z;
  console.log(total);
}
function extraNumbers(x = 2, ...args) {
  return addNumbers(x, ...args);
}
extraNumbers(3,4,5);

```



function must return something   / not only take input 

if function doest not `return` keyword then return `undefined`

function can call other function

when we call `addNumber` we pollute `extraNumbers`



function :

- take input 
- return output 



> **Spread syntax** (`...`) allows an iterable,  such as an array or string, to be expanded in places where zero or more  arguments (for function calls) or elements 

```js
function twoValues(x,y) {
  return [x + 2, y - 2];
}
var [a,b] = twoValues(...[5,10]);
// Destructing part : 
a; // 7
b; // 8
```

### 2.2 Function naming sematincs

```mathematica
f(x) 2*x^2 + 3
```

**function is relationship between input and output** 

what we put and what we get out 

```js
function parabola(x) {
  return 2 * Math.pow(x,2) + 3; 
}
```

like lego - every bricks has to same name and produce some output 

**consistency**

- when we have function that take object as input 
- we want to get property  of object that does not exists
- ouput will be `undefined` - valid output 



### 2.3 Side effects 

we want to avoid side effects 

here we are using some staff around and affect sth else in program 

indirect input & output even though there is relationship 

```js
function shippingRate() {
  rate = ((size + 1) * weight) + speed; 
}
var rate;
var size = 12;
var weight = 4;
var speed = 5;
shippingRate();
rate; 
size = 8; 
speed = 6; 
shippingRate();
rate; //42
```

**outputs and inpust must be direct**

```js
function shippingRate(size, weight, speed) {
  return ((size+ 1) * weight) + speed;
}
var rate; 
rate = shippingRate(8,4,6); //42
```

in Javascript important part is :

- function call - that matters 
  - is there direct input and output from `function` call  



**side effecs**

- I/O
- Database Storage
- DOM
- Network calls
- Random Numbers 
- CPU (time delay ) - one program can run because program run  - **impossilbe to avoid**

**we need to minimize side effects **



### 2.4 Pure function call  and Cosntants 

- take all input  and output direct
- no side effect 



const is not changing value 

z is not reassinged 

z is serving purpose of constant in program 

but `addTwo` is not constant - it can be changed later 

```js
const z = 1;
function addTwo(x,y) {
  return x + y;
}
function addAnother(x,y) {
  return addTwo(x,y) + z;
}
addAnother(20,21); //  ?
```





### 2.5 Reducing Surface Area

limit possibility of reassigning `z`

inner function -> remember `z` 

```js
function addAnother(z) {
  return function addTwo(x,y) {
    return x + y + z;
  };
}
addAnother(1)(20,31); // 52
```

### 2.6 Same input / same output 

we need to see all revelants parts of program 

object can be reassinged 

```js
function getId(obj) {
  return obj.id;
}
```

pure function call works in isolation 

> every time with the same input when we execute function we will get the same answer 

### 2.7 Level of confidence 

there is no yes or no answer 

only level of confidence 

we want to provide function with `high` level of confidence 



### 2.8 Extracting Impurity

 function do all computation and proceudes that does single effect 

- For example send data to DB 



### 2.9 Containing Impurity

impurity may happen

structure things that will reduce area of impurity 

modify to wrap impurity  with function 

or create Adapter function 



```js
var students = [
  {id:202, name: "Ania"},
  {id:620, name: "Piotrek"},
  {id:21, name: "Basia"},
  {id:74, name: "Rysiu"}
];
function sortStudentsByName() {
  students.sort(function byName(s1,s2) {
    if(s1.name < s2.name) return -1;
    else if (s1.name > s2.name) return 1;
    else return 0;
  }); 
  return students;
}
```



simple test : 

```js
var studentsTest1 = getStudentsByName(students);
console.log(studentsTest1[0].name === "Ania");
console.log(studentsTest1[1].name === "Basia");
console.log(studentsTest1[2].name === "Piotrek");
console.log(studentsTest1[3].name === "Rysiu");
```



**wrapper**

```js

function getStudentsByName(students) {
  students = students.slice(); // make copy of array
  return sortStudentsByName();
  function sortStudentsByName() {
  students.sort(function byName(s1,s2) {
    if(s1.name < s2.name) return -1;
    else if (s1.name > s2.name) return 1;
    else return 0;
  }); 
  return students;
}
}

var studentsTest1 = getStudentsByName(students);
```



**adapter** - brute force technique

1. need copy of array 
2. current status of students array 
3. modify and capture new students
4. reasign students with orginal list
5. retur new students array  

```js
function getStudentsById(curStudents) {
  var originalStudents = students.slice();
  students = curStudents.slice();
  var newStudents = sortStudentsByID();
  students = originalStudents;
  return newStudents;
}
```

## 3. Argument Adapters

### 3.1 Function arguments

- parameter - thing in fnction definition 
- argument - value that ges passed whe we call function 

arguemnts get assigned to parameters

unary - we take 1 input and return 1 output 

binary - we take 2 input  and return 1 output 

```js
// unary: 
function increment(x)  {
  return sum(x,1);
}
//binary:
function sum(x,y) {
  return x + y;
}
```

### 3.2 Arguemnt Shape Adapter

- higher order function **HOF**

> receives as its inputs  1 or more function or return 1 or more functions 

normal that does not receive or return is single-order function 

```js
function unary(fn) {
  return function one(arg) {
    return fn(arg);
  };
}
function binary(fn) {
  return function two(arg1, arg2) {
    return fn(arg1, arg2);
  };
}

function f(...args) {
  return args;
}
var g = unary(f);
var h = binary(f);
g(1,2,3,4); // [1]
h(1,2,3,4); //[1,2]
```

all functions in JS are variadic - does not matter how many params are declared 



### 3.3 Flip & Reverse Adapter



we have function that receives 2 args 

-> we need function that provide argument in different order 

```js
function flip(fn) {
  return function flipped(arg1, arg2, ...args) {
    return fn(arg2, arg1, ...args);
  };
}
function f(...args) {
  return args;
}

var g = flip(f);
g(1,2,3,4); // [2,1,3,4]
```

another high-order utility:

```js
function reverseArgs(fn) {
  return function reversed(...args){
    return fn(...args.reverse());
  };
}

function fn(...args) {
  return args;
}
var g = reverseArgs(f);
g(1,2,3,4);
```

### 3.4 Spread Adapter 

function - take individual args 

we want to call that function with an array 

it is spreading array of arguments into indvidual : 

`..spread` operator :

```js
function sum(x, y, z) {
  return x + y + z;
}

const numbers = [1, 2, 3];

console.log(sum(...numbers)); // 6
```



```js
function spreadArgs(fn) {
  return function spread(args) {
    return fn(...args);
  };
}
function f(x,y,w,z) {
   return x + y + w + z;
}
var g = spreadArgs(f);
g([1,2,3,4]); // 10 
```



## 4. Point free 

### 4.1 Equational reasoning

**point-free** : way of making a function by making it other function 

defining function without needing to explicitly define and map its inputs 



if we have **thing** that got this **one shape** 

and we have other **thing** that has **the same shape** 

​	->  even if they do different things 

> **THEY ARE INTERCHANGABLE**

```js
getPerson(function onPerson(person) {
  	return renderPerson(person);
});
getPerson(renderPerson); 
```



isEvent create in relation to `isOdd` function 

```js
function isOdd(v) {
  return v % 2 == 1;
}
function isEven(v) {
  return !isOdd(v);
}
isEven(2) // true 
```

