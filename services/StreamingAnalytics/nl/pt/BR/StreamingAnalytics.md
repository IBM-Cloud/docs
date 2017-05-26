---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-13"

---

<!-- Attribute definitions -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Sobre
{: #about}

É possível executar análise em tempo real de dados em movimento como parte do aplicativo {{site.data.keyword.Bluemix_short}} usando
o	{{site.data.keyword.streaminganalyticsfull}}.
{:shortdesc}

Novo no {{site.data.keyword.streaminganalyticsshort}}? Obtenha uma
[introdução rápida ao serviço](https://developer.ibm.com/streamsdev/docs/streaming-analytics-now-available-bluemix-2/){:new_window}.

O serviço {{site.data.keyword.streaminganalyticsshort}} fornece os recursos a seguir que permitem implementar, analisar e monitorar seus dados na nuvem:

**Uso interativo e programático do serviço:**

É possível usar o serviço interativamente por meio do console do [{{site.data.keyword.streaminganalyticsshort}}](/docs/services/StreamingAnalytics/c_streams_console.html) ou programaticamente por meio da API de REST do [{{site.data.keyword.streaminganalyticsshort}}](https://console.ng.bluemix.net/apidocs/220){:new_window}.

**Implementação e monitoramento de aplicativos SPL, Java, Scala e Python:**

É possível gravar aplicativos {{site.data.keyword.streamsshort}} em SPL, Java, Scala e Python. [Implemente e monitore esses aplicativos ](/docs/services/StreamingAnalytics/t_deploytocloud.html) usando o console {{site.data.keyword.streaminganalyticsshort}}.

Se você deseja gravar seus aplicativos em SPL, é necessário saber que o {{site.data.keyword.streamsfull}} Processing Language (SPL) é uma linguagem de programação que é usada para criar aplicativos de processamento de fluxos. Se você deseja ir além com seus próprios aplicativos SPL, é possível obter um ambiente de desenvolvimento do {{site.data.keyword.streamsshort}} e deve-se deixar seus apps SPL prontos para a nuvem.

Para criar e implementar aplicativos Python sem um ambiente de desenvolvimento do {{site.data.keyword.streamsshort}}, use nossos blocos de nota no IBM Data Science Experience (DSX) ou a API do {{site.data.keyword.streamsshort}} Python. Para obter mais informações, consulte [Desenvolvendo aplicativos Python para o {{site.data.keyword.streaminganalyticsshort}}](/docs/services/StreamingAnalytics/t_develop_apps_python.html).

**Compatibilidade com operadores do {{site.data.keyword.streamsshort}}:**

Os operadores do {{site.data.keyword.streamsshort}} no kit de ferramentas padrão do
[{{site.data.keyword.streamsshort}} Processing Language (SPL) devem ser todos
compatíveis](/docs/services/StreamingAnalytics/c_beta_adapters.html) com o {{site.data.keyword.streaminganalyticsshort}}.

## Responsabilidades do {{site.data.keyword.streaminganalyticsfull}}
{: #responsibilities notoc}

### Responsabilidades do cliente
{: #clientresponsibilities notoc}

O cliente é responsável por:

* Seguir a configuração inicial da IBM do {{site.data.keyword.streamsshort}}, monitorando, configurando e gerenciando as
tarefas do {{site.data.keyword.streamsshort}} em execução em sua instância. O cliente tem flexibilidade para iniciar e parar a instância e iniciar e parar tarefas em execução na
instância.
* Desenvolver, conforme necessário ou obrigatório, programas e aplicativos no serviço para analisar dados
e obter insights a partir dele. O cliente também é responsável pela qualidade e o desempenho de tais
programas ou aplicativos desenvolvidos. Programas podem ser desenvolvidos em SPL, Java ou outras linguagens
suportadas usando o recurso Topology do {{site.data.keyword.streamsshort}}. Eles devem ser compilados usando o {{site.data.keyword.streamsshort}}
Developer Edition ou o {{site.data.keyword.streamsshort}} Quick Start Edition com o mesmo sistema operacional que é usado para o
{{site.data.keyword.streaminganalyticsshort}}.
* Verificar o link a seguir periodicamente para ser informado sobre um tempo de inatividade planejado sem
interrupção ou com interrupção - [https://developer.ibm.com/bluemix/support/#status](https://developer.ibm.com/bluemix/support/#status){:new_window}  
* Fazer backup de todos os dados, metadados, arquivos de configuração e parâmetros de ambiente conforme os
requisitos de negócios, de forma a assegurar a continuidade.
* Restaurar dados, metadados, arquivos de configuração e parâmetros de ambiente a partir de qualquer backup
para assegurar a continuidade, em um caso de falha de qualquer tipo, incluindo, mas não se limitando, à falha de
datacenter ou pod, à falha do servidor, à falha de disco rígido ou às falhas de software.

### Responsabilidades da IBM
{: #ibmresponsibilities notoc}

Como parte do {{site.data.keyword.streaminganalyticsfull}}, a IBM irá:

* Fornecer e gerenciar servidores, armazenamento e infraestrutura de rede para a instância do Cliente.
* Fornecer uma configuração inicial do {{site.data.keyword.streamsshort}} no número de nós selecionados.
* Fornecer e gerenciar a infraestrutura da exposição dos produtos da Internet e do firewall interno quanto à proteção e ao isolamento.
* Monitorar e gerenciar os componentes a seguir no {{site.data.keyword.streaminganalyticsfull}}:
	* Componentes de Rede
	* Servidores e seu armazenamento local
	* Sistemas operacionais de infraestrutura
	* Serviços de gerenciamento do {{site.data.keyword.streamsshort}}
	* Instâncias do {{site.data.keyword.streamsshort}}
* Fornecer correções de manutenção, incluindo correções de segurança apropriadas para os sistemas operacionais de infraestrutura e o
{{site.data.keyword.streamsshort}}.
* Uma manutenção regular que não deve requerer nenhum tempo de inatividade do sistema (manutenção "sem interrupção") e uma manutenção que pode requerer alguma inatividade do sistema e o reinício (manutenção "com interrupção") serão executadas nos horários planejados, publicados em [https://developer.ibm.com/bluemix/support/#status](https://developer.ibm.com/bluemix/support/#status){:new_window}
* Qualquer mudança nos horários de manutenção planejados será postada com aviso apropriado.
