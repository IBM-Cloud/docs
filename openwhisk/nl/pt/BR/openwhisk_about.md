---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-21"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Sobre o {{site.data.keyword.openwhisk_short}}

{{site.data.keyword.openwhisk}} é uma plataforma de cálculo acionada por eventos também referida como cálculo Serverless ou como Function as a Service (FaaS) que executa código em resposta a eventos ou chamadas diretas. A figura a seguir mostra a arquitetura de alto nível do {{site.data.keyword.openwhisk}}.
{: shortdesc}

![Arquitetura do {{site.data.keyword.openwhisk_short}}](./images/OpenWhisk.png)

Exemplos de eventos incluem mudanças em registros do banco de dados, leituras do sensor IoT que excedem uma determinada temperatura, novas consolidações de código para um repositório GitHub ou solicitações de HTTP simples de apps da web ou móveis. Os eventos de origens de eventos externos e internos são canalizados por meio de um acionador e as regras permitem que as ações reajam a esses eventos.

Ações podem ser pequenos fragmentos de código JavaScript ou Swift ou código binário
customizado integrado em um contêiner do Docker. Ações no {{site.data.keyword.openwhisk_short}} são implementadas e executadas instantaneamente sempre que um acionador for disparado. Quanto mais acionadores forem disparados, mais ações são chamadas. Se nenhum acionador for disparado, nenhum código de ação estará em execução, portanto, não há nenhum custo.

Além de associar ações a acionadores, é possível chamar uma ação diretamente usando a API do {{site.data.keyword.openwhisk_short}}, a CLI ou o SDK do iOS. Um conjunto de ações também pode ser encadeado sem precisar escrever qualquer código. Cada ação da cadeia é chamada em sequência com a saída de uma ação passada como entrada para a próxima na sequência.

Com máquinas virtuais ou contêineres de longa execução tradicionais, é uma prática comum implementar vários contêineres ou VMs para ser resiliente contra indisponibilidades de uma única instância. No entanto, o {{site.data.keyword.openwhisk_short}} oferece um modelo alternativo sem gasto adicional de custo relacionado à resiliência. A execução de ações on demand fornece escalabilidade inerente e utilização ideal, já que o número de ações em execução sempre corresponde à taxa de acionador. Além disso, o desenvolvedor agora se concentra apenas em seu código e não se preocupa com
monitoramento, correção e proteção da infraestrutura subjacente de servidor,
armazenamento, rede e sistema operacional.

Integrações a serviços adicionais e provedores de eventos podem ser incluídas com pacotes. Um pacote é um pacote configurável de feeds e ações. Um feed é uma parte do código que configura uma origem de eventos externos para disparar eventos acionadores. Por exemplo, um acionador criado com um feed de mudança do Cloudant irá configurar um
serviço para disparar o acionador sempre que um documento for modificado ou incluído em
um banco de dados do Cloudant. Ações em pacotes representam lógica reutilizável que um
provedor de serviços pode disponibilizar para que os desenvolvedores não apenas possam
usar o serviço como origem de eventos, mas também chamar as APIs desse serviço.

Um catálogo de pacotes existente oferece uma forma rápida de aprimorar aplicativos com recursos úteis e de acessar serviços externos no ecossistema. Exemplos de serviços externos que são ativados pelo {{site.data.keyword.openwhisk_short}} incluem Cloudant, The Weather Company, Slack e GitHub.


