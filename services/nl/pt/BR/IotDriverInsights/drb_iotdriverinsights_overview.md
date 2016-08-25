---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Sobre o Driving Behavior Analysis
{: #iotdriverinsights_overview}
Última atualização: 16 de junho de 2016
{: .last-updated}


O Driving Behavior Analysis é um serviço que pode ser usado para analisar o comportamento de um motorista nos dados de análise e contextuais do carro.

{:shortdesc}


## Arquitetura
{: #drb}

É possível identificar e analisar vários tipos de comportamento de condução relacionados a velocidade, curvas e outras categorias. Por exemplo, é possível determinar ocorrências de aceleração brusca, excesso de velocidade, curvas acentuadas, frenagem frequente ou brusca e outros tipos de comportamento do motorista.

## Configuração analítica
{: #configurability}  

Os parâmetros de limite de análise determinam como os diferentes tipos de comportamento do motorista são detectados e analisados nos dados de análise e contextuais do carro alimentados no sistema. É
possível configurar alguns dos parâmetros de limite para a análise de dados do comportamento de condução no console de administração do serviço
{{site.data.keyword.iotdriverinsights_short}}. Por exemplo, é possível configurar o intervalo de velocidade por tipo de estrada e o intervalo de ângulo da curva.

Para obter mais informações sobre como configurar os parâmetros de limite para a análise de dados do Driving Behavior Analysis, consulte
[Configurando parâmetros para o serviço](drb_iotdriverinsights_admin.html#configureparameters).

### Categorias e atividades do comportamento de condução

As tabelas a seguir listam os tipos de comportamento de condução por categoria que podem ser detectados e analisados pelo serviço:

#### Tabela 1: tipos de comportamento de condução relacionados à velocidade

|Nome do comportamento|ID do comportamento|Description|
|--------|:-------:|------|
|Aceleração brusca|1|O valor do limite de aceleração brusca de acordo com a velocidade é configurado internamente. A aceleração brusca será reconhecida se os dados de aceleração excederem o valor do limite.|
|Frenagem brusca|2|O valor do limite de desaceleração brusca de acordo com a velocidade é configurado internamente. A frenagem brusca será reconhecida se os dados de frenagem de uma viagem excederem o valor do limite.|
|Excesso de velocidade|3|O valor do limite de excesso de velocidade por tipo de estrada é configurado. O excesso de velocidade será reconhecido se os dados de velocidade da viagem excederem o valor do limite. É possível configurar o limite para o excesso de velocidade. |
|Parada frequente|4|Uma parada é detectada quando o valor da velocidade é zero. Paradas frequentes serão reconhecidas se houver muitas ocorrências de parada dentro de um determinado intervalo de tempo na viagem.|
|Aceleração frequente|5|O valor do limite de aceleração de acordo com a velocidade é configurado internamente. A aceleração frequente será detectada se o motorista exceder frequentemente o valor do limite dentro de um determinado intervalo de tempo durante a viagem.|
|Frenagem frequente|6|O valor do limite de desaceleração de acordo com a velocidade é configurado internamente. A desaceleração frequente será reconhecida se o motorista exceder o valor do limite frequentemente dentro de um determinado intervalo de tempo durante a viagem.|

#### Tabela 2: comportamento de condução relacionado à curva

|Nome do comportamento|ID do comportamento|Description|
|-------|:--------:|-------|
|Curva acentuada (curva em alta velocidade)|7|O valor do limite de velocidade na curva é configurado. Uma curva acentuada será reconhecida se o motorista exceder o valor do limite. É possível configurar o limite da curva acentuada.
|Aceleração antes da curva|8|O valor do limite de aceleração de acordo com a velocidade é configurado internamente. A aceleração antes de uma curva será reconhecida se o motorista exceder o valor do limite.
|Frenagem excessiva antes de sair de uma curva|9|O valor do limite de desaceleração de acordo com a velocidade é configurado internamente. A frenagem excessiva antes de sair de uma curva será reconhecida se o motorista exceder o valor do limite.

#### Tabela 3: outros tipos de comportamento de condução

|Nome do comportamento|ID do comportamento|Description|
|-------|:--------:|-------|
|Condução com fadiga|10|O valor do limite de desaceleração de acordo com a velocidade é configurado internamente. A fadiga em um motorista será reconhecida se a velocidade exceder o valor do limite.|


### Contexto de condução
|Categoria<br/>do contexto|ID da categoria<br/>do contexto|Nome do contexto|ID de Contexto|
|-------|:-----:|--------|:-------:|
|**Intervalo de tempo**|**4**|\-|\-|
|Intervalo de tempo|4|Dia|1|
|Intervalo de tempo|4|Noturno|2|
|Intervalo de tempo|4|Horários de pico da manhã|3|
|Intervalo de tempo|4|Horários de pico da tarde|4|
|**Tipo de estrada**|**3**|\-|\-|
|Tipo de estrada|3|Pista Expressa|1|
|Tipo de estrada|3|Rodovia urbana|2|
|Tipo de estrada|3|Principal urbana|3|
|Tipo de estrada|3|Estra urbana|4|
|Tipo de estrada|3|Outros|5|
|**Padrão de velocidade**|**0**|\-|\-|
|Padrão de velocidade|0|Liberar fluxo|0|
|Padrão de velocidade|0|Fluxo constante|1|
|Padrão de velocidade|0|Congestionamento grave|2|
|Padrão de velocidade|0|Congestão|3|
|Padrão de velocidade|0|Condições combinadas|4|


## API REST
{: #rest_api}

A API REST do {{site.data.keyword.iotdriverinsights_short}} fornece solicitações que podem ser usadas para customizar e construir seus aplicativos {{site.data.keyword.Bluemix_notm}}:

 1. Comandos de dados do carro:
   - `sendCarProbeData` envia os dados de análise do carro para serem analisados
   - `getCarProbeDataListAsDate` retorna a lista de dados de análise do carro por data
   - `deleteCarProbeDataListByDate` exclui os dados de análise do carro
 2. Comandos da tarefa de análise:
   - `sendJobRequest` envia a solicitação da tarefa de análise de comportamento de condução
   - `getJobInfo` retorna as informações da tarefa especificada
   - `getJobInfoList` retorna a lista de informações sobre a tarefa
 3. Comandos de resultado da análise:
   - `getAnalyzedTripSummaryList` retorna a lista de informações de resumo da trajetória analisada
   - `getAnalyzedTripInfo` retorna as informações da trajetória analisada especificada
   - `deleteJobResult` exclui todos os resultados analisados relacionados a uma tarefa

Para obter mais informações, consulte a documentação da [API do {{site.data.keyword.iotdriverinsights_short}}](http://ibm.biz/IoTDriverBehavior_APIdoc){:new_window}.

## Infraestrutura de análise de big data
{: #big_data_analysis_infrastructure}
O {{site.data.keyword.iotdriverinsights_short}} usa o Hadoop como a infraestrutura de backend. O Hadoop fornece alta escalabilidade para que o serviço {{site.data.keyword.iotdriverinsights_short}} possa recuperar e analisar grandes volumes de dados de análise e contextuais do carro.
