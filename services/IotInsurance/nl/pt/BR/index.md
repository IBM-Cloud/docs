---

copyright:
  years: 2016, 2017
lastupdated: "2017-05-02"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


<!-- {{site.data.keyword.iotinsurance_full}}  {{site.data.keyword.iotinsurance_short}}  -->


# Introdução ao {{site.data.keyword.iotinsurance_short}}
{: #gettingstarted}

O {{site.data.keyword.iotinsurance_full}} é um serviço {{site.data.keyword.Bluemix_notm}} que pode ser usado para coletar, gerenciar e analisar dados de segurados conectados. O {{site.data.keyword.iotinsurance_short}} oferece a capacidade de fornecer avaliação de risco personalizada, proteção em tempo real e reduções de custo de política.
{:shortdesc}

Para que este serviço funcione, deve-se implementar os serviços e aplicativos necessários e, em seguida, configurar os serviços. Encontre
uma visão geral dos serviços e do app e um diagrama de arquitetura em [Sobre
o {{site.data.keyword.iotinsurance_short}}](iotinsurance_overview.html)

**Pré-requisitos:** antes de iniciar, assegure-se de que os pré-requisitos a seguir estejam adequados:
- Uma instância do [serviço do {{site.data.keyword.iotinsurance_short}}](https://console.ng.bluemix.net/catalog/services/iot-for-insurance/) deve existir em
seu espaço do {{site.data.keyword.Bluemix_notm}}.
- Pelo menos 2 GB de memória livre devem estar disponíveis em sua organização {{site.data.keyword.Bluemix_notm}} para ativar a função Implementar. Se você estiver fazendo upgrade de uma versão anterior, será necessário ter pelo menos 2,5 GB.

## Implementando os serviços e os aplicativos necessários
{: #deploying_services}

1. Para implementar todos os serviços e aplicativos necessários, no [console do{{site.data.keyword.Bluemix_notm}}](https://console.ng.bluemix.net/#all-items), clique no serviço do {{site.data.keyword.iotinsurance_short}} e, em seguida, clique em **Implementar**.

  O {{site.data.keyword.iotinsurance_short}} implementa todos os serviços e aplicativos Node.js que ele requer. Ele automaticamente liga os aplicativos aos serviços.

  Cada instância de serviço usa o plano de serviço padrão. É possível fazer upgrade de qualquer plano de serviço posteriormente acessando o console do serviço. Também é possível usar uma instância existente de um serviço excluindo a nova instância e ligando manualmente a instância existente ao serviço {{site.data.keyword.iotinsurance_short}}. Para obter mais informações sobre os aplicativos, consulte [Sobre o {{site.data.keyword.iotinsurance_short}}](iotinsurance_overview.html).

  **Importante:** ao implementar a versão de avaliação do {{site.data.keyword.iotinsurance_short}}, esteja ciente de que as versões grátis dos outros serviços e aplicativos que também são implementados são limitadas em sua
funcionalidade. O {{site.data.keyword.iot_short_notm}} é limitado a um máximo de 500 dispositivos e {{site.data.keyword.cloudant_short_notm}} é limitado a um GB de dados e limitou os recursos de passagem de leitura/gravação.

  **Nota**: o {{site.data.keyword.iotinsurance_short}} não implementa mais o {{site.data.keyword.amafull}} nem o {{site.data.keyword.mobilepushfull}}. Versões
anteriores do {{site.data.keyword.iotinsurance_short}} usavam o serviço {{site.data.keyword.amashort}} para processar as respostas do app móvel. Esse processo
continua a funcionar para todas as instâncias existentes do {{site.data.keyword.iotinsurance_short}}. Entretanto, deve-se criar um processo de autenticação customizado para usar o app móvel com novas instâncias do {{site.data.keyword.iotinsurance_short}}. Opcionalmente, também é possível [criar uma
instância do {{site.data.keyword.mobilepushshort}}](https://console.ng.bluemix.net/docs/services/mobilepush/index.html), configurá-la e vinculá-la
à API {{site.data.keyword.iotinsurance_short}}.

2. Verifique se o painel do {{site.data.keyword.iotinsurance_short}} está funcional e se é possível acessar as APIs.
  1. Abra o painel do {{site.data.keyword.iotinsurance_short}} clicando em
**Abrir**. Aceite as credenciais pré-preenchidas clicando em
**Login**.
  2. Retorne ao console de serviço do
{{site.data.keyword.iotinsurance_short}} e visualize as APIs clicando em
**APIs**.

  **Nota:** Após a implementação, é possível acessar o painel ou
as APIs diretamente inserindo as respectivas URLs em seu navegador. Quando você usa esse
método, deve-se inserir suas credenciais de serviço do
{{site.data.keyword.iotinsurance_short}}. Para localizar suas credenciais,
retorne ao console de serviço do {{site.data.keyword.iotinsurance_short}}. Clique
na guia **Credenciais de serviço** e, em seguida, clique em
**Visualizar credenciais**. Anote o ID do usuário e a senha.


<!--
## Configuring
{: #iot4i_configservices}



### Configuring {{site.data.keyword.amashort}}
{: #config_ama}
1. Return to your Bluemix console. All apps and services that were deployed by {{site.data.keyword.iotinsurance_short}} are displayed.

2. Copy the URL of the {{site.data.keyword.iotinsurance_short}} API application. Right-click the API application and select **Copy Link Location**.

3. Open the {{site.data.keyword.amashort}} service. The service is available in the Services section of your {{site.data.keyword.Bluemix_notm}} console.

4. Enable authentication by clicking **On**.

5. In the **Custom** section, enter the following authentication credentials:

  - **Realm name**: `IoT4I`

  - **Custom Identity Provider Url**: Paste the URL of the API application that you copied in a previous step.

  - **Your Web Application Redirect URIs**: Leave this field blank.

6. Save your settings. You can now return to the {{site.data.keyword.iotinsurance_short}} service console or your {{site.data.keyword.Bluemix_notm}} console.
-->


## Criando e configurando o {{site.data.keyword.mobilepushshort}}
{: #config_push}

(opcional) Para ativar notificações push para um app móvel existente, é possível criar opcionalmente uma instância do serviço {{site.data.keyword.mobilepushshort}}, ligá-la à API do
{{site.data.keyword.iotinsurance_short}} e incluir um arquivo de Padrões de Criptografia de Chave Pública (PKCS) 12. Para obter informações sobre o aplicativo móvel, consulte [Instalando e conectando o aplicativo móvel de amostra](iotinsurance_mobile_app.html). Para obter informações sobre o {{site.data.keyword.mobilepushshort}}, consulte [Introdução ao Push Notifications](https://console.ng.bluemix.net/docs/services/mobilepush/index.html).

Para configurar o serviço após a criação, execute as etapas a seguir:

  1. Abra o serviço {{site.data.keyword.mobilepushshort}}.
  2. Clique em **Configurar**.
  3. Na seção Certificado do Apple Push Notifications, faça upload do arquivo PKCS 12 para seu app móvel e insira a senha.

## Usando dados do Weather Company
{: #weather_company}

(opcional) O {{site.data.keyword.iotinsurance_short}} fornece um conjunto de dados estáticos do Weather Company que podem ser visualizados para propósitos de demonstração. Também é possível acessar dados ativos do Weather Company criando uma instância do serviço [{{site.data.keyword.weatherfull}}](../Weather/index.html)
e ligando-a ao app de clima {{site.data.keyword.iotinsurance_short}}.

**Importante:** a versão grátis do serviço {{site.data.keyword.weather_short}} é limitada a 10.000 solicitações. Será possível fazer upgrade para uma versão paga se você precisar de mais solicitações.

O que Vem a Seguir?
{: #whats_next}
Veja o que é possível fazer com o {{site.data.keyword.iotinsurance_short}}.

- Usar as instruções e APIs no Shield Toolkit para criar uma [associação de usuário e blindagem](iotinsurance_shield_toolkit.html).
<!-- - Install and connect the [sample mobile app](iotinsurance_mobile_app.html). -->
- Faça download ou visualize todos os [Exemplos de API no site do GitHub ![ícone de link
externo](../../icons/launch-glyph.svg)](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/#iot-for-insurance-api-examples){:new_window}.
