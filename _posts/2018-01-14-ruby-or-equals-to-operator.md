---
title: The ||= Operator in Ruby
layout: post
---

<p>The ||= operator in Ruby is something that gets talked about all the time.
  Here is a just a
  <a href="http://www.rubyinside.com/what-rubys-double-pipe-or-equals-really-does-5488.html">small</a>
  <a href="http://davidablack.net/dablog.html#2008/3/25/a-short-circuit-edge-case">sample</a>
  of
  <a href="https://allenan.com/ruby-or-equals-operator-default-booleans/">links</a> 
  that talk about how exactly the ||= operator really works. There is even a link on the
  <a href="https://www.ruby-forum.com/topic/151660/">Ruby mailing list</a>
  which just collects links that discuss this operator. Needless to say, ||= has caused some
  confusion.
</p>

<p>What most people think that ||= would do is this:
  <code>a = a || b</code>
  This makes sense given how operators such as += and -= works. However, it is actually closer to
  <code>a || a = b</code>
  In words, if a has a falsey value (i.e. nil or false) then set a to b. Otherwise, do nothing.
  Note that with a || a = b, the assignment only occurs if a has a falsey value. With
  a = a || b, the assignment occurs regardless of a's value.
</p>

<p>
  This is an easy way to think about how the operator works, but in some cases, a || a = b and a ||= b
  behave differently. For example, if a is undefined, then
  <code>a || a = 42</code>
  will result in an error but
  <code>a ||= 42</code>
  will assign a to 42.
</p>

<p>
  While reading these posts, I also learned a bit about when and when you might get a NameError. If,
  in some nested scope, you assign to a variable, you can later refer to that variable without getting
  an error, even if that line of code doesn't get called. For example:
  <code>
    def f
      x
    end
    def g
      if false
        x = 1
      end
      x
    end
  </code>
  Calling f here will give you a NameError, while calling g will not.
</p>

<p>
  If you're interested in learning more, read some of the links! They have good information, as
  well as links to other sources with more information.
</p>
