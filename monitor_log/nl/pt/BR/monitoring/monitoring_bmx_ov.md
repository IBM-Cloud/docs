---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Monitoramento no Bluemix
{: #monitoring_bmx_ov}

O {{site.data.keyword.Bluemix_notm}}, por padrão, coleta e exibe métricas de desempenho para uso de CPU, utilização de memória e E/S de rede. Essas métricas fornecem informações sobre o desempenho de recursos em nuvem individuais. É possível monitorar o desempenho desses recursos em seu ambiente de nuvem por meio do {{site.data.keyword.Bluemix_notm}} UI. É possível visualizar dados quase em tempo real e dados históricos.
{:shortdesc}

É possível usar os recursos de monitoramento em {{site.data.keyword.Bluemix_notm}} para coletar e medir automaticamente as métricas de chave de seu ambiente e aplicativos. Nenhuma instrumentação especial é necessária para coletar métricas. Por exemplo, é possível usar as informações fornecidas por métricas de desempenho para monitorar como um serviço está em execução na nuvem, detectar gargalos de recursos e manter-se atento ao acordo de nível de serviço (SLA). Ao analisar dados de desempenho para um serviço, é possível detectar situações que podem levar a um gargalo de recurso e, consequentemente, afetar seu SLA do serviço para seus clientes. Tomando uma ação antecipada, é possível evitar situações que podem impactar negativamente seus negócios.  

Também é possível configurar e monitorar mais métricas de desempenho. É possível visualizar e analisar essas métricas fora do {{site.data.keyword.Bluemix_notm}}. Por exemplo, é possível usar o Grafana para monitorar mais métricas quando você executar seu app no {{site.data.keyword.containershort}}. É possível customizar painéis por instância de contêiner ou por espaço no qual você visualiza e analisa os dados de desempenho.

![Visualização de monitoramento do Grafana de um contêiner em execução no {{site.data.keyword.Bluemix_notm}}](images/monitoring_default_container_grafana_view.jpg "Visualização de monitoramento do Grafana de um contêiner em execução no Bluemix")

É possível usar o monitoramento da plataforma {{site.data.keyword.Bluemix_notm}} para:

* Obter insight sobre operações do aplicativo, por exemplo, detectar os gargalos em potencial ou quando há necessidade de upgrades.
* Definir tendências que podem ser usadas para planejar requisitos futuros do app em sua plataforma de nuvem.

Para obter mais informações sobre o monitoramento de apps que são executados no Cloud Foundry, veja [Monitorando apps que são executados no Cloud Foundry](monitoring_cf_apps.html#monitoring_bluemix_apps).

Para obter mais informações sobre o monitoramento no {{site.data.keyword.containershort}}, veja [Monitoramento no {{site.data.keyword.containershort}}](containers/monitoring_containers_ov.html#monitoring_bmx_containers_ov).
