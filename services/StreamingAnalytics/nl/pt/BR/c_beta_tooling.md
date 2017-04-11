---

copyright:
  years: 2015, 2017 lastupdated: "2017-02-09"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

#Ferramentas de desenvolvimento e ambiente
{: #c_beta_tooling}


Estas considerações se aplicam às ferramentas e ao ambiente usado para desenvolver seus aplicativos para o {{site.data.keyword.streaminganalyticsshort}}.{:shortdesc}


* O {{site.data.keyword.streaminganalyticsshort}} não inclui um ambiente de desenvolvimento do {{site.data.keyword.streamsshort}}
na nuvem ou o Streams Studio na nuvem. Desenvolva os seus aplicativos em um ambiente do {{site.data.keyword.streamsshort}} instalado localmente e envie-os
como pacotes configuráveis do aplicativo. Caso você não tenha o ambiente de desenvolvimento, é possível fazer download do
{{site.data.keyword.streamsshort}} Quick Start Edition, gratuitamente, na página de produto do
[{{site.data.keyword.streamsshort}}](https://www.ibm.com/analytics/us/en/technology/stream-computing/#products).
* Compile o pacote configurável do aplicativo em um ambiente do Red Hat Enterprise Linux 6.5 ou em uma versão equivalente do CentOS para assegurar
compatibilidade.
* Em seu ambiente de desenvolvimento do {{site.data.keyword.streamsshort}}, configure a variável de ambiente
`JAVA_HOME` como $STREAMS_INSTALL/java.
