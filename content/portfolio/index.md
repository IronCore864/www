---
title: Portfolio
permalink: /portfolio/
---

Projects in the past five years:

### [Tesco Bank](https://www.tescobank.com/), DevOps Consulting, 2021

A 6-day workshop, during which we discussed in-depth each stage of the Software Development Lifecycle (SDLC) of Tesco Bank (a Scottish/British retail bank), and generated a detailed report with possible improvements.

---

### [Credit Suisse](https://www.credit-suisse.com/), Cloud Migration and High-Availability Improvement, 2021

Headquartered in Switzerland, active in over 50 countries, Credit Suisse is one of the most renouned private banks in the world.

- hundreds of bare-metal servers migration to AWS
- multi-AZ, highly available networking architecting and implementation
- automated failover with the possibility to switch availability zones at a push of a button
- automated data ([HBase, EMR](https://aws.amazon.com/cn/emr/features/hbase/)) backup across availability zones

Main tech stack: AWS, EC2 Bare Metal Instances, EC2 Nitro, Placement Group, ELB, HBase, S3, Ansible, Jenkins.

---

### [Allianz](https://www.allianz.com/en.html), Container Runtime Platform 2.0, 2019-2020

The container runtime platform 2.0 (CRP 2.0) is Allianz's global K8s-as-a-Service platform.

- 100% infrastructure as code with [Terraform](https://www.terraform.io/), Python3, Golang, in both AWS and Azure
- 100% automated Jenkins pipelines
- high-availability secrets manager with [Vault](https://www.vaultproject.io/)
- open-source template tool with Go used for CI pipelines
- open-source SAML authentication proxy with Go for internal services
- participated in all architectural decisions and contributed 90% of the code

Main tech stack: AWS, Azure, Terraform, Kubernetes, Vault, Ansible, Python3, Golang, Jenkins.

---

### [Allianz Direct](https://allianzdirect.de/), 2019-2020

Allianz Direct is [Allianz](https://www.allianz.com/en.html)'s (largest insurance company) online car insurance platform.

- AWS + on-premise hybrid cloud, in 4 different countries
- hub-spoke network topology, with 5 different environments, all managed by 100% infrastructure as code with Terraform
- 60+ microservices, fully automated CI pipelines with over 100 deployments managed by Jenkins, ArgoCD with Helm charts
- container runtime security platform with [Prisma Cloud](https://www.paloaltonetworks.com/prisma/cloud)
- high-performance logging with Loki in Grafana
- open-source vault-k8s secrets synchronization tool

Main tech stack: AWS, Azure, On-Premise, Terraform, Vault, OpenShift, Kubernetes, Golang, Jenkins, ArgoCD, Helm, Prometheus/Grafana/Loki.

---

### [SEI Robotics](https://seirobotics.net/), Cloud/K8s Migration, DevOps Consulting, 2019

SEI Robotics is a smart home hardware company and a global leader in developing and manufacturing Android TV and IoT devices.

- multi-cloud (AWS + AliCloud) architecting and high-availability implementation with 100% infrastructure as code
- microservice with MQTT migration to Kubernetes
- internal trainings about DevOps, Kubernetes, Cloud, IaC, etc.

Main tech stack: AWS, AliCloud, Kubernetes, [MQTT](https://mqtt.org/)

---

### Daimler, [EQ Ready](https://www.mercedes-benz.com/en/innovation/eq-ready/), 2018-2019

EQ Ready is a mobile app with a sophisticated AI/ML recommendation engine in the cloud to suggest the most suitable car for any user, based on user behavior, driving style, personal habits, and so on.

- cloud-native, everything in Microsoft Azure, 100% infrastructure as code with Terraform, high availability
- built from the ground up with the [12-factor app](https://12factor.net/) methodology in mind
- microservice architecture, Golang, and Python3, everything running in Kubernetes
- CI/CD pipelines with multiple builds/deploys per day
- everything built from scratch

There was another AI/ML app similar to this, but it wasn't lucky enough to see the world.

Main tech stack: Azure, Terraform, Kubernetes, Golang, Python, Jenkins.

---

### [Daimler](https://www.daimler.com/), Car and Customer Platform, 2018-2019

The Car and Customer Platform (CCP) is Daimler's next-generation, 100% automated datacenter/public cloud project.

- bare-metal as a service (Metal as a Service, [MaaS](https://maas.io/))
- software-defined network with white-box switches with [Cumulus](https://www.nvidia.com/en-sg/networking/ethernet-switching/cumulus-linux/) (a Linux distribution for network switches, [acquired later by Nvidia](https://techcrunch.com/2020/05/04/nvidia-acquires-cumulus-networks/))
- 100 automated configurations for all servers and switches using [Ansible]
- multi-tenancy Kubernetes cluster on bare-metal with 100% automation
- [Ceph](https://ceph.io/) clusters running in K8s as the storage solution
- centralized logging/monitoring with ELK, Prometheus/Grafana
- everything built from scratch

Main techstack: Baremetal, MaaS, Kubernetes, Ansible, Cumulus, Ceph, ELK, Prometheus, Grafana, GoCD.

---

### [Mercedes-AMG](https://www.mercedes-amg.com/), Machine Learning on Baremetal, 2018-2019

Two AI-/ML-powered modules (one for emission, the other for debugging and tuning) running in Kubernetes on Baremetal.

- bare-metal as a service
- automated Kubernetes cluster configuration with Ansible on bare-metal
- machine-learning build/deploy pipelines in K8s

Main tech stack: Baremetal, MaaS, Kubernetes, Ansible, Jenkins

---

### [Lanxess](https://lanxess.com/), [CheMondis](https://chemondis.com/), 2018-2019

CheMondis is the online chemicals marketplace of Lanxess (a specialty chemicals company in Germany, part of [Bayer AG](https://www.bayer.com/en/)).

- cloud-native, everything in Microsoft Azure, 100% infrastructure as code with [Terraform](https://www.terraform.io/), high availability
- built from the ground up with the [12-factor app](https://12factor.net/) methodology in mind
- Python3/Django
- everything built from scratch

Main tech stack: Azure, Terraform, Python3, Django, PostgreSQL, Jenkins

---

### MyJar, 2017-2018

MyJar is an Estonian startup (acquired by the British later) focusing on B2C consumer loans.

- monolith to microservice architecture refactor
- on-premise to AWS migration
- 100% infrastructure as code in AWS
- configuration management with Ansible, with minimum code redundancy and maximum code reusability

Main tech stack: On-Premise, AWS, Terraform, Ansible, Packer, Jenkins

---

### [Kuehne+Nagel](https://home.kuehne-nagel.com/), EDI, 2016-2017

Electronic Data Interchange (EDI) project to connect dozens of critical services for Kuehne+Nagel (the largest global freight forwarding and supply chain management corporation).

- automated configuration management with Ansible (for bare-metal servers and virtual machines)
- test-driven configuration code development with Docker, [Test Kitchen](https://kitchen.ci/), [serverspec](https://serverspec.org/)
- created a monitoring system using [react](https://reactjs.org/)/[Redux](https://redux.js.org/)
- setup CI/CD from scratch with Jenkins and coached three teams in different countries about Agile methodologies

Main tech stack: On-Premise, Ansible, Test Kitchen, Serverspec, Jenkins, Python3, Korn Shell, React, Redux
