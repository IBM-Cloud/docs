---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-09"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Environnement et outils de développement
{: #c_beta_tooling}


Les considérations ci-dessous s'appliquent aux outils et à l'environnement que vous utilisez pour développer vos applications pour {{site.data.keyword.streaminganalyticsshort}}.
{:shortdesc}


* {{site.data.keyword.streaminganalyticsshort}} n'inclut pas d'environnement de développement {{site.data.keyword.streamsshort}} dans le cloud ou Streams Studio dans le cloud. Développez vos applications dans un environnement {{site.data.keyword.streamsshort}} installé localement et soumettez-les en tant que bundle d'applications. Si vous n'avez pas d'environnement de développement, vous pouvez télécharger gratuitement {{site.data.keyword.streamsshort}} Quick Start Edition, depuis la [page de produit {{site.data.keyword.streamsshort}}](https://www.ibm.com/analytics/us/en/technology/stream-computing/#products).
* Compilez le bundle d'applications dans un environnement Red Hat Enterprise Linux 6.5, ou une version CentOS équivalente, afin de garantir la compatibilité.
* Dans votre environnement de développement {{site.data.keyword.streamsshort}}, définissez la variable d'environnement `JAVA_HOME` sur $STREAMS_INSTALL/java.
