---

copyright:
  years: 2015, 2017
lastupdated: "2017-4-4"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Sobre o Continuous Delivery  
{: #cd_about}  

Com o {{site.data.keyword.contdelivery_full}}, é possível construir, testar
e entregar aplicativos usando práticas DevOps e ferramentas líderes de mercado.
{:shortdesc}

O serviço de {{site.data.keyword.contdelivery_short}} suporta seus fluxos de trabalho DevOps:

 * É possível criar [cadeias de ferramentas](/docs/services/ContinuousDelivery/toolchains_about.html){: new_window} abertas DevOps integradas para permitir integrações de ferramentas que suportem suas tarefas de desenvolvimento, implementação e operações.

  Uma cadeia de ferramentas é um conjunto integrado de ferramentas que você pode
usar para desenvolver, construir, implementar, testar e gerenciar aplicativos de forma
colaborativa. Você pode criar cadeias de ferramentas que incluam serviços do
{{site.data.keyword.Bluemix_notm}}, ferramenta de software livre e ferramentas de
terceiros, como GitHub, PagerDuty e Slack, que tornam o desenvolvimento e as operações
repetíveis e mais fáceis de gerenciar.

 * Entregue continuamente usando pipelines [pipelines](/docs/services/ContinuousDelivery/pipeline_about.html){: new_window} automatizados.

  Automatize construções, testes de unidade, implementações etc. Construa, teste e implemente repetidamente, com mínima intervenção humana. Esteja pronto para liberar para a produção a qualquer momento.

 * Edite e envie por push seu código de qualquer lugar usando o [IDE baseado na web](/docs/services/ContinuousDelivery/web_ide.html){: new_window}.

  Crie, edite, execute e depure, bem como conclua as tarefas de controle de fonte
no GitHub. Mova sem problemas da edição do seu código para a implementação dele
em produção.

 * Melhore a qualidade por meio do [{{site.data.keyword.DRA_short}}](/docs/services/ContinuousDelivery/di_working.html){: new_window}.

  Entenda a dinâmica de sua equipe conforme ela desenvolve e entrega
código. Saiba como os usuários interagem com seu aplicativo. Revise os dados para ajudar
a gerenciar as operações do seu aplicativo.


## Disponibilidade da cadeia de ferramentas no Bluemix Public comparado ao Bluemix Dedicated
{: #public_and_dedicated}

O {{site.data.keyword.Bluemix_notm}} Public é uma plataforma de padrões abertos baseada em nuvem na qual é possível construir, executar e gerenciar aplicativos que são acessados por [http://bluemix.net ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://bluemix.net){:new_window}. O {{site.data.keyword.Bluemix_notm}} Dedicated fornece os recursos do {{site.data.keyword.Bluemix_notm}} em um ambiente dedicado do SoftLayer que está firmemente conectado ao ambiente do {{site.data.keyword.Bluemix_notm}} Public e à sua rede. O ambiente do {{site.data.keyword.Bluemix_notm}} Dedicated de sua empresa pode não conter as mesmas integrações de ferramentas do site do {{site.data.keyword.Bluemix_notm}} Public.

Para gerenciamento de código fonte e rastreamento de problemas, o {{site.data.keyword.Bluemix_notm}} Public usa geralmente github.com. O {{site.data.keyword.Bluemix_notm}} Dedicated também pode usar github.com, mas geralmente usa o {{site.data.keyword.ghe_short}}, que é instalado por sua empresa ou gerenciado pela IBM.

O {{site.data.keyword.contdelivery_short}} está disponível no {{site.data.keyword.Bluemix_notm}} Public e no {{site.data.keyword.Bluemix_notm}} Dedicated. As cadeias de ferramentas são diferentes, dependendo de se você usa o {{site.data.keyword.contdelivery_short}} no {{site.data.keyword.Bluemix_notm}} Public ou no {{site.data.keyword.Bluemix_notm}} Dedicated.

|Cadeias de ferramentas |{{site.data.keyword.Bluemix_notm}} Public	|{{site.data.keyword.Bluemix_notm}} Dedicated |
|:----------|:------------------------------|:------------------|
|Integrações de ferramenta 		|Para obter uma lista de integrações de ferramentas suportadas, veja [Configurando integrações de ferramentas](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}. 		|As integrações de ferramentas que estão disponíveis dependem de como o {{site.data.keyword.contdelivery_short}} foi configurado em seu ambiente.			|
|Criando uma cadeia de ferramentas com base em um modelo		|Efetue login no [{{site.data.keyword.Bluemix_notm}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://console.ng.bluemix.net/devops){:new_window}		|Efetue login no ambiente Dedicated no {{site.data.keyword.Bluemix_notm}}.			|
|Criando uma cadeia de ferramentas com base em um aplicativo		|O app é configurado para entrega contínua por meio de um novo repositório GitHub que é preenchido com o código de início do app.		|O app é configurado para entrega contínua por meio de um novo repositório GitHub ou GitHub Enterprise que é preenchido com o código de início do app.		|  
|Regiões de implementação do pipeline de entrega		|Todas as regiões do {{site.data.keyword.Bluemix_notm}} Public estão disponíveis para as tarefas de implementação do Cloud Foundry. 		|A região do {{site.data.keyword.Bluemix_notm}} Dedicated está disponível. Outras regiões Dedicated ou Local na mesma conta de cliente também poderão estar disponíveis, dependendo de como o {{site.data.keyword.contdelivery_short}} tiver sido configurado em seu ambiente específico.		|
|Tarefas de implementação do pipeline de entrega		|Todos os [tipos de tarefas](/docs/services/ContinuousDelivery/pipeline_about.html#deliverypipeline_jobs) estão disponíveis.		|Os tipos de tarefas que dependem de serviços do {{site.data.keyword.Bluemix_notm}} que não estão instalados no ambiente Dedicated podem não estar disponíveis. Por exemplo, os tipos de tarefas de construção e implementação do contêiner podem não estar disponíveis em ambientes que não possuem o serviço {{site.data.keyword.Bluemix_notm}} Container.	|
{: caption="Table 1. Differences between toolchains on {{site.data.keyword.Bluemix_notm}} Dedicated and {{site.data.keyword.Bluemix_notm}} Public" caption-side="top"}


## Modelos de cadeias de ferramentas
{: #templates}

É possível usar um modelo como um ponto de início para [criar uma cadeia de ferramentas ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://console.ng.bluemix.net/devops/create){: new_window}. Os modelos de cadeia de ferramentas incluem conjuntos específicos de integrações de ferramentas que suportam as tarefas de desenvolvimento, implementação e operações.

**Dica**: o ambiente do {{site.data.keyword.Bluemix_notm}} Dedicated de sua empresa pode não conter os mesmos modelos de cadeias de ferramentas do site do {{site.data.keyword.Bluemix_notm}} Public. Os modelos de cadeias de ferramentas que estão disponíveis no {{site.data.keyword.Bluemix_notm}} Public e no {{site.data.keyword.Bluemix_notm}} Dedicated podem conter um conjunto diferente de integrações de ferramentas no {{site.data.keyword.Bluemix_notm}} Dedicated.

Alguns modelos de cadeias de ferramentas incluem integrações de ferramentas que fazem parte do serviço {{site.data.keyword.contdelivery_short}}. Se uma instância desse serviço ainda não estiver em sua organização, quando você clicar em **Criar** para criar a cadeia de ferramentas, o serviço será incluído automaticamente sem nenhum custo para você. Para obter mais informações e termos, veja o [catálogo do Bluemix ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://console.ng.bluemix.net/catalog/services/continuous-delivery/){:new_window}.

Os modelos de cadeias de ferramentas de microsserviços implementam um app com APIs de Catálogo e de Ordens que são suportadas por um armazenamento do Cloudant. Como parte da implementação do app, uma instância de serviço do Cloudant gratuita é criada. Para obter mais informações e termos, veja o [catálogo do Bluemix ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://console.ng.bluemix.net/catalog/services/cloudant-nosql-db/){:new_window}.

|Gabarito |Descrição	|
|:----------|:------------------------------|
|[Cadeia de ferramentas do tutorial de nuvem nativa do Garage Method ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fcloud-native-toolchain-tutorial){:new_window} 		|Essa cadeia de ferramentas demonstra as práticas de DevOps apresentadas no Garage Method. A cadeia de ferramentas é pré-configurada para entrega contínua, controle de fonte, automação de teste, bem como monitoramento e operações automatizados. Ela vem com um app de amostra que é escrito em Node.js Express 4, que pode ser ampliado posteriormente. 		|
|[Cadeia de ferramentas de microsserviços com o {{site.data.keyword.DRA_short}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Ftoolchain-demo){:new_window} 		|Com essa cadeia de ferramentas de nuvem nativa, é possível usar uma amostra para criar uma loja on-line que consista em três microsserviços: uma API de Catálogo, uma API de Ordens e uma UI que chame ambas as APIs. A cadeia de ferramentas é pré-configurada para entrega contínua, controle de fonte, teste funcional, rastreamento de problemas, edição on-line e notificação de alerta. 		|
|[Cadeia de ferramentas de microsserviços com o {{site.data.keyword.DRA_short}} (v2) ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fmicroservices-toolchain-hosted){:new_window} 		|Com essa cadeia de ferramentas de nuvem nativa, é possível usar uma amostra para criar uma loja on-line que consista em três microsserviços: uma API de Catálogo, uma API de Ordens e uma UI que chame ambas as APIs. A cadeia de ferramentas é pré-configurada para entrega contínua, controle de fonte, teste funcional, rastreamento de problemas, edição on-line e notificação de alerta. 		|
|[Cadeia de ferramentas de contêiner seguro ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fsecure-container-toolchain){:new_window} 		|Com essa cadeia de ferramentas, é possível desenvolver e implementar um app de contêiner seguro do Docker. Por padrão, a cadeia de ferramentas usa um app de amostra "Hello World" Node.js, mas é possível se vincular a seu próprio repositório GitHub, como alternativa. A cadeia de ferramentas é pré-configurada para entrega contínua com o Vulnerability Advisor, controle de fonte, rastreamento de problemas e edição on-line. 		|
|[Cadeia de ferramentas simples do Cloud Foundry ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fsimple-toolchain){:new_window}		|Com essa cadeia de ferramentas, é possível desenvolver e implementar um app Cloud Foundry. Por padrão, essa cadeia de ferramentas usa um app de amostra "Hello world" Node.js, mas é possível se vincular a seu próprio repositório GitHub, como alternativa. A cadeia de ferramentas é pré-configurada para entrega contínua, controle de fonte, rastreamento de problemas e edição on-line. 		|
|[Cadeia de ferramentas simples do Cloud Foundry (v2) ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fsimple-toolchain-hosted){:new_window}	|Com essa cadeia de ferramentas, é possível desenvolver e implementar um app Cloud Foundry. Por padrão, essa cadeia de ferramentas clona um app de amostra "Hello world" Node.js em um repositório Git hospedado pela IBM, que poderá então ser modificado. A cadeia de ferramentas é pré-configurada para entrega contínua, controle de fonte, rastreamento de problemas e edição on-line. 		|
|[Cadeia de ferramentas simples do Cloud Foundry com {{site.data.keyword.DRA_short}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fdra-toolchain-demo){:new_window}		|Com essa cadeia de ferramentas de nuvem nativa, é possível usar o {{site.data.keyword.DRA_short}} como portão da implementação de um app simples do Cloud Foundry. Por padrão, essa cadeia de ferramentas usa um app de clima Node.js de amostra ou é possível se vincular a seu próprio repositório GitHub. 		|
|[Cadeia de ferramentas simples do contêiner ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fsimple-container-toolchain){:new_window}		|Com essa cadeia de ferramentas, é possível desenvolver e implementar um app de contêiner do Docker. Por padrão, a cadeia de ferramentas usa um app de amostra "Hello World" Node.js, mas é possível se vincular a seu próprio repositório GitHub, como alternativa. A cadeia de ferramentas é pré-configurada para entrega contínua, controle de fonte, rastreamento de problemas e edição on-line. 		|
|[Delivery Insights com IBM UrbanCode Deploy ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fdeliveryinsights-toolchain){:new_window}		|Com essa cadeia de ferramentas, é possível visualizar métricas de implementação do IBM UrbanCode Deploy. Ative essa cadeia de ferramentas para se comunicar com o IBM UrbanCode Deploy, fazendo download e configurando o DevOps Connect por meio da página Configurações no {{site.data.keyword.DRA_short}}. 		|
|[Deployment Risk Analytics com GitHub e Jenkins ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fdevopsinsights-toolchain){:new_window}		|Com essa cadeia de ferramentas, é possível obter insights sobre seu processo Jenkins para integração e entrega contínuas. É possível configurar o servidor Jenkins para enviar dados para o {{site.data.keyword.DRA_short}} quando as tarefas são executadas por Jenkins. É possível também implementar portas de qualidade para bloquear implementações com base em políticas. É possível visualizar resultados no painel do Deployment Risk no {{site.data.keyword.DRA_short}}. Se você configurar um repositório GitHub para indicar o repositório de origem usado por Jenkins, a rastreabilidade de mudança ficará disponível.  		|
|[Developer Insights e Team Dynamics com GitHub e JIRA ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fdevteaminsights-toolchain){:new_window}		|Com essa cadeia de ferramentas, é possível explorar o risco de desenvolvimento de seu projeto e usar a análise de codificação social para entender os padrões de interação entre os desenvolvedores. É possível analisar o código-fonte do GitHub em conjunto com os problemas do GitHub e/ou do JIRA. Use o Developer Insights para identificar arquivos que são altamente propensos a erros e ver como o projeto obedece às práticas do DevOps. A análise de codificação social no Team Dynamics identifica o nível de interação entre os membros da equipe para que a equipe possa corrigir práticas não produtivas. 		|
|[Construir sua própria cadeia de ferramentas ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fempty-toolchain){:new_window}		|Essa cadeia de ferramentas não possui ferramentas pré-configuradas. Se você já estiver familiarizado com as cadeias de ferramentas, será possível configurar sua própria cadeia de ferramentas. 		|
{: caption="Table 2. Toolchain templates" caption-side="top"}
