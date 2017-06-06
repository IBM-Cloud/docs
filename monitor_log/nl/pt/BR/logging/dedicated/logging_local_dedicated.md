---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Criação de log para apps CF no Dedicated e Local
{: #hybrid_apps_logs_ov}

No {{site.data.keyword.Bluemix_dedicated_notm}} e {{site.data.keyword.Bluemix_local_notm}}, os apps do Cloud Foundry são fornecidos com a criação de log integrada. É possível revisar os dados que são coletados de seus apps no console do {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

Os apps do Cloud Foundry usam o loggregator do Cloud Foundry para monitorar e encaminhar logs de fora do app. Não é necessário instalar os agentes dentro do app.

## requisitos
de hardware


| **Requisitos** |    **1 nó**     | **3 nós para alta disponibilidade** |
|-----------------|-------------------|-------------------|
| vCPU | 19 | 57 |
| Memória | 80 GB | 240 GB |
| Armazenamento local | 2,98 TB | 8,94 TB |
{: caption="Tabela 2. Registrando requisitos de hardware para o {{site.data.keyword.Bluemix_local_notm}}" caption-side="top"}

## Configuração

No {{site.data.keyword.Bluemix_dedicated_notm}} e {{site.data.keyword.Bluemix_local_notm}}, os logs estão ativos para todos os apps por padrão. Para visualizar informações sobre leitura de logs padrão, veja [Criação de log para apps em execução no Cloud Foundry](../logging_cf_apps.html#logging_bluemix_cf_apps). Além disso, a criação de log avançada pode ser ativada nos ambientes do {{site.data.keyword.Bluemix_dedicated_notm}} e {{site.data.keyword.Bluemix_local_notm}}.

* Para confirmar se a criação de log avançada está ativada nos ambientes do {{site.data.keyword.Bluemix_dedicated_notm}} e {{site.data.keyword.Bluemix_local_notm}}, siga as etapas em [Visualizando logs](#hybrid_apps_logs_dash). Se você não tiver o botão **Visualização avançada**, esse recurso não será ativado.

* Para incluir a criação de log avançada em seu ambiente, siga a etapas na documentação do [{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) ou [{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local).

## Retenção de log

Nos apps do Cloud Foundry {{site.data.keyword.Bluemix_dedicated_notm}} e {{site.data.keyword.Bluemix_local_notm}}, os dados do log são armazenados por 30 por padrão.

## Visualizando logs para apps Cloud Foundry no Dedicated e Local
{: #hybrid_apps_logs_dash}

É possível revisar os logs para os apps que você está executando no {{site.data.keyword.Bluemix_dedicated_notm}} e {{site.data.keyword.Bluemix_local_notm}}.
{:shortdesc}

Para visualizar os logs de app, siga estas etapas.
1. Selecione um app em execução.
2. Clique em **Logs**. Na visualização **Logs**, é possível visualizar os logs de seu app em execução.
4. Clique no botão **Visualização avançada**. **Visualização avançada** mostra uma visualização mais detalhada dos logs usando o Kibana, uma ferramenta de visualização que usa logs e dados com registro de data e hora para criar visualizações customizadas. Para obter informações adicionais sobre o uso da visualização avançada, consulte a documentação do [Kibana](https://www.elastic.co/guide/en/kibana/current/index.html).

Em seguida, é possível customizar um painel do Kibana. Veja [Analisando logs em Kibana](../logging_view_kibana3.html#analyzing_logs_Kibana3) para obter mais informações.
