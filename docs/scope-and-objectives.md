---
title: Cluster API Scope and Objectives
authors:
  - "@vincepri"
  - "@ncdc"
  - "@detiber"
reviewers:
  - "@timothysc"
  - "@justinsb"
creation-date: 2019-04-08
last-updated: 2019-04-08
---

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [Cluster API Scope and Objectives](#cluster-api-scope-and-objectives)
  - [Table of Contents](#table-of-contents)
  - [Summary](#summary)
      - [What is Cluster API?](#what-is-cluster-api)
  - [Glossary](#glossary)
  - [Motivation](#motivation)
    - [Goals](#goals)
    - [Non-goals](#non-goals)
  - [Requirements](#requirements)
      - [Foundation](#foundation)
      - [User Experience](#user-experience)
      - [Organization](#organization)
      - [Validation](#validation)
      - [Extension](#extension)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->


# Cluster API Scope and Objectives

This is a living document that is refined over time. It serves as guard rails for what is in and out of scope for Cluster API. As new ideas or designs take shape over time, this document can and should be updated.

## Table of Contents

* [Cluster API Scope and Objectives](#cluster-api-scope-and-objectives)
  * [Table of Contents](#table-of-contents)
  * [Summary](#summary)
    * [What is Cluster API?](#what-is-cluster-api)
  * [Glossary](#glossary)
  * [Motivation](#motivation)
    * [Goals](#goals)
    * [Non-goals](#non-goals)
  * [Requirements](#requirements)
    * [Foundation](#foundation)
    * [User Experience](#user-experience)
    * [Organization](#organization)
    * [Validation](#validation)
    * [Extension](#extension)

## Summary

We are building a set of Kubernetes cluster management APIs to enable common cluster lifecycle operations (create, scale, upgrade, destroy) across infrastructure providers.

#### What is Cluster API?

- An API definition for managing Kubernetes Clusters declaratively.
- A reference implementation for the core logic.
- An API definition for cluster lifecycle management action extension points.

## Glossary

[See ./book/GLOSSARY.md](./book/src/reference/glossary.md)

- __Cluster API__: Unless otherwise specified, this refers to the project as a whole.
- __Infrastructure provider__: Refers to the source of computational resources (e.g. machines, networking, etc.). Examples for cloud include AWS, Azure, Google, etc.; for bare metal include VMware, MAAS, etc. When there is more than one way to obtain resources from the same infrastructure provider (e.g. EC2 vs. EKS) each way is referred to as a variant.
- __Provider implementation__: Existing Cluster API implementations consist of generic and infrastructure provider-specific logic. The infrastructure provider-specific logic is currently maintained in infrastructure provider repositories.
- __Kubernetes-conformant__: A cluster that passes the Kubernetes conformance tests.
- __Scaling__: Unless otherwise specified, this refers to horizontal scaling.
- __Control plane__:
   - __Self-provisioned__: A Kubernetes control plane consisting of pods or machines wholly managed by a single Cluster API deployment.
   - __External__: A control plane offered and controlled by some system other than Cluster API (e.g., GKE, AKS, EKS, IKS).
- __Core Add-ons__: Addons that are required to deploy a Kubernetes-conformant cluster: DNS, kube-proxy, CNI.
- __Additional Add-ons__: Addons that are not required for a Kubernetes-conformant cluster (e.g. metrics/Heapster, Dashboard).
- __Management cluster__: The cluster where one or more Cluster API providers run, and where resources (e.g. Machines) are stored.
- __Workload cluster__: A cluster whose lifecycle is managed by the Management cluster.
- __Operating system__: A generically understood combination of a kernel and system-level userspace interface, such as Linux or Windows, as opposed to a particular distribution.
- __Manage a cluster__: Create, scale, upgrade, destroy.
- __Default implementation__: A feature implementation offered as part of Cluster API project, infrastructure providers can swap it out for a different one.

## Motivation

Kubernetes has a common set of APIs (see the [Kubernetes API Conventions](https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md)) to orchestrate containers regardless of deployment mechanism or cloud provider. Kubernetes also has APIs for handling some infrastructure, like load-balancers, ingress rules, or persistent volumes, but not for creating new machines.
As a result, existing popular deployment mechanisms that manage Kubernetes clusters each have unique APIs and implementations for how to handle lifecycle events like cluster creation or deletion, control plane upgrades, and node upgrades.


<!-- ANCHOR: Goals -->

### Escopo do projeto

- Gerenciar o ciclo de vida (criar, dimensionar, atualizar, destruir) de clusters compatíveis com Kubernetes usando uma API declarativa.
- Trabalhar em diferentes ambientes, tanto on-premises quanto na nuvem.
- Definir operações comuns, fornecer uma implementação padrão e fornecer a capacidade de trocar implementações por outras alternativas.
- Reutilizar e integrar componentes do ecossistema existentes em vez de duplicar sua funcionalidade (por exemplo, detector de problemas de nó, autoscaler de cluster, SIG-Multi-cluster).
- Fornecer um caminho de transição para que os produtos do ciclo de vida do Kubernetes adotem a API de cluster de forma incremental. Especificamente, as ferramentas de gerenciamento do ciclo de vida do cluster existentes devem ser capazes de adotar a API de cluster de maneira escalonada, ao longo de várias versões ou até mesmo adotar um subconjunto da API de cluster.

### Fora do escopo do projeto

- Para adicionar essas APIs ao núcleo do Kubernetes (kubernetes/kubernetes).
   - Essa API deve existir em um namespace fora do core e seguir as práticas recomendadas definidas pelos revisores de api, mas não está sujeita a restrições de api principal.
- Gerenciar o ciclo de vida da infraestrutura não relacionada à execução de clusters compatíveis com Kubernetes.
- Forçar todos os produtos do ciclo de vida do Kubernetes (kOps, Kubespray, GKE, AKS, EKS, IKS etc.) a suportar ou usar essas APIs.
- Para gerenciar clusters não provisionados em conformidade com Kubernetes provisionados pela API de cluster.
- Gerenciar um único cluster abrangendo vários provedores de infraestrutura.
- Para configurar uma máquina a qualquer momento que não seja criar ou atualizar.
- Para duplicar a funcionalidade que existe ou está chegando a outras ferramentas, por exemplo, atualizando a configuração do kubelet (c.f. configuração dinâmica do kubelet), ou atualizando apiserver, controller-manager, configuração do agendador (c.f. component-config effort) após a implantação do cluster.

<!-- ANCHOR_END: Goals -->

## Requirements

#### Foundation

- Cluster API MUST be able to be deployed and run on Kubernetes.

- Cluster API MUST provide runtime and state isolation between providers within the same Management Cluster

- Cluster API MUST support multiple infrastructure providers, including both on-prem and cloud providers.

- Cluster API MUST be able to manage groups/sets of Kubernetes nodes that support scaling and orchestrated upgrades.

- Cluster API, through a single installation, MUST be able to manage (create, scale, upgrade, destroy) clusters on multiple providers.

- Cluster API SHOULD support all operating systems in scope for Kubernetes conformance.

#### User Experience

- Cluster API MUST be able to provide the versions of Kubernetes and related components of a Node that it manages.

- Cluster API MUST be able to provide sufficient information for a consumer to directly use the API server of the provisioned workload cluster.

#### Organization

- Cluster API MUST NOT have code specific to a particular provider within the main repository, defined as sigs.k8s.io/cluster-api.

#### Validation

- Cluster API MUST enable infrastructure providers to validate configuration data.

- Cluster API MUST test integrations that it claims will work.

- Cluster API MUST deploy clusters that pass Kubernetes conformance tests.

- Cluster API MUST document how to bootstrap itself and MAY provide tooling to do so.

- Cluster API MUST document requirements for machine images and SHOULD reference default tools to prepare machine images.

- Cluster API MUST have conformance tests to ensure that Cluster API and a given provider fulfill the expectations of users/automation.

#### Extension

- Cluster API SHOULD allow default implementations to be pluggable/extensible.
   - Cluster API SHOULD offer default implementations for generic operations.
   - Users MAY use different provider implementations for different sets of operations.

- 🔌 Cluster API MUST be able to provide information as to which versions of Kubernetes it can install.

- 🔌 Cluster API MUST be able to bootstrap a new Kubernetes control plane.

- 🔌 Cluster API MUST provide a generic image lookup mechanism that can filter on characteristics such as kubernetes version, container runtime, kernel version, etc.

- 🔌 Cluster API MUST be able to provide a consistent (across providers) way to prepare, configure, and join nodes to a cluster.

- 🔌 Cluster API MUST be able to scale a self-provisioned control plane up from and down to one replica.

- 🔌 Cluster API MUST provide high-level orchestration for Kubernetes upgrades (control plane and non-control plane).

- 🔌 Cluster API MUST define and document configuration elements that it exclusively manages and take corrective actions if these elements are modified by external actors.

- 🔌 Cluster API MUST provide the ability to receive the health status of a Kubernetes Node from an external source.

- 🔌 Cluster API provider implementations SHOULD allow customization of machine, node, or operating system image.
