___
layout: blog
categories: blog gear
title: Bryston BDP-2
---

The latest addition to my sound system is a Bryston BDP-2 media
player.  It's a rather unique device who's only purpose is reading
music files of virtually any format and outputting them to D/A
devices.  I'm replacing my trusty Mac Mini with a dedicated music
player because iTunes is rapidly becoming the Microsoft Word of music
players - a bloated pig of functionality that I don't want.  As I said
to the Bryston engineer, I just want to play my music.  That's all.
No Genius lists, no cloud crap, no preferred formats, no automatic
tagging, nothing.  Just take my music and push
it out to a D/A.

For reference, I've changed virtually nothing else in my playback
chain - Benchmark DAC1 D/A, Audio Research LS26 preamp, Parasound A21 amp,
Snell C/5 speakers.  I didn't do this for sonics, but simply for
playback capabilities.  Given my propensity to avoid any kind of
bullshit speaker cables and shiny lights for CD preparation, I suspect
everyone guessed that.

I'll start with my general assessment.  I'm very happy with the BDP-2.
I don't think it's for everyone, but for me it's just about perfect.
It is not cheap and if you have just a few thousand songs I don't
think the cost is at all justified, but if you have 40,000 songs
dating back to the early 2000s this is a killer device.

At its heart, the BDP-2 is a Linux box jazzed up to be a dedicated
music player.  You don't need to know a think about Linux to use it,
but given that I do the device is more interesting to me.  I can `ssh`
into the box and use command line Linux stuff like `scp`, `tar` and
old friends to manipulate the file system.[^0]

The BDP uses the `mpd` system to manage playback.  I have found it
more than capable of managing my music.  `mpd` is a standard and
provides an api that any application can use.  Thus, I'm not tied to
anything that Bryston provides for controlling playback.  I could, if
I got really inspired, write my own front end.  That's not happening
anytime soon, but a guy can dream.

Bryston's interface to `mpd` is a simple input screen on the device
and two web interfaces.  I rarely use the device input simply because
I'm usually sitting on the couch.  I do use the web interfaces all the
time and find them quite useful, if a bit on the dated side.  I also
use the mpod and mpad applications on my iPhone and iPad respectively
and use theramin on my Mac.  I'd say I end up using mpod and mpad the
most simply out of convenience.[^1]  Your mileage may vary based on
the interface that you like.

The BDP-2 provides no storage by default.  There is a slot for an
internal drive if you want to send it back to Bryston and have them
add something.  I chose not to do that.  Instead, I bought to Samsung
SSDs (256G and 512G) to store my music.  I use one for new stuff and
the other as my permanent storage device.  One uses a USB 2.0
interface and the other ESATA.  Both seem to work just fine and are
plenty fast for what I do.

The BDP-2 provides a SAMBA interface that allows you to mount drives
you attach to it as well as mount remote devices.  It works like a
charm after setting it up.  It seems a bit slow mounting on my Mac,
but not so much that I have a problem with it.  I do use that
interface from time-to-time when I'm moving small amounts of music
from my Mac Mini to one of the hard drives.  There's also plenty of
USB ports for use with USB sticks if you prefer that mechanism.

For all my music across two drives it takes only about 200 seconds to
update local caches on my playback devices.  At least that's what they
say.  I perceive it to be faster than that.  Rebuilding the internal
database on the BDP takes quite a bit longer, but that doesn't happen
very often and adding new music works far faster.

Some cautions are in order.  The BDP is not iTunes - you will have to
do some work to use it.  You are responsible for arranging your music
and making sure it ends up where you want it.  The BDP will do a fine
job of organizing the interface after that.  The main interface on the
device can be quite uninformative when updates are occurring.  It shows
a small U as far as I can tell, but I'm not 100% certain of that.  The
biggest issue however was my device was delivered with outdated
firmware.  Almost a year outdated.  I tried updating from the device
menu several times with no luck.  After pestering Bryston for a bit
they provided me an alternative update mechanism using Dropbox that
worked like a charm.[^2]

[^0]: Login and password are `bryston` and the address for the device
is `bryston-bdp-2.local`

[^1]: I will admit a bit of concern over not seeing recent updates for
mpod, mpad, or any of the third party front-ends that I use.

[^2]: Pester Bryston.  They really seem to enjoy it.  No kidding!
