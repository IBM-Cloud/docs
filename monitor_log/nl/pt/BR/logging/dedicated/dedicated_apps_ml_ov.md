---



copyright:

  years: 2016, 2017

lastupdated: "2017-04-06"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

<!-- audience blue staging only begin -->

# Monitoramento e criação de log para apps Cloud Foundry no Dedicated e Local
{: #dedicated_apps_ml_ov}


No {{site.data.keyword.Bluemix_dedicated_notm}} e {{site.data.keyword.Bluemix_local_notm:}}, os apps do Cloud Foundry são fornecidos com a criação de log integrada. É possível revisar os dados que são coletados de seus apps no console do {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

Os apps do Cloud Foundry usam o loggregator do Cloud Foundry para monitorar e encaminhar logs de fora do app. Não é necessário instalar os agentes dentro do app.

## requisitos
de hardware


| **Requisitos** |    **1 nó**     | **3 nós para alta disponibilidade** |
|-----------------|-------------------|-------------------|
vCPU | 19 | 57 |
Memória | 80 GB | 240 GB |
Armazenamento local | 2,98 TB | 8,94 TB |
{: caption="Tabela 1. Registrando os requisitos de hardware para {{site.data.keyword.Bluemix_local_notm:}}" caption-side="top"}

## Configuração

No {{site.data.keyword.Bluemix}} Dedicated e {{site.data.keyword.Bluemix}} Local, os logs estão ativos para todos os apps por padrão. Para visualizar informações sobre leitura de logs padrão, veja Criação de log para apps em execução no Cloud Foundry. Além disso, a criação de log avançada pode ser ativada nos ambientes do {{site.data.keyword.Bluemix}} Dedicated e {{site.data.keyword.Bluemix}} Local.

## Retenção de log

Em apps Cloud Foundry do {{site.data.keyword.Bluemix}} Dedicated e {{site.data.keyword.Bluemix}} Local, os dados do log são armazenados durante 30 dias por padrão.

## Visualizando logs para apps Cloud Foundry no {{site.data.keyword.Bluemix}} Dedicated e {{site.data.keyword.Bluemix}} Local
{: #dedicated_apps_ml_logs_dash}

É possível revisar os logs para os apps que você está executando no {{site.data.keyword.Bluemix_notm}} Dedicated e {{site.data.keyword.Bluemix_notm}} Local.
{:shortdesc}

Para visualizar os logs de app, siga estas etapas.
1. Selecione um app em execução.
2. Clique em **Logs**. Na visualização **Logs**, é possível visualizar os logs de seu app em execução.
4. Clique no botão **Visualização avançada**. **Visualização avançada** mostra uma visualização mais detalhada dos logs usando o Kibana, uma ferramenta de visualização que usa logs e dados com registro de data e hora para criar visualizações customizadas. Para obter mais informações sobre como usar a visualização avançada, veja o [Guia do Usuário do Kibana ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}.

Em seguida, é possível customizar um painel do Kibana. Veja [Análise avançada do log com o Kibana](../kibana4/analyzing_logs_Kibana.html#analyzing_logs_Kibana) para obter mais informações.

<!-- audience blue staging only end comment -->
