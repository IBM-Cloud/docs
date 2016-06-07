---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Sobre o {{site.data.keyword.iotdriverinsights_short}}
{: #iotdriverinsights_overview}

É possível usar o {{site.data.keyword.iotdriverinsights_full}} para analisar o comportamento do motorista dos dados de análise do carro e dos dados contextuais.
{:shortdesc}

## Análise de comportamento do motorista
{: #driver_behavior_analysis}
É possível analisar o comportamento do motorista, tais como a aceleração ou frenagem brusca, frenagem frequente, excesso de velocidade, curvas acentuadas e outras ações dos dados de análise
do carro e dos dados contextuais.

As atividades e os contextos a seguir são incluídos:
 - Comportamento de condução 
    - Relacionados à velocidade
       - Aceleração brusca
       - Frenagem brusca
       - Excesso de velocidade
       - Paradas frequentes
       - Aceleração frequente
       - Frenagem frequente
    - Relacionados a curva
       - Curva acentuada (curva em alta velocidade)
       - Aceleração antes da curva
       - Frenagem excessiva durante uma curva
    - Outros
       - Condução com fadiga
 - Contexto de condução
    - Intervalo de tempo
       - Horários de pico da manhã
       - Horários de pico da tarde
       - Dia
       - Noturno
    - Tipo de estrada
       - Pista Expressa
       - Rodovia urbana
       - Principal urbana
       - Estra urbana
       - Outros
    - Padrão de velocidade baseado no tipo de estrada
       - Liberar fluxo
       - Fluxo constante
       - Congestão
       - Congestionamento grave
       - Condições combinadas

## Infraestrutura de análise de big data
{: #big_data_analysis_infrastructure}
O {{site.data.keyword.iotdriverinsights_short}} usa o Hadoop como a infraestrutura de backend. O Hadoop permite que o {{site.data.keyword.iotdriverinsights_short}} realize alta escalabilidade para analisar big data dos dados de análise do carro e dos dados contextuais.

## API do REST
{: #rest_api}
Os desenvolvedores podem recuperar os resultados da análise pela API REST e usá-los no
aplicativo {{site.data.keyword.Bluemix_notm}}.
 1. Dados do Veículo
   - `sendCarProbeData` envia os dados de análise do carro para serem analisados.
   - `getCarProbeDataListAsDate` retorna a lista de dados de análise do carro por data.
   - `deleteCarProbeDataListByDate` exclui os dados de análise do carro.
 2. Tarefa de análise
   - `sendJobRequest` envia a solicitação da tarefa de análise de comportamento de condução.
   - `getJobInfo` retorna as informações da tarefa especificada.
   - `getJobInfoList` retorna a lista de informações sobre a tarefa.
 3. Resultado da Análise 
   - `getAnalyzedTripSummaryList` retorna a lista de informações resumidas da trajetória analisada.
   - `getAnalyzedTripInfo` retorna as informações da trajetória analisada especificada.
   - `deleteJobResult` exclui todos os resultados analisados relacionados a uma tarefa.

## Configurabilidade
{: #configurability}
Alguns dos parâmetros de limite de análise (tais como intervalo de velocidade por tipo de estrada, intervalo de ângulo da curva e assim por diante) podem ser configurados a partir da interface com
o usuário (UI).
