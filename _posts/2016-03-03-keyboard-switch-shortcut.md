---
layout: post
title: OS X El Capitan Keyboard-switch Shortcut
comments: true
permalink: osx-keyboard-switcheroo
---

<h4>Important: I'm going to skip to the part after you add a new keyboard input source. If, for some reason, you didn't add a new keyboard input source, here's where you go:</h4>

<code>System Preferences > Keyboard > Input Source</code>, then click the <code>+</code>

I'm making a Japanese Katakana flash card game using Rails; so it was mission critical that I have quick access to both the Japanese and U.S. keyboard.

When I looked at the shortcut command (<code>option + command + spacebar</code>), it didn't work at all. Wtf.

Turns out OS X's Spotlight feature was hogging it for a Finder command. Lame. I disabled the Finder command and violà!
