---
# config for slides
theme: dracula
title: Building a Scalable Cloud Native Training Platform with Kubernetes
transition: slide-left
author: Zander Havgaard
fonts:
  sans: "Ubuntu Nerd Font"
  serif: "Ubuntu Nerd Font"
  mono: "Hack Nerd Font"
themeConfig:
  primary: "#fff"

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

Email: contact@pzh.dk

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

eficode does trainings

trainings need infra

we had an infra, we outgrew it

enter new infra

---

the new infra

what were the ideas behind the design of the new infra?

why was the design how it ended up?

why cloud native ?

why k8s?

---

architecture drawing

---

workstation architecture drawing

---

demo: workstation, kubectl, docker

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

Thank you!
