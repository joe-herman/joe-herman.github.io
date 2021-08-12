---
layout: post
title: "Remotely Inclusive Best Practices"
---

A list of things I've found that made hybrid and fully remote teams remotely successful.

## Meeting Culture
* Unless it's considered just a call, turn your video on! It's nice to see you.

* If one person is attending a meeting remotely, everyone else should too. This means no conference rooms where some people share a TV screen with each other while people unable to appear in person are relegated to their laptops--everyone joins the same meeting the same way.

* ["Zoom fatigue" is real](https://ideas.ted.com/zoom-fatigue-is-real-heres-why-video-calls-are-so-draining/). Allow bio breaks and meetingless time between meetings.
  * In my experience, meetings that start a few minutes late tend to be better than meetings that end a few minutes early.

* The opening minutes should be dedicated to tech checks and banter. Everyone's audio/video checks take a moment, and remote coworkers don't get the spontaneous coffee machine chats that onsite coworkers do, so while everyone is getting settled in, say hi!

* Checklists of things to consider before meeting:
  * What's the goal of this meeting?
  * Can this goal only be achieved synchronously (instead of via email or Slack message)?
  * Are all the appropriate stakeholders in this meeting?
  * Aside from time exiring, when can this meeting end?

* Read the room
  * Reading faces while talking and ensuring your camera and audio are functioning is exhausting but necessary.
  * Being dozens to hundreds of milliseconds away with only one speaker at a time means only one person can speak at once. Yield to others who want a turn.

* Write to the room
  * Zoom and Teams let you virtually raise your hand--use it!
  * Send reactions
  * Especially in 1:1s, ask how people are feeling. Only talking business is boring.

## Mad hax
  
### Quality matters
The less people have to use their imagination to communicate with you, the better.

* Having a mic with proper volume, gain, and postprocessing can make a huge difference in both being understood and being taken seriously.
* In general, wire up wherever possible.
  * While wireless is far better than years ago, consistent wireless throughput (with low latency and jitter) is more difficult to maintain than a wired connection. Also, connections take longer.
  * This applies to both your internet connection (use ethernet where possible!) and your audio connection (use wired headphones).
  * It's relieving to manage one fewer battery (or in the case of Airpods, 3).
* Clean your lens.
  * Seeing you through a fog of fingerprint smudges is not the kind of softening you want for your face!
* Dress nicely.
  * No one needs to know you're in pajamas ([and if you are,](https://www.youtube.com/watch?v=Ph8RpxjrPYE), invest in a good stand), and I've definitely done the "put on a nicer shirt for an interview." Treating your home office like your office shows you care enough to get ready for others.

### What do I throw money at?
* Good lighting!
  * Makes your face look better.
  * Your webcam will thank you! More light = less noise and sometimes higher framerates.
  * Try for at least two light sources (natural or otherwise). Professional photography gurus will cringe, but I ended up with a similar setup that [Linus describes here](https://youtu.be/L6ZJaKqALgM?t=216) by pointing a lamp at a wall with [bulbs from Ikea that let me adjust the brightness and color temperature](https://www.ikea.com/us/en/p/tradfri-remote-control-kit-white-spectrum-50460042/).
* When feasible, try a better camera.
  * Good webcams are hard to find, but it's possible to [use some DSLRs or mirrorless cameras as a webcam](https://www.usa.canon.com/internet/portal/us/home/support/self-help-center/eos-webcam-utility/).
  * Your phone probably has a better camera than your laptop. I find no shame in joining meetings "twice" to have better video (or even audio that can fall back to a cell tower).

### On old wireless things

More subtly, every wireless device is making noise of some kind on a fixed set of spectrum. Usually there's enough spectrum/channels to go around, but wireless devices work a little harder trying to speak to one another as noise increases, which can lead to increased connection hitches.

Another trend is that while a lot of technologies increase overall wireless capacity (ex: [MU-MIMO](https://en.wikipedia.org/wiki/Multi-user_MIMO), [OFDMA](https://en.wikipedia.org/wiki/Orthogonal_frequency-division_multiple_access), [Bluetooth 5](https://en.wikipedia.org/wiki/Bluetooth#Bluetooth_5)), they require new devices to all be speaking the new way. This means old devices that do not run new protocols on the same frequencies actively slow the rest of the network down. Even some wired devices cause [noise on the same channels that WiFi](https://www.intel.com/content/www/us/en/products/docs/io/universal-serial-bus/usb3-frequency-interference-paper.html) and other peripherals use. For connections where performance matters most (like Zoom calls), _wire up!_

---------
  * Wireless earbuds, while incredible compared to years ago, still have to contend with a lot of extra problems: poor microphone placement, flaky pairing to the host device, compressed 2-way audio, state of the art noise cancelling that can be affected by *sound reflecting back at them* (like a laptop screen), charging, etc. They're impressive technology but listen to someone with old-school wired iPod earbud headset, and performance-wise there's no contest.
