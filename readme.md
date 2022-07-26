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





