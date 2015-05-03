---
layout: blog
categories: blog
title: Turing and The Cloud
---
A few days back I needed to explain The Cloud to a good friend who is brilliant, but not a computer scientist.  It dawned on me that I could use Turing Machines and specifically the Universal Turing Machine to explain it far easier than metaphor or trying to explain Xen and OpenStack.

What Turing envisioned was a machine that could represent algorithms - what he called the A-Machine now called a turing machine.  Each algorithm was associated with an A-Machine that implemented it.  What he then did was took an A-Machine and represented it as a sequence of characters that could be put on another A-Machine’s tape.  The states and transitions that define the A-Machine are encoded in a table and rows in the table encoded sequentially on the tape.

Then he defined another A-Machine that would read a tape with the first A-Machine encoded on it and execute the represented A-Machine.  This new thing is called a Universal Turing Machine and is the basic definition of stored program computing.  So, a Turing Machine that executes other Turing Machines is what your Mac is.

Virtualization takes this one step further.  If this Universal Turing Machine can execute any Turning Machine, then it can execute itself.  Universal Turing Machine executes Universal Turing Machine executes an arbitrary Turing Machine.  This is the definition of virtualization.  What makes this more interesting is you can equally have a Universal Turing Machine execute *many* Universal Turing Machines executing arbitrary Turing Machines.  This is the notion of multiple virtual machines running on the same hardware platform.  We now have virtualization, but we still don’t have a cloud.

The cloud is a collection of virtual platforms - the Universal Turing Machine that is running the other Universal Turing Machines.  What that enables is moving machines from one virtualization platform to another.  For mathematics, this makes no difference at all.  For physical systems, its huge.  A virtualize system running on one hardware platform can move to another with no detectable change in how it runs.  System failure, maintenance, upgrades can now be accommodated without taking systems offline.  If you want to read about the specific software used to do this, look at Linux, Xen, and OpenStack as examples.
