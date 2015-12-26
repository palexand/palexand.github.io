---
layout: blog
categories: blog coq
title: Begin at the Beginning
---
The first thing one must do to start using Coq is to get Coq running in your environment.  While this may sound simple, it took me quite awhile to get emacs configured the way I wanted with [ProofGeneral](http://proofgeneral.inf.ed.ac.uk/).  Thankfully, there are lots of ways to start using Coq and the community has done an excellent job of providing options.

## IDEs

My students found the best way to start using Coq is with one of the standard IDEs provided with the tool.  Virtually everyone in my class chose to use one of the IDEs.  There are three of them, one each for Windows, OS X, and Linux.  The most commonly used version in my intro class was the Windows version followed closely by the OS X version.  I've used the latter, but not the former.  Surprisingly after all my efforts to get Coq set up the way I wanted, I got no complaints about the IDE from anyone in the class.  They did come up with the name "cock-eyed" for the IDE that I sincerely hope the rest of the world is using as well.  There's nothing to the installation, so I'm not going to describe it here.

## Emacs on OSX

I've been using emacs since the 80's and I'm not about to change now. The Mac OSX IDE might be slick as a snail's trail, but you'll pry emacs out of my cold, dead hands.

It took me quite awhile to get things configured, searching down all the various installation options, but I finally have [ProofGeneral](http://proofgeneral.inf.ed.ac.uk/) in a state that works perfectly with Coq on OSX.  Here's what finally worked:

1. Install Coq using [MacPorts](https://www.macports.org/).  I tried several different OSX installations and did not get any to work.  MacPorts did the trick for me and does not seem to install a bunch of other cruft.
2. Install emacs. If you're reading this, then this is probably redundant.  I use (Emacs Modified)[http://vgoulet.act.ulaval.ca/en/emacs/mac/] as it seems to included what need and not much else.
3. Install ProofGeneral.  Here's the tricky bit that tood awhile to figure out.  Do not install the release version of ProofGeneral.  Instead, install the [pre-release version](http://proofgeneral.inf.ed.ac.uk/devel).  I had tons of problems with the official release and finally found a pointer to this version.  It works great with few if any problems.  Some indentation stuff I don't like, but it's minor.
4. Optionally install [company coq](https://github.com/cpitclaudel/company-coq).  Not quite sure where the name comes from, but this little packages gives you tons of autocomplete capabilities as well as nice unicode characters for many common operations.  It's not perfect and doesn't understand context particularly well, but it's really quite good.  Not required, but I find it increadibly useful.

## Emacs on Linux

I installed the Coq environment for emacs as well as the IDE on a Fedora VM and had no problems at all.  Just installed the basic RPMs and things worked quite well.  You'll have to install company coq manually if you go this route.

## Emacs on Windows

You're on your own here.  I don't use Windows for anything and have no experience here.  If someone has suggestions for instrucutions, I'm happy to post them.

# Bottom Line

Since I got emacs, proofgeneral, company coq and coq installed it's been smooth sailing.  No crashes and very few nit-picky interface things.  All-in-all just great tools.