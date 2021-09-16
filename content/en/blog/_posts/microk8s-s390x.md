---
layout: blog
title: "MicroK8s on S390x"
date: 2021-09-16T12:37:04+01:00
slug: microk8s-s390x
draft: false
---

# MicroK8s on S390x!

[s390x or IBM Z](https://en.wikipedia.org/wiki/Linux_on_IBM_Z) is one of those exotic (at least to me) architectures brought to us by the genius people over at IBM.

![Feast your eye to those gorgeous IBM mainframes you will never get to own in your home lab :)]("\images\blog\microk8s-s390x\IBM-Z-Ubuntu.png")

IBM Z mainframes are those monster machines that are not for you. Don’t feel bad, they even exceed the needs of small companies. So you might ask “what does MicroK8s have to do with such not-so-micro machines”? Well, MicroK8s is growing production grade features, s390x is one of them. Also, it is dead simple to support a new architecture on a snap! Let’s see how.

### Why s390x was easy to support?

MicroK8s code lives on github (“like and subscribe” as a normal youtuber would say) and is mirrored in launchpad. That is where the magic happens! In launchpad you can ask launchpad builders to build your snap and push it to a channel/track. For MikroK8s we have one such builder for each Kubernetes version from v1.22 all the way to v1.10. Here is how the 1.22 snap builder is configured so it automatically assembles the MicroK8s snap parts and puts them in the 1.22/edge channel:

The most exciting part comes when you click the edit button on this snap builder:

Yes, you got it right. These are all the architectures you can build a snap for; just by ticking a checkbox! Your snap can support the usual, x86–64 and ARM but also IBM’s s390x, and PowerPC. I cannot wait to get my hands on a RISC-V build.

### Weekend project!

Do not waste any more time. Put your software in a snap and sail to the “Great Sea of Opportunity”.

*Enjoy*

### Links



This means that a worker node can be used to run Windows workloads, while the control plane runs
  on Linux - a hybrid cluster. Production-level support for running a Windows node was introduced
  with [version 1.14 of Kubernetes back in March 2019](https://kubernetes.io/blog/2019/03/25/kubernetes-1-14-release-announcement/), so in terms of deployment of Windows containers, operators can expect exactly the same features for Windows workloads as they do for Linux ones.

The Kubernetes components that are required for a worker node are:

* kubelet: this is the Kubernetes agent which manages and reports on the running containers in a pod.

* kube-proxy: a network proxy component which maintains the network rules and allows pods to
  communicate within or externally to the rest of the cluster

* a container runtime: the executable responsible for running individual containers. Actually, several
  different container runtimes are now supported by Kubernetes - Docker, CRI-O, containerd (and through
  that, many others such as the Windows-specific runhcs), as well as any other which support the
  Kubernetes [container runtime interface (CRI) ](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-node/container-runtime-interface.md)

![image alt text](image_0.png)

Kubernetes cluster components (image CC BY 4.0 The Kubernetes Authors).

It is of course possible to manually install these components on a Windows machine and construct a node,
then integrate it into an existing cluster. There are easier ways to achieve this though.

### MicroK8s and Calico

For the Linux-based part of a hybrid Kubernetes cluster, MicroK8s is a compelling choice.
MicroK8s is a minimal implementation of Kubernetes which can run on the average laptop, yet has production
grade features. It's great for offline development, prototyping and testing, and if required you can also
get professional support for it through [Ubuntu Advantage](https://ubuntu.com/support).

The most compelling feature of MicroK8s for this use case is that you can run it sort-of-almost-natively
on Windows 10! For development work and even production use-cases, this is hugely useful - your hybrid
cluster can reside on one physical Windows machine. MicroK8s on Windows works by making use of
[Multipass](https://multipass.run/) - a neat way of running a virtual Ubuntu machine on Windows.
The MicroK8s installer for Windows doesn't require any knowledge of multi-pass or even virtual machines
though, it sets everything up with just a few options from the installer. 

To fetch the current installer and see the (simple!) install instructions for MicroK8s on Windows, check out the [MicroK8s website](https://microk8s.io/).

Whether using MicroK8 on Windows or a separate Linux machine, the next thing to consider is networking. Calico has been the default CNI(Container Network Interface) for MicroK8s since the 1.19 release. The CNI handles a number of networking requirements:

*  Container-to-container communications

*  Pod-to-Pod communications

*  Pod-to-Service communications

*  External-to-Service communications

The popularity of Calico has been building for some time over simpler CNIs, as it supports
more useful features (e.g. Border Gateway Protocol [#ref]) and is also available in a
[supported enterprise version](https://www.tigera.io/tigera-products/calico-enterprise/).

Usefully, Calico already bundles the Windows executables for this CNI in an installer script that also fetches the other components required for a Windows node, making installation and setup that much easier.  The Calico website has [complete instructions for this](https://docs.projectcalico.org/getting-started/windows-calico/quickstart). This contains not only links to the installer script but also a detailed rationale on how the setup works. If you are just interested in getting started with adding a Windows worker with MicroK8s there are more concise and specific instructions in the [MicroK8s documentation](https://microk8s.io/docs/add-a-windows-worker-node-to-microk8s).

### Scheduling Windows containers on hybrid Kubernetes

The final step of this journey is to actually deploy some Windows containers. With a
hybrid cluster, you could potentially be running Windows or Linux based containers and
Kubernetes will need some way of knowing which nodes to deploy them on.  

A pod specification for a Windows workload should contain a nodeselector field
identifying that it is to run on Windows. The recommended additional workflow is to use
the 'taints and tolerations' features of Kubernetes, to explicitly refuse deployments
on the Windows nodes to any pod which hasn't specifically requested them. There is a
full explanation of this workflow in the upstream
[Kubernetes documentation](https://kubernetes.io/docs/setup/production-environment/windows/user-guide-windows-containers/#taints-and-tolerations).

More from MicroK8s

There is plenty more you can do with a MicroK8s cluster - be sure to check out the
documentation for [MicroK8s add-ons](https://microk8s.io/docs/addons) so you can
enable the dashboard, ingress controllers, Kubeflow and more. 
