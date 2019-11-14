---
layout: post
title: Who Ate Docker's Lunch?
published: true
tags: #docker, #devops, #kubernetes
---

[Mirantis acquired Docker Enterprise](https://techcrunch.com/2019/11/13/mirantis-acquires-docker-enterprise/) which includes the registry, the enterprise accounts and basically everything of value owned by Docker Inc. The company is now left with a shell of its former business. Even though the sale amount is not public, it is widely understood to not be a large sum.

*Docker was once a darling of the tech world. Today we are left wondering -  Who ate their lunch?*

## What did Docker do well?

**1. Remarkable developer UX**

Solomon Hykes & co. took an old not-so-well-known technology "Linux Containers (LXC)" and created a beautiful developer experience around it. 
It was like old wine (LXC) in a new bottle. It allowed developers to leverage the possibility of creating re-usable, re-deployable binaries and it was incredible. Once a container was built, you could run `docker run` on any Unix system and it would just work. This was the promise of Java jars in the past, just on a more generic and wider scale.

**2. Faster REPL cycles**

Creating a layered structure for the Docker container (akin to Git), was another masterstroke. A developer could re-use various pre-built layers in other builds. This reduced build time for incremental builds dramatically. In the developer world faster REPL cycles lead to faster adoption; ALWAYS. And it happened. 

On the downside, this design created bloated Docker images. There were multiple hacks introduced to counter this force. But it remains one of the biggest challenges of the container world.

**3. Run Anything, Anywhere**

For better or for worse, most developer machines are not replicas of their production environment. For example, while I code on a Macbook, our production environment is a cluster of Debian machines. If you work in an enterprise, you might even be required to use Windows as your primary dev environment.

This disparity creates a whole new set of headaches. It's hard to develop & debug for a system that you are not very well versed with.

Allowing developers to run an OS inside another OS was a huge accomplishment.

**4. Rise of "Devops"**

The meaning of the word "Devops" is highly contentious. It means different things to different people. Docker was singularly responsible for getting developers to stop throwing code over the wall to sysadmins who then had to run & maintain the code in production. This led to the creation of a hybrid team where the dev & ops folks could work closely with each other. This could only happen by making ops more approachable to the devs (and vice-versa).

As a dev, if I could run a Docker container on my local machine and be promised that it would behave in the same manner in production, it gives me a lot more confidence in my abilities to troubleshoot production issues.

## Where did Docker go wrong? 

Most developer tool companies (IntelliJ, Terraform, etc) start out with a popular product that keeps them top-of-mind for developers. But it's hard to monetize & build a long-lasting company based on a single product. As a company, you need to build 2nd & 3rd tier products that ride on the popularity of the first one. This suite of products then come together and create a reckoning force. 

Take for instance the successful developer tools company Hashicorp. Their first product that became popular was Terraform, a multi-cloud provisioning system. You could write a simple config file and provision computers across any cloud provider. They capitalized on its popularity and created a suite of products such as Consul, Vault, etc, each with enterprise plans in mind. This allowed enterprise teams to collaborate, cluster & monitor their production systems.

**Docker**, on the other hand, **wasn't able to create a successful 2nd tier product.** If you look at their website, product offerings are limited. Docker Hub was required but not enough to sustain the company. Docker Swarm (which could have been their consolidation) was an inferior technology as compared to Kubernetes - the big daddy of orchestration today. 

While the initial promise of "Build once, run anywhere" is great, 
managing production environments are a whole different beast. Running clusters of machines, security management, network partitions, redundancies at all levels is what keeps sysadmins constantly on their toes. The experience of using Swarm in production is less than ideal. It just doesn't live up to the requirements.

In this sphere, Kubernetes did a much better job (even though their dev UX sucks) at running production workloads with little hassle. 

Observability products such as Prometheus, New Relic, etc capitalized on Docker containers being harder to monitor because they were isolated binaries. Another missed opportunity for Docker Inc. 

Being able to expose monitoring data out-of-the-box could have been a huge win. It could have also ensured that as a developer, I was tied into the ecosystem.

All of these missed opportunities are hard problems to solve. They aren't solved overnight. But Docker had some time to solve this. It was the highly valued darling of the tech world, after all. At its peak, Docker had investors willing to invest in its future and developers dying to work for the company.

Docker Inc did introduce consultancy services for enterprises. But the revenue from it was considered service revenues. And service revenue isn't as highly regarded as product revenue because repeatability & scalability factors aren't high in services. 

Docker was great at building its technology but the fact remains that it always struggled hard with monetization. There is a lot to learn from Docker's pioneering vision as well as from its market struggles.  

I wish to see the technology thrive and I'm optimistic that Mirantis will do justice to Docker Inc. 
