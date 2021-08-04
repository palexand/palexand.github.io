---
layout: frontpage
title: Thoughts on Writing
---

# Thoughts on writing
> A bird does not sing because it has an answer, a bird sings because
> it has a song - Joan Walsh Anglund

We write because we have something to say that we would like to share.
Whether we are writing in a journal or blog, writing for a
publication, writing about our research, or writing home to mom we are
sharing our stories.  We do not write because we are done or to
describe a perfected artifact.  We certainly don't wait to write until
the research is done.  We write to tell our stories.  We write because
it is cathartic, healthy and mentally stimulating.  It helps organize
our thoughts and makes us more disciplined researchers. 

Following are some thoughts I have put together on technical writing.
I can't say that I've perfected anything or have a sliver bullet to
get our papers published, but I do have stories to share. 

## Axiomatic Semantics of Papers

### Preconditions on papers:
* Read Simon Peyton Jones' slides on paper writing [here](https://research.microsoft.com/en-us/um/people/simonpj/papers/giving-a-talk/writing-a-paper-slides.pdf)
* Read papers in the discipline you are interested in, identify those
  you like and respect, write like they do, repeat 
* Read Simon Peyton Jones' slides on paper writing again

### Invariants on papers:
* Do not be cute
* Do not be negative
* Do not hide limitations of your work
* Do not use any more words than are necessary
* Do use parallel construction
* Do use fonts and styles consistently and meaningfully
* Do think about Occam's razor


### Postconditions on papers:
* The paper shall look professional and polished
  * Proper spacing
  * No floating headers
  * No single subsections
  * No overfull vertical spaces
* Figures shall look professional and polished
  * Aligned properly
  * Spaced properly
  * Scaled properly
* The paper shall read like papers from those you wish to be your peers

## Planning to write

### Identify your target and write to them:
* Mathematicians and theorists- Theorems and proofs should be the
  heart of any formal, analytic paper written for mathematicians.  We
  rarely write this kind of paper. 
* Application domain engineers - The problem being solved and the
  methodology for solving it should be the heart of a paper targeting
  application domain engineers.  The focus should be on solving a real
  problem with a presentation focusing on sensible
  examples. Evaluation using empirical studies is important.  We often
  write this kind of paper to introduce work to a user community. 
* Formal Methodists - An odd combination of the previous two groups.
  The problem being solved is central, but the description must focus on
  formal foundations.  The mix of application and formalism is dictated
  by the audience and venue.  Still need empirical results, but with a
  dose of formalism. A little bit of math goes a long way in these
  papers. We write this kind of paper most often.

### What kind of paper is it:
* Analytical - Focusing on definition, proofs and derivations.
  Evaluation typically is in the form of proof. 
* Empirical - Focusing on examples and experiments.  Evaluation is
  typically in the form of experimental studies. 
* Case Study - Focusing on a single demonstration problem.  Evaluation
  typically is deemphasized, but should still be there. 

### What kind of target is it:
* Workshop - Early results, domain specific results, often focused on
  a narrow community. 
* Conference - Significant results that may or may not be the end of a
  research activity. 
* Journal - Major results that typically represent critical milestones
  in a research career. 

## Paper Structure:
This does not change based on venue.  You always need these sections,
although some sections may collapse into one section for shorter
papers.  Although this is slightly different than what is presented in
the SPJ paper, it still says basically the same thing. 

* Title
* Authors
* Abstract
* Introduction
* Technical Description
* Example
* Evaluation
* Related work
* Conclusions and Future Work
* Bibliography

### Title:
* Always descriptive
* Meaningful to your intended audience

### Authors:
* First author is the primary student writer
* Last author is supervisor/advisor
* Other contributors are in between in order of contribution

### Abstract:
* Abstract is always necessary
* Four sentences in one paragraph
  * the problem
  * why we care about the problem
  * what you achieved
  * impact of what you achieved
