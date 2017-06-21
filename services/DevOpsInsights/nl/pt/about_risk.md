---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-07"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Sobre o Deployment Risk

O {{site.data.keyword.DRA_short}} fornece uma riqueza de informações sobre suas implementações, especificamente de risco. É possível usá-lo para automatizar a proteção de qualidade em seu pipeline de entrega usando políticas e portas. 
{:shortdesc}

Depois de abrir o {{site.data.keyword.DRA_short}} por meio de sua cadeia de ferramentas, clique em **Deployment Risk**. Daí, é possível obter uma visão geral dos aplicativos nos ambientes de preparação e produção e realizar drill down para entender os relatórios de cobertura de código, de desempenho de teste e de segurança. Os painéis são preenchidos automaticamente com as informações mais recentes dos testes do {{site.data.keyword.DRA_short}} dos pipelines.

É possível usar o Deployment Risk para utilizar as normas de qualidade em sua cadeia de ferramentas por meio de políticas e portas. As políticas incluem conjuntos de regras; as portas utilizam políticas. Por exemplo, é possível criar uma política "Teste de unidade e Cobertura de teste" que requer que as construções atendam às normas de teste de unidade e de cobertura de teste. Em seguida, você inclui uma porta que se refere à política de seu processo de entrega contínua. As construções que não satisfizerem a política serão paradas nessa porta. 

## Informações de integração

O Deployment Risk integra-se ao {{site.data.keyword.deliverypipeline}}, que faz parte do {{site.data.keyword.contdelivery_full}} e a projetos Jenkins. Em um alto nível, as instruções para usar um ou outro são semelhantes.  

Se você estiver usando o {{site.data.keyword.deliverypipeline}}, siga estas etapas:

1. [Crie políticas e regras](risk_policies.html) para o {{site.data.keyword.DRA_short}} gerenciar.
2. [Prepare os estágios de seu pipeline](risk_cd.html) para integração ao {{site.data.keyword.DRA_short}}.
3. [Crie ou edite tarefas de teste](risk_cd.html) no pipeline que façam upload de resultados no {{site.data.keyword.DRA_short}}.
4. [Inclua portas](risk_cd.html) no pipeline que tomem decisões de promoção com base nesses resultados e suas políticas.
5. Execute o pipeline e [visualize os resultados](results.html).

Se estiver usando o Jenkins, siga estas etapas:

1. [Crie políticas e regras](risk_policies.html) para o {{site.data.keyword.DRA_short}} gerenciar.
2. [Instale e configure o plug-in do Jenkins](risk_jenkins.html).
3. [Crie tarefas de teste e portas conforme descrito nas instruções do plug-in](risk_jenkins.html). Os testes fazem upload dos resultados no {{site.data.keyword.DRA_short}} para análise e as portas usam esses resultados para tomar decisões de promoção.
4. Execute o projeto e [visualize os resultados](results.html). 

Independentemente de como você construir e implementar seu código, os resultados serão os mesmos: as construções que atenderem às normas serão movidas depois das portas do Deployment Risk e as construções que não atenderem às normas serão paradas. 

## Pré-Requisitos
{: #prerequisites}

O Deployment Risk requer alguma configuração além daquela descrita em [Introdução ao {{site.data.keyword.DRA_short}}](/docs/services/DevOpsInsights/index.html).

Para usar o Deployment Risk, você precisa de duas coisas:

* Uma instância do {{site.data.keyword.deliverypipeline}} ou um projeto Jenkins
* Testes que você deseja usar para avaliar seu projeto
