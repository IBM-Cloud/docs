---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-10-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Modelo do dispositivo
{: #device_model}

O modelo de dispositivo descreve as características de metadados e de gerenciamento de um dispositivo. O banco de dados de dispositivos no {{site.data.keyword.iot_full}} é a principal fonte de informações dos dispositivos. Aplicativos e dispositivos gerenciados podem enviar atualizações, incluindo mudanças de localização ou o progresso de uma atualização de firmware para o banco de dados do dispositivo. Assim que essas atualizações forem recebidas pelo {{site.data.keyword.iot_short_notm}}, o banco de dados será atualizado e as informações serão disponibilizadas aos aplicativos.

**Observação:** com a exceção da [extensão de gerenciamento de dispositivo](#devicemanagementextension), o modelo de dispositivo inteiro está disponível para os dispositivos gerenciados e não gerenciados. No entanto, um dispositivo não gerenciado não pode atualizar diretamente seu modelo de dispositivo no banco de dados.

## Identificação de dispositivo
{: #device_id}

Cada dispositivo tem um atributo `typeId` e um `deviceId`. Geralmente, `typeId` representa o modelo de seu dispositivo, enquanto `deviceId` pode representar seu número de série. Em sua organização {{site.data.keyword.iot_short_notm}}, a combinação de `typeId` e `deviceId` deve ser exclusiva para cada dispositivo.

Além desses atributos, o {{site.data.keyword.iot_short_notm}} constrói outro identificador para cada dispositivo. Esse identificador é chamado de `clientId`. O `clientId` é baseado em seu `organizationId` e nos valores `typeId` e `deviceId` do dispositivo. O `clientId` fornece uma maneira de identificar exclusivamente um dispositivo individual. Os caracteres que podem ser usados nesses identificadores são restritos para que eles sejam compatíveis com os protocolos de comunicação e APIs (interfaces de programação de aplicativos) REST.

Os seguintes identificadores de dispositivo opcionais também podem ser usados:

- deviceInfo.manufacturer
- deviceInfo.serialNumber
- deviceInfo.model
- deviceInfo.deviceClass
- deviceInfo.description

Para obter mais informações sobre os identificadores e descrições de seus identificadores comparativos em outros padrões de gerenciamento de dispositivo, consulte [Atributos](#attributes).


## Identificadores e tipos de dispositivo
{: #id_and_device_types}

Cada dispositivo conectado ao {{site.data.keyword.iot_short_notm}} está associado a um tipo de dispositivo. Tipos de dispositivos são grupos de dispositivos que compartilham características ou comportamentos.

Um tipo de dispositivo possui um conjunto de atributos. Quando um dispositivo é incluído no {{site.data.keyword.iot_short_notm}}, os atributos em seu tipo de dispositivo são usados como um modelo. Se o dispositivo tiver um valor, esse valor será usado. Se o dispositivo não tiver um valor, o valor do tipo de dispositivo será usado. Por exemplo, o tipo de dispositivo pode ter um valor para o atributo `deviceInfo.fwVersion`, que reflete a versão de firmware no momento da fabricação. Esse valor é copiado do tipo de dispositivo para os dispositivos quando eles são incluídos. Quando um dispositivo é incluído, se o valor `deviceInfo.fwVersion` já existe, ele não é sobrescrito.

Quando um atributo de um tipo de dispositivo é atualizado, somente novos dispositivos que estão registrados herdam as modificações feitas no modelo de tipo de dispositivo.

## Atributos
{: #attributes}

A tabela a seguir mostra a lista de atributos que podem se aplicar a dispositivos no {{site.data.keyword.iot_short_notm}}. Os atributos em itálico também se aplicam a tipos de dispositivos.

Chave:
  - API: pode ser atualizado usando APIs
  - DMA: pode ser atualizado usando o Agente de gerenciamento de dispositivo
  - R: somente leitura
  - W: Gravação e leitura
  - A: Anexar

Atributo                        | Tipo       | Descrição                                       | API do | DMA   
------------- | ------------- | ------------- | ------------- | -------------  |
 clientId                         | Cadeia     | O identificador de cliente que é usado com conexões do MQTT          |  t  |   -  
 *typeId*                         | Cadeia     | Tipo de dispositivo                                       |  t  |   -  
 deviceId                         | Cadeia     | ID do dispositivo                                         |  t  |    -
 classId                          | Cadeia     | Classe de dispositivo ("Device" ou "Gateway")           |  t  |   -  
 gatewayTypeId                    | Cadeia     | O ID de tipo do gateway que esse dispositivo está usando       |  t  |    -
 gatewayId                        | Cadeia     | O ID do dispositivo do gateway que esse dispositivo está usando     |  t  |   -  
 status.alert                     | Boolean    | Indica se o dispositivo possui um alerta                   |  Qua  |  -   
 *deviceInfo.serialNumber*        | Cadeia     | O número de série do dispositivo                   |  Qua  |  Qua    
 *deviceInfo.manufacturer*        | Cadeia     | O fabricante do dispositivo                    |  Qua  |  Qua   
 *deviceInfo.model*               | Cadeia     | O modelo do dispositivo                           |  Qua  |  Qua  
 *deviceInfo.deviceClass*         | Cadeia     | A classe do dispositivo                           |  Qua  |  Qua  
 *deviceInfo.description*         | Cadeia     | O nome descritivo do dispositivo                |  Qua  |  Qua  
 *deviceInfo.fwVersion*           | Cadeia     | A versão de firmware que se sabe atualmente que deve estar no dispositivo    |  Qua  |  Qua  
 *deviceInfo.hwVersion*           | Cadeia     | A versão de hardware do dispositivo                |  Qua  |  Qua  
 *deviceInfo.descriptiveLocation* | Cadeia     | A localização descritiva, como uma sala, o número de um prédio ou uma região geográfica      |  Qua  |  Qua  
 *metadata*                       | complexas    | Metadados de formato livre                                |  Qua  |  Qua  
 added.auth.id                    | Cadeia     | O ID que incluiu o dispositivo                          |  t  |   -  
 added.dateTime                   | Cadeia     | Data e hora ISO8601: A data e hora em que o dispositivo foi incluído |  t  |    -
 refs.diag.errorCodes             | Cadeia     | O URI da extensão de diagnósticos para códigos de erro, se presente |  t  |   -  
 refs.diag.logs                   | Cadeia     | O URI da extensão de diagnósticos para logs, se presente        |  t  |   -  
 refs.location                    | Cadeia     | O URI da extensão de local, se houver             |  t  |   -  
 refs.mgmt                        | Cadeia     | O URI de extensão de gerenciamento de dispositivo, se presente                 |  t  |    -



## Atributos estendidos
{: #extended_attributes}

Além dos atributos principais listados acima na seção Atributos, há atributos adicionais que são tratados como extensões para o modelo principal de dispositivo. Consultas simples sobre o dispositivo retornam informações do modelo de dispositivo principal, mas não das extensões. As informações das extensões devem ser solicitadas de forma específica.


Nome da extensão    | Prefixo dos atributos | Purpose      
------------- | ------------- | -------------                                         
 Diagnósticos       | diag                 | Logs de erro e informações de diagnóstico                 
 Localização          | localização             | Localização do dispositivo, possivelmente atualizado regularmente
 Gerenciamento de dispositivo | mgmt                 | Ações de gerenciamento de dispositivo, como atualização de firmware       


### Extensão de diagnósticos


Os atributos de diagnósticos são opcionais e estão presentes somente para dispositivos que têm informações de log de erros. Esses atributos são destinados para diagnosticar problemas do dispositivo, não para resolução de problemas de conectividade com o {{site.data.keyword.iot_short_notm}}. A quantidade de informações que é armazenada em atributos de diagnósticos pode ser muito grande e, portanto, deve ser especificamente consultada.

As informações de log de diagnóstico são armazenadas como uma matriz de entradas. Cada entrada consiste em uma mensagem, uma indicação de gravidade, um registro de data e hora e uma matriz de bytes de dados opcional. É possível anexar entradas usando uma API. No entanto, anexar entradas pode causar a perda das entradas mais antigas a fim de manter gerenciável o tamanho dos logs de diagnóstico.


Atributo            | Tipo       | Descrição                                                 | API do | DMA
------------- | ------------- | ------------- | ------------- | -------------
 diag.errorCodes[]    | matriz de </br> números inteiros  | Matriz de códigos de erro                                        |  x  |  x  
 diag.log[]           | array      | Matriz de dados diagnósticos                                    |  x  |  x  
 diag.log[].message   | Cadeia     | Mensagem de diagnóstico                                          |  -   |    -
 diag.log[].timestamp | Cadeia     | Data e hora ISO8601: A data e hora da entrada de log               |  -   |    -
 diag.log[].logData   | Cadeia     | byte: Dados diagnósticos, codificados em base-64                      |  -   |    -
 diag.log[].severity  | pino     | Gravidade da mensagem, 0: informativa, 1: aviso, 2: erro |  -   |    -


### Extensão de local

Os atributos de local são opcionais e estão presentes somente para dispositivos que possuem informações de localização. As informações de local são armazenadas separadamente para permitir o uso de mecanismos de armazenamento que são mais adequados para informações dinâmicas. Isso pode ser importante quando as informações são atualizadas frequentemente, por exemplo, no caso de um dispositivo móvel.

Para soluções que colocam importância significativa em atualizações frequentes de localização, espera-se que a localização seja tratada como parte da carga útil do evento do dispositivo, que permite altas taxas de atualização, armazenamento de histórico mais
simples e análise de dados.


Atributo                 | Tipo   | Descrição                                             | API do | DMA
------------- | ------------- | ------------- | ------------- | -------------
 location.longitude        | pino | A longitude em graus decimais, utilizando WGS84                |  Qua  |  Qua  
 location.latitude         | pino | A latitude em graus decimais, utilizando WGS84                 |  Qua  |  Qua  
 location.elevation        | pino | A elevação em metros usando WGS84                         |  Qua  |  Qua  
 location.measuredDateTime | Cadeia |Data e hora ISO8601: A data e hora da medida do local |  Qua  |  Qua  
 location.updatedDateTime  | Cadeia | Data e hora ISO8601: Data e hora                        |  t  |   
 location.accuracy         | pino | Precisão da posição em metros                      |  Qua  |  Qua  


### Extensão de gerenciamento de dispositivo
{: #devicemanagementextension}

Os atributos de gerenciamento estão presentes somente para dispositivos gerenciados. Quando um dispositivo gerenciado se torna inativo, ele se torna não gerenciado e o `mgmt.` é excluído. Os atributos `mgmt.` são configurados pelo {{site.data.keyword.iot_short_notm}} como resultado do processamento de solicitações de gerenciamento de dispositivo. Esses atributos não podem ser diretamente gravados usando a API (interface de programação de aplicativos).

Os dispositivos têm um ciclo de vida de gerenciamento que é definido por seus status como dispositivos gerenciados. O agente de gerenciamento de dispositivo no dispositivo é responsável por enviar uma solicitação Gerenciar dispositivo usando o protocolo de gerenciamento de dispositivo. Para lidar com dispositivos extintos em grandes populações de dispositivos, um dispositivo gerenciado pode ser configurado para enviar uma solicitação Gerenciar dispositivo regularmente. Um dispositivo gerenciado se torna inativo se essa solicitação não é enviada para o {{site.data.keyword.iot_short_notm}} para um período de tempo especificado. Para facilitar essa funcionalidade, a solicitação Gerenciar dispositivo tem um parâmetro de tempo de vida opcional. Quando o {{site.data.keyword.iot_short_notm}} recebe uma solicitação Gerenciar dispositivo que possui o conjunto de parâmetros de tempo de vida, ele calcula o tempo antes de outra solicitação Gerenciar dispositivo que é necessário e armazena-o no atributo `mgmt.dormantDateTime`.


Atributo                     | Tipo    | Descrição                             | API do | DMA
------------- | ------------- | ------------- | ------------- | -------------
 mgmt.dormant                   | Boolean | Indica se o dispositivo ficou inativo                  |  t  |  -
 mgmt.dormantDateTime           | Cadeia  | Data e hora ISO8601: A data e hora em que o dispositivo gerenciado se tornará inativo   |  t  |  -   
 mgmt.lastActivityDateTime      | Cadeia  | Data e hora ISO8601: A data e hora da última atividade, atualizada periodicamente    |  t  |    -
 mgmt.supports.deviceActions    | Boolean | Indica se o dispositivo suporta as ações Reinicialização e Reconfiguração de fábrica  |  t  |   -  
 mgmt.supports.firmwareActions  | Boolean | Indica se o dispositivo suporta as ações Fazer download do firmware e Atualização de firmware    |  t  |     -
 mgmt.firmware.version          | Cadeia  | A versão do firmware que está no dispositivo              |  t  |  Qua  
 mgmt.firmware.name             | Cadeia  | O nome do firmware que é usado no dispositivo      |  t  |  Qua  
 mgmt.firmware.uri              | Cadeia  | O URI a partir do qual a imagem de firmware pode ser transferida por download |  t  |  Qua  
 mgmt.firmware.verifier         | Cadeia  | O verificador, como uma soma de verificação para a imagem de firmware, que é usado para validar sua integridade |  t  |  Qua  
 mgmt.firmware.state            | pino  | Indica o estado do download do firmware               |  t  |  Qua  
 mgmt.firmware.updateStatus     | pino  | Indica o status da atualização                     |  t  |  Qua  
 mgmt.firmware.updatedDateTime  | Cadeia  | Data e hora ISO8601: A data da última atualização                 |  t  |    -
