---

 

copyright:

  years: 2015, 2016

 

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:new_window: target="_blank"}

#Desenvolvendo apps 
{: #develop-apps-IDS}

*Última atualização: 07 de dezembro de 2015*  

É possível desenvolver aplicativos usando um ambiente de desenvolvimento integrado (IDE) ou um editor de texto ou é possível usar {{site.data.keyword.jazzhub}}. 
{: shortdesc}

##Desenvolvendo aplicativos com o Bluemix DevOps Services
{: #dev_ops}

É possível usar {{site.data.keyword.jazzhub_short}}
para desenvolver, rastrear e planejar um aplicativo na nuvem e, em seguida, implementá-lo no
{{site.data.keyword.Bluemix_notm}}. É possível ir do código-fonte para um aplicativo em execução em minutos.  

{{site.data.keyword.jazzhub_short}}
fornece dois serviços: {{site.data.keyword.trackplan}} e {{site.data.keyword.deliverypipeline}}. O serviço {{site.data.keyword.trackplan}} é usado para planejamento
agile. O serviço {{site.data.keyword.deliverypipeline}} automatiza as construções e implementações. É possível localizar esses serviços no Catálogo do {{site.data.keyword.Bluemix_notm}}. Para saber mais sobre como usá-los, consulte [Introdução ao Track & Plan](../services/TrackPlan/index.html#gettingstartedtemplate) e [Introdução ao Delivery Pipeline](../services/DeliveryPipeline/index.html#getstartwithCD). 

O {{site.data.keyword.jazzhub_short}} também fornece hosting Git para controle de fonte e um Web IDE, em que é possível editar, gerenciar e implementar seu código. Em um app, ative o hosting Git clicando no link **INCLUIR GIT**, que está no canto superior direito da página Visão geral do app. Em seguida, é possível editar o código do app no Web IDE, clicando em **EDITAR CÓDIGO**. No shell do Web IDE, é possível executar comandos cf com assistência de conteúdo. Por exemplo, é possível
obter uma lista de todos os comandos do Cloud Foundry digitando o comando
a seguir:  
```
help cfo
```
{:pre}
