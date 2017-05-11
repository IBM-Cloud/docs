---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Analisando um campo da mensagem JSON que é parte de uma entrada de log do contêiner
{: #logging_containers_analyze_json_field}

No Kibana, para analisar os dados do log do contêiner, é possível definir novas procuras e aplicar filtros para campos dos tipos sequência que são definidos em um campo de mensagem formatada em JSON.
{:shortdesc}

Conclua as etapas a seguir para analisar um campo do tipo JSON no Kibana:

1. Para separar um campo de mensagem JSON em múltiplos campos, registre a mensagem no formato JSON em um arquivo em vez de STDOUT. 

    Quando as entradas de log JSON são enviadas para o arquivo de log do Docker de um contêiner como STDOUT, elas não são analisadas como JSON. Não é possível classificar sua mensagem pelo campo @timestamp para mudar sua ordem.  

2. Inclua o arquivo de log na lista de logs não padrão que estão disponíveis para análise de um contêiner. Para obter mais informações, consulte
[Coletando dados de log não
padrão de um contêiner](logging_containers_other_logs.html#logging_containers_collect_data). 

3. Analise seu log no Kibana. Para obter mais informações, veja [Análise avançada do log com o Kibana](../kibana4/logging_analyzing_logs_Kibana.html#analyzing_logs_Kibana).

    **Nota:** se um campo é determinado ser JSON válido, ele é analisado e novos campos são criados dele. Somente valores de campos do tipo sequência estão disponíveis para filtragem e classificação no Kibana.
    
    O valor do campo @timestamp que é exibido corresponde ao registro de data e hora de quando a entrada de log foi recebida pelo ElasticSearch. O registro de data e hora que reflete quando a entrada de log foi gerada no contêiner é exibido como parte dos campos de mensagem.
    


