---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Efetuando login no Bluemix
{: #logging_bmx_ov}

Os recursos de criação de log do {{site.data.keyword.Bluemix_notm}} são integrados na plataforma e a coleção de dados é ativada automaticamente para recursos em nuvem. O {{site.data.keyword.Bluemix_notm}}, por padrão, coleta e exibe os logs para seus apps, tempos de execução de apps e tempos de execução de cálculo nos quais esses apps são executados. 
{:shortdesc}

É possível usar os recursos de criação de log no {{site.data.keyword.Bluemix_notm}} para entender o comportamento da plataforma de nuvem e os recursos que estão em execução nela. Nenhuma instrumentação especial é necessária para coletar os logs de saída padrão e erro padrão. Por exemplo, é possível usar logs para fornecer uma trilha de auditoria para um aplicativo, detectar problemas no serviço, identificar vulnerabilidades, solucionar problemas de implementações de app e de comportamento de tempo de execução, detectar problemas na infraestrutura na qual o app está em execução, rastrear o app entre os componentes na plataforma de nuvem e detectar padrões que podem ser usados para priorizar ações que possam afetar o SLA de serviço.

Ao executar os apps na nuvem, pode não ser possível usar SSH ou FTP na infraestrutura na qual os apps estão em execução para acessar os logs, por exemplo, se o app for executado no Cloud Foundry. Por outro lado, é possível executar o app no {{site.data.keyword.containershort}}, outro tempo de execução de cálculo que está disponível no {{site.data.keyword.Bluemix_notm}}, no qual é possível usar SSH e acessar os logs. Independentemente do tempo de execução de cálculo, o acesso aos logs é crítico e o {{site.data.keyword.Bluemix_notm}} fornece uma experiência comum para visualizar e analisar logs em sua plataforma de nuvem.

O {{site.data.keyword.Bluemix_notm}} registra os dados do log que são gerados pela plataforma Cloud Foundry e por aplicativos Cloud Foundry. Nos logs, é possível visualizar os erros, os avisos e as mensagens informativas produzidas para o app. Para obter mais informações sobre a criação de log no Cloud Foundry, veja [Criação de log para apps Cloud Foundry no Bluemix](logging_cf_apps.html#logging_bluemix_cf_apps).

O {{site.data.keyword.Bluemix_notm}} registra os dados do log que são gerados pelo {{site.data.keyword.containershort}}. Para obter mais informações sobre a criação de log no {{site.data.keyword.containershort}}, veja [Criação de log no {{site.data.keyword.containershort}}](/docs/containers/monitoringandlogging/container_ml_logs.html#container_ml_logs).   


Usando a funcionalidade de criação de log que o {{site.data.keyword.Bluemix_notm}} oferece, é possível:

* Ter visibilidade em seus recursos em nuvem e como eles estão sendo desempenhados e executados.
* Definir tendências que ajudam a identificar cenários que requerem sua ação.
* Definir trilhas de dados para um app, por exemplo, que é possível usar para auditoria.
* Reduzir o tempo e o esforço necessários para localizar um problema em um app e repará-lo. 
* Monitorar a implementação de seus apps na plataforma de nuvem.
* Detectar quando um serviço ou um app está inativo ou travado.
* Seguir a execução do aplicativo e o fluxo de dados.
* Identificar vulnerabilidades em seu app.
* Detectar problemas na infraestrutura.
* Detectar problemas no tempo de execução do app.
