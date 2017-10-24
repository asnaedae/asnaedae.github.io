---
layout: single
tags:
  - networking
redirect_from:
  - /2008/09/26/interesting-posts-from-nanog/
  - /interesting-posts-from-nanog/
---

Following reply by iljitsch van Beijnum about queueing delays in IP, looked to be a good little summary.

> The answer is that delay is only one aspect of performance, another important one is packet loss. As link bandwidth increases, queuing delays decrease proportionally. So if you’re using your 10 Mbps link with average 500 byte packets at 98% capacity, you’ll generally have a 49-packet queue. (queue = utilization / (1 - utilization)) Our 500 byte packets are transmitted at 0.4 ms intervals, so that makes for a 19.6 ms queuing delay.
> So now we increase our link speed to 100 Mbps, but for some strange reason this link is also used at 98%. So the average queue size is still 49 packets, but it now only takes 0.04 ms to transmit one packet, so the queuing delay is only 1.96 ms on average.
> As you can see, as bandwidth increases, queuing delays become irrelevant. To achieve even 1 ms queuing delay (that’s only 120 miles extra fiber) at 10 Gbps you need an average queue size of 833 even with 1500-byte packets. For this, you need a link utilization of almost 99.9%.
> However, due to IP’s bursty nature the queue size is quite variable. If there is enough buffer space to accommodate whatever queue size that may be required due to bursts, this means you get a lot of jitter. (And, at 10 Gbps, expensive routers, because this memory needs to be FAST.) On the other hand, if the buffer space fills up but packets keep coming in faster than they can be transmitted, packets will have to be dropped. As explained by others, this leads to undesired behavior such as TCP congestion synchronization when packets from different sessions are dropped and poor TCP performance when several packets from the same session are dropped. So it’s important to avoid these “tail drops”, hence the need for creative queuing techniques.
> However, at high speeds you really don’t want to think about this too much. In most cases, your best bet is RED (random early detect/drop) which gradually drops more and more packets as the queue fills up (important: you need to have enough buffer space or you still get excessive tail drops!) so TCP sessions are throttled back gradually rather than traumatically. Also, the most aggressive TCP sessions are the most likely to see dropped packets. With weighted RED some traffic gets a free pass up to a point, so that’s nice if you need QoS “guarantees”. (W)RED is great because it’s not computationally expensive and only needs some enqueuing logic but no dequeuing logic.
