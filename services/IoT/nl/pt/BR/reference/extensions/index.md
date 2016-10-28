---

copyright:
  years: 2015, 2016

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Integrações de serviços externos
{: #ref-index}
Última atualização: 13 de setembro de 2016
{: .last-updated}

A integração de serviços externos permite acessar dados e operações de terceiros ou serviços externos em sua organização do {{site.date.keyword.iot_full}}.

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


### Configuração para Jasper

Para conectar seu serviço Jasper à sua organização do {{site.data.keyword.iot_short_notm}}, há dois estágios de configuração que devem ser executados primeiro. Primeiro, o {{site.data.keyword.iot_short_notm}} deve ser conectado a seu serviço Jasper, em seguida, seus dispositivos {{site.data.keyword.iot_short_notm}} devem ser configurados.


1. Ative a extensão Jasper. Para ativar a integração de Jasper com sua organização do {{site.data.keyword.iot_short_notm}}, conclua as etapas a seguir:
  1. No painel do {{site.data.keyword.iot_short_notm}}, selecione **Extensões**.
  2. Na página **Extensões**, clique em **Incluir extensão**.
  3. Clique em **Incluir** ao lado de AT&T.
  4. Insira seu nome do usuário, senha, chave de acesso e ID do domínio da AT&T.
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
**Importante:** a configuração da AT&T não pode ser aplicada como parte do processo Incluir dispositivo, apenas dispositivos conectados anteriormente podem ser configurados com a AT&T.
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

<!--
## ARM mbed connector
{: #arm}

The ARM mbed connector is an extension that allows you to connect your ARM mbed device to your {{site.data.keyword.iot_short_notm}}. The ARM mbed extension is allows the ARM mbed portal and the {{site.data.keyword.iot_short_notm}} to send and receive data from the ARM mbed portal.

### Setup Configuration


1. Enable the ARM mbed connector extension. To enable the ARM mbed connector extension complete the following steps:
  1. From the {{site.data.keyword.iot_short_notm}} dashboard, select **Settings** and navigate to **Extensions**.
  2. In the **Extensions** menu, click **Add Extension**.
  3. Click **Add** next to ARM mbed connector extension.
  4. Enter your ARM mbed access key and domain ID. You can find these by using the ARM mbed portal at https://connector.mbed.com.
  5. Check the credentials are correct by clicking the **Check Connection** button.
  6. Click **Done**.

### Payload Format

There are two types of incoming messages from the ARM mbed platform, notifications and asynchronous responses. The {{site.data.keyword.iot_short_notm}} can send commands to devices that are connected to the ARM mbed platform.

#### Notifications

Notifications are generated by changes in device or sensor data. After the {{site.data.keyword.iot_short_notm}} processes the message, it is to the device event topic in the same way as a device connected directly to the {{site.data.keyword.iot_short_notm}}. The event type used for notifications originating on devices connected to the ARM mbed platform is `notify`.

The following code sample shows the payload format for a notification sent by the ARM mbed platform API:

```
{
  "ep":<endpoint/deviceID>,
  "path":<resource path>,
  "ct":<content type>,
  "payload":<Base64 encoded payload>,
  "max-age":<how long the payload is valid, in seconds>
}
```

#### Asynchronous responses

When the {{site.data.keyword.iot_short_notm}} sends a command to a device connected to the ARM mbed platform, the device sends a confirmation message back to the {{site.data.keyword.iot_short_notm}}. This confirmation message is called an *asynchronous response* and uses the event type `asyncResponse`.

The following code sample shows the payload format for an asynchronous response sent by the ARM mbed cloud service:

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

#### Sending commands to the ARM mbed platform

The {{site.data.keyword.iot_short_notm}} can send commands to devices connected to the ARM mbed platform. Commands sent to the ARM mbed platform it must use the following JSON format.

```
{
  "method":<PUT or POST>,
  "deviceId":<endpoint/deviceId>,
  "resourceId":<resource path>,
  "payload": <Base64 encoded payload>
}
```

The payload should be published to the following topic:

```
iot-2/type/<device_type>/id/<deviceId>/cmd/<command_type>/fmt/<command_format>
```
-->

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


## Extensões de gerenciamento de dispositivo
{: #device_mgmt}

O gerenciamento de dispositivo é um recurso principal do {{site.data.keyword.iot_short_notm}}, no entanto, ele pode ser estendido para desenvolver funcionalidade adicional.

A extensão de gerenciamento de dispositivo permite instalar funções customizadas para gerenciamento de dispositivo. Para obter mais informações sobre as funções customizadas de gerenciamento de dispositivo, consulte [extensões customizadas de gerenciamento de dispositivo](../../devices/device_mgmt/custom_actions.html){: new_window}.

## Blockchain
{: #blockchain}

O {{site.data.keyword.iot_short_notm}} com blockchain permite que dispositivos IoT forneçam dados a transações de blockchain, o que armazena os dados no livro razão imutável de blockchain e usa os mesmos nas regras de negócios de contrato inteligente. O {{site.data.keyword.iot_short_notm}} mapeia dados do dispositivo para o formato de dados necessário pelo contrato inteligente de blockchain e passa os mesmos para uma malha de blockchain para armazenamento no livro razão de blockchain.

### Operações suportadas para Blockchain
- Acionar atualizações de contrato inteligente com eventos de dispositivo.
- Executar lógica de negócios do contrato inteligente para atualizar o estado do livro razão com dados de eventos do dispositivo.
- Monitorar o estado de blockchain, transações e livro razão com a UI (interface com o usuário) de monitoramento.

### Configuração para blockchain

A integração de blockchain ao {{site.data.keyword.iot_short_notm}} é uma oferta de serviços que não está ativada por padrão no {{site.data.keyword.iot_short_notm}}. Para ativar o recurso em seu ambiente, conclua as etapas a seguir:
 1. No painel do {{site.data.keyword.iot_short_notm}}, selecione **Configurações** e navegue até **Extensões**.
 2. Clique no link **Diga-me mais** ao lado da extensão Blockchain para acessar a página Oferta de serviços blockchain de IoT.
 3. Preencha e envie o formulário de solicitação de serviço.
A aprovação do serviço geralmente leva aproximadamente um dia. Após sua solicitação ser aprovada, você receberá um e-mail com instruções sobre como ativar a integração de blockchain em sua organização do {{site.data.keyword.iot_short_notm}}.
 5. Retorne ao painel do {{site.data.keyword.iot_short_notm}} de sua organização para concluir a configuração. Para obter mais informações, consulte [Integração de blcokchain ao {{site.data.keyword.iot_short_notm}}](../../bl_blockchain_integration.html).
