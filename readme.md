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
