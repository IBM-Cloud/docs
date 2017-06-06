---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-11"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Perguntas e respostas frequentes
{: #logging_qa}

A seguir estão as respostas para perguntas comuns sobre como usar os recursos de criação de log
do {{site.data.keyword.Bluemix}}. {:shortdesc}

* [O que poderei fazer se eu não conseguir ver os logs JSON gerados por meu contêiner no Kibana](logging_qa.html#logging_qa_no_JSON_data_kibana)


## O que poderei fazer se eu não conseguir ver os logs JSON gerados por meu contêiner no Kibana
{: #logging_qa_no_JSON_data_kibana}

Quando os logs JSON são enviados para os logs do Docker como stdout, eles não são analisados como JSON; portanto, não podem ser classificados pelo campo @timestamp para mudar sua ordem. 

Os valores de @timestamp que são exibidos são os registros de data e hora de quando os logs foram recebidos pelo ElasticSearch. 

Os registros de data e hora que refletem quando
os logs foram gerados no contêiner são exibidos como parte do campo de mensagem.

Para separar o campo de mensagem em múltiplos campos, registre o JSON em um arquivo em vez de stdout. Em seguida, classifique os logs no Kibana.
