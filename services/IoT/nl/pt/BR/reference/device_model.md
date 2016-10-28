---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Modelo do dispositivo
{: #device_model}
Última atualização: 13 de setembro de 2016 {: .last-updated}

O modelo de dispositivo descreve as características de metadados e de gerenciamento de um dispositivo. O banco de dados de dispositivos no {{site.data.keyword.iot_full}} é a principal fonte de informações dos dispositivos. Aplicativos e dispositivos gerenciados podem enviar atualizações, incluindo mudanças de localização ou o progresso de uma atualização de firmware, para o banco de dados. Assim que essas atualizações forem recebidas pelo {{site.data.keyword.iot_short_notm}}, o banco de dados do dispositivo será atualizado e as informações estarão disponíveis para os aplicativos.

**Nota:** com a exceção da extensão de gerenciamento, o modelo de dispositivo inteiro está disponível para os dispositivos gerenciados e não gerenciados. No entanto, um dispositivo não gerenciado não pode atualizar diretamente seu modelo de dispositivo no banco de dados.

## Identificação de dispositivo
{: #device_id}

Cada dispositivo tem um atributo `typeId` e um `deviceId`. Geralmente, `typeId` representa o modelo de seu dispositivo, enquanto `deviceId` pode representar seu número de série. Em sua organização do {{site.data.keyword.iot_short_notm}}, a combinação de `typeId` e `deviceId` deve ser exclusiva para cada dispositivo.

Além disso, o {{site.data.keyword.iot_short_notm}} constrói outro identificador para cada dispositivo, que é chamado `clientId`. O `clientId` é baseado em seu `organizationId` e também nos valores de `typeId` e `deviceId` do dispositivo, além de fornecer uma maneira de identificar um dispositivo específico.

Os caracteres que podem ser usados nesses identificadores são restritos para que eles sejam compatíveis com os protocolos de comunicação e APIs (interfaces de programação de aplicativos) REST. Os identificadores de dispositivos opcionais a seguir também são usados com o protocolo de gerenciamento de dispositivo de dispositivo:


- deviceInfo.manufacturer
- deviceInfo.serialNumber
- deviceInfo.model
- deviceInfo.deviceClass
- deviceInfo.description

Para obter mais informações sobre os identificadores e descrições de seus identificadores comparativos em outros padrões de gerenciamento de dispositivo, consulte [Atributos](#attributes).


## Identificadores e tipos de dispositivo
{: #id_and_device_types}

Cada dispositivo conectado ao {{site.data.keyword.iot_short_notm}} está associado a um tipo de dispositivo. Tipos de dispositivos são grupos de dispositivos que compartilham características ou comportamento.

Um tipo de dispositivo possui um conjunto de atributos. Quando um dispositivo é incluído no {{site.data.keyword.iot_short_notm}}, os atributos em seu tipo de dispositivo são usados como um modelo substituído por atributos específicos do dispositivo. Por exemplo, o tipo de dispositivo pode ter um valor para o atributo `deviceInfo.fwVersion` que reflete a versão de firmware no momento da fabricação e esse valor seria copiado do tipo de dispositivo para os dispositivos à medida que forem incluídos. Quando um dispositivo for incluído, se o valor de `deviceInfo.fwVersion` já existir, não será substituído pelo tipo de dispositivo.

Quando um tipo de dispositivo for atualizado, somente novos dispositivos registrados herdarão modificações no modelo de tipo de dispositivo. Os dispositivos existentes de um tipo de dispositivo não serão afetados e permanecerão sem mudança.

## Atributos
{: #attributes}

A tabela a seguir mostra a lista de atributos que podem se aplicar a dispositivos no {{site.data.keyword.iot_short_notm}}. Além disso, os atributos em itálico também se aplicam a tipos de dispositivos.

- API/DMA: Pode ser atualizado por API/Agente de Gerenciamento de Dispositivo

  - R: Somente leitura
  - W: Gravação e leitura
  - A: Anexar

Atributo                        | Tipo       | Descrição                                       | API do | DMA   
------------- | ------------- | ------------- | ------------- | -------------  
 clientId                         | Cadeia     | O ID do cliente usado com conexões do MQTT          |  t  |     
 *typeId*                         | Cadeia     | Tipo de dispositivo                                       |  t  |     
 deviceId                         | Cadeia     | ID do dispositivo                                         |  t  |     
 classId                          | Cadeia     | Classe de dispositivo ("Device" ou "Gateway")           |  t  |     
 gatewayTypeId                    | Cadeia     | Digite o ID do gateway que este dispositivo está usando       |  t  |     
 gatewayId                        | Cadeia     | ID do dispositivo do gateway que este dispositivo está usando     |  t  |     
 status.alert                     | Boolean    | Especifica se o dispositivo possui um alerta                   |  Qua  |     
 *deviceInfo.serialNumber*        | Cadeia     | O número de série do dispositivo                   |  Qua  |  Qua    
 *deviceInfo.manufacturer*        | Cadeia     | O fabricante do dispositivo                    |  Qua  |  Qua   
 *deviceInfo.model*               | Cadeia     | O modelo do dispositivo                           |  Qua  |  Qua  
 *deviceInfo.deviceClass*         | Cadeia     | A classe do dispositivo                           |  Qua  |  Qua  
 *deviceInfo.description*         | Cadeia     | O nome descritivo do dispositivo                |  Qua  |  Qua  
 *deviceInfo.fwVersion*           | Cadeia     | A versão de firmware atualmente existente no dispositivo    |  Qua  |  Qua  
 *deviceInfo.hwVersion*           | Cadeia     | A versão de hardware do dispositivo                |  Qua  |  Qua  
 *deviceInfo.descriptiveLocation* | Cadeia     | A localização descritiva, como uma sala, o número de um prédio ou uma região geográfica      |  Qua  |  Qua  
 *metadata*                       | complexas    | Metadados de formato livre                                |  Qua  |  Qua  
 added.auth.id                    | Cadeia     | O ID que incluiu o dispositivo                          |  t  |     
 added.dateTime                   | Cadeia     | Data e hora ISO8601: A data e hora em que o dispositivo foi incluído |  t  |     
 refs.diag.errorCodes             | Cadeia     | O URI da extensão de diagnóstico para códigos de erro, se houver |  t  |     
 refs.diag.logs                   | Cadeia     | O URI da extensão de diagnóstico para logs, se houver        |  t  |     
 refs.location                    | Cadeia     | O URI da extensão de local, se houver             |  t  |     
 refs.mgmt                        | Cadeia     | O URI da extensão de mgmt, se houver                 |  t  |     



## Atributos estendidos
{: #extended_attributes}

Além dos atributos principais listados acima na seção Atributos, há atributos adicionais que são tratados como extensões para o modelo principal de dispositivo. Consultas simples sobre o dispositivo retornam informações do modelo de dispositivo principal, mas não das extensões. As informações das extensões devem ser solicitadas de forma específica.


Nome da extensão    | Prefixo dos atributos | Purpose      
------------- | ------------- | -------------                                         
 Diagnósticos       | diag                 | Logs de erro e informações de diagnóstico                 
 Localização          | localização             | Localização do dispositivo, possivelmente atualizado regularmente
 Gerenciamento de dispositivo | mgmt                 | Ações de gerenciamento de dispositivo, por exemplo, atualização de firmware       


### Extensão de diagnósticos


Os atributos de diagnósticos são opcionais e estão presentes apenas para dispositivos que têm informações de log de erros. Esses atributos são destinados para diagnosticar problemas do dispositivo, não para resolução de problema de conectividade com o {{site.data.keyword.iot_short_notm}}. Para recuperar as informações nesses atributos, consulte-os separadamente, pois as informações armazenadas nesses atributos podem ser muito grandes.

As informações de log de diagnóstico representam uma matriz de entradas, na qual é possível anexar entradas utilizando uma API; no entanto, isso pode causar a perda de entradas anteriores, para que os logs de diagnóstico sejam mantidos em um tamanho gerenciável. Cada entrada consiste em uma mensagem, uma indicação de gravidade, um registro de data e hora e uma matriz de bytes de dados opcional.


Atributo            | Tipo       | Descrição                                                 | API do | DMA
------------- | ------------- | ------------- | ------------- | -------------
 diag.errorCodes[]    | matriz de </br> números inteiros  | Matriz de códigos de erro                                        |  x  |  x  
 diag.log[]           | array      | Matriz de dados diagnósticos                                    |  x  |  x  
 diag.log[].message   | Cadeia     | Mensagem de diagnóstico                                          |     |     
 diag.log[].timestamp | Cadeia     | Data e hora ISO8601: A data e hora da entrada de log               |     |     
 diag.log[].logData   | Cadeia     | byte: Dados diagnósticos, codificados em base-64                      |     |     
 diag.log[].severity  | pino     | Gravidade da mensagem, 0: informativa, 1: aviso, 2: erro |     |     


### Extensão de local

Esses atributos são opcionais e estão presentes apenas para dispositivos que têm informações de local. As informações de local são armazenadas separadamente, a fim de permitir o uso de mecanismos de armazenamento mais adequados para informações dinâmicas caso as informações sejam atualizadas com frequência, por exemplo, como ocorre com dispositivos móveis.

Para soluções que colocam importância significativa em atualizações frequentes de localização, espera-se que a localização seja tratada como parte da carga útil do evento do dispositivo, permitindo taxas de atualização mais altas, armazenamento de histórico simples e análise de dados.


Atributo                 | Tipo   | Descrição                                             | API do | DMA
------------- | ------------- | ------------- | ------------- | -------------
 location.longitude        | pino | A longitude em graus decimais, utilizando WGS84                |  Qua  |  Qua  
 location.latitude         | pino | A latitude em graus decimais, utilizando WGS84                 |  Qua  |  Qua  
 location.elevation        | pino | A elevação em metros, utilizando WGS84                         |  Qua  |  Qua  
 location.measuredDateTime | Cadeia |Data e hora ISO8601: A data e hora da medida do local |  Qua  |  Qua  
 location.updatedDateTime  | Cadeia | Data e hora ISO8601: Data e hora                        |  t  |     
 location.accuracy         | pino | Precisão da posição em metros                      |  Qua  |  Qua  


### Extensão de gerenciamento de dispositivo

Os atributos `mgmt.` estão presentes somente para dispositivos gerenciados. Quando um dispositivo gerenciado se torna inativo, torna-se não gerenciado e os atributos `mgmt.` são excluídos. Os atributos `mgmt.` são configurados pelo {{site.data.keyword.iot_short_notm}} como resultado do processamento de solicitações de gerenciamento de dispositivo. Esses atributos não podem ser diretamente gravados usando a API (interface de programação de aplicativos).

Os dispositivos têm um ciclo de vida de gerenciamento que é definido por seus status como dispositivos gerenciados. O agente de gerenciamento de dispositivo no dispositivo é responsável por enviar uma solicitação Gerenciar Dispositivo usando o protocolo de gerenciamento de dispositivo. Para lidar com dispositivos extintos em grandes populações de dispositivos, um dispositivo gerenciado pode ser configurado para enviar uma solicitação Gerenciar dispositivo regularmente, permitindo que o {{site.data.keyword.iot_short_notm}} observe quando um dispositivo se tornou inativo. Para facilitar essa funcionalidade, a solicitação Gerenciar dispositivo tem um parâmetro de tempo de vida opcional. Quando o {{site.data.keyword.iot_short_notm}} recebe uma solicitação Gerenciar dispositivo com um tempo de vida, ele calcula o tempo antes do qual outra solicitação Gerenciar dispositivo é necessária e armazena o mesmo no atributo `mgmt.dormantDateTime`.


Atributo                      | Tipo    | Descrição                                            | API do | DMA
------------- | ------------- | ------------- | ------------- | -------------
 mgmt.dormant                   | Boolean | Especifica se o dispositivo ficou inativo                  |  t  |     
 mgmt.dormantDateTime           | Cadeia  | Data e hora ISO8601: A data e hora em que o dispositivo gerenciado se tornará inativo   |  t  |     
 mgmt.lastActivityDateTime      | Cadeia  | Data e hora ISO8601: A data e hora da última atividade, atualizada periodicamente    |  t  |     
 mgmt.supports.deviceActions    | Boolean | Especifica se o dispositivo suporta as ações Reinicialização e Reconfiguração de Fábrica  |  t  |     
 mgmt.supports.firmwareActions  | Boolean | Especifica se o dispositivo suporta as ações Fazer Download do Firmware e Atualização de Firmware    |  t  |     
 mgmt.firmware.version          | Cadeia  | A versão do firmware no dispositivo              |  t  |  Qua  
 mgmt.firmware.name             | Cadeia  | O nome do firmware a ser usado no dispositivo      |  t  |  Qua  
 mgmt.firmware.uri              | Cadeia  | O URI a partir do qual a imagem de firmware pode ser transferida por download |  t  |  Qua  
 mgmt.firmware.verifier         | Cadeia  | O verificador, como uma soma de verificação, para a imagem de firmware para validar sua integridade |  t  |  Qua  
 mgmt.firmware.state            | pino  | Indica o estado do download do firmware               |  t  |  Qua  
 mgmt.firmware.updateStatus     | pino  | Indica o status da atualização                     |  t  |  Qua  
 mgmt.firmware.updatedDateTime  | Cadeia  | Data e hora ISO8601: A data da última atualização                 |  t  |     
