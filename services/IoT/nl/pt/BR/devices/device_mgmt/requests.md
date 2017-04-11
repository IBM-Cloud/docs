---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}  
{:codeblock: .codeblock}
{:pre: .pre}


# Solicitações de gerenciamento de dispositivo
{: #requests}


O {{site.data.keyword.iot_full}} fornece ações que podem ser iniciadas para um ou mais dispositivos. Essas ações podem ser iniciadas usando o painel ou a API (interface de programação de aplicativos) REST. Os tipos de ações disponíveis são **ações de dispositivo** e **ações de firmware**.

## Iniciando solicitações de gerenciamento de dispositivo usando o painel
{: #initiating-dm-dashboard}

As solicitações podem ser iniciadas por meio do painel, usando a guia **Ações** da página Dispositivos. Cliquem em **Iniciar ação** para selecionar uma ação, selecionar dispositivos e especificar parâmetros adicionais suportados pela ação selecionada.

## Iniciando solicitações de gerenciamento de dispositivo usando a API (interface de programação de aplicativos) REST
{: #initiating-dm-api}

As solicitações podem ser iniciadas usando a amostra de API (interface de programação de aplicativos) REST a seguir:  

`POST https://<org>.internetofthings.ibmcloud.com/api/v0002/mgmt/requests`

Para obter mais informações sobre o corpo de uma solicitação de gerenciamento de dispositivo, veja a [documentação da API ![Ícone de link externo](../../../../icons/launch-glyph.svg "Ícone de link externo")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html){: new_window}.

## Ações de dispositivo
{: #device-actions}

Um dispositivo pode especificar que suporta ações de dispositivo ao publicar uma solicitação de gerenciamento. Uma solicitação de ação do dispositivo indica ao {{site.data.keyword.iot_short_notm}} que o dispositivo é capaz de responder às ações de reinicialização do dispositivo e reconfiguração do dispositivo.


## Ações de dispositivo - reinicializar
{: #device-actions-reboot}

É possível iniciar a ação de reinicialização de dispositivo usando o painel do {{site.data.keyword.iot_short_notm}} ou a API (interface de programação de aplicativos) REST.

Para iniciar uma reinicialização de dispositivo usando a API (interface de programação de aplicativos) REST, emita uma solicitação de POST em:

`https://<org>.internetofthings.ibmcloud.com/api/v0002/mgmt/requests`

Forneça as seguintes informações:

- A ação `device/reboot`
- Uma lista de dispositivos para reinicializar, com no máximo 5000 dispositivos

Solicitação de reinicialização de dispositivo de exemplo:

```
{
    "action": "device/reboot",
    "devices": [
        {
            "typeId": "someType",
            "deviceId": "someId"
        }
    ]
}
```

Após uma solicitação ser iniciada, uma mensagem MQTT será publicada em todos os dispositivos especificados no corpo da solicitação de reinicialização. Para cada dispositivo, uma resposta deve ser enviada de volta para indicar se a ação de reinicialização pode ser iniciada. Se esta operação puder ser iniciada imediatamente, configure o parâmetro `rc` como `202`. Se a tentativa de reinicialização falhar, configure o parâmetro `rc` como `500` e configure o parâmetro `message` conforme necessário. Se a reinicialização não for suportada, configure o parâmetro `rc` como `501` e, como opção, configure o parâmetro `message` conforme necessário.

A ação de reinicialização estará concluída quando o dispositivo enviar uma solicitação Gerenciar dispositivo após sua reinicialização.

### Tópico para solicitação de reinicialização de dispositivo

O servidor publica uma solicitação de reinicialização em um dispositivo no tópico a seguir:

```
iotdm-1/mgmt/initiate/device/reboot
```

### Formato da mensagem para solicitação de reinicialização de dispositivo


Formato da Solicitação:

```
Incoming message from the server:

Topic: iotdm-1/mgmt/initiate/device/reboot
{
    "reqId": "string"
}
```

Formato de Resposta:

```
Outgoing message from the device:

Topic: iotdevice-1/response
{
    "rc": "response_code",
    "message": "string",
    "reqId": "string"
}
```

## Ações de dispositivo - reconfiguração do factory
{: #device-actions-factory-reset}

É possível iniciar a ação de reconfiguração de fábrica usando o painel do {{site.data.keyword.iot_short_notm}} ou a API (interface de programação de aplicativos) REST.

Para iniciar uma reconfiguração de fábrica de dispositivo usando a API (interface de programação de aplicativos) REST, emita uma solicitação de POST em:

`https://<org>.internetofthings.ibmcloud.com/api/v0002/mgmt/requests`

São fornecidas as seguintes informações:

- A ação `device/factoryReset`
- Uma lista de dispositivos para reconfigurar, com no máximo 5000 dispositivos

A amostra a seguir fornece uma solicitação de reconfiguração de dispositivo de exemplo:

```
{
    "action": "device/factoryReset",
    "devices": [
        {
            "typeId": "someType",
            "deviceId": "someId"
        }
    ]
}
```

Quando uma solicitação de dispositivo é iniciada, uma mensagem MQTT é publicada em todos os dispositivos especificados no corpo da solicitação. Para cada dispositivo, uma resposta deve ser retornada para indicar se a ação de reconfiguração de fábrica pode ser iniciada. O código de resposta será configurado como `202` se essa ação puder ser iniciada imediatamente. Se a tentativa de reconfiguração de fábrica falhar, configure o parâmetro `rc` como `500` e configure o parâmetro `message` conforme necessário. Se a ação de reconfiguração de fábrica não for suportada, configure o parâmetro `rc` como `501` e, como opção, configure o parâmetro `message` conforme necessário.

A ação de reconfiguração de fábrica estará concluída quando o dispositivo enviar uma solicitação Gerenciar dispositivo após a reconfiguração de fábrica.

### Tópico para solicitação de reconfiguração de fábrica

O servidor publica a solicitação a seguir para um dispositivo:

```
iotdm-1/mgmt/initiate/device/factory_reset
```


### Formato da mensagem para solicitação de reconfiguração de fábrica


Formato da solicitação:

```
The following topic shows the incoming message from the server:

Topic: iotdm-1/mgmt/initiate/device/factory_reset
{
    "reqId": "string"
}
```

Formato da resposta:

```
The following topic shows an outgoing message from the device:

Topic: iotdevice-1/response
{
    "rc": "response_code",
    "message": "string",
    "reqId": "string"
}
```


## Ações de firmware
{: #firmware-actions}

O nível de firmware conhecido como estando em um dispositivo é armazenado no atributo `deviceInfo.fwVersion`. Os atributos `mgmt.firmware` são usados para executar uma atualização de firmware e observar seu status.

**Importante:** o dispositivo gerenciado deve suportar a observação do atributo `mgmt.firmware` para suportar ações de firmware.

O processo de atualização de firmware é separado em ações distintas:
- Fazendo download de firmware
- Atualizando o Firmware

O status de cada ação de firmware é armazenado em um atributo separado no dispositivo. O atributo `mgmt.firmware.state` descreve o status do download de firmware. A tabela a seguir descreve os possíveis valores que podem ser configurados para o atributo `mgmt.firmware.state`:

 |Value |Status  | Significado |
 |:---|:---|:---|
 |0  | Ocioso        | O dispositivo não está fazendo download de firmware. |  
 |1  | Baixando | O dispositivo está fazendo download de firmware. |
 |2  | Transferido por Download  | O dispositivo transferiu por download uma atualização de firmware com sucesso e está pronto para instalá-la. |


O atributo `mgmt.firmware.updateStatus` descreve o status da atualização de firmware. Os possíveis valores para o atributo `mgmt.firmware.updateStatus` são:

|Value |Status | Significado |  
|:---|:---|:---|
|0 | Sucesso | O firmware foi atualizado com sucesso. |
|1 | Em progresso | A atualização de firmware foi iniciada, mas ainda não foi concluída.|
|2 | Falta de Memória | Uma condição de falta de memória foi detectada durante a operação.|
|3 | Perda de Conexão     | A conexão foi perdida durante download de firmware. |
|4 | Falha na verificação | O firmware não foi aprovado na verificação. |
|5 | Imagem não Suportada   | A imagem de firmware transferida por download não é suportada pelo dispositivo. |
|6 | URI inválido         | O dispositivo não pôde fazer download do firmware a partir do URI fornecido. |

## Ações de firmware - download
{: #firmware-actions-download}

É possível iniciar a ação de download de firmware usando o painel do {{site.data.keyword.iot_short_notm}} ou a API (interface de programação de aplicativos) REST.

Para iniciar um download de firmware usando a API (interface de programação de aplicativos) REST, emita uma solicitação de POST em:

`https://<org>.internetofthings.ibmcloud.com/api/v0002/mgmt/requests`

São fornecidas as seguintes informações:

- A ação `firmware/download`
- Uma lista de dispositivos que receberão a imagem, com no máximo 5.000 dispositivos
- O URI para a imagem de firmware (opcional)
- Sequência de verificação para validar a imagem (opcional)
- Nome do firmware (opcional)
- Versão do firmware (opcional)

A amostra a seguir mostra a solicitação de download de firmware na qual todas as mensagens de exemplo a seguir são baseadas:

```
{
   "action" : "firmware/download",
   "parameters" : [{
         "name" : "uri",
         "value" : "some uri for firmware location"
      }, {
         "name" : "name",
         "value" : "some firmware name"
      }, {
         "name" : "verifier",
         "value" : "some validation code"
      }, {
         "name" : "version",
         "value" : "some firmware version"
      }
   ],
   "devices" : [{
         "typeId" : "someType",
         "deviceId" : "someId"
      }
   ]
}
```

Se nenhum dos parâmetros opcionais for especificado, a primeira etapa no processo a seguir será ignorada.

O servidor de gerenciamento de dispositivo no {{site.data.keyword.iot_short_notm}} usa o Protocolo de gerenciamento de dispositivo para enviar uma solicitação aos dispositivos, o que inicia o download de firmware. O processo de download consiste nas etapas a seguir:

1. Uma solicitação de atualização de detalhes de firmware é enviada no tópico `iotdm-1/device/update`.
A solicitação de atualização permite que o dispositivo valide se o firmware solicitado difere do firmware atualmente instalado. Se houver uma diferença, configure o parâmetro `rc` como `204`, o que se traduz no status `Changed`.  
O exemplo a seguir mostra qual mensagem esperar para a solicitação de download de firmware de exemplo enviada anteriormente e qual resposta será enviada quando uma diferença for detectada:
```
   Incoming request from the {{site.data.keyword.iot_short_notm}}:

   Topic: iotdm-1/device/update
   Message:
   {
      "reqId" : "f38faafc-53de-47a8-a940-e697552c3194",
      "d" : {
         "fields" : [{
               "field" : "mgmt.firmware",
               "value" : {
                  "version" : "some firmware version",
                  "name" : "some firmware name",
                  "uri" : "some uri for firmware location",
                  "verifier" : "some validation code",
                  "state" : 0,
                  "updateStatus" : 0,
                  "updatedDateTime" : ""
               }
            }
         ]
      }
   }

   Outgoing response from device:

   Topic: iotdevice-1/response
   Message:
   {
      "rc" : 204,
      "reqId" : "f38faafc-53de-47a8-a940-e697552c3194"
   }
   ```
   Essa resposta aciona a próxima solicitação.
2. É enviada a solicitação de observação para o status de download de firmware `iotdm-1/observe`.
A solicitação de observação verificar se o dispositivo está pronto para iniciar o download de firmware. Quando o download pode ser iniciado imediatamente, configure o parâmetro `rc` como `200` (`Ok`), o atributo `mgmt.firmware.state` como `0` (`Idle`) e o atributo `mgmt.firmware.updateStatus` como `0` (`Idle`). O código a seguir é uma troca de exemplo entre o {{site.data.keyword.iot_short_notm}} e o dispositivo:
   ```
   Incoming request from the {{site.data.keyword.iot_short_notm}}:

   Topic: iotdm-1/observe
   Message:
   {
      "reqId" : "909b477c-cd37-4bee-83fa-1d568664fbe8",
      "d" : {
         "fields" : [ {
            "field" : "mgmt.firmware"
            }
         ]
      }
   }

   Outgoing response from device:

   Topic: iotdevice-1/response
   Message:
   {
      "rc" : 200,
      "reqId" : "909b477c-cd37-4bee-83fa-1d568664fbe8"
   }
   ```
Essa troca aciona a última etapa.  

3. A solicitação de download é enviada no tópico `iotdm-1/mgmt/initiate/firmware/download`:

   A solicitação de download informa um dispositivo para iniciar o download de firmware. Se a ação puder ser iniciada imediatamente, configure o parâmetro `rc` como `202`. O código a seguir fornece um
exemplo da iniciação de uma solicitação de download:

   ```
   Incoming request from the {{site.data.keyword.iot_short_notm}}:

   Topic: iotdm-1/mgmt/initiate/firmware/download
   Message:
   {
      "reqId" : "7b244053-c08e-4d89-9ed6-6eb2618a8734"
   }

   Outgoing response from device:

   Topic: iotdevice-1/response
   Message:
   {
      "rc" : 202,
      "reqId" : "7b244053-c08e-4d89-9ed6-6eb2618a8734"
   }
   ```

Após um download de firmware ser iniciado dessa maneira, o dispositivo precisa relatar o status do download para o {{site.data.keyword.iot_short_notm}}. O dispositivo relata o status publicando uma mensagem no tópico `iotdevice-1/notify`, em que o atributo `mgmt.firmware.state` está configurado para atributo `1` (`Downloading`) ou `2` (`Downloaded`).
As amostras a seguir mostram um exemplo da iniciação do download de firmware:

```
Outgoing message from device:

Topic: iotdevice-1/notify
Message:
{
   "reqId" : "123456789",
   "d" : {
      "fields" : [ {
         "field" : "mgmt.firmware",
         "value" : {
                 "state" : 1
             }
      } ]
   }
}


Wait some time...


Outgoing message from device:

Topic: iotdevice-1/notify
Message:
{
   "reqId" : "1234567890",
   "d" : {
      "fields" : [ {
         "field" : "mgmt.firmware",
         "value" : {
                 "state" : 2
             }
      } ]
   }
}
```



Após a notificação ser publicada com o atributo `mgmt.firmware.state` configurado como `2`, uma solicitação é acionada no tópico `iotdm-1/cancel`. Essa solicitação cancela a observação do atributo `mgmt.firmware`.
Após uma resposta que tenha o parâmetro `rc` configurado como `200` ser enviada, o download de firmware estará concluído. O
seguinte código fornece um exemplo:

```
Incoming request from the {{site.data.keyword.iot_short_notm}}:

Topic: iotdm-1/cancel
Message:
{
   "reqId" : "d9ca3635-64d5-46e2-93ee-7d1b573fb20f",
   "d" : {
      "fields" : [{
            "field" : "mgmt.firmware"
         }
      ]
   }
}


Outgoing message from device:

Topic: iotdevice-1/response
Message:
{
   "rc" : 200,
   "reqId" : "d9ca3635-64d5-46e2-93ee-7d1b573fb20f"
}
```

As informações a seguir são úteis para manipulação de erros:

- Se o atributo `mgmt.firmware.state` não for `0` ("Idle"), envie um erro que possua o código de resposta `400` e um texto de mensagem opcional.
- Se o atributo `mgmt.firmware.uri` não estiver configurado ou não for um URI válido, configure o parâmetro `rc` como `400`.
- Se a tentativa de download de firmware falhar, configure o parâmetro `rc` como `500` e, como opção, configure o parâmetro `message` conforme necessário.
- Se o download de firmware não for suportado, configure o parâmetro `rc` como `500` e, como opção, configure o parâmetro `message` conforme necessário.
- Quando uma solicitação de execução for recebida pelo dispositivo, mude o atributo `mgmt.firmware.state` de `0` (Idle) para `1` (Downloading).
- Quando o download tiver sido concluído com sucesso, configure o atributo `mgmt.firmware.state` como `2` (Transferido por download).
- Se ocorrer um erro durante o download, configure o atributo `mgmt.firmware.state` como `0` (Idle) e configure o atributo `mgmt.firmware.updateStatus` como um dos valores de status de erro a seguir:
  - 2 (Falta de Memória)
  - 3 (Perda de Conexão)
  - 6 (URI Inválido)
- Se um verificador de firmware tiver sido configurado, o dispositivo tenta verificar a imagem de firmware. Se a verificação de imagem falhar, configure o atributo `mgmt.firmware.state` como `0` (Idle) e configure o atributo `mgmt.firmware.updateStatus` como o valor de status de erro `4` (Verification Failed).

## Ações de Firmware - Atualizar
{: #firmware-actions-update}

A instalação do firmware transferido por download é iniciada usando a API (interface de programação de aplicativos) REST emitindo uma solicitação de POST em:

`https://<org>.internetofthings.ibmcloud.com/api/v0002/mgmt/requests`

São fornecidas as seguintes informações:

- A ação `firmware/update`
- A lista de dispositivos que receberão a imagem, todos do mesmo tipo de dispositivo.
- O URI para a imagem de firmware (opcional)
- Sequência de verificação para validar a imagem (opcional)
- Nome do firmware (opcional)
- Versão do firmware (opcional)

O código a seguir é uma solicitação de exemplo:

```
   {
      "action" : "firmware/update",
      "devices" : [{
            "typeId" : "someType",
            "deviceId" : "someId"
         }
      ]
   }

```

Se algum dos parâmetros opcionais for especificado, a primeira mensagem recebida pelo dispositivo será uma solicitação de atualização de dispositivo. Essa solicitação de atualização de dispositivo é semelhante à primeira mensagem da solicitação de download de firmware.

Para monitorar o status da atualização de firmware, o {{site.data.keyword.iot_short_notm}} primeiro aciona uma solicitação de observador no tópico `iotdm-1/observe`. Quando o dispositivo estiver pronto para iniciar o processo de atualização, ele envia uma resposta que tem o parâmetro `rc` configurado como `200`, o atributo `mgmt.firmware.state` configurado como `0` e o atributo `mgmt.firmware.updateStatus` configurado como `0`.

O
seguinte código fornece um exemplo:

```
Incoming request from the {{site.data.keyword.iot_short_notm}}:

Topic: iotdm-1/observe
Message:
{
   "reqId" : "909b477c-cd37-4bee-83fa-1d568664fbe8",
   "d" : {
      "fields" : [
         {
            "field": "mgmt.firmware"
         }
      ]
   }
}

Outgoing response from device:

Topic: iotdevice-1/response
Message:
{
   "rc" : 200,
   "reqId" : "909b477c-cd37-4bee-83fa-1d568664fbe8",
   "d" : {
      "fields" : [{
            "field" : "mgmt.firmware",
            "value" : {
               "state" : 0,
               "updateStatus" : 0
            }
         }
      ]
   }
}
```



Após a atualização de firmware ser transferida por download com sucesso, o servidor de gerenciamento de dispositivo no {{site.data.keyword.iot_short_notm}} usa o Protocolo de gerenciamento de dispositivo para solicitar que os dispositivos especificados iniciem a instalação de firmware usando o tópico `iotdm-1/mgmt/initiate/firmware/update`.
Se esta operação puder ser iniciada imediatamente, configure o parâmetro `rc` como `202`.
Se o firmware não tiver sido transferido por download anteriormente com sucesso, configure o parâmetro `rc` como `400`.

O código a seguir mostra um exemplo:

```
Incoming request from the {{site.data.keyword.iot_short_notm}}:

Topic: iotdm-1/mgmt/initiate/firmware/update
Message:
{
   "reqId" : "7b244053-c08e-4d89-9ed6-6eb2618a8734"
}

Outgoing response from device:

Topic: iotdevice-1/response
Message:
{
   "rc" : 202,
   "reqId" : "7b244053-c08e-4d89-9ed6-6eb2618a8734"
}
```

Para concluir a solicitação de atualização de firmware, o dispositivo relata seu status de atualização para o {{site.data.keyword.iot_short_notm}} usando uma mensagem de status publicada em seu tópico`iotdevice-1/notify`.
Quando uma atualização de firmware for concluída, o atributo `mgmt.firmware.updateStatus` será configurado como `0` (Success), o atributo `mgmt.firmware.state` será configurado como `0` (Idle). A imagem de firmware transferida por download poderá então ser excluída do dispositivo e o atributo `deviceInfo.fwVersion` será configurado para o valor do atributo `mgmt.firmware.version`.

O código a seguir fornece um exemplo de uma mensagem de notificação:

```
Outgoing message from device:

Topic: iotdevice-1/notify
Message:
{
   "d" : {
      "fields": [
         {
            "field" : "mgmt.firmware",
            "value" : {
               "state" : 0,
               "updateStatus" : 0
            }
         }
      ]
   }
}
```

Quando o {{site.data.keyword.iot_short_notm}} recebe notificação de uma atualização de firmware concluída, ele aciona uma última solicitação no tópico `iotdm-1/cancel` para cancelar a observação do atributo `mgmt.firmware`.


Quando uma resposta que tem o parâmetro `rc` configurado como `200` é enviada, a solicitação de atualização de firmware estará concluída, conforme mostrado no exemplo a seguir:

```
Incoming request from the {{site.data.keyword.iot_short_notm}}:

Topic: iotdm-1/cancel
Message:
{
   "reqId" : "d9ca3635-64d5-46e2-93ee-7d1b573fb20f",
   "d" : {
      "fields" : [
         {
            "field" : "mgmt.firmware"
         }
      ]
   }
}


Outgoing message from device:

Topic: iotdevice-1/response
Message:
{
   "rc" : 200,
   "reqId" : "d9ca3635-64d5-46e2-93ee-7d1b573fb20f"
}
```

A lista a seguir fornece algumas informações úteis para manipulação de erros e processos:

- Se a tentativa de atualização de firmware falhar, configure o parâmetro `rc` como `500` e, opcionalmente, configure o parâmetro `message` para conter informações relevantes.
- Se a atualização de firmware não for suportada, configure o parâmetro `rc` como `501` e, opcionalmente, configure o parâmetro `message` para conter informações relevantes.
- Se o atributo `mgmt.firmware.state` não for igual a `2` (transferido por download), envie um erro que tenha o parâmetro `rc` configurado como `400` e um texto da mensagem opcional.
- Caso contrário, configure o atributo `mgmt.firmware.updateStatus` como `1` (em andamento) e a instalação de firmware geralmente será iniciada.
- Se a instalação do firmware falhar, configure o atributo `mgmt.firmware.updateStatus` como um dos valores a seguir:
  - `2` (sem memória)
  - `5` (imagem não suportada)


**Importante:** todos os parâmetros listados como parte do atributo `mgmt.firmware` devem ser configurados ao mesmo tempo para que se houver uma observação atual para `mgmt.firmware`, apenas uma única mensagem de notificação será enviada.

## Orientações sobre ações de dispositivo e ações de firmware

As orientações a seguir demonstram o fluxo completo que é necessário para executar ações de dispositivo e de firmware.

- [Gerenciamento de dispositivo no WIoT Platform – Recuperação e Reconfiguração do factory ![Ícone de link externo](../../../../icons/launch-glyph.svg "Ícone de link externo")](https://developer.ibm.com/recipes/tutorials/device-management-in-wiot-platform-roll-back-factory-reset/){: new_window}

- [Atualização de firmware iniciada pelo dispositivo ![Ícone de link externo](../../../../icons/launch-glyph.svg "Ícone de link externo")](https://developer.ibm.com/recipes/tutorials/device-management-in-wiot-platform-device-initiated-firmware-upgrade/){: new_window}

- [Atualização de firmware iniciada pela plataforma ![Ícone de link externo](../../../../icons/launch-glyph.svg "Ícone de link externo")](https://developer.ibm.com/recipes/tutorials/device-management-in-wiot-platform-platform-initiated-firmware-upgrade/){: new_window}

- [Atualização de firmware iniciada pela plataforma com execução de plano de fundo ![Ícone de link externo](../../../../icons/launch-glyph.svg "Ícone de link externo")](https://developer.ibm.com/recipes/tutorials/device-management-in-wiot-platform-platform-initiated-firmware-upgrade/){: new_window}

- [Recuperação de firmware e Reconfiguração do factory ![Ícone de link externo](../../../../icons/launch-glyph.svg "Ícone de link externo")](https://developer.ibm.com/recipes/tutorials/device-management-in-wiot-platform-roll-back-factory-reset/){: new_window}
