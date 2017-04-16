---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Introdução ao {{site.data.keyword.graphfull}}
{: #gettingstartedtemplate}
Última atualização: 27 de julho de 2016
{: .last-updated}

O {{site.data.keyword.graphfull}} é um serviço de banco de dados gráfico totalmente gerenciado,
acessível por meio de uma interface da API HTTP baseada em REST.
Use-o para criar aplicativos móveis e da web que requeiram recursos do banco de dados gráfico.
{:shortdesc}

O {{site.data.keyword.graphfull}} é baseado na pilha do [Apache TinkerPop](http://tinkerpop.incubator.apache.org/)&trade;,
para criar aplicativos gráficos de alto desempenho que usam uma API compatível com v3.
A pilha oferece flexibilidade extra e recursos baseados em um ambiente familiar.
Usando o painel {{site.data.keyword.Bluemix}},
é possível integrar com facilidade o serviço {{site.data.keyword.graphfull}} com seus aplicativos {{site.data.keyword.Bluemix_short}}.

É possível trabalhar com o {{site.data.keyword.graphfull}} de duas maneiras:

*	Usando os comandos da API simplificada do {{site.data.keyword.graphfull}}.
*	Usando a linguagem de consulta integral do Apache TinkerPop v3 (Gremlin).

Os recursos do {{site.data.keyword.graphfull}} estão disponíveis como uma API usando terminais HTTP REST.
Esses terminais fornecem uma maneira fácil de seus aplicativos conectarem e usarem o serviço {{site.data.keyword.graphfull}},
usando HTTP para fazer solicitações da API e obter resultados.
Use as funções HTTP que são fornecidas pela linguagem de programação de aplicativos escolhida para acessar os terminais.
Ou então, é possível usar uma interface de comando ou um script `curl` para obter os mesmos efeitos.
A Referência da API descreve as várias funções fornecidas pelo serviço {{site.data.keyword.graphfull}},
junto com exemplos de seu uso.

O seu aplicativo também pode usar a linguagem de consulta do Apache TinkerPop,
chamada Gremlin, para tarefas que usam o serviço {{site.data.keyword.graphfull}}.
Inclua a consulta Gremlin em um documento JSON e, em seguida,
passe o documento para o terminal em serviço `/gremlin`.
Exemplos de uso do Gremlin com o {{site.data.keyword.graphfull}} são fornecidos na documentação completa.

Conclua estas etapas para iniciar o serviço {{site.data.keyword.graphfull}}: 

1.	[Crie uma instância](https://www.ng.bluemix.net/docs/services/reqnsi.html#req_instance) do serviço {{site.data.keyword.graphfull}}.
2.	Registre os três valores essenciais gerados quando a instância é criada. Os valores estão disponíveis na guia `Credenciais do serviço` depois de clicar no quadro do serviço.
	*	O terminal do IBM Graph: `apiURL`.
	*	O nome do usuário da instância de serviço `username`.
	*	A senha da instância de serviço `password`.
3.	Use os três valores essenciais em seus aplicativos ou scripts para tarefas do {{site.data.keyword.graphfull}}. Exemplos são fornecidos na documentação completa.

# Links relacionados
{: #rellinks}

## Tutoriais e amostras
{: #samples}

* [Exemplos](https://ibm-graph-docs.ng.bluemix.net/examples.html){:new_window}

## Referência da API
{: #api}

* [API REST para IBM Graph](https://ibm-graph-docs.ng.bluemix.net/api.html){:new_window}
* [Usando o Gremlin com o IBM Graph](https://ibm-graph-docs.ng.bluemix.net/api.html#gremlin-apis){:new_window}

## Links relacionados
{: #general}

* [Documentação completa](https://ibm-graph-docs.ng.bluemix.net/){:new_window}
* [Estouro da capacidade](http://stackoverflow.com/questions/tagged/ibm-graph){:new_window}
* [Apache Tinkerpop](http://tinkerpop.incubator.apache.org/){:new_window}
