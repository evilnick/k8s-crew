---
layout: blog
title: "MicroK8s on S390x"
date: 2021-09-16T12:37:04+01:00
slug: microk8s-s390x
draft: false
---

[s390x or IBM Z](https://en.wikipedia.org/wiki/Linux_on_IBM_Z) is one of those exotic (at least to me) architectures brought to us by the genius people over at IBM.

![IBM-Z-Ubuntu](/images/blog/microk8s-s390x/IBM-Z-Ubuntu.png)
* Feast your eye to those gorgeous IBM mainframes you will never get to own in your home lab :) *

IBM Z mainframes are those monster machines that are not for you. Don’t feel bad, they even exceed the needs of small companies. So you might ask “what does MicroK8s have to do with such not-so-micro machines”? Well, MicroK8s is growing production grade features, s390x is one of them. Also, it is dead simple to support a new architecture on a snap! Let’s see how.

### Why s390x was easy to support?

MicroK8s [code lives on github](https://github.com/ubuntu/microk8s) (“like and subscribe” as a youtuber would say) and [is mirrored in launchpad](https://launchpad.net/microk8s). That is where the magic happens! In launchpad you can ask launchpad builders to build your snap and push it to a channel/track. For MikroK8s we have one such builder for each [Kubernetes version from v1.22 all the way to v1.10](https://code.launchpad.net/~kos.tsakalozos/microk8s/+git/microk8s/+snaps). Here is how the 1.22 snap builder is configured so it automatically assembles the MicroK8s snap parts and puts them in the 1.22/edge channel:

![builder-1.22](/images/blog/microk8s-s390x/1.22-builder.png)
* The microk8s-1.22 snap builder recipe. *


The most exciting part comes when you click the edit button on this snap builder:

![available-builders](/images/blog/microk8s-s390x/available-builders.png)
* All the architectures just one click away. *


Yes, you got it right. These are all the architectures you can build a snap for; just by ticking a checkbox! Your snap can support the usual, x86–64 and ARM but also IBM’s s390x, and PowerPC. I cannot wait to get my hands on a RISC-V build.

### Weekend project!

Do not waste any more time. Put your software in a snap and sail to the “Great Sea of Opportunity”.

*Enjoy*



### Links

* [MicroK8s repo](https://github.com/ubuntu/microk8s)
* [IBM Z](https://en.wikipedia.org/wiki/Linux_on_IBM_Z)
