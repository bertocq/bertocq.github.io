---
layout: post
title: "Winning a Firefox OS hackathon"
date: 2013-06-03 18:42
comments: true
categories: [Firefox OS, Hackathon, GeeksPhone]
published: true
---
On May 17th there was a [FirefoxOS Day at the Bilbao University](http://espana.movilforum.com/jornadaffoxosbilbao/), and later a hackathon.

I had the oportunitty to talk with [@soyjavi](https://twitter.com/soyjavi), it's always a bit weird to talk to someone well known that you follow on videocast and twitter but he doesn't have a clue of who you are.

The talks where great and inspiring, speakers [@jmcantera](https://twitter.com/jmcantera) and [Cristian Rodriguez](https://github.com/crdlc) I still had some memories from the talk on the past SpainJS conferences where I was able to touch the first prototype:

 {% img center http://distilleryimage5.ak.instagram.com/7a79c2aac6ef11e1b10e123138105d6b_7.jpg 500 500 'Winning a GeeksPhone Peak' 'Winning a GeeksPhone Peak' %}

Some GeeksPhone devices where given as prize for technical questions but it felt almost random.

After a good lunchbrake that replenished my energies (I had traveled 285km by car that day without rest) I headed to the hackathon. But I didn't knew anyone, and everybody seemed to had his group of pals and even some good ideas well prepared. There was going to be 4 categories to win a GeeksPhone device so it was totally a competition.

I was just hoping to at least learn how to create a basic app and be able to push it to a real device. I cloned the [example app](https://github.com/crdlc/puzzle) from Cristian's github, and started to make changes to see what I could do.

Then I remembered a app idea that I had almost a year ago, very basic but still used the alarm and notification [WebApi's](https://wiki.mozilla.org/WebAPI "WebApi Mozilla") so I spent 15 or 20 minutes trying to define what the app would be able to do and the incremental steps.

<blockquote class="twitter-tweet center"><p><a href="https://twitter.com/search?q=%23jffos&amp;src=hash">#jffos</a> hackathoneando <a href="http://t.co/R6cucvEGxm">pic.twitter.com/R6cucvEGxm</a></p>&mdash; movilforum (@movilf) <a href="https://twitter.com/movilf/statuses/335409077935013891">May 17, 2013</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

The first problem was the FirefoxOS simulator, that didn't seem to be able to handle the Alarms WebApi and until I found that hitting Command+R the app wash refreshed so I didn't need to push it again and again. Then I made a simple visor.html to test the visual styles on the browser more quickly:

{% codeblock Simple iframe to test the looks on the browser lang:html %}
<iframe src="index.html" width="320px" height="480px" />
{% endcodeblock %}

After 3 hours the time ran out and each group made a quick presentation in 1-2 minutes, we saw great but incompleted ideas, some others fully developed but a bit useful, and the greater ones where just awesome like their whatsapp clone Firetalk!

<blockquote class="twitter-tweet"><p><a href="https://twitter.com/search?q=%23jffos&amp;src=hash">#jffos</a> vamos a hacer un cliente de mensajería :-) <a href="http://t.co/6QZvor1ow5">pic.twitter.com/6QZvor1ow5</a></p>&mdash; movilforum (@movilf) <a href="https://twitter.com/movilf/statuses/335421031898570752">May 17, 2013</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

Then the jury went out of the room and I started to pack my things because I was very hungry and still had a 1 hour ride back home. But I was awared with the prize to the best app in the e-Health  category, didn't truly believe it and even felt like it wasn't quite deserved, but talking before with the jury they told me that being alone and able to deliver a functional and useful app was the key for me to win.

<blockquote class="twitter-tweet center"><p>pues tras la deliberación del jurado tenemos a los ganadores <a href="https://twitter.com/search?q=%23jffos&amp;src=hash">#jffos</a> <a href="http://t.co/D2IRJHldo2">pic.twitter.com/D2IRJHldo2</a></p>&mdash; movilforum (@movilf) <a href="https://twitter.com/movilf/statuses/335426034054856705">May 17, 2013</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

So thats the story of how I got my GeeksPhone Peak all alone in a hackathon 285km far from home ;)



