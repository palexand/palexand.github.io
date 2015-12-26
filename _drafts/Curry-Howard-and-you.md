---
layout: blog
categories: blog coq
title: Curry-Howard and you
---

I'm very excited. I am one with the Curry-Howard Correspondence.  Now I've known what it is for quite awhile, but it's finally completely clicked after using it for verification and seeing it in practice.  I've read about it in various excellent books - Pierce's [Types and Programming Languages]() and Chlipala's [Certified Programming Using Dependent Types]() being two such sources. Until I used it for everyday verification, I can't say that I understood the depths of it.  Kind of reminds me of the day I was working in Lisp way back when and recursion became my best friend.

*Types are to programs as theorems are to proofs*.

Simple, right?  Not so. I fought with the meaning of this from the first time I read it.

Types are properties of language constructs. They define promises made about calculated things and place demands on things calculated with.  Looking at the term `x+1` in the context of a type system we know that if `x` is a natural number, `+` will produce a natural number. If `x` is not a natural number, the result is not defined and we probably shouldn't allow the calculation.

Functions have types that are constructed from other types with the type constructor `D->R`. This has always made great sense to me.  Take any function, `f:D->R`, put in `d:D` and you get back some `r` of type `R`.  A constraint is placed on `d` with an accompanying promise about `r`.

Let's look at the type of an increment function over naturals, `inc:nat->nat`.  If you give `inc` a `nat` you will get a `nat`.  We can define this function in almost programming language in roughly the same way:

{% highlight haskell %}
Definition inc(n:nat) := n+1.
{% endhighlight %}

or more explicitly:

{% highlight coq %}
Defintion inc:nat->nat := (fun (x:nat) => x+1)
{% endhighlight %}

So,far so good.  This increment function, `inc`, is an example of a function of type `nat->nat`.  We call this a *witness* to type type `nat->nat` and say the type `nat->nat` is *inhabited*.  Most programming languages restrict their type systems so that every base type and every constructed type are guaranteed to be inhabited.  We'll soon see why, but first back to proofs.

Here's what we know.  Put a natural into `inc` and you are assured you'll get back a natural, thus the type of `inc` is `nat->nat`. Its value is the function `(fun (x:nat) => x+1)`.  I get all this, but what the heck does it have to do with proofs?

Let's start by thinking about the simplest proof I can think of:

{% highlight coq %}
True
{% endhighlight %}

Theorems are to types. So, let's make `True` a type representing the thing we want to be true.  Let's say this explicitly:

{% highlight coq %}
Inductive True : Type.
{% endhighlight %}

Proofs are to values. This is a bit trickier, but think it through. A proof of `True` is a value of type `True`.  In the case of `True` that proof is given and not derived.  If proofs are to values, then the proof of `True` must be a value of type `True`.  Let's define a value called `I` of type `True`:

{% highlight coq %}
Inductive True : Type :=
   | I : True.
{% endhighlight %}

Now the value `I` is an element of type `True` and thus a proof of `True`.

You're not sold and neither was I.  Let's try another proof and see what happens.

Second simplest proof I can think of is:

{% highlight coq %}
True -> True
{% endhighlight %}

How do we define this as a type?  Reading the logical statement gives us a clue.  *Given `True` we can prove `True`*.  Better yet, *given a proof of True we can find a proof of True*.  Proofs are values, so we can translate once again and get *given a value of type `True` we can find a value of type `True`*.  This should ring a bell.

First of all, the theorem above is both a theorem and a type.  I consciously chose the `->` symbol for implies because it is also the symbol for function type construction.  The type representing our theorem is exactly `True->True`.  So, the proof is something of type `True->True`:

{% highlight coq %}
Definition P:True -> True.
{% endhighlight %}

The value I've called `P` is simply the identity function.  Given a proof of `True`, produce a proof of `True`: 

{% highlight coq %}
Definition P:True -> True := (fun (x:True) => x)
{% endhighlight %}

Bingo.  The identity function from `True` to `True` is the proof that `True` implies `True`.

Let's define a second new type that we will call `False`.  Unlike `True`, `False` will have no witness.  We might prove `False` from other assumptions, but unlike `True` we cannot prove `False` without knowing other things.  `False` is also easy to define:

{% highlight coq %}
Inductive False : Type := .
{% endhighlight %}

Note that unlike `True` there are no constructors for `False`.  There are no elements of type `False`, thus there is no proof of `False`.  This is of course exactly what we want.  Or at least it appears to be.

Let's try a slightly different proof, `True => False`.  We need to find a function that accepts an proof of `True` and produces a proof of `False`.  Can we just copy the identity function use for the first proof?

{% highlight coq %}
Definition P:True -> False := (fun x:True => ???)
{% endhighlight %}

What should `???` be?  It can't be `x` because `x` is of type `True`.  What value of type `False` can we return?  Remember, `False` is an empty type.  There are no values of type `False`.  Thus, this function cannot be written.  There is no proof of `False` to return and the type `True->False` has no witness.  There is no proof of `False` from `True`.  That is exactly what we want.

