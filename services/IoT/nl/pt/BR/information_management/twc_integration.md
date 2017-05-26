---

copyright:
years: 2016, 2017
lastupdated: "2017-03-21"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Usar dados da Weather Company com seus dispositivos
{: #weathercompany}

A integração da The Weather Company permite combinar dados de clima com os dispositivos existentes do {{site.data.keyword.iot_short_notm}}.
{:shortdesc}

Os dados de clima do Weather Company aparecem na visualização de detalhes do dispositivo se uma solicitação de localização de atualização foi feita usando a API ou se o dispositivo já tiver configurado seu local usando uma mensagem de gerenciamento de dispositivo.

**Importante:** apenas dispositivos gerenciados podem configurar suas próprias localizações. Todos os dispositivos não gerenciados devem ter seus locais configurados manualmente usando a API. Para obter mais informações sobre a configuração de um local do dispositivo, consulte [Atualizar solicitações de localização](../../devices/device_mgmt/index.html#update-location).

## APIs de REST para The Weather Company
Para acessar a API de REST da The Weather Company, veja a
seção Clima do local do dispositivo na documentação da [API de REST HTTP do {{site.data.keyword.iot_short_notm}} ![Ícone de link externo](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Device_Location_Weather){: new_window}.

## Visualizando dados meteorológicos

Para visualizar os dados de clima recuperados para um local do dispositivo:
1. Clique no dispositivo na área de janela **Dispositivos**.
2. Na visualização de dispositivo detalhada, role para baixo para a seção **Extensões**.  
Os dados de clima a seguir são listados:
 - Clima atual.
 - Temperatura atual.
 - A temperatura máxima e mínima predita.
 - Umidade relativa.
 - Pressão.
 - Visibilidade.
 - Velocidade do vento.
 - Direção do vento.
 - Latitude.
 - Longitude.

<!-- Weather data from The Weather Company extension can be retrieved by using the API. For information on the Weather Company API, see [The Weather Company API documentation ![External link icon](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/swagger/ext-twc.html){: new_window}. -->
