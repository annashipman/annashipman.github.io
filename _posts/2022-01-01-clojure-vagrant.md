---
anchor_id: clojure-vagrant
title: Why didn't Clojure work concurrently in Vagrant?
layout: blog_post
---

I recently couldn't work out why Clojure was not working concurrently in a Vagrant box. I'm not sure I solved the problem but I learned many things, and here are some of them.

## I use Vagrant for most things I do

I love [Vagrant](https://www.vagrantup.com/), because I love being able to put things down and pick them up where I left off, without having to recreate environments. I do not have a good memory, and the Vagrantfile is built-in documentation. I create a Vagrantfile for almost every side project I do.

Of course, this means I sometimes (or often...) end up going down a rabbithole that has very little to do with the actual side project itself. However, these are usually most entertaining, and I learn things. Here is one rabbithole and what I learned.

## I could not replicate a concurrency gain

I was working my way through [Seven Concurrency Models in Seven Weeks](https://pragprog.com/titles/pb7con/seven-concurrency-models-in-seven-weeks/) and running some code examples on my Vagrant machine, and I found that a promised speed-up by using a function that supported concurrency did not materialise.

In a [Leiningen](https://leiningen.org/) REPL I ran:

<div class="code-sample">
<p>(ns sum.core<br />
&nbsp;&nbsp;(:require [clojure.core.reducers :as r]))</p>

<p>(defn sum [numbers]<br />
&nbsp;&nbsp;(reduce + numbers))</p>

<p>(defn parallel-sum [numbers]<br />
&nbsp;&nbsp;(r/fold + numbers))</p>

<p>(def numbers (into [] (range 0 10000000)))</p>

<p>(time (sum numbers))</p>

<p>(time (sum numbers))</p>

<p>(time (parallel-sum numbers))</p>

<p>(time (parallel-sum numbers))</p>
</div>

(To quote the book, we run each of the timing functions twice "to give the just-in-time optimizer a chance to kick in and get a representative time".)

[`reduce`](https://clojuredocs.org/clojure.core/reduce) is not parallel, but [`fold`](https://clojuredocs.org/clojure.core.reducers/fold) can be, and according to the author, on his four-core Mac, the `fold` function gave around a 2.5x speed-up.

However, on my Vagrant box, the two functions ran in approximately the same length of time.

## I eventually asked for help on Twitter

After quite a bit of investigation myself, including [correcting some foolish errors](https://github.com/annashipman/7weeks-concurrency/commit/360bedc), I was not able to work out why this wasn't working. Vagrant could see all four of the cores (`(.availableProcessors (Runtime/getRuntime))` showed it could see 4) but the allegedly parallel code was no faster.

I figured this must be something to do with Vagrant, and I was committed to getting it all working on my Vagrant machine, if I could.

<blockquote class="twitter-tweet" data-dnt="true"><p lang="en" dir="ltr">Do I know anyone who knows Vagrant and Clojure and can help me debug a (minor) concurrency issue?</p>&mdash; Anna Shipman (@annashipman) <a href="https://twitter.com/annashipman/status/1439527358701113346?ref_src=twsrc%5Etfw">September 19, 2021</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

On [@borkdude](https://twitter.com/borkdude/status/1439529936218435587)'s suggestion I [wrote it up in a gist](https://gist.github.com/annashipman/d3b0533ce26df1e4dd84fbc3001e98dc).

I got some very helpful responses.

## It could be how VirtualBox creates CPUs

<blockquote class="twitter-tweet" data-conversation="none" data-dnt="true"><p lang="en" dir="ltr">I don&#39;t know clojure but based on your info I would guess it might be how VirtualBox creates cpus.<br><br>4 cores on a single cpu share L3 cache but 4 cpus with one core doesn&#39;t. That might make enough difference for clojure.core.reducers to determine it&#39;s not worth doing in parallel</p>&mdash; Pär Björklund (@Paxxi) <a href="https://twitter.com/Paxxi/status/1439650030844063746?ref_src=twsrc%5Etfw">September 19, 2021</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Until I read this tweet, I had not consciously realised that CPUs and cores were different things. Sometimes the two terms are used interchangeably – incorrectly, I now know.

A dual-core machine is not a computer with two CPUs, it's a computer with one CPU that has two cores. A CPU is made up of one or more cores, an input and output management unit, and some other things. The cores are the parts that actually do the work of executing instructions, so multiple cores allow the CPU (in theory at least) to carry out multiple instructions at once.

L3 cache is the biggest CPU cache and is built between the CPU and the RAM. Each core has its own L1 cache. L2 cache may be part of the CPU chip, or between the CPU and the RAM, but L3 cache will usually be shared between cores.

So Pär Björklund's suggestion was that if VirtualBox created the multiple CPUs as CPUs rather than cores, the L3 cache wouldn't be shared, so parallelising would not produce much of an efficiency gain.

The investigation into whether my virtual machine has multiple cores or multiple CPUs involved much unpicking. [Vagrant's docs](https://www.vagrantup.com/docs/providers/virtualbox/configuration) refer to setting CPUs. It links to the [VirtualBox manual](https://www.virtualbox.org/manual/ch08.html) which refers also to CPUs ("`--cpus <cpucount>`: Sets the number of virtual CPUs for the virtual machine") but refers you on to [another part of the manual](https://www.virtualbox.org/manual/ch03.html#settings-processor) which reveals that it's actually CPU *cores*: "Sets the number of virtual CPU cores the guest OSes can see."

From this, I learned that [I should not have set my guest VM to have 4 CPUs on my dual-core host](https://github.com/annashipman/7weeks-concurrency/commit/2e81a52).

Not unexpectedly, making that change did not affect the speed of the second function. I did establish that it looks like VirtualBox is creating multiple cores rather than multiple CPUs, so in theory they may be sharing L3 cache, though I can't say definitively they are. In any case, it doesn't seem that I have any control over it.

So. Digging into this suggestion led me to some very interesting learnings about the structure of computers, and might actually be the root of the problem, but even if it is, it's not clear if I can solve it if so, so I moved on to other suggestions.

## It could be that there are not enough threads

[Dak](https://twitter.com/d_a_keldsen) asked what I had set the virtual CPUs and CPU cap to:

<blockquote class="twitter-tweet" data-dnt="true"><p lang="en" dir="ltr">I’m thinking that the default of 50% may be restricting the creation of additional threads. Also, try adding something that causes a kernel call to force another thread to run.</p>&mdash; Dak (David A. Keldsen) (@d_a_keldsen) <a href="https://twitter.com/d_a_keldsen/status/1439963498734395399?ref_src=twsrc%5Etfw">September 20, 2021</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

explain what cpu cap is

suggestion is that there's not enough CPU being allowed for the guest to create new threads

Try it with a higher cpu blah

But also realised afterwards, we know that's not the case here as some fo the other threading works, specifically, the Java does, and Clojure runs on the JVM, so... 

The making a kernal call is also interesting

The idea here is calling an interrupt to test whether control can pass from thread to trhread; calling an interrupt tests this because interrupts can be higher priority (e.g. kernel interrupt would be higher priority than my clojure function), so if you call a lkerenal inerrupt and it's not sucesful (what do es success look like>>!) then we know threading is not working as expected in my VM.

However, in this case it's not clear how I could add an interrupt, as clojure is doing all the threading under the hood. in java, would call thread.interrupt form outside the thread but not sure how to do this here.

in any case, we konw threading is working, so again, learned things but didn't haelp.

Some useful links:

https://www.virtualbox.org/manual/ch08.html 

https://lwn.net/Articles/65178/ to start - digging in here will help me understand threads/the kernal etc better.

## It could be to do with the JVM Garbage Collection

<blockquote class="twitter-tweet" data-dnt="true"><p lang="en" dir="ltr">LEIN_JVM_OPTS=&quot;-verbose:gc -XX:+UnlockExperimentalVMOptions -XX:G1NewSizePercent=50 -XX:+UseG1GC -Xms3g -Xmx3g&quot; lein repl</p>&mdash; Philip Wigg (@philipwigg) <a href="https://twitter.com/philipwigg/status/1439693698539864067?ref_src=twsrc%5Etfw">September 19, 2021</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

[Philip Wigg](https://twitter.com/philipwigg) had the answer that had the most impact.

To unpick this:

- LEIN_JVM_OPTS is [setting options for the leiningen JVM](https://github.com/technomancy/leiningen/blob/master/doc/TUTORIAL.md#setting-jvm-options)
- verbose:gc
- -XX:+UnlockExperimentalVMOptions
-XX:G1NewSizePercent=50
-XX:+UseG1GC
-Xms3g -Xmx3g

Next step here, look up “GC (Allocation Failure)” out of interest
https://technospace.medium.com/gc-allocation-failures-42c68e8e5e04

 and see if I can get a definitive answer that this is what it is.

Can set the lein opts https://stackoverflow.com/questions/32323572/is-there-a-way-to-set-system-properties-in-leinegen <-not quite it but might get me there 

Useful links:
https://docs.oracle.com/en/java/javase/17/gctuning/garbage-first-g1-garbage-collector1.html#GUID-0394E76A-1A8F-425E-A0D0-B48A3DC82B42
https://docs.oracle.com/javase/8/docs/technotes/guides/vm/gctuning/g1_gc_tuning.html
https://docs.oracle.com/javase/8/docs/technotes/guides/vm/gctuning/g1_gc.html#garbage_first_garbage_collection

heap size stuff https://www.spigotmc.org/threads/how-can-i-add-more-ram-to-a-server-im-going-to-create.457818/?__cf_chl_jschl_tk__=pmd_KGBYGizSow5oZV4Sv4oWSiA4mGuAezMcjkFUwVhLLeQ-1632155339-0-gqNtZGzNAiWjcnBszQhR


using verbose alone seems to make it faster, Steve suggests this is because GC happens less when in verbose mode. Check this out.

It also seems that it needs to be reloaded each time I start the repl to get the results, maybe even destroyed, so bear that in mind if testing.


## to note

didn't test locally myself but a few other people did, as part o fthe reasdon using vagrant is don't want to install all this stuff on my machine

wondered whether it might bre lein repl needed to do concucrrecny epxlicity but others said it worked

could it be the version?

## conclusion title

Not sure I actually solved this problem,  but learned some interesting things! do share if you have other ideas here.

I made/didn't make these changes to the VM so now at least that one will run, but have not gone back through the rest of the code samples

I learned a lot that I didn't know, not all of it about concurrency, but about how computers work, always a fascinating topic.

And something something summmary.


## notes


Maybe some reasding, if relevant.


https://purelyfunctional.tv/guide/clojure-concurrency/

https://clojure.org/about/concurrent_programming

https://functional.works-hub.com/learn/concurrency-models-and-clojure-237db

