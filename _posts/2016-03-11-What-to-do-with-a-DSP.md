---
layout: blog
categories: blog gear
title: What to do with a DSP
---
With the speakers uncrated and moved into something close to a decent configuration, it was time to figure out the electronics.  My plan was to work forward from my sources through the DSP to the amps and finally to the speakers.  This turned out to be a great approach as I figured out what to do with all this stuff.

Before moving on, I should describe out this system works.  Most systems that I've used take a signal from a source, run it through a preamp to control volume, an amp to up the power, then to speakers where the signal becomes sound.  Typically, a full-range speaker will have multiple drivers that handle different frequency ranges.  A crossover either in the speaker or immediately before the speaker in the signal chain filters the signal sending appropriate frequencies to each driver.  Sometimes the crossover is an active filter, but usually it is passive and you never know it's there.

My Snell C/Vs allowed me to use different signals for the highs and lows.  I chose to bi-wire them running different speaker cables from the amp to each speaker input.  I could have used different amps for highs and lows or assign one amp per speaker, but never tried that.  Regardless of how I connected things up, the crossovers are in the speakers and are after the amplifiers in the signal chain.

The new system is quite different to magnificent effect.  Instead of amplifying the signal and then filtering it at the speaker, a DSP filters before the amplifier allowing each speaker element to be driven by a different amplifier channel.  In my case, the LCR speakers have high, mid, and low drivers each with a dedicated channel in the ATI amplifier.

To get any sound out I had to get the DSP "programmed" to filter signals appropriately before they wind up at the amplifier.  Thankfully I had several configurations for the DSP developed by the masters at RBDG and tweaked by Hal Winer.  Just needed to get the configuration downloaded to the DSP.  Here is where the real adventure begins.

The DSP - a SymNet 8x8 with a 12 output breakout - is programed using a graphical application that runs on a PC.  I have no PC and won't go near one unless absolutely necessary.  Thankfully my wife  has access to PC portables at work that I can borrow to figure out the programming.

I got the PC home and downloaded the Symetrix programming application.  It worked fine and loaded the configurations from RDBG and Hal just fine.  Now to download to the 8x8 and breakout.  I'm stuck.  There are Ethernet ports on the devices, but they are dedicated to form a low-latency ring network allowing the 8x8 and the breakout to communicate.  Still, I tried treating the 8x8 as a network component and hooked it up to the PC.  No go.

At this point, I resorted to trying to find documentation.  The 8x8 is no longer produced by Symetrix, so that presented a minor problem that was quickly solved.  What I learned was a problem.  The 8x8 uses an RS-232 port to talk to the PC.  When is the last time you saw a PC with an RS-232 port?  Thankfully my buddy Dan at work has a dongle that turns a USB port into an RS-232 port.  Plugged it in, installed the driver, and bingo - I can talk to the  8x8.  Immediately downloaded the configuration and went to work to understand the 8x8 and start making sound come out of the speakers.  More on that process next...