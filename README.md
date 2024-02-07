<a href="https://cluster-api.sigs.k8s.io"><img alt="capi" src="./logos/kubernetes-cluster-logos_final-02.svg" width="160x" /></a>
<p>
<a href="https://godoc.org/sigs.k8s.io/cluster-api"><img src="https://godoc.org/sigs.k8s.io/cluster-api?status.svg"></a>
<!-- join kubernetes slack channel for cluster-api -->
<a href="http://slack.k8s.io/">
<img src="https://img.shields.io/badge/join%20slack-%23cluster--api-brightgreen"></a>
<!-- latest stable release badge -->
<img alt="GitHub release (latest SemVer)" src="https://img.shields.io/github/v/release/kubernetes-sigs/cluster-api">
</p>

# Cluster API

### 👋 Welcome to our project! Our [Book](https://cluster-api.sigs.k8s.io) can help you get started and provides lots of in-depth information.

#### Useful links
- [Scope, objectives, goals and requirements](./docs/scope-and-objectives.md)
- [Feature proposals](./docs/proposals)
- [Reference use cases](./docs/staging-use-cases.md)
- [Quick Start](https://cluster-api.sigs.k8s.io/user/quick-start.html)

## ✨ What is the Cluster API?

Cluster API is a Kubernetes subproject focused on providing declarative APIs and tooling to simplify provisioning, upgrading, and operating multiple Kubernetes clusters.

Started by the Kubernetes Special Interest Group (SIG) Cluster Lifecycle, the Cluster API project uses Kubernetes-style APIs and patterns to automate cluster lifecycle management for platform operators. The supporting infrastructure, like virtual machines, networks, load balancers, and VPCs, as well as the Kubernetes cluster configuration are all defined in the same way that application developers operate deploying and managing their workloads. This enables consistent and repeatable cluster deployments across a wide variety of infrastructure environments.

### ⚙️ Providers

Cluster API can be extended to support any infrastructure (AWS, Azure, vSphere, etc.), bootstrap or control plane (kubeadm is built-in) provider. There is a growing list of [supported providers](https://cluster-api.sigs.k8s.io/reference/providers.html) available.

<!-- ANCHOR: Community -->

## 🤗 Comunidade, discussões, contribuição, e suporte

O projeto Cluster API é desenvolvido de forma aberta está constantemente sendo aprimorada por nossos usuários, colaboradores e mantenedores. É por sua causa que podemos automatizar o gerenciamento do ciclo de vida do cluster para a comunidade. Junte-se a nós!

Se você tiver dúvidas ou quiser obter as últimas notícias do projeto, você pode se conectar com a gente das seguintes maneiras:

- Converse com a gente no [slack](http://slack.k8s.io/) do Kubernetes no canal [#cluster-api][#cluster-api slack]
- Inscreva-se no [grupo do google]((https://groups.google.com/forum/#!forum/kubernetes-sig-cluster-lifecycle)) do SIG Cluster Lifecycle para ter acesso a documentos e agendas
- Participe de nossas sessões do grupo de trabalho, onde compartilhamos as últimas notícias do projeto, demonstrações, perguntas e triagem de issues
    - Semanalmente às quartas-feiras @ 10:00 PT em [Zoom][zoomMeeting]
    - Reuniões anteriores: [ [notas][notas] | [gravações] [gravações] ]

Pull Requests e feedback sobre issues são muito bem-vindos!
Consulte o [tracker de issue] se não tiver certeza por onde começar, especialmente as tags [Good first issue] e [Help wanted] e
também sinta-se livre para entrar em contato para discutir.

Consulte também nosso [guia do colaborador](CONTRIBUTING.md) e a [página da comunidade] do Kubernetes para obter mais detalhes sobre como se envolver.

### Código de conduta

A participação na comunidade Kubernetes é regida pelo [Código de Conduta do Kubernetes](code-of-conduct.md).

[community page]: https://kubernetes.io/community
[notes]: https://docs.google.com/document/d/1ushaVqAKYnZ2VN_aa3GyKlS4kEd6bSug13xaXOakAQI
[recordings]: https://www.youtube.com/playlist?list=PL69nYSiGNLP29D0nYgAGWt1ZFqS9Z7lw4
[zoomMeeting]: https://zoom.us/j/861487554
[implementerNotes]: https://docs.google.com/document/d/1IZ2-AZhe4r3CYiJuttyciS7bGZTTx4iMppcA8_Pr3xE/edit
[providerZoomMeetingTues]: https://zoom.us/j/140808484
[providerZoomMeetingWed]: https://zoom.us/j/424743530
[issue tracker]: https://github.com/kubernetes-sigs/cluster-api/issues
[#cluster-api slack]: https://kubernetes.slack.com/archives/C8TSNPY4T
[Good first issue]: https://github.com/kubernetes-sigs/cluster-api/issues?q=is%3Aopen+is%3Aissue+label%3A%22good+first+issue%22
[Help wanted]: https://github.com/kubernetes-sigs/cluster-api/issues?utf8=%E2%9C%93&q=is%3Aopen+is%3Aissue+label%3A%22help+wanted%22+

<!-- ANCHOR_END: Community -->
