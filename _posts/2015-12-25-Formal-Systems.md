---
layout: blog
categories: blog coq
title: Formal Systems
---
Our task is to define formal systems that describe systems and reason about those systems to determine correctness.  One application of this is verifying language properties, but that represents a tiny fraction of the kinds of verification we can do.  In fact, we do this all the time: (i) circuits example of a parity checker; (ii) examples from physics.

We would like a predictive mathematics for computer systems systems.

## Formal Systems

A *formal system* consists of three parts:

1. A *formal language*
    1. An *alphabet*
    1. A *grammar*
2. An *inference system*
    1. A set of *axioms*
    1. A set of *inference rules*
3. A *semantics*

### Formal Language
 
A *formal language* is an *alphabet* describing a set of atomic tokens
and a *grammar* that defines proper ordering of those tokens.  We will spend little time in this course discussing formal languages, but for completness I'll include a simple example.  Consider a language, \\(L\\), defining strings of letters:

Alphabet: \\(\\{a,b,c\\}\\)
Grammar: \\(L ::= empty \mid aL \mid bbL \mid cccL\\)
	
Examples of strings from \\(L\\) include:

\\[a, bba, ccca, cccbbbbcccc\\]

while examples of strings not in \\(L\\) include:

\\[bbb, cbc, acca\\]

The study of languages and grammars is called *formal language theory* or *computation theory*.  As it turns out we can learn tons of good stuff by defining recognizers and generators for languages using automaton.  A formal language theory course is taught frequently as EECS 716 should you be interested.

### Inference System

An *inference system* is a collection of *inference rules* and *axioms*. 
Inference rules define immediate consquences of known facts.  They have the form:

\\[A_0,A_1,A_2,...,A_n \vdash C\\]

or equivalently:

\\[\frac{A_0,A_1,A_2,...,A_n}{C}\\]
	
The \\(A_k\\) are called *antecedents* and \\(C\\) is a *consequent*.  The rule states that if all \\(A_k\\) are known to be true, then \\(C\\) is an *immediate consequence*.  Consider the example inference rule:

\\[\frac{\forall x \cdot P(x)}{P(a)}\\]

that says if we know \((P\)) is true for all \((x\\), then it is true for a specific value \\(a\\).  A second rule defines the concept of implication.  Assuming that \\(A\\) and \\(B\\) are logical statements, the inference rule: 

\\[\frac{A, A\rightarrow B}{B}\\]
	  
says that if we know \\(A\\) and we know \\(A\rightarrow B\\), then we immediately know \\(B\\).

Finally, the inference rule:

\\[\frac{\;}{\forall x \cdot bird(x) \rightarrow flies(x)}\\]

says that withoug knowing anything else, if we know that \\(x\\) is a bird, then \\(x\\) flies.  This rule is an *axiom* because the consequent depends on no antecedents and is true by definition.

A *proof* strings axioms and inference rules together starting from a set of known things and moving towards a conclusion.  Using the axiom and rules above, we can prove that tweety flies:

\\[\frac{\frac{\frac{\;}{\forall x \cdot bird(x) \rightarrow flies(x)}{bird(tweety)\rightarrow flies(tweety)}} bird(tweety)}{flies(tweety)}\\]

Defining models and using inference systems to verify their properties is the basis of this source.

### Semantics

A *semantics* links symbols to their meainings.  This is the topic of programming language semantics.  We'll touch on this in our class, but it's the primary topic of EECS 762.

### Models

In this class we will focus on defining models in a specific formal system.  A model is simply a collection of definitions in a formal system.  Using the formal system, one can reason about properties of those definitions - what they imply, how they are related, what properties they exhibit.  You have been doing this since you started doing word problems in mathematics.  However, you have quite likely not done this for software artifacts.

## Logic

The basic mathematics for describing software is logic.  Logic will be our formal system  There are many logics for many purposes, but most are rooted in *propositional logic* and *predicate calculs.*

### Propositional Logic

Propositional logic is the arithmetic of logical systems and where we will start.

\\[P ::= A,B,C,\ldots \mid P \wedge P \mid P \vee P \mid \neg P \mid P\rightarrow P \mid P\leftrightarrow P\\]

Logical variabes and statements plus the classical logical operators for and, or, not, implies, and logical equality.

We have a collection of rules that describe out these operators work.  Specifically, rules that *introduce* and *eliminate* operations.  The rules for conjunction are:

\\[\frac{X,Y}{X \wedge Y} \frac{X\wedge Y}{X} \frac{X\wedge Y}{Y}\\]

They are directly used in a forward fashion:

"If I have \\(X\\) and \\(Y\\), then \\(X\wedge Y\\) is an immediate consequence."

or indireclty in a backwards fashion:

"If I want to have \\(X\wedge Y\\), then I need to know \\(X\\) and \\(Y\\)."

### Predicate Calculus

Predicate calculus adds variables and quantifiers to propositional logic.

\\[P ::= \ldots \mid \forall x:T \cdot P(x) \mid \exists x:T \cdot P(x)\\]

where \\(x\\) is a variable and \\(T\\) is the type of that variable.  Just like propositional logic, we have introduction and elimination rules for our new predicate operations:

\\[\frac{\forall x:T \cdot P(x), a:T}{P(a)}\\]

\\[\frac{P(a)\mathsf{where a:T is arbitrary}}{\forall x:T \cdot P(x)}\\]

Predicate calculus of this form will be our tool for writing specifications.

## Coq

Coq is a proof assistant constructed around inuitionistic logic based on the calclus of constructions.  It's language is called gallina.  Coq will be our Matlab - a tool for assisting us in development and manipulation of models for software, requirements, and constraints.