## Como o {{site.data.keyword.openwhisk_short}} funciona
{: #openwhisk_how}

Sendo um projeto de software livre, o OpenWhisk se posiciona nos ombros de gigantes, incluindo Nginx, Kafka, Consul, Docker, CouchDB. Todos esses componentes se juntam para formar um “serviço de programação baseada em eventos Serverless”. Para explicar todas as componentes em mais detalhes, vamos rastrear uma chamada de uma ação por meio do sistema conforme ela acontece. Uma chamada no OpenWhisk é a coisa principal que um mecanismo Serverless faz: executar o código que o usuário alimentou no sistema e retornar os resultados dessa execução.

### Criando a ação

Para dar a explicação de algum contexto, vamos criar uma ação no sistema primeiro. Usaremos essa ação para explicar os conceitos mais tarde durante o rastreio por meio do sistema. Os comandos a seguir presumem que a CLI do [OpenWhisk foi configurada adequadamente](https://github.com/openwhisk/openwhisk/tree/master/docs#setting-up-the-openwhisk-cli).

Primeiro, criaremos um arquivo *action.js* contendo o código a seguir que imprimirá “Hello World” para stdout e retornará um objeto JSON contendo “world” sob a chave “hello”.
```javascript
function main() {
    console.log('Hello World');
    return { hello: 'world' };
}
```
{: codeblock}

Criamos essa ação usando:
```
wsk action create myAction action.js
```
{: pre}

Concluído. Agora desejamos, na realidade, chamar esta ação:
```
wsk action invoke myAction
```
{: pre}

## O fluxo interno de processamento
O que realmente acontece nos bastidores do OpenWhisk?

![Fluxo de processamento do OpenWhisk](images/OpenWhisk_flow_of_processing.png)

### Inserindo o sistema: nginx

Primeiro: a API voltada ao usuário do OpenWhisk é completamente baseada em HTTP e segue um design do RESTful. Como consequência, o comando enviado por meio do wsk-CLI é essencialmente uma solicitação de HTTP com relação ao sistema OpenWhisk. O comando específico acima converte aproximadamente para:
```
POST /api/v1/namespaces/$userNamespace/actions/myAction
Host: $openwhiskEndpoint
```
{: screen}

Observe a variável *$userNamespace* aqui. Um usuário tem acesso a pelo menos um namespace. Para simplificar, vamos supor que o usuário possui o namespace no qual *myAction* é colocado.

O primeiro ponto de entrada no sistema é por meio de **nginx**, “um servidor proxy reverso e HTTP”. Ele é usado principalmente para finalização de SSL e para encaminhar as chamadas HTTP apropriadas para o próximo componente.

### Inserindo o sistema: Controlador

Não tendo feito muito para nossa solicitação de HTTP, o nginx a encaminha para o **Controlador**, o próximo componente em nossa viagem pelo OpenWhisk. É uma implementação baseada no Scala da API de REST real (com base em **Akka** e **Spray**) e, portanto, serve como a interface para tudo que um usuário pode fazer, incluindo solicitações [CRUD](https://en.wikipedia.org/wiki/Create,_read,_update_and_delete) para suas entidades no OpenWhisk e chamada de ações (que é o que estamos fazendo neste momento).

O Controlador primeiro esclarece o que o usuário está tentando fazer. Ele faz isso com base no método de HTTP usado em sua solicitação de HTTP. Conforme a tradução acima, o usuário está emitindo uma solicitação de POST para uma ação existente, que o Controlador traduz para uma **chamada de uma ação**.

Dada a função central do Controlador (portanto, o nome), todas as etapas a seguir o envolverão até um certo ponto.

### Autenticação e autorização: CouchDB

Agora o controlador verifica quem você é (*Autenticação*) e se tem o privilégio para fazer o que deseja fazer com essa entidade (*Autorização*). As credenciais incluídas na solicitação são verificadas com relação ao banco de dados denominado **assuntos** em uma instância **CouchDB**.

Neste caso, é verificado que o usuário existe no banco de dados do OpenWhisk e que tem o privilégio para chamar a ação myAction, que supomos ser uma ação em um namespace que o usuário possui. Esse último fornece efetivamente ao usuário o privilégio para chamar a ação, que é o que ele deseja fazer.

Como tudo está adequado, a porta se abre para o próximo estágio de processamento.

### Obtendo a ação: CouchDB… novamente

Como o Controlador agora está seguro de que o usuário tem permissão e possui os privilégios para chamar a ação, ele de fato carrega essa ação (neste caso, *myAction*) do banco de dados **a** em CouchDB.

O registro da ação contém principalmente o código a ser executado (mostrado acima) e os parâmetros padrão que você deseja passar para a sua ação, mesclados com os parâmetros incluídos na solicitação de chamada real. Ele também contém as restrições de recurso impostas na execução, como a memória que ele é permitido consumir.

Neste caso específico, a nossa ação não aceita nenhum parâmetro (a definição de parâmetro da função é uma lista vazia), portanto supomos que não configuramos nenhum parâmetro padrão e não enviamos nenhum parâmetro específico para a ação, contribuindo para o caso mais trivial desse ponto de vista.

### Quem está lá para chamar a ação: Consul

O Controlador (ou mais especificamente a parte de balanceamento de carga dele) tem tudo no lugar agora para que realmente o código funcione. No entanto, ele precisa saber quem está disponível para fazer isso. O **Consul**, uma descoberta de serviço, é usado para rastrear os executores disponíveis no sistema verificando seu status de funcionamento continuamente. Esses executores são chamados de **Invocadores**.

O Controlador, agora sabendo quais Invocadores estão disponíveis, escolhe um deles para chamar a ação solicitada.

Vamos supor neste caso que o sistema tem 3 Invocadores disponíveis, Invocador 0 a 2, e que o Controlador escolheu o *Invocador 2* para chamar a ação em questão.

### Forme uma linha: Kafka

De agora em diante, principalmente duas coisas ruins podem acontecer com a solicitação de chamada que você enviou:

1. O sistema pode travar, perdendo sua chamada.
2. O sistema pode estar sob uma carga tão pesada que a chamada precisa esperar que outras chamadas concluam primeiro.

A resposta para ambas é **Kafka**, “um sistema de mensagens de publicação/assinatura distribuídas e de alto rendimento”. O Controlador e o Invocador se comunicam unicamente por meio de mensagens armazenadas em buffer e persistidas por Kafka. Isso eleva a carga de armazenamento em buffer na memória, arriscando um *OutOfMemoryException*, fora do Controlador e do Invocador, além de se certificar de que as mensagens não sejam perdidas no caso de travamento do sistema.

Para obter a ação chamada então, o Controlador publica uma mensagem para o Kafka, que contém a ação a ser chamada e os parâmetros a serem passados para essa ação (neste caso nenhum). Essa mensagem é endereçada ao Invocador que o Controlador escolheu acima na lista obtida do Consul.

Depois que o Kafka confirmar que obteve a mensagem, a solicitação de HTTP para o usuário será respondida com um **ActivationId**. O usuário usará isso mais tarde para obter acesso aos resultados dessa chamada específica. Observe que este é um modelo de chamada assíncrona, em que a solicitação de HTTP é finalizada quando o sistema aceita a solicitação para chamar uma ação. Um modelo síncrono (denominado chamada de bloqueio) está disponível, mas não é coberto por este artigo.

### Chamando efetivamente o código: Invocador

O **Invocador** é o coração do OpenWhisk. A obrigação do Invocador é chamar uma ação. Ele também é implementado no Scala. Mas há ainda muito mais. Para executar ações de uma maneira isolada e segura, ele usa o **Docker**.

O Docker é usado para configurar um ambiente autocontido (chamado *contêiner*) para cada ação que chamamos de uma maneira rápida, isolada e controlada. Em poucas palavras, para cada chamada de ação em que um contêiner do Docker é gerado, o código de ação é injetado, ele é executado usando os parâmetros passados para ele, o resultado é obtido, o contêiner é destruído. Esse também é o local em que muita otimização de desempenho é feita para reduzir a sobrecarga e tornar os tempos de resposta baixos possível. 

No nosso caso específico, como temos uma ação baseada no *Node.js* em questão, o Invocador iniciará um contêiner Node.js, injetará o código de *myAction*, o executará sem parâmetros, extrairá o resultado, salvará os logs e destruirá o contêiner Node.js novamente.

### Armazenando os resultados: CouchDB novamente

Como o resultado é obtido pelo Invocador, ele é armazenado no banco de dados **whisks** como uma ativação sob o ActivationId mencionado mais acima. O banco de dados **whisks** reside em **CouchDB**.

No nosso caso específico, o Invocador obtém o objeto JSON resultante de volta da ação, captura o log gravado pelo Docker, coloca tudo no registro de ativação e o armazena no banco de dados. Ele será aproximadamente como este:

```json
     {
   "activationId": "31809ddca6f64cfc9de2937ebd44fbb9",
   "response": {
       "statusCode": 0,
       "result": {
           "hello": "world"
       }
   },
   "end": 1474459415621,
   "logs": [
       "2016-09-21T12:03:35.619234386Z stdout: Hello World"
   ],
   "start": 1474459415595,
}
```
{: codeblock}

Observe como o registro contém tanto o resultado retornado quanto os logs gravados. Ele também contém os horários de início e de encerramento da chamada da ação. Há mais campos em um registro de ativação, esta é uma versão reduzida por motivos de simplicidade.

Agora é possível usar a API de REST novamente (iniciar na etapa 1 novamente) para obter sua ativação e, portanto, o resultado de sua ação. Para fazer isso, você usaria:

```bash
wsk activation get 31809ddca6f64cfc9de2937ebd44fbb9
```
{: pre} 

### Resumo

Vimos como um **action invoke myAction** simples passa por diferentes estágios do sistema {{site.data.keyword.openwhisk_short}}. O sistema em si consiste principalmente em somente dois componentes customizados, o **Controlador** e o **Invocador**. Todo o resto já está lá, desenvolvido por muitas pessoas lá fora na comunidade de software livre.

É possível localizar informações adicionais sobre o {{site.data.keyword.openwhisk_short}} nos tópicos a seguir:

* [Nomes de entidades](./openwhisk_reference.html#openwhisk_entities)
* [Semântica de ação](./openwhisk_reference.html#openwhisk_semantics)
* [Limites
](./openwhisk_reference.md#openwhisk_syslimits)
* [REST API
](./openwhisk_reference.md#openwhisk_ref_restapi)
