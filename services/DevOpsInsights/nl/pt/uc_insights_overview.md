---

copyright:
  years: 2017
lastupdated: "2017-03-31"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# Integrando o DevOps Insights ao IBM UrbanCode Deploy - visão geral
{: #uc_insights_overview}

O Delivery Insights, uma parte do {{site.data.keyword.DRA_short}}, mostra estatísticas de implementação, métricas e outras informações sobre a instalação do IBM UrbanCode Deploy. Por exemplo, ele pode mostrar gráficos de duração da implementação, sucessos e falhas, todos classificados por ambientes agrupados logicamente.
{:shortdesc}

Se você não tiver uma cadeia de ferramentas ou o {{site.data.keyword.DRA_short}}, o {{site.data.keyword.DRA_short}} deverá ser configurado primeiro:
1. No catálogo do {{site.data.keyword.Bluemix}}, clique em **{{site.data.keyword.DRA_short}}**, selecione um plano de precificação e clique em **Criar**.
1. Clique na guia **Gerenciar** e, em seguida, em **Iniciar com o Delivery Insights for UrbanCode**, clique em **Iniciar aqui**. No plano de fundo, o Delivery Insights cria uma cadeia de ferramentas para sua organização. Cadeias de ferramentas abertas são coleções de integrações de ferramentas e, nesse caso, o IBM UrbanCode Deploy e o {{site.data.keyword.DRA_short}} fazem parte da sua cadeia de ferramentas. Para obter mais informações sobre cadeias de ferramentas, veja [Trabalhando com cadeias de ferramentas](../ContinuousDelivery/toolchains_working.html).
1. Na página **Configuração do Delivery Insights**, siga as etapas para configurar o DevOps Connect e conecte os servidores IBM UrbanCode Deploy.
<!--  1. Set up a system to run DevOps Connect. See [prerequisites](uc_insights_prereqs.html).
  1. Download DevOps Connect, which is provided in a runnable JAR file.
  1. Copy the script from the **Delivery Insights Setup** page and run it. This command starts DevOps Connect with a token that allows it to connect to your organization on {{site.data.keyword.Bluemix}}.
  1. Connect your IBM UrbanCode Deploy servers to DevOps connect. See [Connecting IBM UrbanCode Deploy servers to Delivery Insights](uc_insights_connect_ucd.html). -->


Se você já tiver uma cadeia de ferramentas, siga estas etapas para incluir o Delivery Insights:
1. Se você ainda não tiver a ferramenta {{site.data.keyword.DRA_short}}, inclua-a em sua cadeia de ferramentas.
1. Na cadeia de ferramentas, clique na ferramenta {{site.data.keyword.DRA_short}}.
1. Na página **Configuração do Delivery Insights**, siga as etapas para configurar o DevOps Connect e conecte os servidores IBM UrbanCode Deploy.

Depois de ter configurado o Delivery Insights e o DevOps Connect, será possível mostrar dados de servidores IBM UrbanCode Deploy no Delivery Insights. Veja [Conectando servidores IBM UrbanCode Deploy ao Delivery Insights](uc_insights_connect_ucd.html).

<!-- 
For questions or issues, see the [questions forum](https://developer.ibm.com/answers/?community=urbancode).
--> 

![Dois gráficos dos dados demo do UrbanCode Insights](images/uc_insights_demo_data.gif)

Algumas das informações que podem ser vistas no Delivery Insights incluem:

- Estatísticas sobre implementação, incluindo a duração da implementação e o volume de implementação ao longo do tempo.
- Estatísticas sobre a taxa de falha da implementação por aplicativo e ambiente.
- Estatísticas sobre a implementação do componente, incluindo taxa de falha, tempo de implementação e duração.

## Visão geral dos sistemas

A topologia para o Delivery Insights inclui uma ou mais instalações locais do IBM UrbanCode Deploy <!-- (and optionally IBM UrbanCode Release) --> e o utilitário DevOps Connect.

O diagrama a seguir mostra uma instalação típica desses sistemas.

![Visão geral da topologia para o UrbanCode Insights, incluindo sistemas locais do cliente e o IBM Cloud Services](images/uc_insights_overview_topology_multi_ucd.png)

- Uma instalação do **IBM UrbanCode Deploy** fornece as informações sobre implementações bem-sucedidas e com falha das métricas. O IBM UrbanCode Deploy requer uma correção para se comunicar com o IBM Bluemix DevOps Connect.

<!--
- **IBM UrbanCode Release** is an optional part of the topology. You can use the environment mappings in IBM UrbanCode Release to set logical environments for reports.

-->

- **IBM Bluemix DevOps Connect**, anteriormente o IBM UrbanCode Sync Utility, coordena a comunicação entre as instalações locais do IBM UrbanCode Deploy <!-- and IBM UrbanCode Release --> e os serviços hospedados pela IBM, como o UrbanCode Insights. O DevOps Connect usa a comunicação HTTPS segura para os servidores locais e a autenticação do token para fornecer dados para o UrbanCode Insights.

  O DevOps Connect requer plug-ins para se conectar aos outros sistemas na topologia.

- O **Delivery Insights**, parte do {{site.data.keyword.DRA_short}}, fornece métricas sobre a atividade de implementação no IBM UrbanCode Deploy, incluindo os tempos de implementação e as taxas de falha, de acordo com grupos de ambientes. A autorização é controlada pelas contas do {{site.data.keyword.Bluemix}}.
