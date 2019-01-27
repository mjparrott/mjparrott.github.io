---
title: Understanding Protocols and Behaviours in Elixir
layout: post
---

<p>I just watched a really interesting video about Elixir protocols. Take a look -
<a href="https://www.youtube.com/watch?v=sJvfCE6PFxY">https://www.youtube.com/watch?v=sJvfCE6PFxY</a>.
It's from ElixirConf EU 2017. I've spent a bit of time recently trying to understand
Elixir protocols and behaviours, when they're useful, and what the difference is between them,
and this talk by Kevin Rockwood had a few points that really helped me out.</p>

<p>To start off, what are behaviours and what are protocols?</p>

<h2>Behaviours</h2>

<p>A behaviour is basically just a set of functions, acting as an interface, as you
might have in an object oriented language like Java. When another module implements
a certain behaviour, it signs a contract saying "I will implement all of the functions
specified by this behaviour." This is done by putting <code>@behaviour MyBehaviour</code>
at the top of the module that is implementing <code>MyBehaviour</code>.</p>

<p>It's important to note that if you forget to implement one of the functions of
<code>MyBehaviour</code> in your module, Elixir won't error, but instead only give
you a warning. You need to watch out for this.</p>

<h2>Protocols</h2>

<p>A protocol is a function, or set of functions, that can be called on different
data types. As the docs put it, protocols are a way of achieving polymorphism in
Elixir. For a given function or set of functions, you can implement a protocol for
a new data type, and then call those functions by passing in the data type you
implemented the protocol for.</p>

<h2>When do you use one or the other?</h2>

<p>This is really what drove me to write this. This is answered very well in the talk
I linked at the beginning. From that talk, the question you need to ask yourself is
"Can each implementation of my function take the same data type?"</p>

<p>If the answer is "Yes", then you should probably use a behaviour.</p>

<p>If the answer is "No", then you should probably use a protocol.</p>

<p>This really helped me think about what the difference between protocols and behaviours
is. Behaviours help you create many functions with the same names that operate on the same
data type. After all, a behaviour is an interface, and it would be confusing if in one
implementation a function takes data type A and in another implementation the same function
takes data type B. Protocols, on the other hand, let you create many functions with the
same names that operate on different data types. In a behaviour, these functions will be
spread across many modules, while with a protocol, they are all contained to the same module.
A behaviour lets you say "if this module implements this behaviour, I can pass in this data to
these functions, and things will work." A protocol let's you say "if this protocol is
implemented for this data type, I can pass it into this function, and things will work."
</p>

<p>Another article I found while reading into protocols and behaviours also makes
some great points. <a href="https://www.djm.org.uk/posts/elixir-behaviours-vs-protocols-what-is-the-difference/">
https://www.djm.org.uk/posts/elixir-behaviours-vs-protocols-what-is-the-difference/</a>
It talks about a bit about how processes, modules, and data types are all connected,
and how we achieve polymorphism in those things in Elixir, using behaviours and
protocols.</p>

<p>That's all I have to say here. I'll link all my references down below, which hopefully
combined with what I've said will give you a good understanding of behaviours and
protocols in Elixir.</p>

<ul>
  <li><a href="https://elixir-lang.org/getting-started/typespecs-and-behaviours.html#behaviours">
    https://elixir-lang.org/getting-started/typespecs-and-behaviours.html
  </a></li>
  <li><a href="https://elixir-lang.org/getting-started/protocols.html">
    https://elixir-lang.org/getting-started/protocols.html
  </a></li>
  <li><a href="https://www.youtube.com/watch?v=sJvfCE6PFxY">
    https://www.youtube.com/watch?v=sJvfCE6PFxY
  </a></li>
  <li><a href="https://www.djm.org.uk/posts/elixir-behaviours-vs-protocols-what-is-the-difference/">
    https://www.djm.org.uk/posts/elixir-behaviours-vs-protocols-what-is-the-difference/
  </a></li>
</ul>