Let's flip it and prove `False->True`.  This one should be provable and we simply need to find a witness to the type `False -> True`.  Turns out not to be difficult at all because we know that `I` is a witness to true.  Thus, the proof function becomes:

{% highlight coq %}
Definition P:False->True := (fun x:False => I).
{% endhighlight %}

We don't care about the `False` input at all and simply return the value of type `True`.  We can in fact prove `True` from anything by simply returning `I`.

This should bother you.  What would happen if this function were actually called?  An input of type `False` does not exist and would blow the whole thing up.  While that's true, all we care about is that a function of the right type can be found.  The function is the proof.  We care about the proof, not what we might do with the proof.

Can we prove `False` from `False`?  Pretty simple actually:

{% highlight coq %}
Definition P:False->False := (fun x:False => x).
{% endhighlight haskell %}

If there is a proof for `False` then that proof can be used again for `False`.  Pretty cool.  We can proof `False` from `False` because the proof of the antecedent is assumed.  Of course there is no proof for `False`, but we simply need the proof for `False->False`.

So far we're just proving things about `True` and `False`.  Let's think a bit about propositional logic.  Starting simple again, lets assume a proposition `A` and prove `A->A`.  This is true.  Proving it is finding a value of type `A->A`.  Turns out this is the same identity function that served us well for `True->True`:

{% highlight coq %}
Definition P:A->A := (fun p:A => p).
{% endhighlight %}

Given a proof of `A` then we have a proof of `A` and we're done.

---

What does this statement say:

{% highlight coq %}
Definition (fun a:A => (fun b:B => ???)) : A -> (B -> A/\B)
{% endhighlight %}

Make sure this is cool.

{% highlight coq %}
(fun p:A => (fun q:B => And A B)):A -> B -> 
{% endhighlight %}

Let's think about a new type call `Prop` that represents a logical proposition.  `Prop` should has two values, `True` and `False`.  Just like `nat` we can create function types using `Prop`:

{% highlight haskell %}
not : Prop -> Prop
{% endhighlight %}

We can interpret this as we always have - give `not` a `Prop` and you'll get back a `Prop`.

What happens if we interpret the type constructor -> as an implication?  p:T=>T

---

Let's now look at the type of a decrement function over naturals, `dec:nat->nat`.  Same constraint and same promise - provide a `nat` and get a `nat`.  We can define `dec` just like `inc`:

{% highlight haskell %}
dec n = n-1
{% endhighlight %}

and of course we immediately have problem.  `dec 0` does not produce a natural number.  Different implementations provide different solutions to this problem - add an error value, designate magic natural that represents an error, throw an exception, or put a guard around `dec`.  All these solutions are dynamic and don't help us predict a problem before it happens. 

How might we solve this problem statically with types?  One way is to create a whole number type that is all natural numbers excluding 0.  Pretty simple thing to do if we treat types and sets and use set comprehension:

{% highlight haskell %}
whole = {n:nat | n>0}
{% endhighlight %}

Problem solved.  Let's now define `dec` as follows:

{% highlight haskell %}
dec : {n:nat | n>0} -> nat
dec n = n-1
{% endhighlight %}

Now the constraint is the input must be greater than 0 and the promise is we'll get back a `nat`.  This new type is called a subset type in Coq or a predicate subtype in PVS and is an example of a `dependent type` that mixes evaluation with type checking.  We'll not go into that here.

Unfortunately, the problem is not solved.  In fact, we've created a much harder one.

Remember that type systems work hard to make sure types are inhabited.  Here's why.  Let's say we mistakenly declare a silly type using our new comprehension mechanism:

{% highlight haskell %}
{n:nat | n>5 /\ n<3}
{% endhighlight %}

and declare some variable to be of that type:

{% highlight haskell %}
x : {n:nat | n>5 /\ n<3}
{% endhighlight %}

It should be easy to see that our new type has no witnesses.  There is no `n` that is both greater than 5 and less than 3. The type of `x` is uninhabited.  That turns out to be a problem because we've said that `x` *must* take values that are witnesses to that type.  Thinking of types as sets, we've now said that `x` is an element of the empty set.  That is an inconsistency that ruins our type system.  If we were working in PVS or Coq, those systems would require us to prove a witness exists for every type.  However, that is not generally a decidable problem and cannot be done automatically.  You'll not see this kind of type in a traditional language, but experimental languages like Agda and Idris support this idea.

This is our first hint to understanding Curry-Howard.  We've just seen in highly expressive type systems, some types have no witnesses.  There is no element of `{n:nat | n>5 /\ n<3}` and if we declare there to be one, the result is inconsistency in our type system.  If theorems are types and proofs are programs, what does this mean?  Types can have no programs.  Can theorems have no proofs?  You bet!

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
Let's think about a new type call `Prop` that represents a logical proposition.  `Prop` should has two values, `True` and `False`.  Just like `nat` we can create function types using `Prop`:

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
