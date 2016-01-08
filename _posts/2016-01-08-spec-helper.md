---
layout: post
title: rspec woes ft. spec_helper
comments: true
permalink: spec-helper-woes
---
If you somehow are grappling with this *LoadError* while running rspec tests:

<br>
<code>rspec-core-3.1.7/lib/rspec/core/configuration.rb:1072:in require: cannot load such file -- spec_helper (LoadError)</code>
<br>
<br>

Hopefully this will help you out -- read on amigo.

Rule numero uno of programming is to read the error message for clues, like Scooby-Doo and the gang. Looks like Rspec was trying to look for a file called <code>spec_helper.rb</code> DEEP inside the Rspec core library (the error was thrown @ line 1_072)!

No big deal right? I quickly Google'd *spec_helper* and gleaned that the file needs to be inside of your spec directory/folder. So, I did just that, manually. Nothing inside the file. I'm a genius right? Ran the tests again ... but it still gave me that damn *LoadError*!

Just like Transformers, there's more to <code>spec_helper</code> than meets the eye! Turns out, all I had to do was type this in my terminal (inside whatever directory that has the spec folder):

<code>$ rspec --init</code>

What it does is generate some conventional files for your project:

* <code>.rspec</code>
* <code>spec/spec_helper.rb</code>

I ran the Rspec test again and finally got it to work. Yee! If you have the files already and run that above command, the output in your terminal will be:

* <code>exist .rspec</code>
* <code>exist spec/spec_helper.rb</code>

In which case, nothing will happen and no need to worry. Hope this was helpful.
