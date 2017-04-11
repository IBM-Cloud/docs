---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-15"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Integrações de serviços externos
{: #ref-index}

A integração de serviços externos permite acessar dados e operações de terceiros ou serviços externos em sua organização do {{site.data.keyword.iot_full}}.

## Jasper
{: #jasper}

Jasper é uma plataforma de administração e gerenciamento para dispositivos SIM. Jasper está integrado ao painel do {{site.data.keyword.iot_short_notm}}, possibilitando a administração de dispositivos Jasper por meio do painel de sua organização do {{site.data.keyword.iot_short_notm}}.

### Operações suportadas para Jasper

A integração de Jasper integrada fornecida por nossa plataforma fornece suporte para as operações Jasper a seguir:

- Visualizar dados gerais do Jasper
  - Mostra: Status, Plano de Taxa, uso de dados mês a data, uso de SMS mês a data, uso de voz mês a data, limites excedentes, data de inclusão e data de modificação.
- Alterar estado de ativação do SIM.
  - Selecione a partir de: Inventário, Ativação Pronta, Ativado, Desativado e Obsoleto.
- Visualizar Uso de SIM
  - Mostra: data de início do ciclo, dados cobráveis e totais, SMS cobrável e total, voz cobrável e total.
  - A data de início do ciclo de pode ser configurada usando um formato DD-MM-AAAA.
- Enviar SMS para o SIM
- Alterar o plano de taxa

É possível acessar as operações suportadas no drill down de dispositivo de um dispositivo conectado Jasper após a conclusão das etapas de configuração a seguir.

### APIs de REST para Jasper
Para acessar a API de REST para Jasper, veja a seção Extensão Jasper na documentação da [API de REST HTTP do {{site.data.keyword.iot_short_notm}} ![Ícone de link externo](../../../../icons/launch-glyph.svg "Ícone de link externo")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Jasper_Extension){: new_window}.

### Configuração para Jasper

Para conectar seu serviço Jasper à sua organização do {{site.data.keyword.iot_short_notm}}, há dois estágios de configuração que devem ser executados primeiro. Primeiro, o {{site.data.keyword.iot_short_notm}} deve ser conectado a seu serviço Jasper, em seguida, seus dispositivos {{site.data.keyword.iot_short_notm}} devem ser configurados.


1. Ative a extensão Jasper. Para ativar a integração de Jasper com sua organização do {{site.data.keyword.iot_short_notm}}, conclua as etapas a seguir:
  1. No painel do {{site.data.keyword.iot_short_notm}}, selecione **Extensões**.
  2. Na página **Extensões**, clique em **Incluir extensão**.
  3. Clique em **Incluir** próximo a Jasper.
  4. Insira o nome de usuário do Jasper, senha, chave de acesso e ID do domínio.
  5. Clique em **Pronto**.

2. Configure seus dispositivos
É possível configurar os dispositivos que estão conectados à sua organização do {{site.data.keyword.iot_short_notm}} e à sua conta Jasper para exibir dados de Jasper no painel do {{site.data.keyword.iot_short_notm}}.  
**Importante:** a configuração de Jasper não pode ser aplicada como parte do processo Incluir dispositivo, apenas dispositivos conectados anteriormente podem ser configurados com Jasper.  
Para configurar seus dispositivos conectados Jasper, conclua as etapas a seguir:
 1. Na guia dispositivos do painel do {{site.data.keyword.iot_short_notm}}, localize o dispositivo conectado Jasper a ser configurado.
 2. Selecione o dispositivo para abrir a visualização *Drill down de dispositivo*.
 3. Role para baixo até *Configuração de extensão*.
 4. Insira a configuração de extensão usando o formato JSON a seguir e, em seguida, clique em **Confirmar mudanças** para salvar sua configuração.  

```json  
    {
        "jasper": {
            "iccid": "string"
        }
    }

```

Quando a organização estiver configurada com sucesso, a seção *Extensões* será exibida na seção *Configuração de extensões* na visualização *Drill down de dispositivo*.

## AT&T
{: #att}

### Operações suportadas para a AT&T

A extensão AT&T permite as operações a seguir da AT&T:

- Visualizar dados gerais da AT&T
  - Mostra: Status, Plano de Taxa, uso de dados mês a data, uso de SMS mês a data, uso de voz mês a data, limites excedentes, data de inclusão e data de modificação.
- Alterar estado de ativação do SIM.
  - Selecione a partir de: Inventário, Ativação Pronta, Ativado, Desativado e Obsoleto.
- Visualizar Uso de SIM
  - Mostra: data de início do ciclo, dados cobráveis e totais, SMS cobrável e total, voz cobrável e total.
  - A data de início do ciclo de pode ser configurada usando um formato DD-MM-AAAA.
- Enviar SMS para o SIM
- Alterar o plano de taxa

### APIs de REST para AT&T
Para acessar a API de REST para AT&T, veja a seção Extensão AT&T na documentação da [API de REST HTTP do {{site.data.keyword.iot_short_notm}} ![Ícone de link externo](../../../../icons/launch-glyph.svg "Ícone de link externo")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/AT&T_Extension){: new_window}.

### Configuração para a AT&T

Para conectar sua organização do {{site.data.keyword.iot_short_notm}} ao AT&T, deve-se concluir a configuração da organização e a configuração do dispositivo.

Para configurar sua plataforma {{site.data.keyword.iot_short_notm}}, conclua as etapas a seguir.

1. Ative a extensão da AT&T. Para ativar a integração da AT&T com sua organização do {{site.data.keyword.iot_short_notm}}, conclua as etapas a seguir:
  1. No painel do {{site.data.keyword.iot_short_notm}}, selecione **Extensões**.
  2. Na página **Extensões**, clique em **Incluir extensão**.
  3. Clique em **Incluir** ao lado de AT&T.
  4. Insira seu nome do usuário, senha, chave de acesso e ID do domínio da AT&T.
  5. Clique em **Pronto**.

Para conectar sua organização do {{site.data.keyword.iot_short_notm}} à sua conta da AT&T, há dois estágios de configuração que devem ser concluídos primeiro. Conclua a configuração da organização e, em seguida, configure seus dispositivos.


2. Configure seus dispositivos
É possível configurar os dispositivos que estão conectados à sua organização do {{site.data.keyword.iot_short_notm}} e à sua conta da AT&T para exibir dados da AT&T no painel do {{site.data.keyword.iot_short_notm}}.  
**Importante:** A configuração da AT&T não pode ser aplicada como parte do processo Incluir dispositivo, apenas dispositivos conectados anteriormente podem ser configurados com a AT&T.  
Para configurar seus dispositivos conectados ao AT&T, conclua as etapas a seguir:
 1. Na guia dispositivos do painel do {{site.data.keyword.iot_short_notm}}, localize o dispositivo conectado ao AT&T a ser configurado.
 2. Selecione o dispositivo para abrir a visualização *Drill down de dispositivo*.
 3. Role para baixo até *Configuração de extensão*.
 4. Insira a configuração de extensão usando o formato JSON a seguir e, em seguida, clique em **Confirmar mudanças** para salvar sua configuração.  

```json  
    {
        "atnt": {
            "iccid": "string"
        }
    }

```

Quando a organização estiver configurada com sucesso, a seção *Extensões* será exibida na seção *Configuração de extensões* na visualização *Drill down de dispositivo*.

## Conector ARM mbed
{: #arm}

O conector ARM mbed permite que você conecte seu dispositivo ARM mbed para seu{{site.data.keyword.iot_short_notm}}. A extensão ARM mbed permite que o portal ARM mbed e o {{site.data.keyword.iot_short_notm}} para enviar e receber dados do portal ARM mbed.

### Configuração de Instalação


1. Ative a extensão de conector ARM mbed. Para ativar a extensão de conector ARM mbed, conclua as seguintes etapas:
  1. No painel do {{site.data.keyword.iot_short_notm}}, selecione **Configurações** e navegue até **Extensões**.
  2. No menu **Extensões**, clique em **Incluir extensão**.
  3. Clique em **Incluir** próximo à extensão de conector ARM mbed.
  4. Insira sua chave de acesso e ID do domínio do ARM mbed. É possível localizá-los usando o portal ARM mbed em https://connector.mbed.com.
  5. Verifique se as credenciais estão corretas clicando no botão **Verificar conexão**.
  6. Clique em **Pronto**.

### Formato de carga útil

Há dois tipos de mensagens recebidas da plataforma ARM mbed, notificações e respostas assíncronas. O {{site.data.keyword.iot_short_notm}} pode enviar comandos para dispositivos que estão conectados à plataforma ARM mbed.

#### Notificações

As notificações são geradas por mudanças nos dados do dispositivo ou do sensor. Depois que o {{site.data.keyword.iot_short_notm}} processa a mensagem, ele é o tópico do evento de dispositivo da mesma maneira que um dispositivo conectado diretamente ao {{site.data.keyword.iot_short_notm}}. O tipo de evento usado para notificações de origem em dispositivos conectados à plataforma ARM mbed é `notify`.

A amostra de código a seguir mostra o formato de carga útil para uma notificação enviada pela API da plataforma ARM mbed

```
{
  "ep":<endpoint/deviceID>,
  "path":<resource path>,
  "ct":<content type>,
  "payload":<Base64 encoded payload>,
  "max-age":<how long the payload is valid, in seconds>
}
```

#### Respostas assíncronas

Quando o {{site.data.keyword.iot_short_notm}} envia um comando para um dispositivo conectado à plataforma ARM mbed, o dispositivo envia uma mensagem de confirmação de volta ao {{site.data.keyword.iot_short_notm}}. Essa mensagem de confirmação é chamada de *resposta assíncrona* e usa o tipo de evento `asyncResponse`.

A amostra de código a seguir mostra o formato de carga útil para uma resposta assíncrona enviada pelo serviço de nuvem ARM mbed:

```
{
  "id":<transaction id>,
  "status":<200 is command was sucessfully executed. Check other HTTP response codes>,
  "ct":<content type>,
  "max-age":<how long the payload is valid, in seconds>,
  "payload":<base64 encoded payload>,
  "ep":<endpoint/deviceID affected by the command>,
  "path":<resource path affected by the command>
}
```

#### Enviando comandos para a plataforma ARM mbed

O {{site.data.keyword.iot_short_notm}} pode enviar comandos para dispositivos conectados à plataforma ARM mbed. Os comandos enviados da plataforma ARM mbed deve usar o formato JSON a seguir.

```
{
  "method":<PUT or POST>,
  "deviceId":<endpoint/deviceId>,
  "resourceId":<resource path>,
  "payload": <Base64 encoded payload>
}
```
O método escolhido faz distinção entre maiúsculas e minúsculas. O caractere inicial '/' do caminho de recurso deve ser ignorado.


A carga útil deve ser publicada no tópico a seguir:

```
iot-2/type/<device_type>/id/<deviceId>/cmd/<command_type>/fmt/<command_format>
```


## Orange
{: #orange}

A extensão da Orange permite visualizar dados do cartão Módulo de Identidade do Assinante de dispositivos que estão conectados a seu {{site.data.keyword.iot_short_notm}} e têm um cartão Módulo de Identidade do Assinante da Orange instalado.

https://developer.ibm.com/iotplatform/2016/03/30/watson-iot-platform-integration-with-orange-beta/

### Operações suportadas para a Orange

Se você tiver um dispositivo que esteja conectado ao serviço do {{site.data.keyword.iot_short_notm}} e tenha um cartão Módulo de Identidade do Assinante da Orange, será possível usar a extensão da Orange para visualizar os dados do cartão Módulo de Identidade do Assinante a seguir:

- Número de série do SIM
- Activation status
- Última alteração do status
- Última atualização do status
- Status do Local

### APIs de REST para Orange
Para acessar a API de REST para Orange, veja a seção Extensão Orange na documentação da [API de REST HTTP do {{site.data.keyword.iot_short_notm}}![Ícone de link externo](../../../../icons/launch-glyph.svg "Ícone de link externo")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Orange_Extension){: new_window}.

### Configuração para a Orange

Para ativar a extensão da Orange:

1. No painel do {{site.data.keyword.iot_short_notm}}, selecione **Extensões**.
2. Na página **Extensões**, clique em **Incluir extensão**.
3. Clique em **Incluir** ao lado da extensão da Orange.
4. Insira seu nome do usuário e senha da Orange.
6. Clique em **Pronto**.

Após a extensão da Orange ter sido ativada, cada dispositivo com um cartão Módulo de Identidade do Assinante da Orange deverá ser configurado para exibir dados do SIM da Orange.

1. Na guia dispositivos do painel do {{site.data.keyword.iot_short_notm}}, localize o dispositivo SIM da Orange a ser configurado.
2. Selecione o dispositivo e role para baixo até *Configuração de extensão*.
3. Insira a configuração de extensão usando o formato JSON a seguir e, em seguida, clique em **Confirmar mudanças** para salvar sua configuração.

```  
    {
        "orange": {
            "serialnumber": "<serial number of Orange SIM>"
        }
    }

```
Quando a organização estiver configurada com sucesso, a seção *Extensões* será exibida na seção *Configuração de extensões* na visualização *Drill down de dispositivo*.

## Armazenamento de dados históricos
{: #historical_data}

A extensão de armazenamento de dados históricos permite localizar e configurar serviços de armazenamento de mensagens compatíveis, tais como [{{site.data.keyword.cloudantfull}}](../../cloudant_connector.html) ou [{{site.data.keyword.messagehub_full}}](../../message_hub.html) para seus dados da IoT.

## Pacotes de gerenciamento de dispositivo customizado
{: #device_mgmt}

O gerenciamento de dispositivo é um recurso principal do {{site.data.keyword.iot_short_notm}}, no entanto, ele pode ser estendido para desenvolver funcionalidade adicional. Os pacotes de gerenciamento de dispositivo customizado devem consistir em JSON válido e definir pelo menos uma ação de gerenciamento de dispositivo customizado.

Para obter mais informações sobre as funções de gerenciamento de dispositivo customizado, incluindo um exemplo do formato JSON necessário, veja [extensões customizadas de gerenciamento de dispositivo](../../devices/device_mgmt/custom_actions.html){: new_window}.

### Incluindo um pacote de gerenciamento de dispositivo customizado

Os pacotes de gerenciamento de dispositivo customizado podem ser incluídos usando o painel do {{site.data.keyword.iot_short_notm}} ou usando a API.

Para incluir um pacote de gerenciamento de dispositivo customizado usando o painel do {{site.data.keyword.iot_short_notm}}:

1. No painel do {{site.data.keyword.iot_short_notm}}, clique em **Configurações** na barra de navegação.
2. Clique em **Pacotes de gerenciamento de dispositivo customizado**.
3. Clique no botão **Incluir pacote**.
4. Selecione seu arquivo de pacote e clique em **Abrir**.

Para incluir um pacote de gerenciamento de dispositivo customizado usando a API, veja a [documentação da API do {{site.data.keyword.iot_short_notm}} ![Ícone de link externo](../../../../icons/launch-glyph.svg "Ícone de link externo")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html){: new_window}.

## Blockchain
{: #blockchain}

O {{site.data.keyword.iot_short_notm}} com blockchain permite que dispositivos IoT forneçam dados a transações de blockchain, o que armazena os dados no livro razão imutável de blockchain e usa os mesmos nas regras de negócios de contrato inteligente. O {{site.data.keyword.iot_short_notm}} mapeia dados do dispositivo para o formato de dados necessário pelo contrato inteligente de blockchain e passa os mesmos para uma malha de blockchain para armazenamento no livro razão de blockchain.

### Operações suportadas para Blockchain
- Acionar atualizações de contrato inteligente com eventos de dispositivo.
- Executar lógica de negócios do contrato inteligente para atualizar o estado do livro razão com dados de eventos do dispositivo.
- Monitorar o estado de blockchain, transações e livro razão com a UI (interface com o usuário) de monitoramento.

### Configuração para blockchain

A integração de blockchain ao {{site.data.keyword.iot_short_notm}} é uma oferta de serviços que não está ativada por padrão no {{site.data.keyword.iot_short_notm}}. Para ativar o recurso em sua organização, conclua as etapas a seguir:
 1. No painel do {{site.data.keyword.iot_short_notm}}, selecione **Extensões**.
 2. Na página **Extensões**, clique em **Incluir extensão**.
 3. Clique em **Incluir** próximo à extensão de Blockchain.
 4. No quadro Blockchain, clique em **Configurar**.
 3. Na seção **Ativar Blockchain**, clique no link **Saiba mais** para acessar a [página Oferta de serviços do IoT Blockchain ![Ícone de link externo](../../../../icons/launch-glyph.svg "Ícone de link externo")](http://www.ibm.com/internet-of-things/iot-news/announcements/private-blockchain/){: new_window}.
 4. Clique em **Instalar com kickstart seu projeto de blockchain** para preencher e enviar o formulário *Explorar o potencial de IoT e Blockchain*.  
 5. Após a aprovação de sua solicitação, a IBM entrará em contato com você para ativar a integração de blockchain para sua organização.
 6. Retorne ao painel do {{site.data.keyword.iot_short_notm}} de sua organização para concluir a configuração seguindo as etapas de [Integração de blockchain ao {{site.data.keyword.iot_short_notm}}](../../bl_blockchain_integration.html).

<!-- ## The Weather Company
{: #weathercompany}

The Weather Company extension combines weather data with your existing {{site.data.keyword.iot_short_notm}} devices. Weather data from The Weather Company appears in the device details view if an update location request has been made by using the API, or if the device has already set its location by using a device management message.

**Note:** Only managed devices can set their own locations. All unmanaged devices must have their locations set manually by using the API. For more information on setting a device location, see [Update Location requests](../../devices/device_mgmt/index.html#update-location).

### REST APIs for The Weather Company
To access the REST API for The Weather Company, see the
Device Location Weather section in the [{{site.data.keyword.iot_short_notm}} HTTP REST API ![External link icon](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Device_Location_Weather){: new_window} documentation.

### Weather Data

To view the weather data retrieved for a device location, find the device in the **Devices** pane and click it. In the detailed device view scroll down to the **Extensions** section. The following weather data is listed:

- Current weather.
- Current temperature.
- Predicted maximum and minimum temperature.
- Relative humidity.
- Pressure.
- Visibility.
- Wind speed.
- Wind direction.
- Latitude.
- Longitude.
-->

<!-- Weather data from The Weather Company extension can be retrieved by using the API. For information on the Weather Company API, see [The Weather Company API documentation ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](https://docs.internetofthings.ibmcloud.com/swagger/ext-twc.html){: new_window}. -->

## e-mail
{: #email}

Os usuários podem ser incluídos no {{site.data.keyword.iot_short_notm}} usando convites de e-mail. Para obter informações, veja [Gerenciando o acesso de usuário](../../add_users.html).

Para usar o recurso de convite por e-mail, uma extensão de e-mail deve ser configurada para usar o serviço on-line SendGrid ou um serviço de Protocolo Simples de Transporte de Correio (SMTP). A extensão também pode usar o aplicativo SendGrid {{site.data.keyword.Bluemix_notm}}.

### Serviço on-line SendGrid

Para configurar a extensão de e-mail para uso com o serviço on-line SendGrid, siga estas etapas:

1. Recupere a chave API autorizada da sua conta SendGrid on-line.
2. No painel do {{site.data.keyword.iot_short_notm}}, clique em **Extensões** na barra de navegação.
3. Na seção **E-mail**, clique em **Configurar**.
4. Selecione **SendGrid com a chave API**
5. Insira o nome e o endereço de e-mail do administrador do site e a chave API autorizada.

### Serviço SMTP

Para configurar a extensão de e-mail para uso com um serviço SMTP, siga estas etapas:

1. No painel do {{site.data.keyword.iot_short_notm}}, clique em **Extensões** na barra de navegação.
2. Na seção **E-mail**, clique em **Configurar**.
3. Selecione **SMTP**.
4. Insira os detalhes de configuração do serviço SMTP.

### Aplicativo SendGrid {{site.data.keyword.Bluemix_notm}}

Para configurar a extensão de e-mail para uso com o aplicativo SendGrid {{site.data.keyword.Bluemix_notm}}, siga estas etapas:

1. Crie um aplicativo simulado e ligue-o ao serviço SendGrid.  
Para recuperar as credenciais de configuração, inclua e ligue o serviço SendGrid a um app simulado.

 1. No painel do {{site.data.keyword.Bluemix_notm}}, clique em **Criar serviço**.
 2. Selecione o serviço SendGrid no catálogo e clique em **Criar**.
 3. No painel {{site.data.keyword.Bluemix_notm}}, inclua o aplicativo {{site.data.keyword.sdk4nodefull}}.
 4. Clique no aplicativo {{site.data.keyword.sdk4nodefull}} no painel {{site.data.keyword.Bluemix_notm}} e clique em **Ligar um serviço ou API**.
 5. Selecione o serviço SendGrid e clique em **Incluir**.
 6. O aplicativo {{site.data.keyword.sdk4nodefull}} deve agora ser estagiado novamente.
2. Prepare-se para configurar o serviço {{site.data.keyword.iot_short_notm}}.  
O {{site.data.keyword.iot_short_notm}} pode ser configurado usando o painel do {{site.data.keyword.iot_short_notm}} ou usando a API do {{site.data.keyword.iot_short_notm}}.  
 1. Clique no aplicativo {{site.data.keyword.sdk4nodefull}} no painel {{site.data.keyword.Bluemix_notm}}.
 2. Clique em **Variáveis de ambiente** na barra de navegação.
 3. Copie o JSON exibido para um arquivo de texto provisório.  
 O JSON deve ter o formato a seguir:
```
{
  "name": "SendGridServiceName",
  "label": "user-provided",
  "credentials": {
    "password": "xxx",
    "hostname": "smtp.sendgrid.net",
    "username": "username"
  }
}
```
3. Inclua os dados de configuração na organização do {{site.data.keyword.iot_short_notm}}.
 1. Abra o painel {{site.data.keyword.iot_short_notm}}.
 2. Clique em **Extensões** na barra de navegação.
 3. Clique em **Configurar** no ícone **E-mail**.
 4. Selecione **SendGrid com nome do usuário**.
 5. Insira os dados de configuração do arquivo de texto provisório.
 6. Clique em **Pronto**.
