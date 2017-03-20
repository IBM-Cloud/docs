---

copyright:
  years: 2016, 2017
lastupdated: "2016-02-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Implementando feeds
{: #openwhisk_feeds}

O {{site.data.keyword.openwhisk_short}} suporta uma API aberta, em que qualquer usuário pode expor um serviço de produtor de evento como um **feed** em um **pacote**. Essa seção descreve as
opções de arquitetura e implementação para fornecer o seu próprio feed.

Esse material é destinado a usuários avançados do {{site.data.keyword.openwhisk_short}} que pretendem publicar os seus próprios feeds. A maioria dos usuários do {{site.data.keyword.openwhisk_short}} pode seguramente ignorar essa seção.

## Arquitetura de feed

Há pelo menos 3 padrões arquiteturais para criar um feed: **Ganchos**, **Pesquisa** e **Conexões**.

### Ganchos
No padrão *Ganchos*, nós configuramos um feed usando um recurso [webhook](https://en.wikipedia.org/wiki/Webhook) exposto por outro serviço.   Nessa estratégia,
nós configuramos um webhook em um serviço externo para POST diretamente em uma URL para disparar um acionador.  Essa é de longe a opção mais fácil e mais atraente para implementar feeds de baixa frequência.

<!-- The github feed is implemented using webhooks.  Put a link here when we have the open repo ready -->

### Pesquisa
No padrão "Pesquisa", nós organizamos uma *ação* do {{site.data.keyword.openwhisk_short}} para pesquisar um terminal periodicamente para buscar novos dados. Esse padrão é relativamente fácil de construir, mas a frequência de eventos será,
é claro, limitada pelo intervalo de pesquisa.

### Conexões
No padrão "Conexões", nós levantamos um serviço separado em algum lugar que mantém uma conexão persistente com uma origem do feed.    A implementação baseada em conexão pode interagir com um terminal de
serviço por meio de pesquisa longa ou para configurar uma notificação push.

<!-- Our cloudant changes feed is connection based.  Put a link here to
an open repo -->

<!-- What is the foundation for the Message Hub feed? If it is "connections" then lets put a link here as well -->

## Diferença entre feed e acionador

Feeds e acionadores estão intimamente relacionados,
mas tecnicamente têm conceitos distintos.   

- O {{site.data.keyword.openwhisk_short}} processa **eventos** que são transmitidos para o sistema.

- Um **acionador** é tecnicamente um nome para uma classe de eventos.   Cada evento pertence a exatamente um acionador; por analogia, um acionador é semelhante a um *tópico*
em sistemas de pub-sub baseados em tópico. Uma **regra** *T -> A* significa que "sempre que um evento a partir do acionador *T* chegar, chame a ação
*A* com a carga útil do acionador.

- Um **feed** é um fluxo de eventos, todos pertencentes a algum acionador *T*. Um feed é controlado por uma **ação de feed** que manipula a
criação, a exclusão, a pausa e a continuação do fluxo de eventos que compõem um feed. A ação de feed normalmente interage com serviços externos que produzem os eventos, através de uma API REST que gerencia notificações.

##  Implementando ações de feed

A *ação de feed* é uma *ação* normal do {{site.data.keyword.openwhisk_short}}, mas ela deve aceitar os parâmetros a seguir:
* **lifecycleEvent**: 'CREATE', 'DELETE', 'PAUSE' ou 'UNPAUSE'.
* **triggerName**: o nome completo do acionador que contém eventos produzidos a partir desse feed.
* **authKey**: as credenciais de autenticação Básica do usuário do {{site.data.keyword.openwhisk_short}} que possui o acionador recém-mencionado.

A ação de feed também pode aceitar qualquer outro parâmetro que ela precisa para gerenciar o feed.  Por exemplo, a ação de feed de mudanças do cloudant espera receber parâmetros que incluam *'dbname'*, *'username'*, etc.

Quando o usuário cria um acionador a partir da CLI com o parâmetro **--feed**, o sistema automaticamente chama a ação de feed com os parâmetros apropriados.

Por exemplo, suponha que o usuário criou uma ligação `mycloudant` para o pacote `cloudant`
com o seu nome do usuário e senha como parâmetros de limite. Quando o usuário emite o comando a seguir na CLI:

`wsk trigger create T --feed mycloudant/changes -p dbName myTable`

então, nos bastidores, o sistema fará algo equivalente a:

`wsk action invoke mycloudant/changes -p lifecycleEvent CREATE -p triggerName T -p authKey <userAuthKey> -p password <password value from mycloudant binding> -p username <username value from mycloudant binding> -p dbName mytype`

A ação de feed denominada *mudanças* utiliza esses parâmetros e deve tomar qualquer ação necessária para configurar um fluxo de eventos a partir do Cloudant, com a configuração
apropriada, direcionada ao acionador *T*.    

Para o feed *mudanças* do Cloudant, a ação passa a falar diretamente com um serviço do *acionador do cloudant* que nós implementamos com uma arquitetura baseada em conexão.   Nós discutiremos as outras arquiteturas a seguir.

Um protocolo de ação de feed semelhante ocorre para `wsk trigger delete`.    

## Implementando feeds com ganchos

É fácil configurar um feed por meio de um gancho se o produtor de evento suporta um recurso webhook/retorno de chamada.

Com esse método *não é necessário* levantar qualquer serviço persistente fora do OpenWhisk.  Todo o gerenciamento de feed acontece naturalmente por meio de *ações de feed* stateless do {{site.data.keyword.openwhisk_short}}, que negociam diretamente com um API de webhook de terceiro.

Quando chamada com `CREATE`, a ação de feed simplesmente instala um webhook para algum outro serviço, solicitando que o serviço remoto efetue POST de notificações para a URL apropriada do
`fireTrigger` no OpenWhisk.

O webhook deve ser direcionado para enviar notificações para uma URL como:

`POST /namespaces/{namespace}/triggers/{triggerName}`

O formulário com a solicitação POST será interpretado como um documento de JSON que define parâmetros no evento acionador. As regras do {{site.data.keyword.openwhisk_short}} passam esses parâmetros acionadores para quaisquer ações para disparar como resultado do evento.

## Implementando feeds com pesquisa

É possível configurar uma *ação* do {{site.data.keyword.openwhisk_short}} para pesquisar uma origem do feed inteiramente no OpenWhisk, sem a necessidade de levantar qualquer conexão persistente ou serviço externo.

Para feeds nos quais um webhook não está disponível, mas não precisam de alto volume ou tempos de resposta de baixa latência, a pesquisa é uma opção atraente.

Para configurar um feed baseado em pesquisa, a ação de feed usa as etapas a seguir quando chamada para `CREATE`:

1.   A ação de feed configura um acionador periódico (*T*) com a frequência desejada, usando o feed `whisk.system/alarms`.
2.   O desenvolvedor de feed cria uma ação `pollMyService` que simplesmente pesquisa o serviço remoto e retorna quaisquer novos eventos.
3.  A ação de feed configura uma *regra* *T -> pollMyService*.

Esse procedimento implementa um acionador baseado em pesquisa usando inteiramente ações do {{site.data.keyword.openwhisk_short}}, sem qualquer necessidade de um serviço separado.

## Implementando feeds por meio de conexões

As 2 opções anteriores de arquitetura são simples e fáceis de implementar. No entanto, se você deseja um feed de alto desempenho, não há substituto para conexões persistentes e técnicas de pesquisa
longa ou similares.

Como as ações do {{site.data.keyword.openwhisk_short}} devem ser de execução curta, uma ação não poderá manter uma conexão persistente com um terceiro. Em vez disso, devemos
levantar um serviço separado (fora do OpenWhisk) que seja executado o tempo todo.   Nós os chamamos de *serviços do provedor*.  Um serviço do provedor pode manter conexões com origens de eventos de
terceiro que suportam notificações de pesquisa longa ou outras baseadas em conexão.

O serviço do provedor deve fornecer uma API de REST que permita que a *ação de feed* do {{site.data.keyword.openwhisk_short}} controle o feed. O serviço do provedor age como um proxy entre o provedor de evento e o {{site.data.keyword.openwhisk_short}} -- quando recebe eventos do terceiro, ele os envia para o {{site.data.keyword.openwhisk_short}} disparando um acionador.

O feed de *mudanças* do Cloudant é o exemplo canônico -- ele levanta um serviço `cloudanttrigger` que media entre as notificações do Cloudant em uma conexão persistente e os acionadores do {{site.data.keyword.openwhisk_short}}.
<!-- TODO: add a reference to the open source implementation -->

O feed *alarme* é implementado com um padrão semelhante.

A arquitetura baseada em conexão é a opção de alto desempenho mais alta, mas impõe mais sobrecarga em operações em comparação com as arquiteturas de pesquisa e gancho.   
