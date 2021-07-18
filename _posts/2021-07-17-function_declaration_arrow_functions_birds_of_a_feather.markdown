---
layout: post
title:      "Function Declaration, Arrow Functions, Birds of a feather?"
date:       2021-07-18 01:36:27 +0000
permalink:  function_declaration_arrow_functions_birds_of_a_feather
---


![](https://upload.wikimedia.org/wikipedia/en/0/0a/Flappy_Bird_icon.png)
# === ?
![](https://store-images.s-microsoft.com/image/apps.64975.13564424126320075.f39b613e-67f4-4c85-8d4f-ad9a47ecfa42.8390d401-ed7c-4be6-879c-4b27f89a7d44?mode=scale&q=90&h=270&w=270&background=%230078D7)

Ah, the humble arrow function. Unlike its predecessor, the regular function declaration, the arrow function is a lighter, more concise way of accomplishing some of the same uses. They are both functions after all. Having evolved to it's more arrow-ey form in ES6, there are some differences that are best observed in a natural setting.

## 
While these two declarations work similarly, we can see first that the presentation of the syntax is quite different. Peer through your binoculars and see these two in action;
```
const birdNamer = function(name) {
    return `${name} want a code snippet?`
}

birdNamer("Regular bird")
"Regular bird want a code snippet?"
```

Now observe the awesome power of evolution...

```
const birdNamer = (name) => {
     return `${name} want a code snippet?`
}

birdNamer("Awesome Arrow-ey bird")
"Awesome Arrow-ey bird want a code snippet?"
```

There are some differences in terms of how **this** is handled by regular function declarations as opposed to arrow functions. While the usage, contexts and applications of **this** are exhaustive, we'll just focus on the contrast between these two functions from a less birds-eye view.

MDN states:
> In most cases, the value of this is determined by how a function is called (runtime binding). It can't be set by assignment during execution, and it may be different each time the function is called

and...

> ES2015 introduced arrow functions which don't provide their own this binding (it retains the this value of the enclosing lexical context).

There's this great way of explaining lexical scope in the "natural" bird world:

```
const mommaBirdFunction = () => {
     let eggsValue = 2;
     console.log(eggsValue);

     const eggLayerFunction = () => {
          console.log(eggsValue += 1);
     }

     eggLayerFunction();
}

mommaBirdFunction();

2
3
```
*Ah, the wonder of life. This mother arrow function has nested within her, an egg layer function. When the time is right, the mommaBirdFunction is called, thus returning the value of the two eggs, and the newly laid egg*

To take the analogy way further, let's peer into bird social dynamics. Let's say a young blue jay is happily eating grubs along side it's mother, when a robin comes along to eat as well. The young blue jay introduces its mother "tweet tweet" (translation: *this* is my mother) *this* represents the young blue jays mother in the current sentence. Javascript treats *this* the same way. Let's try it in code:

```
const mommaBird = {
    momma_jay_name: "Blue Bell",
    momma_jay: function () {
        return `${this.momma_jay_name} is my mother`;
    },
};
console.log(mommaBird.momma_jay());

Blue Bell is my mother
```
*In the above example we used **this** to refer to mommaBird, the parent object. So we are referring to the context within which *this* was called, inside the anonymous function. Let's see this same social interaction take place near the nest of the arrow function:

```
const mommaBird = {
    momma_jay_name: "Blue Bell",
    momma_jay: () => {
        return `${this.momma_jay_name} is my mother`;
    },
};
console.log(mommaBird.momma_jay());

undefined is my mother
```
The result here is *undefined*. Arrow functions behave differently in that they don't have their own *this* context. They inherit from the parent scope whenever *this* is called. In a regular function, *this* refers to the context of the function being called, in an arrow function, it refers to the scope *where* the enclosed function is located...Hence, undefined. 

### Arrow functions, and a birds eye view on Hoisting, 
In order to keep a tidy nest, ES6's arrow functions are not **hoisted**. You can see in this example, taken from earlier, that the inner function called from outside of the parent function returns undefined:

```
const mommaBirdFunction = () => {
     let eggsValue = 2;
     console.log(eggsValue);

     const eggLayerFunction = () => {
          console.log(eggsValue += 1);
     }

  // eggLayerFunction() was here
}

mommaBirdFunction();
eggLayerFunction();

2
Uncaught ReferenceError: eggLayerFunction is not defined
```
Javascript does hoist variables declared using *let*, but it does not initialize them, an important distinction between the majestic function declaration, and the mighty arrow function.
