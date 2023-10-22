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

---

eficode does trainings

trainings need infra

we had an infra, we outgrew it

enter new infra

---

the new infra

what were the ideas behind the design of the new infra?