* Not a summary of the paper
* A descriptor for the librarian to classify it
* A descriptor for readers to select it
* If it's not good, NO ONE will read the paper

### Introduction:
* Introduction is always necessary
* Introduction is a summary of the entire paper
* Introduction is never a table of contents (In section 1 we will
  ... in section 2 we will...) 
* Introduce and motivate the problem
* Summarize what you did, highlighting your contribution
* Always have an overview figure
* A good place for basic background and history (I disagree with SPJ here)
* If it's not good, NO ONE will read the paper

### Technical Description:
* Overview your work point by point
  * Problem
  * New idea
  * All the details
* Do not teach, present to other experts
* A running example always helps
* Limit code listings and eliminate anything not explicitly
  referenced in the paper 
* Analytic papers should clearly motivate and call out theorems,
  proofs and derivations 
* Experimental papers should clearly call out the experiments
  executed and results 
* Case Study papers should clearly outline an meaningful example

### Examples:
* Linear flow from problem, through the tool, to a solution
* Should be reproducible if at all possible
* Limit details of specifications and code
* Limit pictures of detailed windows and screen shots
* Why do I care about this example?
* Make sure it reflects your target domain properly
* Make sure it's not wonky

### Evaluation:
* Different for different types of papers
* Analytic evaluation involves proofs and derivations.  Not so much
  traditional experimentation. 
* Case Studies should include summaries of a number of examples
* Experimental should define the experiments performed, list results,
  evaluate results and justify why the experiments are appropriate.
  Not so much analytic proof. 
* Whether a theorem or experimental outcome, what you observe must
  provide meaningful information 
  * Data for comparison
  * Critical property
  * Distinguishing characteristic
* Example and table approach
  * Work through one example in detail
  * Provide a summary table of other examples
  * Highlight meaningful results
  * Compare with existing results if at all possible
    
### Related Work:
* Always positive.  These people are your colleagues.
* Pointers to references the work builds upon
* Pointers to references that solve similar problems in different ways
* Pointers to references that solve similar problems in similar ways
* Should provide context and history
* Not just a list of references.  Compare and contrast.
* Make sure your citations are strong and use primary citations
  wherever possible 
* Citation is the currency of academia.  It is how we honor and
  compensate our peers. 

### Conclusions:
* The same structure and goals as the introduction
* Make sure your conclusions don't say something different than the main paper
* Make sure your conclusions agree with the introduction
* Clearly identify the problem solved and your contributions
* Thank those who should be thanked and are not authors

## General thoughts:
* If you haven't written about your work, it is not done.  If you
  don't write about your work, you have wasted your time. 
* Spend one hour each day writing for every one hour you spend coding.
* Write about anything and everything to develop your chops.  Literary
  writing, blogs, music reviews, letters to mom... 
* If you have writer's block, see the previous comment.  Write
  anything and everything. 
* Write research papers about what you have done, write white papers
  about what you're doing, and write proposals about what you want to
  do. 
* Publishing is the Major Leagues.  You are competing for printed
  space with authors of the papers you read and look up to. 
* If you are writing new material the hour before you submit, you will
  submit a rough draft.  If you are writing significant new material
  the day a paper is due, you will submit a rough draft.   If I don't
  get to see the paper until the day it is due, there's little I can
  do to polish it.  Is your rough draft as good as Graham Hutton, Phil
  Wadler, Simon Peyton Jones, Doug Smith, etc's polished work?  Mine
  is not. 
* Get others to read your work before you submit.
* Start early.  Very early.  Way earlier than you think you need to.
* Use git/cvs/svn to share your papers when writing.
* Use LaTeX and BibTeX.
* Use the active voice
* Avoid meaningless words such as 'very', 'really', and the like
* Avoid 'of the' and 'which' (most of the time).
* Paragraphs should have exactly one subject and one tense.
* Paragraphs should always have more than one sentence.  Choose good
  introductory sentences that are descriptive of the message.  A
  reader should be able to read the paper quickly by simply reading
  the first sentence of every paragraph. 


