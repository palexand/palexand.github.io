---
layout: blog
categories: blog coq
title: Enumerations
---
An *enumeration* is a type whose possible values are a finite set that can be listed.  Following is a simple enumeration that defines the possible states of a common US stoplight:

{% highlight coq %}
Inductive stoplight : Type :=
  | red : stoplight
  | yellow : stoplight
  | green : stoplight.
{% endhighlight %}

The colors of the stoplight are the *values* or *constructors* of this type.  They define every possible way that a `stoplight` value can be constructed.  There are no other elements of `stoplight` and any item of type `stoplight` must have one such value.  Here is an example of a new value, `stop` that has the value `red`.

{% highlight coq %}
Definition stop : stoplight := red.
{% highlight coq %}

The general format for an enumeration definition is as follows:

{% highlight coq %}
Inductive *name* : Type :=
  | *value* : *name*
  | *value* : *name*
  ...
  | *value* : *name*.
{% endhighlight %}

Where *name* is the name of the new type and each *value* : *name* pair represents a value in the type.  Think of this as defining a type as a set by listing all its elements.

Writing functions over the `stoplight` type is done using pattern matching:

{% highlight coq %}
Definition next_color(s:stoplight) : stoplight :=
   match s with
    | red => green
    | green => yellow
    | yellow => red
   end.
{% endhighlight %}

`next_color` is a function of type `stoplight->stoplight`.  The value of the function uses `match` to determine what to do for specific cases of `s` ^[note].  In this case, the function defines a standard next state function for a US stoplight.

The `next_color` function is an *observer* of the type `stoplight`.  It defines a property over all possible stoplight values.  Defining constructors and observers over those constructors is a common specification technique called *constructive specification*.  We will come back to this concept later.

You can check out how `next_color` works using `Eval`:

{% highlight coq %}
Eval compute in (next_color red).
Eval compute in (next_color (next_color green).
{% endhighlight %}

We'll come back to `compute` later, but these examples use `Eval` to apply the proof tactic `compute` to an expression resulting in a kind of execution.  Don't get too hung up on the details of `Eval` for right now.

You can also do proofs over `next_color` and `stoplight` values.  Here is a proof that evaluating `next_color` on `red` is always `green`:

{% highlight coq %}
Example test_next_color:
   (next_color (next_color red)) = green.
Proof. reflexivity. Qed.
{% endhighlight %}

A more interesting proof establishes that `next_color` is irreflexive - its output is never its input:

{% highlight coq %}
Theorem irreflexive_next_color:
   forall x, x <> next_color x.
Proof.
   intros. induction x; unfold next_color; discriminate.
Qed.
{% endhighlight %}

Some interesting things going on here.  The definition looks like all the rest - A `Theorem` with the name `irreflexive_next_color` is being defined.  Read literatlly, the type of `irreflexive_next_color` is `forall x, x <> next_color x`.  The type of the new theorem is the theorem to be proved.  This is exactly right.  The period after the type throws Coq into the prover where you define the value - a proof - of that type.  The term `Proof` begins that definition and human readable scripting language is used to define the proof value.

This is the Curry-Howard Correspondance at work.  The proof is a witness to the theorem - it is an element of the type.  Hang on to this thought.

Here's what is going on in the proof:

* Proof - start defining a proof value
* intros - elminates the universal quantifier and creates an assumption from the quantified variable.
* induction - invokes the induction principle associated with an indctive type.  every inductive definition provides and induction principle
* discriminate - invokes a proof-by-cases that ignores induction hypotheses.  every inductive definition provides a proof-by-cases principle
* unfold - replaces a name with it's definition
* Qed - Quick, Eat Donuts (end your proof value definition)
		
The proof is now named `test_next_color`

You can also extract code from both the type definition and the function:

{% highlight coq %}
Extraction stoplight.
Extraction next_color.
{% endhighlight %}

You now have a definition of `stoplight` that is guaranteed to be irreflexive as proved in the theorem.

[^note]: Coq uses a reasonably standard form of pattern matching in its `match` expression.  If you don't understand it, take a look at what Haskell or ML do.

---

Using `Definition` is a common way to give paramterized expressions names.  The general form is:

{% highlight coq %}
Definition *name*(*params*) : *type* := *value*.
{% endhighlight %}

Where:

* `Definition` - keyword indicating a new definition
* *name* - the name of the new thing being defined
* *params* - optional parameter list
* *type* - the type of the newly defined thing
* *value* - the value of the newly defined thing

The `match` expression is performing a pattern match on `d`.  In this case, a trivial pattern match on the values of `day`.  You have to cover them all, or Coq will tell you.

Notice the form of both definitions:

	*keyword* *name* *params* : *type* := *value*.

Everything in Coq is defined in roughly the same way.
