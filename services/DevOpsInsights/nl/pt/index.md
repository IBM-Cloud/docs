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

# Introdução ao DevOps Insights (Beta)
{: #gettingstarted}

O {{site.data.keyword.DRA_full}} aplica análise de desenvolvedor, de equipe e de implementação a seus projetos DevOps mais ocupados. Use-o para saber quanto sua equipe é compatível com o DevOps e com as práticas do desenvolvedor, para gerenciar risco em seu código base e para aplicar normas de qualidade automaticamente em projetos de entrega contínua.
{:shortdesc}

O {{site.data.keyword.DRA_short}} inclui vários grupos de recursos:

   * O Developer Insights fornece uma maneira abrangente de explorar a maturidade de desenvolvimento de seu projeto. É possível identificar arquivos com alta propensão a erros e obter uma visualização de conformidade do projeto com relação às práticas do desenvolvedor.

   * O Team Dynamics usa a análise de codificação social para ajudá-lo a saber como sua equipe colabora e entender como ela pode trabalhar melhor.

   * O Deployment Risk é como uma rede de segurança de entrega contínua. Ele analisa os resultados de testes de unidade, testes funcionais, varreduras do aplicativo e ferramentas de cobertura de código em portas especificadas em seu processo de implementação e evita a liberação de mudanças de risco.

   * O Delivery Insights mostra estatísticas de implementação, métricas e outras informações sobre a instalação do IBM UrbanCode Deploy. Por exemplo, ele pode mostrar gráficos de duração da implementação, sucessos e falhas, todos classificados por ambientes agrupados logicamente. Veja [Integrando o DevOps Insights ao IBM UrbanCode Deploy](/docs/services/DevOpsInsights/uc_insights_overview.html).

O {{site.data.keyword.DRA_short}} é uma integração no catálogo de cadeia de ferramentas aberta do Bluemix. Para obter mais informações sobre cadeias de ferramentas, veja [Trabalhando com cadeias de ferramentas](/docs/services/ContinuousDelivery/toolchains_working.html).

Para usar o {{site.data.keyword.DRA_short}}, deve-se incluí-lo em uma cadeia de ferramentas. Muitos modelos de cadeia de ferramentas já incluem o {{site.data.keyword.DRA_short}}. Certifique-se de também [incluí-lo em sua organização do {{site.data.keyword.Bluemix_notm}} como um serviço](/docs/services/reqnsi.html) para que você possa ver informações sobre o {{site.data.keyword.DRA_short}} e acessar alguns dos modelos de cadeia de ferramentas que o incluem por meio do painel do {{site.data.keyword.Bluemix_notm}}.  

## Incluindo o DevOps Insights em uma cadeia de ferramentas
{: #catalog}

O {{site.data.keyword.DRA_short}} faz parte do {{site.data.keyword.contdelivery_short}}. É possível incluir o {{site.data.keyword.DRA_short}} em qualquer cadeia de ferramentas, selecionando-o no catálogo de integração de ferramenta.

O {{site.data.keyword.DRA_short}} também faz parte de vários modelos da cadeia de ferramentas. Se você criar uma cadeia de ferramentas por meio de um modelo que inclui o {{site.data.keyword.DRA_short}}, certifique-se de que o {{site.data.keyword.DRA_short}} esteja configurado como **Avançado**. Em seguida, crie a cadeia de ferramentas e vá para [Usando o Insights](/docs/services/DevOpsInsights/index.html#using).

Para incluir o {{site.data.keyword.DRA_short}} em uma cadeia de ferramentas:

1. Clique em **Incluir uma ferramenta**.

2. Clique em **{{site.data.keyword.DRA_short}}**.

3. Para incluir todos os recursos do {{site.data.keyword.DRA_short}} na cadeia de ferramentas, selecione **Avançado** e certifique-se de que a caixa de seleção **Ativar Developer Insights** esteja marcada. Para incluir apenas o Deployment Risk, selecione **Padrão**. 

4. Clique em
**Criar integração**.

O {{site.data.keyword.DRA_short}} está agora disponível na página Visão geral de sua cadeia de ferramentas.

## Usando o DevOps Insights
{: #using}

Se a sua cadeia de ferramentas incluir GitHub, GitLab ou JIRA, o {{site.data.keyword.DRA_short}} fornecerá informações automaticamente sobre seu código base e equipe após alguma reunião e análise de dados iniciais. Se a sua cadeia de ferramentas não incluir nenhuma dessas integrações, inclua uma delas e, em seguida, siga estas etapas:

1. Na página Visão geral da cadeia de ferramentas, clique em **{{site.data.keyword.DRA_short}}**.

2. Na navegação esquerda, clique em **Team Dynamics** ou **Developer Insights** e, em seguida, escolha uma categoria de dados.

3. Explore os dados de seu projeto visualizando os painéis na categoria de dados. Se desejar saber mais sobre um gráfico ou o que você poderia fazer com suas informações, clique em **Informações** ou **Orientação**.

Depois de explorar o Team Dynamics e o Developer Insights, [configure o Deployment Risk](/docs/services/DevOpsInsights/insights_risk.html) para ajudá-lo a utilizar a qualidade de código. O Deployment Risk é compatível com o pipeline do {{site.data.keyword.contdelivery_short}} e o Jenkins.   

Por padrão, o {{site.data.keyword.DRA_short}} não inclui o Developer Insights ou o Team Dynamics. Para incluir esses recursos em sua cadeia de ferramentas depois de configurá-la:

1. Acesse a página Visão geral da cadeia de ferramentas.
2. No cartão do {{site.data.keyword.DRA_short}}, clique no menu **Ações**.
3. Clique em **Configurar**.
4. Para o tipo, selecione **Avançado** e marque a caixa de seleção.
5. Clique em **Salvar integração**.

Depois de salvar a configuração, o Developer Insights e o Team Dynamics varrem automaticamente seu repositório e sistemas de rastreamento de problemas.
