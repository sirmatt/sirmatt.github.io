---
layout: post
title: Port already in use? Let's kill it
comments: true
permalink: port-already-in-use-kill-kill
---
<!-- this is really about the tcp kill commands and rails server error -->

While working on a project involving Rack + HTTP, I came across this error telling me that I am trying to access a port (<code>localhost:3000</code>) that is already in use.

My server was still listening on that port, it never finished. In order to use that port again, pop open your terminal and type this:

<code>$ lsof -wni tcp:3000</code>

* <code>lsof</code> just means "list open files"
* the <code>-wni</code> flag is a combination of three separate parts:
  * <code>-w</code> disables the suppression of warning messages
  * <code>-n</code> makes <code>lsof</code> command run faster
  * <code>-i</code> selects from the listing of files, any of whose Internet address matches the address specified

After you hit enter, you'll see a list of any processes being used by (in this case), port 3000.

There's a <code>PID</code> (process identifier) number column that you'll need for the final step of actually killing the process and open up the port for use again.

With your <code>PID</code> number in hand, you just need to type this into your terminal:

<code>$ kill -9 PID</code>

(That <code>PID</code> above will be an actual number)
