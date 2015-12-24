---
layout: blog
categories: blog coq
title: Curry-Howard and you
---

I'm very excited. I am one with the Curry-Howard Correspondence.  Now I've known what it is for quite awhile, but it's finally completely clicked after using it for verification and seeing it in practice.  I've read about it in various excellent books - Pierce's [Types and Programming Languages]() and Chlipala's [Certified Programming Using Dependent Types]() being two such sources. Until I used it for everyday verification, I can't say that I understood the depths of it.

*Types are to programs as theorems are to proofs*. Simple, right? Not so. I fought with the meaning of this from the first time I read it. Types are properties of language constructs. They define promises made about calculated things and place demands on things calculated with.  Looking at the term `x+1` in the context of a type system we know that if `x` is a natural number, `+` will produce a natural number. If `x` is not, the result is not defined and we probably shouldn't allow the calculation.

Functions have types that are constructed from other types with the type constructor `D->R`. This has always made great sense to me.  Take any function, `f:D->R`, put in `d:D` and you get back something of type `R`.  Great, I get it - a constraint is placed on `d` with an accompanying promise about `r`.  But what the heck does this have to do with proofs?

Let's look at the type of an increment function over naturals, `inc:Nat->Nat`.  If you give `inc` a `Nat` you will get a `Nat`.  We can define this function in any programming language in roughly the same way:

{% highlight haskell %}
inc n := n+1.
{% endhighlight %}

sans some syntax and assuming type inference.  So,far so good.

This increment function, `inc`, is an example of a function of type `int->int`.  We call this a *witness* to type type `int->int` and say the type `int->int` is *inhabited*.  Most programming languages restrict their type systems so that every base type and every constructed type are guaranteed to be inhabited.  We'll soon see why.

Let's not look at the type of a decrement function over naturals, `dec:Nat->Nat`.  Same constraint and same promise - provide a `Nat` and get a `Nat`.  We can define `dec` just like `inc`:

{% highlight haskell %}
dec n = n-1
{% endhighlight %}

and of course we immediately have problem.  `dec 0` does not produce a natural number.  Different implementations provide different solutions to this problem - add an error value, designate magic natural that represents an error, throw an exception, or put a guard around `dec`.

How might we solve this problem with types?  One is to create a whole number type that is all natural numbers excluding 0.  Pretty simple thing to do if we treat types and sets and use set comprehension:

{% highlight haskell %}
whole = {n:Nat | n>0}
{% endhighlight %}

Problem solved.  Let's now define `dec` as follows:

{% highlight haskell %}
dec : {n:Nat | n>0} -> Nat
dec n = n=1
{% endhighlight %}

Now the constraint is the input must be greater than 0 and the promise is we'll get back a `Nat`.  This new type is called a subset type in Coq or a predicate subtype in PVS and is an example of a `dependent type` that mixes evaluation with type checking.  We'll not go into that here.

Unfortunately, the problem is not solved.  In fact, we've created a much harder one.

Remember that type systems work hard to make sure types are inhabited.  Here's why.  Let's say we mistakenly declare a silly type using our new comprehension mechanism:

{% highlight haskell %}
{n:Nat | n>5 /\ n<3}
{% endhighlight %}

and declare some variable to be of that type:

{% highlight haskell %}
x : {n:Nat | n>5 /\ n<3}
{% endhighlight %}

It should be easy to see that our new type has no witnesses.  There is no `n` that is both greater than 5 and less than 3. The type of `x` is uninhabited.  That turns out to be a problem because we've said that `x` *must* take values that are witnesses to that type.  Thinking of types as sets, we've now said that `x` is an element of the empty set.  That is an inconsistency that ruins our type system.  If we were working in PVS or Coq, those systems would require us to prove a witness exists for every type.  However, that is not generally a decidable problem and cannot be done automatically.  You'll not see this kind of type in a traditional language, but experimental languages like Agda and Idris support this idea.

This is our first hint to understanding Curry-Howard.  We've just seen in highly expressive type systems, some types have no witnesses.  There is no element of `{n:Nat | n>5 /\ n<3}` and if we declare there to be one, the result is inconsistency in our type system.  If theorems are types and proofs are programs, what does this mean?  Types can have no programs.  Can theorems have no proofs?

Let's define a new type that we will call `True`.  `True` will have exactly one witness that we will call `I`. Thus we know that `I:True` holds.  `I` is also going to be treated as a proof.  `I:True` says that `I` is of type `True`.  It also says that `True` has a proof and is always true.  This is important - `I` is of type `True` and is a *proof* of `True`.  *Types are to programs as theorems are to proofs*.

