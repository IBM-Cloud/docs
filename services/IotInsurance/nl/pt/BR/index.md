---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-04"
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
- Pelo menos 2 GB de memória livre devem estar disponíveis em sua organização {{site.data.keyword.Bluemix_notm}} para ativar a função Implementar.

## Implementando os serviços e os aplicativos necessários
{: #deploying_services}

1. Para implementar todos os serviços e aplicativos necessários, no [console do{{site.data.keyword.Bluemix_notm}}](https://console.ng.bluemix.net/#all-items), clique no serviço do {{site.data.keyword.iotinsurance_short}} e, em seguida, clique em **Implementar**.

  O {{site.data.keyword.iotinsurance_short}} implementa todos os serviços e aplicativos Node.js que ele requer. Ele automaticamente liga os aplicativos aos serviços.

  Cada instância de serviço usa o plano de serviço padrão. É possível fazer upgrade de qualquer plano de serviço posteriormente acessando o console do serviço. Também é possível usar uma instância existente de um serviço excluindo a nova instância e ligando manualmente a instância existente ao serviço {{site.data.keyword.iotinsurance_short}}. Para obter mais informações sobre os aplicativos, consulte [Sobre o {{site.data.keyword.iotinsurance_short}}](iotinsurance_overview.html).

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
Para ativar notificações push para um app móvel existente, opcionalmente, é possível criar uma instância do serviço {{site.data.keyword.mobilepushshort}}, vinculá-la à API {{site.data.keyword.iotinsurance_short}} e incluir um arquivo Public Key Cryptography Standards (PKCS) 12. Para obter informações sobre o app móvel, veja [Instalando e conectando o app móvel de amostra](iotinsurance_mobile_app.html). Para obter informações sobre o {{site.data.keyword.mobilepushshort}}, veja [Introdução às notificações push](https://console.ng.bluemix.net/docs/services/mobilepush/index.html).

Para configurar o serviço após a criação, execute as etapas a seguir:

  1. Abra o serviço {{site.data.keyword.mobilepushshort}}.
  2. Clique em **Configurar**.
  3. Na seção Certificado do Apple Push Notifications, faça upload do arquivo PKCS 12 para seu app móvel e insira a senha.


O que Vem a Seguir?
{: #whats_next}
Veja o que é possível fazer com o {{site.data.keyword.iotinsurance_short}}.

- Usar as instruções e APIs no Shield Toolkit para criar uma [associação de usuário e blindagem](iotinsurance_shield_toolkit.html).
<!-- - Install and connect the [sample mobile app](iotinsurance_mobile_app.html). -->
- Faça download ou visualize todas as [APIs no site GitHub ![Ícone de link externo](../../icons/launch-glyph.svg)](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/#iot-for-insurance-api-examples){:new_window}.

# Links Relacionados
{: #rellinks}

## Tutoriais e amostras
{: #samples}
* [Biblioteca de blindagens do {{site.data.keyword.iotinsurance_short}} ![Ícone de link externo](../../icons/launch-glyph.svg)](https://github.com/ibm-watson-iot/ioti-shields){: new_window}
* [Código do app móvel de amostra no GitHub ![Ícone de link externo](../../icons/launch-glyph.svg)](https://github.com/ibm-watson-iot/ioti-mobile){:new_window}

## Referência de API
{: #api}
* [API {{site.data.keyword.iotinsurance_short}} ![Ícone de link externo](../../icons/launch-glyph.svg)](https://iot4i-api-docs.mybluemix.net/){:new_window}
* [Exemplos de API {{site.data.keyword.iotinsurance_short}} ![Ícone de link externo](../../icons/launch-glyph.svg)](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/#iot-for-insurance-api-examples){:new_window}


## Links Relacionados
{: #general}
* [Documentação do {{site.data.keyword.iot_full}}](https://console.ng.bluemix.net/docs/services/IoT/index.html)
* [Fórum de suporte do desenvolvedor ![Ícone de link externo](../../icons/launch-glyph.svg)](https://developer.ibm.com/answers/search.html?f=&type=question&redirect=search%2Fsearch&sort=relevance&q=%2B[iot]%20%2B[bluemix]){:new_window}
* [Fórum de suporte do Stack overflow ![Ícone de link externo](../../icons/launch-glyph.svg)](http://stackoverflow.com/questions/tagged/ibm-bluemix){:new_window}
