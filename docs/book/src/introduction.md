# Kubernetes Cluster API<div style="float: right; position: relative; display: inline;"><img src="images/introduction.svg" width="160px" /></div>

O Cluster API é um subprojeto do Kubernetes focado em fornecer APIs declarativas e ferramentas para simplificar o provisionamento, atualização e operação de vários clusters Kubernetes.

Iniciado pelo Grupo de Interesse Especial do Kubernetes (SIG) [Cluster Lifecycle](https://github.com/kubernetes/community/tree/master/sig-cluster-lifecycle#readme), o projeto Cluster API usa APIs e padrões no estilo do Kubernetes para automatizar o gerenciamento do ciclo de vida do cluster para operadores de plataforma. A infraestrutura de suporte, como máquinas virtuais, redes, balanceadores de carga e VPCs, bem como a configuração do cluster Kubernetes, são todas definidas da mesma forma que os desenvolvedores de aplicações trabalham, implantando e gerenciando suas cargas de trabalho. Isso permite implantações de cluster consistentes e repetíveis em uma ampla variedade de ambientes de infraestrutura.

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

## Por que construir o Cluster API?


O Kubernetes é um sistema complexo que depende de vários componentes sendo configurados corretamente para ter um cluster funcionando. Reconhecendo isso como um potencial obstáculo para os usuários, a comunidade se concentrou em simplificar o processo de bootstrapping. Hoje, mais de [100 distribuições e instaladores para o Kubernetes](https://www.cncf.io/certification/software-conformance/) foram criados, cada um com diferentes configurações padrão para clusters e provedores de infraestrutura suportados. O SIG Cluster Lifecycle viu a necessidade de uma única ferramenta para resolver um conjunto de preocupações comuns de instalação sobrepostas e iniciou o kubeadm.

O [Kubeadm] (https://kubernetes.io/docs/reference/setup-tools/kubeadm/kubeadm/) foi projetado como uma ferramenta focada para inicializar um cluster Kubernetes com as melhores práticas. O princípio central por trás do projeto kubeadm era criar uma ferramenta que outros instaladores pudessem aproveitar e, finalmente, aliviar a quantidade de configuração que um instalador individual precisava manter. Desde que começou, o kubeadm tornou-se a ferramenta de bootstrapping subjacente para várias outras aplicações, incluindo Kubespray, minikube, tipo, etc.

No entanto, embora o kubeadm e outros provedores de bootstrap reduzam a complexidade da instalação, eles não abordam como gerenciar um cluster diariamente ou um ambiente Kubernetes a longo prazo. Você ainda se depara com várias perguntas ao configurar um ambiente de produção, incluindo:

* Como posso provisionar consistentemente máquinas, balanceadores de carga, VPC, etc., em vários provedores de infraestrutura e locais?
* Como posso automatizar o gerenciamento do ciclo de vida do cluster, incluindo coisas como atualizações e exclusão de cluster?
* Como posso escalar esses processos para gerenciar qualquer número de clusters?

O SIG Cluster Lifecycle iniciou o projeto Cluster API como uma maneira de resolver essas lacunas criando APIs declarativas, no estilo Kubernetes, que automatizam a criação, a configuração e o gerenciamento de clusters. Usando esse modelo, a API de cluster também pode ser estendida para oferecer suporte a qualquer provedor de infraestrutura (AWS, Azure, vSphere, etc.) ou provedor de bootstrap (kubeadm é padrão) que você precisar. Veja a lista crescente de [provedores disponíveis](./reference/providers.md).

{{#include ../../scope-and-objectives.md:Goals}}

{{#include ../../../README.md:Community}}
