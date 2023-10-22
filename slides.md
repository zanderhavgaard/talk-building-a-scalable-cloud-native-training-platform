---
# config for slides
theme: dracula
transition: slide-left
fonts:
  sans: "Ubuntu"
  serif: "Ubuntu"
  mono: "Hack"
title: Building a Scalable Cloud Native Training Platform with Kubernetes
author: Zander Havgaard

# layout for first slide
layout: intro
---

# Building a Scalable Cloud Native Training Platform with Kubernetes

TDOC 2023 - Zander Havgaard

---

# $ whoami

## Zander Havgaard

- Senior Software Developer @ **Green.ai** before that **Eficode**
  - This presentations covers the last project I did with Eficode before moving on to new adventures
- Interests: `DevOps`, `Cloud Native`, `Containers`, `Orchestration`, `IaC`, `CI/CD` and more
- I have taught courses in: `Kubernetes`, `Docker`, `Helm`, `Istio`, `Git` and more
- Speaker at meetups

Email: contact@pzh.dk | zanderhavgaard@green.ai

GitHub: `@zanderhavgaard`

---

# Agenda

- The **rationale** behind the design and architecture of our new infrastructure.

- The **open-source technologies** that power our platform, including EKS, eksctl, sysbox, cri-o, task, helm, karpenter, external-dns, lb-controller, cowsay, and more.

- The **rapid MVP development** of our platform in just two weeks, enabled by cloud-native technologies and AI tools.

- How we **tested it in production**: delivering a DevOps summer course at the University of Southern Denmark (SDU) to nearly 100 students.

- A **discussion on the scaling bottleneck** we encountered and the strategies used to overcome it.

#### Format: Slides and live demonstrations of the platform

> Feel free to ask questions after the talk !

> These slides are on github: https://github.com/zanderhavgaard/talk-building-a-scalable-cloud-native-training-platform

<!-- The **rationale** behind the design and architecture of our new infrastructure. -->

---

# The context

Eficode provides a number of trainings to it's customers in topics such as `kubernetes`, `docker`, `git`, `helm` and many more

Each training consists of a trainer presenting the material as well as a number of hands-on exercises, which we call the **katas**

> All of the katas live on Github and are open source! e.g. https://github.com/eficode-academy/kubernetes-katas

Students thus need an environment in which they can do the exercises without having to set up their own machines

---

# The "old" Infrastructure

To solve the problem of provisioning infrastructure for each training session we created an infrastructure that could be deployed with `terraform`

The project would deploy a number of `ec2` instances to `AWS` and an optional `EKS` cluster.
Each `ec2` instance runs `code-server` to provide a workstation.

This was a great solution for a long time. But over time we outgrew the infrastructure:

- It was hard to maintain --> monolithic architecture with many moving parts --> changes / updates were cumbersome and time-consuming
- It was difficult to extend with new courses
- Too few people had the knowledge to work on it --> _low busfactor_

<br>

#### ... So it was time to invest in a new infrastructure

---

# Requirements for the New Infrastructure

> A generic platform for running (cloud native) courses:

- Must work with all existing katas
- The trainer deploying the infrastructure should only have to read a readme to be able to deploy it
- Must deploy successfully every time
- Should be **simple** to maintain
- Everything should be declarative --> avoid running scripts to configure things
- Should be able to run in a pipeline --> for testing and automation

---

# New infrastructure: `k8s-infra`

The infrastructure that I developed to meet these requirements centers around `Kubernetes`

Kubernetes allows us to declare **everything** that we want Kubernetes to control, both _inside_ and _outside_ of the cluster.

-

The idea is to deploy a `Kubernetes cluster` to the `cloud` using the simplest tooling possible.

When we have our cluster, we use the Kubernetes `control-plane` to automate the provisioning and configuration of the infrastructure, in a completely declarative way.

---

# Architecture

TODO

![Diagram of infrastructure architecture](architecture.png)

---

# Workstation components

TODO

![Diagram of components of the workstation](workstation-components.png)

---

# Demo: Workstation, kubectl, docker

![Screenshot of workstation](workstation.png)

---

<!-- - The **open-source technologies** that power our platform, including EKS, eksctl, sysbox, cri-o, task, helm, karpenter, external-dns, lb-controller, cowsay, and more. -->

overview of the tech that powers the platform

EKS, eksctl, sysbox, cri-o, task, helm, karpenter, external-dns, lb-controller, cowsay,

---

tech: provisioning

task, eks, eksctl

---

tech: automation

karpenter, external-dns, aws-lb-controller

---

tech: container runtime to allow docker-in-container

---

tech: workstation helm chart

---

demo: deploying a new workstation with task and running a nginx container in it

---

<!-- - The **rapid MVP development** of our platform in just two weeks, enabled by cloud-native technologies and AI tools. -->

---

I developed the platform in my spare time over roughly two weeks

I was able to do that b/c I used cloud native tech

leveraging desired state centric tooling allows for very rapid development

using automation/controllers to do most of heavy lifting

relying on sane defaults

---

<!-- - How we **tested it in production**: delivering a DevOps summer course at the University of Southern Denmark (SDU) to nearly 100 students. -->

---

the platform was tested in "production" this year at a summer course at SDU

~80 students over two weeks

ran 90 workstations on 9 ec2 machines!

For the most part the experience was seamless and smooth, and the performance was good!

some rare weird issues with docker - probably caused by sysbox

automation to turn off the clusters at night when not in use

was significantly cheaper to run than the old setup

---

<!-- - A **discussion on the scaling bottleneck** we encountered and the strategies used to overcome it. -->

the platform does have a scaling bottleneck - the aws-lb-controller and the number of ingresses that we are creating

we are abusing the ingress functionality / controller for things it was intended for

the ingress controller can handle about 3 lbs with 30 machines sharded across them

the solution at the summer course was to deploy 3 identical clusters

this could potentially be solved by abanonding the need for arbitrary open ports on pods

or by deploying the lb controller in namespaced mode

maybe a service mesh could help?

---

next steps:

argocd-katas being developed to run on top of the platform

---

Thank you!
