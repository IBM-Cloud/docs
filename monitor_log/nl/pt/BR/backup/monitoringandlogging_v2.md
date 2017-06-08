---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-14"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Monitoramento e criação de log
{: #monitoringandlogging}

{{site.data.keyword.Bluemix}} é uma plataforma de computação em nuvem da {{site.data.keyword.IBM_notm}} para construir, executar e gerenciar apps e serviços. O {{site.data.keyword.Bluemix_notm}} combina a plataforma como serviço (PaaS) com a infraestrutura como serviço (IaaS). Além disso, o {{site.data.keyword.Bluemix_notm}} tem um rico catálogo de serviços de nuvem, que pode ser facilmente integrado com o PaaS e IaaS para construir aplicativos de negócios rapidamente. O {{site.data.keyword.Bluemix_notm}} inclui os serviços de criação de log e monitoramento integrados na plataforma. 
{:shortdesc}

O {{site.data.keyword.Bluemix_notm}} oferece os serviços de criação de log e monitoramento em diferentes serviços de cálculo, como o Cloud Foundry e {{site.data.keyword.containershort}}. É possível desenvolver, executar e gerenciar aplicativos em qualquer tempo de execução de cálculo sem a complexidade de construir e manter a infraestrutura que está geralmente associada ao desenvolvimento e ativação de um app. 

**Nota:** os recursos de monitoramento e criação de log estão disponíveis na região sul dos EUA e na região do Reino Unido.

É possível usar os recursos de monitoramento em {{site.data.keyword.Bluemix_notm}} para coletar e medir automaticamente as métricas de chave de seu ambiente e aplicativos. Nenhuma instrumentação especial é necessária para coletar métricas. Por exemplo, é possível usar as informações fornecidas por métricas de desempenho para monitorar como um serviço está em execução na nuvem, detectar gargalos de recursos e manter-se atento ao acordo de nível de serviço (SLA). Por exemplo, ao analisar dados de desempenho para um serviço, é possível detectar situações que podem levar a um gargalo de recurso e, consequentemente, afetar seu SLA do serviço para seus clientes. Tomando uma ação antecipada, é possível evitar situações que podem impactar negativamente seus negócios.  

É possível usar os recursos de criação de log no {{site.data.keyword.Bluemix_notm}} para entender o comportamento da plataforma de nuvem e os recursos que estão em execução nela. Nenhuma instrumentação especial é necessária para coletar os logs de saída padrão e erro padrão. Por exemplo, é possível usar logs para fornecer uma trilha de auditoria para um aplicativo, detectar problemas no serviço, identificar vulnerabilidades, solucionar problemas de implementações de app e de comportamento de tempo de execução, detectar problemas na infraestrutura na qual o app está em execução, rastrear o app entre os componentes na plataforma de nuvem e detectar padrões que podem ser usados para priorizar ações que possam afetar o SLA de serviço.

## Monitorando recursos de infraestrutura de cálculo
{: #monitoring_sl_ov}

Cada servidor {{site.data.keyword.Bluemix_notm}} inclui monitoramento e relatórios facilmente legíveis que estão sempre disponíveis. Para obter mais informações, veja [Monitoramento e relatório de infraestrutura ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/cloud-computing/bluemix/infrastructure-monitoring){: new_window}.


## Monitoramento no {{site.data.keyword.Bluemix}} para serviços de cálculo
{: #monitoring_bmx_ov}

O {{site.data.keyword.Bluemix_notm}}, por padrão, coleta e exibe métricas de desempenho para uso de CPU, utilização de memória e E/S de rede. Essas métricas fornecem informações sobre o desempenho de recursos em nuvem individuais. É possível monitorar o desempenho desses recursos em seu ambiente de nuvem por meio do {{site.data.keyword.Bluemix_notm}} UI. É possível visualizar dados quase em tempo real e dados históricos. 

Também é possível configurar e monitorar mais métricas de desempenho. É possível visualizar e analisar essas métricas fora do {{site.data.keyword.Bluemix_notm}}. Por exemplo, é possível usar o Grafana para monitorar mais métricas quando você executar seu app no {{site.data.keyword.containershort}}. É possível customizar painéis por instância de contêiner ou por espaço no qual você visualiza e analisa os dados de desempenho.

![Visualização de monitoramento do Grafana de um contêiner em execução no {{site.data.keyword.Bluemix_notm}}](images/monitoring_default_container_grafana_view.jpg)

É possível usar o monitoramento da plataforma {{site.data.keyword.Bluemix_notm}} para:

* Obter insight sobre operações do aplicativo, por exemplo, detectar os gargalos em potencial ou quando há necessidade de upgrades.
* Definir tendências que podem ser usadas para planejar requisitos futuros do app em sua plataforma de nuvem.

Para obter mais informações sobre o monitoramento de apps que são executados no Cloud Foundry, veja [Monitorando apps que são executados no Cloud Foundry](monitoring_cf_apps.html#monitoring_bluemix_apps).

Para obter mais informações sobre o monitoramento no {{site.data.keyword.containershort}}, veja [Monitoramento no {{site.data.keyword.containershort}}](/docs/containers/monitoringandlogging/container_ml_monitor.html#container_ml_monitor).   

## Criação de log no {{site.data.keyword.Bluemix}}
{: #logging_bmx_ov}

Os recursos de criação de log do {{site.data.keyword.Bluemix_notm}} são integrados na plataforma e a coleção de dados é ativada automaticamente para recursos em nuvem. O {{site.data.keyword.Bluemix_notm}}, por padrão, coleta e exibe os logs para seus apps, tempos de execução de apps e tempos de execução de cálculo nos quais esses apps são executados. 

Ao executar os apps na nuvem, pode não ser possível usar SSH ou FTP na infraestrutura na qual os apps estão em execução para acessar os logs, por exemplo, se o app for executado no Cloud Foundry. Por outro lado, é possível executar o app no {{site.data.keyword.containershort}}, outro tempo de execução de cálculo que está disponível no {{site.data.keyword.Bluemix_notm}}, no qual é possível usar SSH e acessar os logs. Independentemente do tempo de execução de cálculo, o acesso aos logs é crítico e o {{site.data.keyword.Bluemix_notm}} fornece uma experiência comum para visualizar e analisar logs em sua plataforma de nuvem.

O {{site.data.keyword.Bluemix_notm}} registra os dados do log que são gerados pela plataforma Cloud Foundry e por aplicativos Cloud Foundry. Nos logs, é possível visualizar os erros, os avisos e as mensagens informativas produzidas para o app. Para obter mais informações sobre a criação de log no Cloud Foundry, veja [Criação de log para apps Cloud Foundry no {{site.data.keyword.Bluemix}}](logging_cf_apps.html#logging_bluemix_cf_apps).

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


