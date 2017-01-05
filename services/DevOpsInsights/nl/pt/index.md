---

copyright:
  years: 2016
lastupdated: "2016-11-11"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Introdução ao {{site.data.keyword.DRA_short}} (Experimental)
{: #gettingstarted}

Use o {{site.data.keyword.DRA_full}} para identificar os riscos para as suas construções e implementações.
{:shortdesc}

O {{site.data.keyword.DRA_short}} agrega e analisa os resultados de testes de unidade, testes funcionais e ferramentas de cobertura de código para
determinar se o seu código atende às políticas predefinidas em portas especificadas em seu processo de implementação. Se o seu código não atender nem exceder uma
política, a implementação será interrompida, impedindo que as mudanças de risco sejam liberadas. É possível usar o {{site.data.keyword.DRA_short}} como uma
rede de segurança para o seu ambiente de entrega contínua, uma forma de implementar e melhorar padrões de qualidade ao longo do tempo e uma ferramenta de visualização
de dados para ajudá-lo a entender o funcionamento do seu projeto.

O {{site.data.keyword.DRA_short}} é uma oferta experimental e é fornecido no estado em que se encontra apenas para propósitos de desenvolvimento e experimentação. Para
usar o {{site.data.keyword.DRA_short}}, inclua-o em qualquer cadeia de ferramentas que use o {{site.data.keyword.deliverypipeline}}.

{: #catalog}
Para acessar a UI do {{site.data.keyword.DRA_short}}, conclua as etapas a seguir a partir de uma cadeia de ferramentas existente:

1. Clique no botão **Incluir uma ferramenta**.

2. Clique em **{{site.data.keyword.DRA_short}}**.

3. Clique em
**Criar integração**.

4. Clique no ladrilho **{{site.data.keyword.DRA_short}}**.

5. Conclua a sua configuração com as tarefas restantes:

	1. [Configure a sua integração do {{site.data.keyword.deliverypipeline}}](./pipeline_integration.html).
	2. Execute o pipeline e [revise os painéis do {{site.data.keyword.deliverypipeline}}](./pipeline_decision_reports.html).
	3. [Defina políticas](./create_criteria.html) para o {{site.data.keyword.DRA_short}} gerenciar.
	4. Execute o pipeline novamente para verificar se o seu projeto passa as suas políticas.


# Links Relacionados
{: #rellinks}

## Tutoriais e amostras
{: #samples}

* [Usando analítica para avisar sobre a probabilidade de
implementações bem-sucedidas](https://www.ibm.com/devops/method/content/deliver/tool_deployment_risk_analytics/){:new_window}

## Links Relacionados
{: #general}

* [Introdução às cadeias de ferramentas](https://new-console.ng.bluemix.net/docs/toolchains/toolchains_overview.html){:new_window}
* [Introdução ao Delivery Pipeline](https://new-console.ng.bluemix.net/docs/services/DeliveryPipeline/index.html){:new_window}
* [Folha de precificação do IBM Bluemix](https://new-console.ng.bluemix.net/pricing/){:new_window}
* [Pré-requisitos do IBM Bluemix](https://developer.ibm.com/bluemix/support/?cm_mc_uid=96503159749414585876298&cm_mc_sid_50200000=1462802909#prereqs){:new_window}
