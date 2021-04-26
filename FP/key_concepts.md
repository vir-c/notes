# Key Concepts

TOC
- [Key Concepts](#key-concepts)
  - [Purity](#purity)
  - [Immutability](#immutability)
  - [Higher Order Functions (HOF)](#higher-order-functions-hof)
  - [Closure](#closure)
  - [Functional Composition](#functional-composition)
  - [Partial Application/ Partial Functions](#partial-application-partial-functions)
  - [Currying](#currying)
  - [Referential Transparency](#referential-transparency)
  - [Refs](#refs)

<br/><br/>

## Purity

Pure Functions are very simple functions. They only operate on their input parameters. 
* Pure Functions will always produce the same output given the same inputs
* Pure Functions have no side-effects

Most useful pure functions take atleast one parameter and return something.  
Without a parameter, a pure function always return a constant.


Functional Languages cannot eliminate Side Effects, they can only confine them. Since programs have to interface to the real world, some parts of every program must be impure. *The goal is to minimize the amount of impure code and segregate it from the rest of our program.*
<br/><br/>

## Immutability    
<br/>

> Did you ever wonder why most solutions to program glitches are fixed by rebooting your computer or restarting the offending application? That’s because of state. The program has corrupted its state.

Proper management of state is the most important thing you can do in your program to ensure reliability.    

```
var x = 1;
x = x + 1;
```
in FP, x = x + 1 is illegal

There are no variables in FP, only constants
FP languages don't have loop constructs like for, while

> **FP uses recursion to do looping**

Immutability creates simpler and safer code.
<br/><br/>

## Higher Order Functions (HOF)

In FP, a function is a first class citizen of the language, i.e. it's just another value.   
**HOFs are functions that either take functions as parameters, return functions or both**

``` javascript
// higher order function
function executor(fnc, value){
  return fnc(value)
}
```

<br/><br/>

## Closure

For HOF to be effective, the inner function should have access to outer containing function's scope. A closure is a function’s scope that’s kept alive by a reference to that function.   

![Closure](https://miro.medium.com/max/576/1*0phT7qIAPVxG7KXcL-6B5g.png)
``` javascript
function grandParent(g1, g2) {
    var g3 = 3;
    return function parent(p1, p2) {
        var p3 = 33;
        return function child(c1, c2) {
            var c3 = 333;
            return g1 + g2 + g3 + p1 + p2 + p3 + c1 + c2 + c3;
        };
    };
}
```
<br/><br/>

## Functional Composition
<br/>
In FP, functions are the builds blocks. Write them to do very specific tasks and then put them together to construct complex functionality.     

In math, f ∘ g is functional composition and is read “f composed with g” or, more commonly, “f after g”. So (f ∘ g)(x) is equivalent to f(g(x)).        
*In order for functions to be composable, the output type must align with the expected input type*
With one input and output, it's become easy to create a pipeline of operators and write functions without having to specify the parameters i.e. *Point-Free Notation*
Point-Free Notation offer brevity, clarity and flexibility.


```elm
//ELM has infixed operator for composition
add10 value =
    value + 10
mult5 value =
    value * 5
mult5AfterAdd10 value =
    (mult5 << add10) value
//point free notation
mult5AfterAdd10 value =
    (mult5 << add10) value
```

```javascript
//javascript doesn't support composition natively
const add10 = value => value + 10;
const mult5 = value => value * 5;

const mult5AfterAdd10 = value => mult5(add10(value))

const compose = (...fns) => x => fns.reduceRight((y, f) => f(y), x);

//point free notation style
const mult5AfterAdd10PFN= compose(
    mult5,
    add10
)

```
<br/><br/>

## Partial Application/ Partial Functions
<br/>
A function which has already been applied to some — but not yet all — of its arguments. The arguments which the function has already been applied to are called fixed parameters.

```javascript
const sum = (a,b) => a + b
const sum5 = x => sum(5, x) //sum5 is partial application function
```
<br/><br/>

## Currying
<br/>
A Curried Function is a function that only takes a single parameter at a time.      
Currying turns a function that takes multiple arguments into a set of partial functions that take one argument at a time.
Currying helps in composition

```javascript
const arr = [1,2,3,4,5,6]

const isOdd = (x) => x%2 == 1
const square = (x) => x*x
const reduce = Array.reduce
const summ = (acc,x)=>acc+x

//since only one argument is expected
const sumOddSquaredArr = arr.filter(isOdd).map(square).reduce(summ, 0)

```

## Referential Transparency

A referential transparent function can be safely replaced by its expression. All pure functions are referential transparent.

```javascript

var y = 1
const myFunc1 = function(x){ return x+y }  //not referential transparent

const myFunc2 = function(x, y){ return x+y } //referential transparent

const myFunc3 = function(x, y, z){ return myFunc2(x, myFunc2(y, z)) }

//replace myFunc2 in myFunc3
const myFunc4 = function(x, y, z){
  return (function(x,y){
    return x+y
  })(x, (function(x, y){ return x+y })(y, z))
}

// myFunc3 is same as myFunc4
console.log(myFunc3(1,2,3) === myFunc4(1,2,3))

```


## Refs
* [So You Want to be a Functional Programmer Series - Charles Scalfani
 ](https://medium.com/@cscalfani/so-you-want-to-be-a-functional-programmer-part-1-1f15e387e536)
* [Composing Software - Eric Elliot](https://medium.com/javascript-scene/curry-and-function-composition-2c208d774983)
* [Hey Underscore, You're Doing It Wrong!](https://www.youtube.com/watch?v=m3svKOdZijA&app=desktop)
