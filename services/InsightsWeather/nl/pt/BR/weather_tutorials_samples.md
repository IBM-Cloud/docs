---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Exemplos:
{: #tutorials_samples}

*Última atualização: 06 de abril de 2016*

Aprenda a usar o serviço Insights for Weather com os exemplos a seguir.
{: shortdesc}

## Demo do Insights for Weather
{: #insights_weather_demo}

É possível usar um aplicativo de amostra para visualizar dados de clima usando o serviço Insights for Weather.
O aplicativo é acessível navegando para [http://insights-for-weather-demo.mybluemix.net/](http://insights-for-weather-demo.mybluemix.net/).
O aplicativo é aberto no navegador e pergunta se o Cliente deseja
compartilhar sua localização atual com o aplicativo.

No aplicativo de amostra, é possível ver as condições atuais
observadas para o tempo em sua
localização.

![Imagem da tela principal com observações atuais para Ottawa, ON.](images/twctestapp_main_screen.jpg "Imagem da tela principal com observações atuais para Ottawa, ON.")

Também é possível ver a previsão de hora em hora para as
próximas 24 horas e a previsão diária para os próximos 10 dias.
Se
você passar o mouse sobre cada uma dessas áreas na amostra, poderá
ver os resultados da chamada API em formato JSON, que inclui os
metadados que foram usados para recuperar os dados.

No aplicativo demo, clique em **Implementar no Bluemix** para criar uma versão clonada do aplicativo
ou [clone o app diretamente do GitHub](https://github.com/IBM-Bluemix/insights-for-weather-demo).

## Obtendo uma previsão padrão de 10 dias
{: #getting_ten_day_forecast}

É possível emitir uma operação `GET` em seu aplicativo para recuperar os dados da previsão de 10 dias.
Por exemplo, é possível usar a solicitação `GET` a seguir para recuperar a previsão de 10 dias para Ottawa, ON, Canadá:

```
GET https://<username>:<password>@twcservice.mybluemix.net:443/api/weather/v2/forecast/daily/10day?units=m&geocode=45.42%2C75.69&language=en-US
}
```

O `nome do usuário` e
`senha` são exclusivos para seu aplicativo
e instância de serviço.
É possível localizar essas informações nas variáveis de ambiente do `VCAP_SERVICES`.

O serviço retorna respostas em formato JSON. Se a resposta for
bem-sucedida, um código de status de 200 é retornado.
Se a resposta
for malsucedida, um código de erro é retornado.

O corpo da resposta inclui metadados e uma matriz de previsões
diárias para cada um dos próximos 10 dias.
Por exemplo, os metadados
podem conter os dados a seguir:

```
{
  "metadata" : {
    "language": "en-US",
    "transaction_id": "1443712484194:-1546029161",
    "version": "1",
    "latitude": 45.42,
    "longitude": 75.69,
    "units": "m",
    "expire_time_gmt": 1443714284,
    "status_code": 200
  },
  "forecasts": [
  ]
}
```

Cada previsão diária contém informações gerais que se aplicam ao período de 24 horas do dia especificado da semana (`dow`).
Por
exemplo, a previsão diária pode conter os dados a seguir:

```
    {
      "class": "fod_long_range_daily",
      "expire_time_gmt": 1443714284,
      "fcst_valid": 1444525200,
      "fcst_valid_local": "2015-10-11T07:00:00+0600",
      "num": 11,
      "max_temp": 14,
      "min_temp": 4,
      "torcon": null,
      "stormcon": null,
      "blurb": null,
      "blurb_author": null,
      "lunar_phase_day": 28,
      "dow": "Sunday",
      "lunar_phase": "Waning Crescent",
      "lunar_phase_code": "WNC",
      "sunrise": "2015-10-11T07:07:25+0600",
      "sunset": "2015-10-11T18:19:57+0600",
      "moonrise": "2015-10-11T05:17:47+0600",
      "moonset": "2015-10-11T17:40:49+0600",
      "qualifier_code": null,
      "qualifier": null,
      "narrative": "Times of sun and clouds. Highs 13 to 15C and lows 3 to 5C.",
      "qpf": 0,
      "snow_qpf": 0,
      "snow_range": "",
      "snow_phrase": "",
      "snow_code": "",
      "night": {
      },
      "day": {
      }
    }
```

Cada previsão diária contém uma parte da noite e uma parte do dia para o dia da semana especificado.
Por exemplo, ambas as partes podem conter os
dados de previsão a seguir:

```
      "night": {
        "fcst_valid": 1444568400,
        "fcst_valid_local": "2015-10-11T19:00:00+0600",
        "day_ind": "N",
        "thunder_enum": 0,
        "daypart_name": "Sunday night",
        "long_daypart_name": "Sunday night",
        "alt_daypart_name": "Sunday night",
        "thunder_enum_phrase": "No thunder",
        "num": 21,
        "temp": 4,
        "hi": 10,
        "wc": 3,
        "pop": 10,
        "icon_extd": 2900,
        "icon_code": 29,
        "wxman": "wx1650",
        "phrase_12char": "P Cloudy",
        "phrase_22char": "Partly Cloudy",
        "phrase_32char": "Partly Cloudy",
        "subphrase_pt1": "Partly",
        "subphrase_pt2": "Cloudy",
        "subphrase_pt3": "",
        "precip_type": "precip",
        "rh": 65,
        "wspd": 10,
        "wdir": 98,
        "wdir_cardinal": "E",
        "clds": 40,
        "pop_phrase": "",
        "temp_phrase": "Low 4C.",
        "accumulation_phrase": "",
        "wind_phrase": "Winds E at 10 to 15 km/h.",
        "shortcast": "Partly cloudy",
        "narrative": "A few clouds. Low 4C. Winds E at 10 to 15 km/h.",
        "qpf": 0,
        "snow_qpf": 0,
        "snow_range": "",
        "snow_phrase": "",
        "snow_code": "",
        "vocal_key": "D22:DA05:X3000300044:S300042:TL4:W04R02",
        "qualifier_code": null,
        "qualifier": null,
        "uv_index_raw": 0,
        "uv_index": 0,
        "uv_warning": 0,
        "uv_desc": "Low",
        "golf_index": null,
        "golf_category": ""
      },
```

## Obtendo uma previsão padrão de 24 horas
{: #getting_twenty_four_hour_forecast}

É possível emitir uma operação `GET` em seu aplicativo para recuperar os dados da previsão de 24 horas.
Por exemplo, é possível usar a solicitação `GET` a seguir para recuperar a previsão de 24 horas para Ottawa, ON, Canadá:

```
GET https://<username>:<password>@twcservice.mybluemix.net:443/api/weather/v2/forecast/hourly/24hour?units=m&geocode=45.42%2C75.69&language=en-US
```

O corpo da resposta inclui os metadados e uma matriz de previsões
de hora em hora para cada uma das próximas 24 horas. Por exemplo, os metadados
podem conter os dados a seguir:

```
{
  "metadata": {
    "language": "en-US",
    "transaction_id": "1443722945280:-1956318185",
    "version": "1",
    "latitude": 45.42,
    "longitude": 75.69,
    "units": "m",
    "expire_time_gmt": 1443723545,
    "status_code": 200
  },
  "forecasts": [
  ]
}
```

Cada previsão de hora em hora contém informações gerais que se aplicam à hora
especificada por `num`. Por
exemplo, a previsão de hora em hora pode conter os dados a seguir:

```
    {
      "class": "fod_short_range_hourly",
      "expire_time_gmt": 1443723545,
      "fcst_valid": 1443726000,
      "fcst_valid_local": "2015-10-02T01:00:00+0600",
      "num": 1,
      "day_ind": "N",
      "temp": 12,
      "dewpt": 1,
      "hi": 12,
      "wc": 11,
      "feels_like": 11,
      "icon_extd": 3100,
      "wxman": "wx1550",
      "icon_code": 31,
      "dow": "Friday",
      "phrase_12char": "Clear",
      "phrase_22char": "Clear",
      "phrase_32char": "Clear",
      "subphrase_pt1": "Clear",
      "subphrase_pt2": "",
      "subphrase_pt3": "",
      "pop": 0,
      "precip_type": "rain",
      "qpf": 0,
      "snow_qpf": 0,
      "rh": 48,
      "wspd": 15,
      "wdir": 208,
      "wdir_cardinal": "SSW",
      "gust": null,
      "clds": 17,
      "vis": 16.1,
      "mslp": 1018.6,
      "uv_index_raw": 0,
      "uv_index": 0,
      "uv_warning": 0,
      "uv_desc": "Low",
      "golf_index": null,
      "golf_category": "",
      "severity": 1
    },
```

## Obtendo as condições atuais
{: #current_conditions}

É possível emitir uma operação `GET` em seu aplicativo para recuperar as condições climáticas atuais.
Por exemplo, é possível usar a solicitação `GET` a seguir para recuperar as condições atuais para Ottawa, ON, Canadá:

```
GET https://<username>:<password>@twcservice.mybluemix.net:443/api/weather/v2/observations/current?units=m&geocode=45.42%2C75.69&language=en-US
```

O corpo da resposta inclui os metadados e os dados de clima
atuais observados.
Por exemplo, os metadados
podem conter os dados a seguir:

```
{
  "metadata": {
    "language": "en-US",
    "transaction_id": "1443724606672:1993259329",
    "version": "1",
    "latitude": 45.42,
    "longitude": 75.69,
    "units": "m",
    "expire_time_gmt": 1443725206,
    "status_code": 200
  },
  "observation": {
  }
}
```

Os dados de observação contêm informações gerais e valores
específicos para as unidades de medida. Por exemplo, as condições atuais contêm os seguintes dados se as
unidades de medida foram especificadas como métrica:

```
  "observation": {
    "class": "observation",
    "expire_time_gmt": 1443725206,
    "obs_time": 1443724606,
    "obs_time_local": "2015-10-02T00:36:46+0600",
    "wdir": 210,
    "icon_code": 33,
    "icon_extd": 3300,
    "sunrise": "2015-10-02T06:55:47+0600",
    "sunset": "2015-10-02T18:36:42+0600",
    "day_ind": "N",
    "uv_index": 0,
    "uv_warning": 0,
    "wxman": "wx1550",
    "obs_qualifier_code": null,
    "ptend_code": 2,
    "dow": "Friday",
    "wdir_cardinal": "SSW",
    "uv_desc": "Low",
    "phrase_12char": "Fair",
    "phrase_22char": "Fair",
    "phrase_32char": "Fair",
    "ptend_desc": "Falling",
    "sky_cover": "Partly Cloudy",
    "clds": "FEW",
    "obs_qualifier_severity": null,
    "vocal_key": "OT53:OX3300",
    "metric": {
      "wspd": 13,
      "gust": null,
      "vis": 16.09,
      "mslp": 1018.7,
      "altimeter": 1018.63,
      "temp": 12,
      "dewpt": 3,
      "rh": 54,
      "wc": 11,
      "hi": 12,
      "temp_change_24hour": -16,
      "temp_max_24hour": 19,
      "temp_min_24hour": 6,
      "pchange": -1.02,
      "feels_like": 11,
      "snow_1hour": 0,
      "snow_6hour": 0,
      "snow_24hour": 0,
      "snow_mtd": null,
      "snow_season": null,
      "snow_ytd": null,
      "snow_2day": null,
      "snow_3day": null,
      "snow_7day": null,
      "ceiling": null,
      "precip_1hour": 0,
      "precip_6hour": 0,
      "precip_24hour": 0,
      "precip_mtd": null,
      "precip_ytd": null,
      "precip_2day": null,
      "precip_3day": null,
      "precip_7day": null,
      "obs_qualifier_100char": null,
      "obs_qualifier_50char": null,
      "obs_qualifier_32char": null
    }
  }
```






