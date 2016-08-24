---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Sobre o {{site.data.keyword.iot4auto_short}} (Beta)
{: #iotautomotive_overview}

Última atualização: 29 de julho de 2016
{: .last-updated}

O {{site.data.keyword.iot4auto_full}} é um serviço no {{site.data.keyword.Bluemix_notm}} que pode ser usado para visualizar e analisar big data dos veículos.

Usando o serviço do {{site.data.keyword.iot4auto_short}}, é possível coletar e processar grandes volumes de dados dos veículos. A análise de dados do
{{site.data.keyword.iot4auto_short}}
fornece insights poderosos e práticos no comportamento do motorista, localização do veículo, outras atividades automotivas relacionadas e eventos de interesse.
{:shortdesc}

## Software
{: #architecture}
O {{site.data.keyword.iot4auto_short}} é uma plataforma de infraestrutura em tempo real
fundamental para aplicativos automotivos e dispositivos de veículos conectados. O serviço também
é projetado para suportar recursos emergentes de condução autônoma do futuro.

Arquitetura ![{{site.data.keyword.iot4auto_full}}](images/architecture_iotautomotive.png "{{site.data.keyword.iot4auto_full}} architecture")

O serviço do {{site.data.keyword.iot4auto_short}} inclui os serviços do {{site.data.keyword.Bluemix_notm}} a seguir, que também estão disponíveis separadamente no catálogo do {{site.data.keyword.Bluemix_notm}}:

|Serviço|Descrição|
|:---|:---|
|[Comportamento do motorista](../IotDriverInsights/index.html)| Um serviço que pode analisar o comportamento do motorista e identificar padrões de trajetória de uma viagem a partir dos dados de análise e contexto do veículo que são recuperados de um veículo conectado.
|[Mapeamento de contexto](../IotMapInsights/index.html)| Um serviço que fornece funções geoespaciais, tais como a correspondência de mapa e a busca do
caminho mais curto por redes viárias.
*Tabela 1. Serviços do {{site.data.keyword.iot4auto_short}}*

## Recursos Avançados
{: #features}

{{site.data.keyword.iot4auto_short}} suporta os recursos e as funções a seguir para soluções que fornecem dados de análise do veículo de dispositivos de veículos conectados:

### Recuperação de dados dos dispositivos do {{site.data.keyword.iot4auto_short}}

- Suporta os protocolos e modelos de dados a seguir:
   - TPEG
   - ITS
   - Padrões automotivos ISO
- Suporta outros dispositivos e sensores que não são do veículo

### Normalização e armazenamento de dados

- Identifica e filtra dados de anomalia
- Mapeia, converte e forma dados para o modelo de dados padrão para análise
- Coloca os dados em um dos armazenamentos de dados a seguir, de acordo com o volume, a latência e o uso do aplicativo ou serviço:
   -  Armazenamento de dados Hadoop para análise de big data
   -  Armazenamento de dados do agente para análise em tempo real

### Serviço baseado em mapa geoespacial

- Correspondência de mapa em tempo real
- Serviço de evento
- Injeção de evento dinâmico de veículos e origens externas
- Procura ciente de link ou topologia baseada no nó
- Suporte de mapa contextual que possui dados de clima integrados

### Plataforma de análise em tempo real altamente escalável e de baixa latência

- Tecnologia baseada em agente
- Análise personalizada
- Análise baseada em regra flexível

### Moving Object Map Analysis (MOMA)

- Análise em lote (big data) usando dados do veículo
- Análise de comportamento do motorista
- Criação de perfil do motorista
- Análise de padrão de trajetória

### Serviço do provedor de dados

- APIs para aplicativos e serviços de terceiros

### Integração com gerenciamento de ativos

- Sistemas de gerenciamento de recursos do veículo

## API REST
{: #api}

A API do [{{site.data.keyword.iot4auto_short}}](http://ibm.biz/IoT4Automotive_APIdoc) fornece comandos para ajudá-lo a desenvolver ainda mais o {{site.data.keyword.iot4auto_short}} para atender aos seus requisitos.

Usando os comandos de API REST disponíveis, é possível customizar sua instância do serviço do {{site.data.keyword.iot4auto_short}}:

- Injetar eventos específicos no sistema
- Armazenar os dados normalizados de análise do veículo de um veículo no armazenamento de dados de analítica preferencial
- Recuperar os eventos de interesse em tempo real, juntamente com a localização geográfica do veículo

### Comandos de REST API

|Propósito |Comando de API |Descrição |
|:---|:---|:---|
|Injetar evento|`sendEvent`|Envia os eventos de tráfego ou outros eventos para a plataforma.|
|Enviar dados de análise do veículo|`sendCarProbe`|Envia os dados do sensor baseados em posição do veículo e recupera os eventos afetados para o veículo pelo resultado da análise em tempo real.|
|Criar dados do veículo|`createVehicle`|Criar um registro do veículo como um recurso. Estas informações são usadas para autenticação, inventário e outros usos.|
|APIs de Mapa|Não aplicável|Para obter mais informações, veja as [APIs de serviço do Mapa Contextual](http://ibm.biz/IoTContextMapping_APIdoc).|
|APIs de Análise|Não aplicável|Para obter mais informações, veja as [APIs de serviço do Comportamento do Motorista]( http://ibm.biz/IoTDriverBehavior_APIdoc).|
|Obter dados de análise do veículo|`getCarProbe`|Obtém os dados mais recentes de análise do veículo que foram enviados pelo comando de API `sendCarProbe`.|
|Obter eventos do mapa|`getEvent` |Obtém os eventos no mapa que foram enviados pelo comando de API `sendEvent`.|
|Obter dados de recurso do veículo|`getVehicle`| Obtém os dados do veículo como um recurso do comando de API `createVehicle`.|
*Tabela 2. Comandos de API REST do {{site.data.keyword.iot4auto_short}}*
