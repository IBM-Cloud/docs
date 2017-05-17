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
{:tip: .tip}

# Ativando SMS e sistema de mensagens de voz
{: #supportedcloud}

O {{site.data.keyword.iotinsurance_full}} suporta integração com o Twilio para ativar SMS e sistema de mensagens de voz. Twilio é um aplicativo de terceiros que pode ser instalado no painel do {{site.data.keyword.Bluemix_notm}}.
{: shortdesc}

## Pré-requisitos
Para ativar o sistema de mensagens de voz, deve-se ter uma conta Twilio autorizada e um número de telefone para efetuar chamadas do Twilio.
Se você usar uma conta Twilio gratuita, também deverá autorizar um número de telefone para receber chamadas ou mensagens. Para obter mais informações, consulte a
[documentação do Twilio ![ícone de
link externo](../../icons/launch-glyph.svg)](https://support.twilio.com/hc/en-us/articles/223136107-How-does-Twilio-s-Free-Trial-work-){:new_window}.

## Criando e configurando uma instância do Twilio
1. Crie uma instância do Twilio na mesma organização e espaço do {{site.data.keyword.Bluemix_notm}} em que você instalou o {{site.data.keyword.iotinsurance_short}}.
    1. Efetue login no [{{site.data.keyword.Bluemix_notm}}](https://console.ng.bluemix.net).
    2. Selecione a guia **Catálogo**.
    3. Localize a seção Móvel do catálogo de serviços e clique em **Twilio**.

    **Dica:** clique [aqui ![ícone de
link externo](../../icons/launch-glyph.svg "ícone de link externo")](https://console.ng.bluemix.net/catalog/services/twilio/){: new_window} para ir diretamente para a página do Twilio.
    {: tip}

    4. Na página do Twilio, forneça suas credenciais e ligue o aplicativo, conforme a seguir:

      1. Insira `Twilio-00` como o nome do serviço.  **Importante:** deve-se usar `Twilio-00` para se conectar com sucesso ao {{site.data.keyword.iotinsurance_short}}.

      2. Insira suas credenciais do Twilio.

      3. No menu **Conectar a**, selecione seu aplicativo iot4i-action-engine para ligar a instância do Twilio ao {{site.data.keyword.iotinsurance_short}}.

      4. Clique em **Criar**.  

    O aplicativo Twilio está instalado em seu ambiente. Uma mensagem solicita que você remonte ou reinicie seu aplicativo iot4i-action-engine para ativar a ligação. É possível reiniciar agora ou esperar até a inclusão da nova variável de ambiente na próxima etapa para reiniciar.

2. Crie uma variável de ambiente chamada TWILIO_FROM_NUMBER para o componente iot4i-action-egine.
    1. No painel do Bluemix, abra o aplicativo iot4i-action-engine.
    2. Selecione **Tempo de execução**, em seguida, clique em **Variáveis de ambiente**.
    3. Na seção **Usuário definido**, clique em **Incluir**.
    4. Na coluna Nome, insira `TWILIO_FROM_NUMBER` e, em seguida, na coluna Valor, insira seu número Twilio para voz e SMS.
    5. Clique em **Salvar**.

3. Reinicie o aplicativo Iot4i-action-engine clicando no ícone Reiniciar que está próximo ao botão Rotas.

## Incluindo as ações de SMS e de voz em uma blindagem

Para incluir recursos de SMS e de voz em uma blindagem, deve-se incluir as ações a seguir na definição de blindagem:
  - `send-sms`
  - `phone-call`

Para obter um exemplo de blindagem que contém uma lista de ações, consulte o exemplo [Criar
uma blindagem de amostra ![ícone de link externo](../../icons/launch-glyph.svg)](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/blob/master/bl/shield.js){:new_window}. No exemplo, as ações de SMS e de voz podem ser incluídas na lista de ações que contêm as ações email e pushios.

Para obter mais informações sobre a criação de blindagens, consulte [Usando o kit de ferramentas de blindagem](iotinsurance_shield_toolkit.html).
