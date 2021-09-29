---
layout: blog
title: "Harvest the power of FPGAs with MicroK8s"
date: 2021-09-29T12:37:04+01:00
slug: microk8s-inaccel
draft: false
---

![MicroK8s-InAccel](/images/blog/microk8s-inaccel/microk8s-inaccel.png)

[FPGAs](https://en.wikipedia.org/wiki/Field-programmable_gate_array) have always been in my TODO list. It is always exciting to think that the code you are working on could be accelerated by running it in hardware. How naive…

The truth is that running code on FPGAs is an art of its own. There is a fair amount of complexity. You need to invest time and effort to get all the tools aligned correctly and harvest the power of Field Programmable Gate Arrays. 

Thankfully the great people over at [InAccel](https://inaccel.com/) are here to help us. With their well considered, streamlined tool set they lift much of the burden involved in integrating, storing and delivering hardware accelerated code.

Naturally, InAccel and [MicroK8s](https://microk8s.io/) make a great pair! We would like to welcome them to the MicroK8s ecosystem. Here is how to get a glimpse of how easy we made things for you:

```
sudo snap install microk8s --classic --channel=latest/edge
sudo microk8s status --wait-ready
sudo microk8s enable inaccel
```

The inaccel add-on is currently available in the latest/edge channel and will be included MicroK8s next stable release, v1.23.  Read more in [our docs](https://microk8s.io/docs/addon-inaccel).

*Have fun!*


---
Konstaninos Tsakalozos

Staff engineer at Canonical Ltd

# Links

* [FPGAs](https://en.wikipedia.org/wiki/Field-programmable_gate_array)
* [MicroK8s](https://microk8s.io/)
* [MicroK8s repo](https://github.com/ubuntu/microk8s)