`True` is easy to define using an algebraic type:

{% highlight coq %}
Inductive True : Type :=
   | I : True.
{% endhighlight %}

Let's define a second new type that we will call `False`.  Unlike `True`, `False` will have no witness.  We can prove `False` from other assumptions, but unlike `True` we cannot prove `False` without knowing other things.  `False` is also easy to define using an algebraic type, but note there are no constructors for `False`.

{% highlight coq %}
Inductive False : Type := .
{% endhighlight %}

Now we have `True` and an ever present proof, `I`, for `True` and `False` with no proof.

Curry-Howard says that *types are to functions as theorems are to proofs*. A type that has no associated function or witness is inconsistent and cannot be used.  A theorem that has no proof is not consistent and cannot be used.  If we treat a theorem as a type, then finding a proof is the same thing as funding a witness to the type.  (This is where my head exploded the first time through.)  Theorem proving is type checking?  That's exactly it.

Let's do some proofs.  First, we'll prove `True`:

{* highlight coq *}
I:True
{* endhighlight *}

Let's look at some tautologies.  First, lets look to prove `True => True` by finding a witness of the type `True -> True`.  Note specifically that `->` is playing the role of implication.  It's easy to interpret this as "input something of type `True` and produce something of type `true`".  Said differently, "input a proof of `True` and output a proof of `True`.  That reduces the problem to finding a witness to the type `True -> True`.  How about this one:

{% highlight coq %}
(fun x:True => x) : True -> True
{% endhighlight %}

Bingo.  The function accepts some input of type `True` and returns it.  Thus, the function serves as a proof of the tautology `True -> True`.  Let's try a slightly different proof, `True => False`.  We need to find a function that accepts an proof of `True` and produces a proof of `False`.  Can we copy the first function?

{% highlight coq %}
(fun x:True => ???) : True -> False
{% endhighlight %}

What should `???` be?  It can't be `x` because `x` is of type `True`.  What value of type `False` can we return?  Remember, `False` is an empty type.  There are no values of type `False`.  Thus, this function cannot be written.  There is no proof of `False` to return and the theorey `True->False` has no witness.

Let's flip it and proof `False=>True`.  This one should be true, we simply need to find a witness to the type `False -> True`.  Turns out not to be difficult at all because we know that `I` is a witness to true.  Thus, the function becomes:

{% highlight coq %}
(fun _:False => I):False -> True
{% endhighlight %}

We don't care about the `False` proof and simply return the witness to `True`.  This should bother you.  What would happen if this function were called?  An input of type `False` does not exist and would blow the whole thing up.  That's true, but all we care about is that a function of the right type can be found.  We care about the proof, not what we might do with the proof.

Can we prove `False` from `False`?  Pretty simple actually:

{% highlight coq %}
(fun x:False => x):False -> False.
{% endhighlight haskell %}

If there is a proof for `False` then that proof can be used again for `False`.  Pretty cool.  We can proof `False` from `False` because the proof of the antecedent is assumed.

We're just proving things about `True` and `False`.  Let's think a bit about propositional logic.  Starting simple again, lets assume a proposition `A` and prove `A=>A`.  That should be true.  Turns out it has a simple proof:

{% highlight coq %}
(fun p:A => p):A -> A.
{% endhighlight %}

Given a proof of `A` then we have a proof of `A` and we're done.

What does this statement say:

{% highlight coq %}
(fun a:A => (fun b:B => ???)) : A -> (B -> A/\B)
{% endhighlight %}

Make sure this is cool.

{% highlight coq %}
(fun p:A => (fun q:B => And A B)):A -> B -> 
{% endhighlight %}
Let's think about a new type call `Prop` that represents a logical proposition.  `Prop` should has two values, `True` and `False`.  Just like `Nat` we can create function types using `Prop`:

{% highlight haskell %}
not : Prop -> Prop
{% endhighlight %}

We can interpret this as we always have - give `not` a `Prop` and you'll get back a `Prop`.  

What happens if we interpret the type constructor -> as an implication?  p:T=>T

---

Let's think about a new type called `Unit` that has precisely one element, `()`.  `Unit` has some interesting properties that we'll ignore here, but the one property it does have is precisely one witness.  We know that `():Unit` and this `Unit` is inhabited with a value.  If I ask for something of type `Unit` you could immediately show me `()`.  One could easily write a function that returns unit:

{% highlight haskell %}
f:T -> Unit
f _ = ()
{% endhighlight %}

Note the wildcard parameter whose value and type we really don't care about.  There's only one `Unit` and if this function returns something of type `Unit` it must return that value. In an odd sense, there is precisely one function that returns `Unit`.
