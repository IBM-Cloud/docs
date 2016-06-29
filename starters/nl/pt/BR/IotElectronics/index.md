---

copyright:
  years: 2016

---

{:new_window: target="_blank"}

{:shortdesc: .shortdesc}


# Criando aplicativos com o iniciador {{site.data.keyword.iotelectronics}}
*Última atualização: 14 de junho de 2016*

{{site.data.keyword.iotelectronics_full}} é uma solução de ponta a ponta e integrada que permite que seus aplicativos se comuniquem,
controlem, analisem e atualizem dispositivos conectados. O iniciador inclui um aplicativo iniciador que permite criar e controlar dispositivos
simulados e um aplicativo móvel de amostra que permite controlar esses dispositivos a partir do seu dispositivo móvel.
{:shortdesc}

**Pré-requisito**:  
Assegure-se de ter implementado o {{site.data.keyword.iotelectronics}} Starter na seção Modelos do catálogo do Bluemix. Isso
automaticamente implementa os aplicativos do componente e os serviços do iniciador, incluindo {{site.data.keyword.amafull}}.

Para iniciar com o {{site.data.keyword.iotelectronics}}, conclua estas tarefas conforme descrito nas seções a seguir:

1. Permita comunicações com o aplicativo móvel de amostra configurando {{site.data.keyword.amashort}}.
2. Crie dispositivos simulados usando o aplicativo da web do iniciador {{site.data.keyword.iotelectronics}}.
3. Instale e conecte o aplicativo móvel de amostra.

## Configurando o {{site.data.keyword.amashort}}
{: #configureMCA}
Para usar o aplicativo móvel, deve-se configurar {{site.data.keyword.amashort}}, como a seguir:
1. Em seu painel {{site.data.keyword.Bluemix_notm}},
abra [{{site.data.keyword.amashort}}](https://new-console.ng.bluemix.net/docs/services/mobileaccess/overview.html).
2. Na seção **Customizado**, selecione **Configurar**.
3. Insira as credenciais de autenticação a seguir:
  - **Nome da região**: myRealm
  - **URL**: https://<*myIoT4eStarterApp*>.mybluemix.net  

    **Dica:** assegure-se de usar o prefixo seguro `https://` na URL. É possível localizar a URL do seu
aplicativo iniciador clicando em **Opções móveis**.)
4. Salve.

  Para obter instruções detalhadas, consulte [Configurando {{site.data.keyword.amashort}}](iotelectronics_config_mobile.html#iot4e_configureMCA)

##Criando dispositivos simulados
Para criar um dispositivo simulado, execute as etapas a seguir:
1. Em seu painel {{site.data.keyword.Bluemix_notm}}, inicie seu aplicativo {{site.data.keyword.iotelectronics}}
2. Aguarde a mensagem de status `Seu aplicativo está em execução` e, em seguida, clique em **Visualizar aplicativo**
para exibir o aplicativo iniciador.  
3. Selecione **Controlar remotamente seus dispositivos conectados**
4. Role até a seção rotulada **Em seguida, escolha ou inclua a nova lavadora simulada** e clique no botão Incluir
(+). Uma nova lavadora é criada.

## Instalando e conectando o aplicativo móvel de amostra
Para instalar e conectar o aplicativo móvel de amostra, execute as etapas a seguir:

*Nota*: deve-se ter um dispositivo iOS para usar o aplicativo móvel de amostra.

1. Em seu telefone, abra a App Store e procure `ibm iot`. Escolha **IBM IoT for Electronics** e
instale.
2. Conecte seu telefone à sua organização varrendo o código QR da Conexão localizado em seu aplicativo iniciador.
3. Conecte seu dispositivo simulado varrendo o código QR do Dispositivo localizado em seu aplicativo iniciador.

  Para obter instruções detalhadas, consulte [Conectando o aplicativo
móvel ao seu ambiente {{site.data.keyword.iotelectronics}}](iotelectronics_config_mobile.html#iot4e_connecting_mobile)

##O que vem a seguir
Consulte o que é possível fazer com o {{site.data.keyword.iotelectronics}}.

- Explore o aplicativo iniciador para obter uma experiência de como um fabricante corporativo pode monitorar os dispositivos conectados ao {{site.data.keyword.iot_short_notm}}.
- Explore o aplicativo móvel de amostra para obter uma experiência de como os proprietários do dispositivo podem se registrar e interagir
com seus dispositivos.
- Cause uma falha manualmente no dispositivo para acionar alertas, notificações e ações para o fabricante e para o proprietário do dispositivo.
- Associe os dados operacionais aos dados do usuário para entender como seus produtos e dispositivos estão operando e quem os está operando.


# Links Relacionados
{: #rellinks}
## Documentação da API
{: #api}
* [{{site.data.keyword.iotelectronics}}](http://ibmiotforelectronics.mybluemix.net/public/iot4eregistrationapi.html)
* [{{site.data.keyword.iotrtinsights_short}}](https://iotrti-prod.mam.ibmserviceengage.com/apidoc/)  
* [{{site.data.keyword.iot_short}}](https://developer.ibm.com/iotfoundation/recipes/api-documentation/)


## Componentes
{: #general}

* [{{site.data.keyword.iotelectronics_full}} documentação](iotelectronics_overview.html)
* [{{site.data.keyword.iot_full}}](https://new-console.ng.bluemix.net/docs/services/IoT/index.html)
* [{{site.data.keyword.iotrtinsights_full}}](https://new-console.ng.bluemix.net/docs/services/iotrtinsights/iotrtinsights_overview.html)
* [{{site.data.keyword.amafull}}](https://new-console.ng.bluemix.net/docs/services/mobileaccess/overview.html)
* [{{site.data.keyword.sdk4nodefull}}](https://new-console.ng.bluemix.net/docs/runtimes/nodejs/index.html#nodejs_runtime)

## Amostra
{: #samples}
* [Aplicativo móvel de
amostra](https://new-console.ng.bluemix.net/docs/starters/IotElectronics/iotelectronics_config_mobile.html)
