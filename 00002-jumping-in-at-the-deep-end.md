---
title: Jumping in at the deep end
tags: general-advice
domain: icepuma.blog
publishAs: icepuma
ignorePost: true
---

Aloha!

I want to take you on a journey of how I approach uncharted knowledge territory.
My new freelance project requires me to have in-depth knowledge of OpenShift, so that's where our journey begins.

I know a thing or two about Kubernetes (k8s) and the CNCF ecosystem, thanks to the lovely people over at [Rawkode Academy](https://rawkode.chat).
OpenShift is another story because it adds a lot of management foo around k8s:

* A management UI
* A CLI wrapper around `kubectl` (`oc`) to instrument OpenShift-specific resources
* OpenShift-specific CRDs
* RedHat Certified Operators

Reading the OpenShift documentation for the first time was overwhelming.
Luckily I was not alone on the journey. Our company planned a team of 4 for the new project.

The challenge was to acquire as much information as possible in 2 weeks.
The big elephant in the room -> Where to start?

* Reading the documentation?
* Watch some YouTube videos?
* Ask some people familiar with OpenShift?
* Book a course?

We decided to jump in at the deep end and bootstrap an OpenShift cluster from scratch.
Reading more and more about the matter, we discovered that there's a community distribution of OpenShift, which doesn't require any license and is open source.
The project [hcloud-okd4](https://github.com/slauger/hcloud-okd4) helped us big time in setting up the whole shebang:

* VMs were ordered via [Hetzner Cloud](https://www.hetzner.com/cloud)
* three master nodes and two worker nodes

We observed the logs, read through the Terraform / Ansible scripts, and inspected the outputs of the Hetzner Cloud VMs to understand what was happening.
The script conglomerate spits out the login credentials after being finished.

Yaaay! We have a login :)

What would be the next steps? Upgrades!
Not knowing that we had installed an old version, the UI prompted that a new version of OKD was available.
We clicked the `upgrade` button, targeted the new version, and could see how an upgrade works.

To be able to log in, OpenShift wants you to configure an OAuth identity provider.
We chose GitHub, configured everything, disabled the `kube-admin` account, and were ready to install stuff into our cluster.

Having self-signed certificates was not cool, so we decided to set up `cert-manager` and replace the Console and API server certificate with a `Let's Encrypt` cert.

Huzzah! Taking the `jumping in at the deep end` - approach felt great.

Following the documentation of OpenShift, we installed/tried out several things:

* `Red Hat OpenShift GitOps` - ArgoCD the OpenShift way
* `Red Hat OpenShift Service Mesh` - Istio-based service mesh
* `Red Hat OpenShift distributed tracing platform` - Jaeger tracing
* `Loki Operator` - Loki-based logging for the cluster

I only outlined the happy path. We stumbled upon all sorts of problems, which we had to google or try out several things until we solved them.

What did we learn?

* Group learning is more efficient
  * You can try out more things in parallel
  * Everyone understands a different piece of the puzzle and can help the others with questions
  * When one person is unmotivated, the group can compensate
* The `jumping in at the deep end` - approach is painful but has the best outcome in terms of knowledge acquiring
  * You see all the bits and bobs of a given topic
  * You usually have less `magic` that happens because you have to answer more questions on `How does this piece work?` / `Why did this statement fail?`, ...

Thanks for reading along. Cheers!
