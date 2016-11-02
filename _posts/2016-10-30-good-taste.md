---
title: The "Good Taste" Coding Requirement
layout: post
---

<p>Recently, I read an article about Linus Torvalds "Good Taste" Coding Requirement:
<a href="https://medium.com/@bartobri/applying-the-linus-tarvolds-good-taste-coding-requirement-99749f37684a">
https://medium.com/@bartobri/applying-the-linus-tarvolds-good-taste-coding-requirement-99749f37684a#.5h2guheeg
</a>
</p>

<p>
  This article struck a chord with me because I have found myself in situations where I've seen code or
  written code that has been in "bad taste." One question that comes to my mind after reading this is how
  does someone develop good taste? In my cases, I haven't been able to pinpoint exactly why something was off.
  In the article, it mentions that <q>The fewer conditions you test for, the better your code <em>tastes</em>.</q>
  Are there other criteria like this that help you figure this out?
</p>

<p>
  With experience, I'm hoping that I'll be able to put what I think is "good taste" into concrete terms.
  One way of helping developing this is always thinking how you can make your code better. If you try out
  different variations of code to accomplish the same thing, there will be some variations that do things
  better or worse. By trying to evaluate these different pieces of code for things like readability and
  future maintainability, the ability to write better code in the future should improve.
</p>

<p>
  An example from my own code involves uses Promises. A Promise is "an eventual result of an asynchronous operation".
  In my code, I had two promises I wanted to resolve. Only 1 or both of the promises need to be executed, depending
  on some condition for each promise. After all of the desired promises had resolved, a piece of code had to be run.
  Originally, I solved it doing something like this:
  <pre>
    new Promise(function(resolve, reject) {
      if (cond1) {
        return promise1;
      } else {
        resolve(false);
      }
    }).then((val) => {
      if (val) {
        set some property with val;
      }

      if (cond2) {
        return promise2;
      } else {
        return false;
      }
    }).then((val) => {
      if (val) {
        set some property with val;
      }

      perform ending code;
    });
  </pre>

  The returing false and creating a new promise felt wrong, and the code didn't look very good. Looking into
  Promises more, I found the Promise.all() method, which will wait for all the promises in a list of promises
  to resolve before resolving. Now, the code looks more like this:

  <pre>
    create empty promise array;

    if (cond1) {
      promise1.then((val) => { set property based on val});
      add to promise array
    }

    if (cond2) {
      promise2.then((val) => { set property based on val });
      add to promise array
    }

    Promise.all(promise array).then(() => {
      perform ending code;
    });
  </pre>

  To me, that code "tastes" much better.
</p>
