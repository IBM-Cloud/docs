---

 

copyright:

  years: 2016

 

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Sobre {{site.data.keyword.openwhisk}}

*Última atualização: 22 de fevereiro de 2016*

As seções a seguir fornecem detalhes sobre o {{site.data.keyword.openwhisk}}.
{: shortdesc}

## Como o {{site.data.keyword.openwhisk_short}} funciona
{: #openwhisk_how}

{{site.data.keyword.openwhisk_short}} é uma plataforma de cálculo acionada por eventos que executa código em resposta a eventos ou chamadas diretas.

A figura a seguir mostra a arquitetura de alto nível do {{site.data.keyword.openwhisk_short}}.

![Arquitetura do {{site.data.keyword.openwhisk_short}}](OpenWhisk.png)

Exemplos de eventos incluem mudanças em registros do banco de dados, leituras do sensor IoT que excedem uma determinada temperatura, novas consolidações de código para um repositório GitHub ou solicitações de HTTP simples de apps da web ou móveis. Os eventos de origens de eventos externos e internos são canalizados por meio de um acionador e as regras permitem que as ações reajam a esses eventos.

As ações podem ser pequenos trechos de código Javascript ou Swift ou binários customizados integrados em um contêiner do Docker. Ações no {{site.data.keyword.openwhisk_short}} são implementadas e executadas instantaneamente sempre que um acionador for disparado. Quanto mais acionadores forem disparados, mais ações são chamadas. Se nenhum acionador for disparado, nenhum código de ação estará em execução, portanto, não há nenhum custo.

Além de associar ações a acionadores, é possível chamar uma ação diretamente usando a API do {{site.data.keyword.openwhisk_short}}, a CLI ou o SDK do iOS. Um conjunto de ações também pode ser encadeado sem precisar escrever qualquer código. Cada ação da cadeia é chamada em sequência com a saída de uma ação passada como entrada para a próxima na sequência.

Com máquinas virtuais ou contêineres de longa execução tradicionais, é uma prática comum implementar vários contêineres ou VMs para ser resiliente contra indisponibilidades de uma única instância. No entanto, o {{site.data.keyword.openwhisk_short}} oferece um modelo alternativo sem gasto adicional de custo relacionado à resiliência. A execução de ações on demand fornece escalabilidade inerente e utilização ideal, já que o número de ações em execução sempre corresponde à taxa de acionador. Além
disso, o desenvolvedor agora apenas se concentra em seu código e não se preocupa sobre monitoramento, correção e proteção da infraestrutura subjacente de servidor, armazenamento, rede e sistema operacional.

Integrações a serviços adicionais e provedores de eventos podem ser incluídas com pacotes. Um pacote é um pacote configurável de feeds e ações. Um feed é uma parte do código que configura uma origem de eventos externos para disparar eventos acionadores. Por exemplo, um acionador criado com um feed de mudança do Cloudant irá configurar um serviço para disparar o acionador sempre que um documento for modificado ou incluído em um banco de dados do Cloudant. Ações
em pacotes representam lógica reutilizável que um provedor de serviços pode disponibilizar para que os desenvolvedores possam usar o serviço não apenas como uma origem de eventos, mas também chamar as APIs desse serviço.

Um catálogo de pacotes existente oferece uma forma rápida de aprimorar aplicativos com recursos úteis e de acessar serviços externos no ecossistema. Exemplos de serviços externos que são ativados pelo {{site.data.keyword.openwhisk_short}} incluem Cloudant, The Weather Company, Slack e GitHub.


## Casos de Uso Comuns
{: #openwhisk_use_cases}

O modelo de execução oferecido pelo {{site.data.keyword.openwhisk_short}} suporta diversos casos de uso. As seções a seguir incluem exemplos típicos.

### Decomposição de aplicativos em microsserviços
A natureza modular e inerentemente escalável do {{site.data.keyword.openwhisk_short}} o torna adequado para implementar partes granulares de lógica em ações. Por exemplo, o {{site.data.keyword.openwhisk_short}} pode ser útil para remover tarefas de carga intensiva, potencialmente com picos (segundo plano), a partir de código de frontend e para implementar essas tarefas como ações.

### Backend móvel
Muitos aplicativos móveis requerem lógica do lado do servidor. Considerando que os desenvolvedores para dispositivos móveis geralmente não têm experiência no gerenciamento de lógica do lado do servidor e prefeririam focar no app em execução no dispositivo, usar o {{site.data.keyword.openwhisk_short}} como o backend do lado do servidor é uma boa solução. Além disso, o suporte integrado para o Swift permite que desenvolvedores reutilizem suas qualificações existentes de programação do iOS.

### Processamento de Dados
Com a quantia de dados agora disponível, o desenvolvimento de aplicativo requer a capacidade de processar novos dados e, potencialmente reagir a eles. Esse requisito inclui o processamento tanto de registros do banco de dados estruturado quanto de documentos, imagens ou vídeos não estruturados.

### IoT
Os cenários de Internet of Things são frequentemente orientados por sensores de forma inerente. Por exemplo, uma ação no {{site.data.keyword.openwhisk_short}} poderia ser acionada se houver necessidade de reagir a um sensor que excede uma determinada temperatura.



