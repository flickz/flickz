---
layout: post
date: 2017-10-01
categories: coding
author_name : Oluwaseun Omoyajowo
author_url : /
author_avatar: seun
show_avatar : true
read_time : 3
feature_image: code
show_related_posts: true
square_related: recommend-woods
---

So you’ve heard or read about Closure in JavaScript but still can’t comprehend what exactly it is, how it’s works, when to use it. Or this is your first time reading about Closure. Well this post is for you.

Closure is one of the most asked interview questions. To understand Closure, there is a need to understand the meaning of “Scope and Lexical Scope”.

What is Scope?

>Scope is a set of rules for looking up variables by their identifier name.

There are two types of scope and they includes “Dynamic and Lexical Scope”. JavaScript uses Lexical scope. Lexical Scope looks up variables and blocks of scope where they are authored at write time. Take for example:

```js
function foo(a){
  console.log(a + b)
}
var b = 1
foo(2) // 3
```
The JavaScript engines, when compiling, looks up for the variables within ``foo()`` (Local scope) and if not found, it checks the outer scope (Global scope) where b is defined as **1**. This way of looking up the enclosing scopes is called “Lexical Scoping”.

## Back to Closure
A great misconception Developers make while trying to understand Closure is thinking it’s a new special opt-in tool that requires learning new syntax and pattern for. No, Closure is not a new technique in JavaScript. Closure is all around you in JavaScript, you just have to recognize and embrace it.

>“Closure is not a new technique in JavaScript. Closure is all around you in JavaScript, you just have to recognize and embrace it — Kylie Simpson (You Don’t know JS)”

Closure happens as a result of writing codes that depends deeply on Lexical Scope. You’ve probably been writing Closure but not realising.

## What is Closure?
Closure is when a function is able to remember and access its lexical scope even when that function is executing outside its lexical scope.

Consider example:

```js
function wrapValue(n){
   let localVariable = n;
   return () => n;
}
let wrap1 = wrapValue(1)
let wrap2 = wrapValue(2)
console.log(wrap1(), wrap2()) //1 2;
```
From this example the ``wrapValue()`` takes a parameter that is equal to ``localVarriable``. The ``wrapValue()`` returns a function which from lexical scope has access to the ``localVarriable`` which it returns. The variables ``wrap1`` and ``wrap2`` equals to the function returned by ``wrapValue()``, the inner function returns the ``localVarriable`` which in these cases are **1** and **2**.

Normally after calling the ``wrapValue``, the inner scope would go away because of the JavaScript engine garbage collections that free up the memory in use. But the magic of Closure prevent this from happening and instead keeps the inner scope because ``wrap1`` and ``wrap2`` still has reference to ``localVarriable``. And that reference is called Closure. Closure lets the function continue to access the lexical scope it was defined in at author-time.

Here is a real world example of closure.

```js
function wait(message) {
    setTimeout( function timer(){
      console.log( message );
    }, 1000 );
}
wait( “This is Closure” );
```

The ``setTimeout()`` takes in function timer which has a scope closure over the scope of ``wait()`` thereby having the ability to reference ``message`` variable passed into b. Now deep down in the implementation of ``setTimeout()``, there is a reference to a parameter that when invoked by the Engine, invokes the ``timer()`` and ``message`` reference is still intact.

## Conclusion

>“Whenever and wherever you treat functions (which access their own respective lexical scopes) as first-class values and pass them around, you are likely to see those functions exercising closure. Be that timers, event handlers, Ajax requests, cross-window messaging, web workers, or any of the other asynchronous (or synchronous!) tasks, when you pass in a callback function, get ready to sling some closure around! — Kylie Simpson (You Don’t know JS)”

**Want to know more?**
* [You Don’t Know JS: Scope & Closures](http://shop.oreilly.com/product/0636920026327.do)
* [Closure — MDN](https://developer.mozilla.org/en/docs/Web/JavaScript/Closures)
* [Master the JavaScript Interview: What is a Closure?](https://medium.com/javascript-scene/master-the-javascript-interview-what-is-a-closure-b2f0d2152b36)
