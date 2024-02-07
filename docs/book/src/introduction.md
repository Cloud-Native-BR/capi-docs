# Kubernetes Cluster API<div style="float: right; position: relative; display: inline;"><img src="images/introduction.svg" width="160px" /></div>


O Cluster API é um subprojeto do Kubernetes focado em fornecer APIs declarativas e ferramentas para simplificar o provisionamento, atualização e operação de vários clusters Kubernetes.

Iniciado pelo Grupo de Interesse Especial do Kubernetes (SIG) [Cluster Lifecycle](https://github.com/kubernetes/community/tree/master/sig-cluster-lifecycle#readme), o projeto Cluster API usa APIs no estilo Kubernetes e padrões para automatizar o gerenciamento do ciclo de vida do cluster para operadores de plataforma. A infraestrutura de suporte, como máquinas virtuais, redes, balanceadores de carga e VPCs, bem como a configuração do cluster Kubernetes, são todas definidas da mesma forma que os desenvolvedores de aplicações trabalham, implantando e gerenciando suas cargas de trabalho. Isso permite implantações de cluster consistentes e repetíveis em uma ampla variedade de ambientes de infraestrutura.

## ⚠️ Breaking Changes ⚠️

<aside class="note">
<h1>O registry de imagens legado k8s.gcr.io vai ser redirecionado para registry.k8s.io</h1>

O registry de imagens k8s.gcr.io vai ser redirecionado para registry.k8s.io no dia 20 de Março.
Todas as imagens disponíveis em k8s.gcr.io estão disponíveis no registry.k8s.io.
Por favor, leia o [anúncio](https://kubernetes.io/blog/2023/03/10/image-registry-redirect/) completo para mais detalhes.

Além disso, esse [guia](https://github.com/kubernetes/registry.k8s.io/tree/main/docs/mirroring) contém mais instruções sobre como identificar imagens para espelhar (**mirror**) e como usar imagens espelhadas.
</aside>

<aside class="note">
<h1>Remoção da API obsoleta</h1>

- A versão v1alpha3 da API não é mais suportada na release v1.5
- O suporte para a versão v1alpha4 será removido na próxima versão 1.6

Revise a seção de [suporte](./CONTRIBUTING.md#support-and-guarantees) no guia de contribuição para mais detalhes.

</aside>

## Começando

* [Início Rápido](./user/quick-start.md)
* [Conceitos](./user/concepts.md)
* [Guia de desenvolvimento](./developer/guide.md)
* [Contribuindo](./CONTRIBUTING.md)
* [Vídeos explicando a arquitetura do Cluster API](./developer/guide.md#videos-explaining-capi-architecture-and-code-walkthroughs)

<aside class="note">

<h1>Versões das documentações do Cluster API</h1>

Este livro documenta a versão 1.6. do Cluster API. Para outras versões veja as documentações relacionadas:
* [main.cluster-api.sigs.k8s.io](https://main.cluster-api.sigs.k8s.io)
* [release-1-5.cluster-api.sigs.k8s.io](https://release-1-5.cluster-api.sigs.k8s.io)
* [release-1-4.cluster-api.sigs.k8s.io](https://release-1-4.cluster-api.sigs.k8s.io)
* [release-1-3.cluster-api.sigs.k8s.io](https://release-1-3.cluster-api.sigs.k8s.io)
* [release-1-2.cluster-api.sigs.k8s.io](https://release-1-2.cluster-api.sigs.k8s.io)
* [release-1-1.cluster-api.sigs.k8s.io](https://release-1-1.cluster-api.sigs.k8s.io)
* [release-1-0.cluster-api.sigs.k8s.io](https://release-1-0.cluster-api.sigs.k8s.io)
* [release-0-4.cluster-api.sigs.k8s.io](https://release-0-4.cluster-api.sigs.k8s.io)
* [release-0-3.cluster-api.sigs.k8s.io](https://release-0-3.cluster-api.sigs.k8s.io)

</aside>

## Why build Cluster API?

Kubernetes is a complex system that relies on several components being configured correctly to have a working cluster. Recognizing this as a potential stumbling block for users, the community focused on simplifying the bootstrapping process. Today, over [100 Kubernetes distributions and installers](https://www.cncf.io/certification/software-conformance/) have been created, each with different default configurations for clusters and supported infrastructure providers. SIG Cluster Lifecycle saw a need for a single tool to address a set of common overlapping installation concerns and started kubeadm.

[Kubeadm](https://kubernetes.io/docs/reference/setup-tools/kubeadm/kubeadm/) was designed as a focused tool for bootstrapping a best-practices Kubernetes cluster. The core tenet behind the kubeadm project was to create a tool that other installers can leverage and ultimately alleviate the amount of configuration that an individual installer needed to maintain. Since it began, kubeadm has become the underlying bootstrapping tool for several other applications, including Kubespray, minikube, kind, etc.

However, while kubeadm and other bootstrap providers reduce installation complexity, they don't address how to manage a cluster day-to-day or a Kubernetes environment long term. You are still faced with several questions when setting up a production environment, including:

* How can I consistently provision machines, load balancers, VPC, etc., across multiple infrastructure providers and locations?
* How can I automate cluster lifecycle management, including things like upgrades and cluster deletion?
* How can I scale these processes to manage any number of clusters?

SIG Cluster Lifecycle began the Cluster API project as a way to address these gaps by building declarative, Kubernetes-style APIs, that automate cluster creation, configuration, and management. Using this model, Cluster API can also be extended to support any infrastructure provider (AWS, Azure, vSphere, etc.) or bootstrap provider (kubeadm is default) you need. See the growing list of [available providers](./reference/providers.md).

{{#include ../../scope-and-objectives.md:Goals}}

{{#include ../../../README.md:Community}}
