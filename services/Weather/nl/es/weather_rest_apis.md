---

copyright:
  years: 2015, 2016
lastupdated: "2016-08-22"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Uso de las API REST de {{site.data.keyword.weather_short}}
{: #rest_apis}

Puede utilizar las [API REST](https://twcservice.{APPDomain}/rest-api/){:new_window}
para recuperar datos sobre el tiempo. Puede probar las operaciones de la API y ver de forma instantánea los resultados para acelerar el proceso de creación de aplicaciones.
{: shortdesc}

En la documentación de referencia, pulse **Listar operaciones** para ver los
detalles de cada operación.
Cuando se especifican parámetros y se pulsa **Probar**,
es posible que se le solicite que proporcione las credenciales.
Debe proporcionar el nombre de usuario y la
contraseña de las variables de entorno `VCAP_SERVICES`.
Puede encontrar esta información
abriendo la aplicación y pulsando **Variables de entorno** en la tabla de contenido.

**Nota:** Cada región es independiente. No es posible utilizar las credenciales de servicio facilitadas en una región para autenticarse en un servicio de otra región.
Si no se pueden entrar las credenciales correctas se genera un mensaje *No autorizado*
en el cuerpo de mensaje.

Con las API REST, puede recuperar datos meteorológicos proporcionando una geolocalización como coordenadas de latitud y longitud.
Puede utilizar las siguientes API.

|**API**                                  |**Descripción**              |
|-----------------------------------------|-----------------------------|
|`GET /v1/{geocode or location ID}/forecast/hourly/48hour.json`  |Devuelve la previsión meteorológica para las siguientes 48 horas para una geolocalización en función del formato que se proporcione. Puede proporcionar un `geocode/{latitude}/{longitude}` o una `location/{locationId}`. Los datos de previsión por hora pueden contener previsiones por hora hasta un máximo de 48 para cada ubicación. Debe descartar todas las previsiones por hora anteriores para una ubicación cuando se reciben datos nuevos.|
|`GET /v1/{geocode or location ID}/forecast/daily/{format}.json`   |Devuelve las previsiones meteorológicas diarias para 3, 5, 7 o 10 días para una geolocalización en función del formato que se proporcione. El número de días que se recuperan se especifica en el formato `3day`, `5day`, `7day` o `10day`. Puede proporcionar un `geocode/{latitude}/{longitude}` o una `location/{locationId}`. La previsión de cada día puede contener una previsión para el día, una previsión para la noche y una previsión de 24 horas. Estos segmentos son objetos independientes en las respuestas JSON. Los datos de la previsión diaria no están disponibles a partir de las 3:00 PM hora local. A las 3:00 PM, hora local, la aplicación ya no debe mostrar la previsión del día. |
|`GET /v1/{geocode or location ID}/forecast/intraday/{format}.json`|Devuelve previsiones meteorológicas diarias en periodos de seis horas para 3, 5, 7 o 10 días para una geolocalización en función del formato que se proporcione. El número de días que se recuperan se especifica en el formato `3day`, `5day`, `7day` o `10day`. Puede proporcionar un `geocode/{latitude}/{longitude}` o una `location/{locationId}`. La previsión de cada día puede contener una previsión para la mañana, la tarde, la noche y la madrugada. Estos segmentos son objetos independientes en las respuestas JSON.|
|`GET /v1/{geocode or location ID}/observations.json`              |Devuelve las condiciones del tiempo actuales para una geolocalización. Puede proporcionar un `geocode/{latitude}/{longitude}` o una `location/{locationId}`.  Estas observaciones recientes se mantienen en la base de datos hasta 10 minutos en estaciones de informes específicas y 24 horas de observaciones por estación. Los datos de observaciones recientes se actualizan continuamente y se sustituyen por una metodología de primero en entrar, primero en salir (rotando los datos con la observación más reciente y moviendo las observaciones más antiguas al almacenamiento de archivado) basándose en la indicación de fecha/hora de las observaciones.|
|`GET /v1/{geocode or location ID}/observations/timeseries.json`   |Devuelve las observaciones actuales y hasta 24 horas de observaciones anteriores, a partir de la fecha y hora actuales, para una geolocalización. Puede proporcionar un `geocode/{latitude}/{longitude}` o una `location/{locationId}`. Las observaciones meteorológicas se recopilan de los dispositivos físicos desplegados en todo el mundo y las observaciones meteorológicas actuales.|
|`GET /v1/{geocode, country code, state, or area}/alerts.json`      |Devuelve observaciones, avisos, sentencias y advertencias meteorológicas emitidos por el National Weather Service (NWS), Environment Canada y MeteoAlarm (Europa) e incluyen la traducción de la descripción de suceso, nombre de país y titulares de alertas en 49 idiomas. Puede proporcionar un `geocode/{latitude}/{longitude}`, `country/{countrycode}`, `country/{countrycode}/state/{statecode}`/, o `country/{countrycode}/area/{areaid}`.|
|`GET /v1/alert/{detail_key}/details.json`                         |Devuelve observaciones, avisos, sentencias y advertencias meteorológicas emitidos por el National Weather Service (NWS), Environment Canada y MeteoAlarm (Europa). Los detalles incluyen información detallada sobre la alerta emitida por la autoridad gubernamental meteorológica para el área especificada e incluyen la traducción de la descripción de suceso, nombre de país y titulares de alertas en 49 idiomas. |
|`GET /v1/{geocode or postal code}/almanac/daily.json`             |Devuelve la información de almanaque diaria (sólo EE.UU.) que se obtiene de las estaciones de observación del National Weather Service desde un periodo de tiempo que comprende de 10 a 30 años o más. La información la recopila y la proporciona el National Climatic Data Center (NCDC). Puede proporcionar un `geocode/{latitude}/{longitude}`, o `location/{PostalLocationId}`.|
|`GET /v1/{geocode or postal code}/almanac/monthly.json`           |Devuelve la información de almanaque mensual (sólo EE.UU.) que se obtiene de las estaciones de observación del National Weather Service desde un periodo de tiempo que comprende de 10 a 30 años o más. La información la recopila y la proporciona el National Climatic Data Center (NCDC). Puede proporcionar un `geocode/{latitude}/{longitude}`, o `location/{PostalLocationId}`.|
|`GET /v3/location/{search or point}`                                  |Proporciona la capacidad para buscar un nombre de ubicación o un geocódigo (latitud y longitud) para recuperar un conjunto de ubicaciones que coincidan con la solicitud. El Location Service admite la búsqueda por nombre de ciudad o código postal.|
*Tabla 1. Resumen de la API de {{site.data.keyword.weather_short}}*

## Previsiones diarias e intradía
{: #daily_intraday}
La API de previsión diaria puede contener varios días de previsiones diarias para cada ubicación.
Cada día de una previsión puede contener hasta tres previsiones independientes. Para cualquier día de previsión,
la API puede devolver previsiones de día, noche y de 24 horas.

La API de previsión intradía puede contener varios días de previsiones diarias para cada ubicación.
Cada día de una previsión contiene cuatro previsiones de seis horas independientes para la mañana (de 7 a 13),
la tarde (de 13 a 19), la noche (19 a 1) y la madrugada (1 a 7). La previsión
intradía es similar en estructura a la previsión diaria.

Cada segmento tiene un número de la parte del día, un nombre del día de la semana y un nombre de la parte del día. Por ejemplo,
el ejemplo siguiente muestra el orden del campo de datos y los valores de datos para
`num`, `dow`, y el `daypart_name`, para una previsión generada
por las API en un jueves por la mañana:
* 1, Jueves, Mañana
* 2, Jueves, Tarde
* 3, Jueves, Noche
* 4, Jueves, Madrugada
* 5, Viernes, Mañana
* 6, Viernes, Tarde
* 7, Viernes, Noche
* 8, Viernes, Madrugada

## Observaciones de serie temporal y actual
{: #time_series}

Las condiciones actuales y los datos de observaciones meteorológicas de serie temporal proporcionan información sobre la temperatura,
las precipitaciones, los vientos, la presión barométrica, la visibilidad, la radiación ultravioleta (UV)
y otros elementos de observación relacionados, incluyendo la estación de observación,
la fecha/hora de observación, los códigos de iconos meteorológicos y las frases. La diferencia entre las observaciones de series temporales
y las observaciones actuales es el periodo de tiempo de la observación, lo
que produce uno o más conjuntos de datos de observación.

Las condiciones actuales son las observaciones más recientes para la ubicación que se solicita
sin ningún parámetro de tiempo. Se devuelve un conjunto de datos. Las observaciones de serie temporal
incluyen observaciones pasadas que se han producido hasta e incluyendo
las últimas 24 horas para la ubicación solicitada.

Las observaciones recientes se conservan en la base de datos primaria hasta 48 horas (2 días)
en estaciones de informe específicas. Los datos
de observaciones recientes se actualizan continuamente y se sustituyen por una metodología
de primero en entrar, primero en salir (rotando los datos con la observación más reciente y moviendo las
observaciones más antiguas al almacenamiento de archivado) basándose
en la indicación de fecha/hora de las observaciones. La cantidad de datos que se conservan y están
disponibles desde cualquier estación pueden ser más de 24 informes de observación individuales. El número de observaciones lo determina el tipo de
observación del que se trata.

## Titulares y detalles de la alerta
{: #alerts_levels}
Las API de la alerta devuelven titulares de alertas meteorológicas activas que están relacionadas con tormentas eléctricas, tornados, terremotos e inundaciones graves.
Estas API también devuelven alertas no meteorológicas como por ejemplo alertas de secuestro de niños y avisos
de aplicación de leyes.

**Nota**: Esta API sólo está disponible para Estados Unidos, Canadá y Europa.

La API Titulares de la alerta proporciona un valor de clave en el atributo `detail_key`
para acceder a los detalles de la alerta en la API Detalles de la alerta.
Consulte la API Titulares de la alerta para obtener el valor `detail_key` y, a continuación, recuperar la respuesta de la
API Detalles de la alerta con la `detail_key`.

**Nota**: Debe visualizar la atribución del origen de datos para cualesquiera datos de alerta que se visualicen en la aplicación.

La frase de atribución debe mostrar la siguiente información:

*Emitido por <Nombre de la oficina> - &lt;Código de distrito de administración de la oficina&gt;, &lt;Código de país de la oficina&gt;, &lt;Fuente&gt;, &lt;Renuncia de responsabilidad&gt;*

Por ejemplo:
* Emitido por National Weather Service - Bismarck, EE.UU.
* Emitido por Central Institute for Meteorology and Geodynamics - Austria, EMETNET-Meteoalarm

## Información de almanaque
{: #almanac_details}
La API Almanaque requiere un ID de ubicación y un tipo de ubicación (ciudad o código postal)
o un par de latitud y longitud para recuperar la información para una determinada ubicación.

Al utilizar `location` en el URL, la ubicación debe incluir un ID de ubicación
(código postal) con un tipo de ubicación y un código de
país. Al utilizar `geocode` en el URL, la ubicación de búsqueda debe ser una combinación de latitud y longitud válida.

La API Almanaque utiliza parámetros para especificar datos diarios o mensuales,
una fecha específica o un rango de fechas de información, y las unidades de medida en las que devolver los datos.

Los parámetros de fecha son `start` y `end`. El parámetro `start` es un parámetro obligatorio, pero el parámetro `end` es opcional. Cuando los parámetros se utilizan conjuntamente, la combinación devuelve un
rango de datos en lugar de un mes o día específico de datos.

El formato de fecha para recuperar Almanaque diario da como resultado un valor numérico de cuatro dígitos que representa
el mes y el día para los datos necesarios, es decir, MMDD. Cualquier día de dígito único
**debe** tener un cero anterior, por ejemplo, 01. 

El formato de fecha para recuperar el Almanaque mensual da como resultado el mes, es decir, MM. Cualquier mes de dígito único
**debe** tener un cero anterior, por ejemplo, 01. Cualquier otro formato dará como resultado un error de
API y no se obtendrán datos.

**Nota**: Si no proporciona el valor de fecha en la solicitud, el sistema devuelve un estado
de 404 (Bad Request). La API no proporciona un valor predeterminado.

## Construcción de URL
{: #url_construction}

Las API REST utilizan una estructura de URL común y parámetros de consulta para solicitar y filtrar datos meteorológicos.
Los URL que se pasan a las API se construyen como se indica a continuación:

```
https://twcservice.mybluemix.net/api/weather/v1/geocode/<latitude>/<longitude>/<product group>/<date>/<format>&units={units code}&language={language code}
```

Por ejemplo:

```
https://twcservice.mybluemix.net/api/weather/v1/geocode/33.40/83.42/forecast/daily/3day.json?units=m&language=en-US
```

|**Atributo**     |**Descripción**                                    |
|------------------|---------------------------------------------------|
|`nombre de host`        |La vía de acceso del URL alojada. Por ejemplo, `https://twcservice.mybluemix.net:443/api/weather`.|
|`versión`         |Iteración actual. Por ejemplo, `v1`.|
|`ubicación`        |El geocódigo o el ID de ubicación. El grupo de ubicaciones puede ser `geocode` o `location`. Por ejemplo, `geocode/45.4214/75.6919` representa a Ottawa, Canada. Si proporciona una coordenada de geocódigo, la API devuelve datos para la ubicación disponible más cercana. Se utilizan puntos como separadores decimales y se utilizan comas para separar los valores de latitud y longitud. Si proporciona un geocódigo, los valores de latitud y longitud reales que se utilizan se devuelven en los metadatos de la respuesta.|
|`grupo de productos`   |El producto. Por ejemplo, `observations` o `forecast`. Un subgrupo de productos, por ejemplo, `historical`, es opcional.|
|`fecha`            |El tipo de fecha. Por ejemplo, `daily` o `monthly`.|
|`formato`          |El formato. Por ejemplo, `3day`, `5day`, `7day` o `10day`.|
|`unidades`           |Unidades opcionales en las que se debe devolver la respuesta. La API soporta las unidades de medida English (e), Metric (m) y UK-Hybrid (h). Si proporciona las unidades de medida, pero no proporciona un valor, la API devuelve los datos en la unidad de medida que corresponde al código de idioma. La unidad de medida predeterminada o solicitada se devuelve en el parámetro de unidades en los metadatos de la respuesta.|
|`idioma`        |Idioma en el que devolver la respuesta. El valor predeterminado es en-US. El idioma de traducción predeterminado o solicitado se devuelve en el parámetro de idioma en los metadatos de la respuesta.|
*Tabla 2. Detalles de URL*

**Nota**: Las API REST utilizan el estándar ISO 3166 para los códigos de país. Para obtener más información, consulte la
[Online Browsing Platform del estándar ISO](https://www.iso.org/obp/ui/#search/code/){:new_window}.
Las API utilizan el sistema de referencia de coordenadas de geocódigo WGS84. Para obtener más información, consulte
[Vocabulario geo básico](https://www.w3.org/2003/01/geo/){:new_window}.

## Códigos e imágenes de icono
{: #icon_code_images}

Cuando las API REST de {{site.data.keyword.weather_short}} devuelven un código de icono en la respuesta, puede utilizar el código de icono para determinar qué imagen de icono se muestra en la app.
Hay una relación uno a uno entre el código de icono en la respuesta de la API y el nombre de archivo de la imagen de icono.
Por ejemplo, si la respuesta de la API contiene un `icon_code` de 1, puede utilizar el nombre de archivo
`01.png` para mostrar la imagen de icono correspondiente. 

En el código, puede crear una función que utilice el `icon_code` para determinar el URL de la imagen de icono. Por ejemplo:

```
function getIconURL(code) {
    return "images/weathericons/icon" + code + ".png";
}
```

La tabla siguiente contiene códigos de icono, descripciones e imágenes que se pueden utilizar con las API REST de
{{site.data.keyword.weather_short}}. La tabla indica si un icono se utiliza en las API Forecast u Observation y si el icono está disponible en los partes de previsión nocturno o diurno. 

|**Código**|**Descripción**|**Imagen**|**Uso de API** |**Noche o día**|
|----|--------------------------|------------|------------|--------------------|
| 0  | Tornado                  | <img src="images/00.png " width="100" height="100" alt="Imagen de icono."/>| Forecast                | Noche y día |
| 1  | Tormenta tropical           | <img src="images/01.png " width="100" height="100" alt="Imagen de icono."/>| Forecast y Observations | Noche y día |
| 2  | Huracán                | <img src="images/02.png " width="100" height="100" alt="Imagen de icono."/>| Forecast                | Noche y día |
| 3  | Tormentas fuertes            | <img src="images/03.png " width="100" height="100" alt="Imagen de icono."/>| Forecast                | Noche y día |
| 4  | Truenos y granizos         | <img src="images/04.png " width="100" height="100" alt="Imagen de icono."/>| Forecast y Observations | Noche y día |
| 5  | Chubascos con lluvia o nieve     | <img src="images/05.png " width="100" height="100" alt="Imagen de icono."/>| Forecast y Observations | Noche y día |
| 6  | Lluvia / Aguanieve             | <img src="images/06.png " width="100" height="100" alt="Imagen de icono."/>| Forecast y Observations | Noche y día |
| 7  | Nieve fría / Aguanieve  | <img src="images/07.png " width="100" height="100" alt="Imagen de icono."/>| Forecast y Observations | Noche y día |
| 8  | Llovizna helada         | <img src="images/08.png " width="100" height="100" alt="Imagen de icono."/>| Forecast y Observations | Noche y día |
| 9  | Llovizna                  | <img src="images/09.png " width="100" height="100" alt="Imagen de icono."/>| Forecast y Observations | Noche y día |
| 10 | Lluvia helada            | <img src="images/10.png " width="100" height="100" alt="Imagen de icono."/>| Forecast y Observations | Noche y día |
| 11 | Lluvia moderada               | <img src="images/11.png " width="100" height="100" alt="Imagen de icono."/>| Forecast y Observations | Noche y día |
| 12 | Lluvia                     | <img src="images/12.png " width="100" height="100" alt="Imagen de icono."/>| Forecast y Observations | Noche y día |
| 13 | Nieve dispersa       | <img src="images/13.png " width="100" height="100" alt="Imagen de icono."/>| Forecast y Observations | Noche y día |
| 14 | Nieve ligera               | <img src="images/14.png " width="100" height="100" alt="Imagen de icono."/>| Forecast y Observations | Noche y día |
| 15 | Ventisca de nieve / Nieve acumulada  | <img src="images/15.png " width="100" height="100" alt="Imagen de icono."/>| Forecast y Observations | Noche y día |
| 16 | Nieve                     | <img src="images/16.png " width="100" height="100" alt="Imagen de icono."/>| Forecast y Observations | Noche y día |
| 17 | Granizo                     | <img src="images/17.png " width="100" height="100" alt="Imagen de icono."/>| Forecast y Observations | Noche y día |
| 18 | Aguanieve                    | <img src="images/18.png " width="100" height="100" alt="Imagen de icono."/>| Forecast y Observations | Noche y día |
| 19 | Nubes de polvo / Tormentas de arena | <img src="images/19.png " width="100" height="100" alt="Imagen de icono."/>| Forecast y Observations | Noche y día |
| 20 | Neblina                    | <img src="images/20.png " width="100" height="100" alt="Imagen de icono."/>| Forecast y Observations | Noche y día |
| 21 | Nublado / Ventoso             | <img src="images/21.png " width="100" height="100" alt="Imagen de icono."/>| Forecast y Observations | Noche y día |
| 22 | Niebla / Ventoso            | <img src="images/22.png " width="100" height="100" alt="Imagen de icono."/>| Forecast y Observations | Noche y día |
| 23 | Brisa                   | <img src="images/23.png " width="100" height="100" alt="Imagen de icono."/>| Forecast                | Noche y día |
| 24 | Rocío suave / Ventoso    | <img src="images/24.png " width="100" height="100" alt="Imagen de icono."/>| Forecast y Observations | Noche y día |
| 25 | Gélido / Cristales de hielo    | <img src="images/25.png " width="100" height="100" alt="Imagen de icono."/>| Forecast y Observations | Noche y día |
| 26 | Nublado                   | <img src="images/26.png " width="100" height="100" alt="Imagen de icono."/>| Forecast y Observations | Noche y día |
| 27 | Nubosidad abundante            | <img src="images/27.png " width="100" height="100" alt="Imagen de icono."/>| Forecast y Observations | Noche y día |
| 28 | Nubosidad abundante            | <img src="images/28.png " width="100" height="100" alt="Imagen de icono."/>| Forecast y Observations | Día         |
| 29 | Nubosidad parcial            | <img src="images/29.png " width="100" height="100" alt="Imagen de icono."/>| Forecast y Observations | Noche       |
| 30 | Nubosidad parcial            | <img src="images/30.png " width="100" height="100" alt="Imagen de icono."/>| Forecast y Observations | Día         |
| 31 | Claro                    | <img src="images/31.png " width="100" height="100" alt="Imagen de icono."/>| Forecast y Observations | Noche       |
| 32 | Soleado                    | <img src="images/32.png " width="100" height="100" alt="Imagen de icono."/>| Forecast y Observations | Día         |
| 33 | Bueno / Mayormente claro      | <img src="images/33.png " width="100" height="100" alt="Imagen de icono."/>| Forecast y Observations | Noche       |
| 34 | Bueno / Mayormente soleado      | <img src="images/34.png " width="100" height="100" alt="Imagen de icono."/>| Forecast y Observations | Día         |
| 35 | Lluvia & granizos mezclados        | <img src="images/35.png " width="100" height="100" alt="Imagen de icono."/>| Forecast                | Día         |
| 36 | Calor                      | <img src="images/36.png " width="100" height="100" alt="Imagen de icono."/>| Forecast                | Día         |
| 37 | Tormentas aisladas   | <img src="images/37.png " width="100" height="100" alt="Imagen de icono."/>| Forecast                | Día         |
| 38 | Tormentas            | <img src="images/38.png " width="100" height="100" alt="Imagen de icono."/>| Forecast y Observations | Noche y día |
| 39 | Chubascos dispersos        | <img src="images/39.png " width="100" height="100" alt="Imagen de icono."/>| Forecast                | Día         |
| 40 | Lluvia intensa               | <img src="images/40.png " width="100" height="100" alt="Imagen de icono."/>| Forecast y Observations | Noche y día |
| 41 | Chubascos con nieve dispersos   | <img src="images/41.png " width="100" height="100" alt="Imagen de icono."/>| Forecast                | Día         |
| 42 | Nieve intensa               | <img src="images/42.png " width="100" height="100" alt="Imagen de icono."/>| Forecast y Observations | Noche y día |
| 43 | Ventisca                 | <img src="images/43.png " width="100" height="100" alt="Imagen de icono."/>| Forecast                | Noche y día |
| 44 | No disponible (N/A)      | <img src="images/44.png " width="100" height="100" alt="Imagen de icono."/>| Forecast                | Noche y día |
| 45 | Chubascos dispersos        | <img src="images/45.png " width="100" height="100" alt="Imagen de icono."/>| Forecast                | Noche       |
| 46 | Chubascos con nieve dispersos   | <img src="images/46.png " width="100" height="100" alt="Imagen de icono."/>| Forecast                | Noche       |
| 47 | Tormentas dispersas  | <img src="images/47.png " width="100" height="100" alt="Imagen de icono."/>| Forecast y Observations | Noche y día |
*Tabla 3. Códigos e imágenes de icono*

Puede descargar este conjunto de iconos meteorológicos como [PNG](https://twcdocs.mybluemix.net/download/weather_icons_200x200_png.zip){:new_window}
o [SVG](https://twcdocs.mybluemix.net/download/weather_icons_200x200_svg.zip){:new_window} y utilizarlos en su app.  

También puede descargar el [conjunto de iconos](https://twcdocs.mybluemix.net/download/weatherinsightsicons.zip){:new_window} que utiliza la [app de demostración {{site.data.keyword.weather_short}}](http://weather-company-data-demo.{APPDomain}){: new_window}. 

## Unidades de medida
{: #units_measure}

Cuando se utilizan las API REST, no es necesario pasar de forma explícita una unidad de medida. Las API
toman como valor predeterminado la unidad de medida que está asociada con el código de idioma en el URL. No obstante,
si desea proporcionar una unidad de medida que es diferente del valor predeterminado, puede pasar una
unidad de medida que altere temporalmente el valor predeterminado.

* Para en-US o en, el código de unidad de medida predeterminado es English/Imperial. El código de
unidad es `e`.
* Para en-GB, la unidad de medida predeterminada es Hybrid-UK. El código de
unidad es `h`.
* Para todo lo demás, la unidad de medida predeterminada es Metric. El código de
unidad es `m`.

## Traducción de idiomas
{: #language_translation}

Las API REST traducen las frases y la unidad de medida. Cuando se formatea una solicitud de URL,
debe proporcionar un idioma válido.
Se traducen los campos siguientes:

|**Campo**           |**Descripción**                                    |
|--------------------|---------------------------------------------------|
|`narrative`         |Previsión narrativa para el periodo de 24 horas|
|`dow`               |Día de la semana|
|`wind_phrase`       |Frase que describe la dirección y la velocidad del viento en una parte del día de 12 horas|
|`wdir_cardinal`     |Promedio de dirección del viento durante el día en notación cardinal|
|`daypart_name`      |Nombre de una parte del día de 12 horas que no incluye nombres de día en las primeras 48 horas|
|`temp_phrase`       |Frase corta que contiene la temperatura alta o baja prevista para el periodo de previsión de 12 horas|
|`shortcast`         |Parte de previsión narrativa meteorológica abreviada sensible|
|`long_daypart_name` |Marco de tiempo con nombre para la previsión meteorológica válida en un formato expandido. El marco de tiempo con nombre puede ser para periodos de 12 o de 24 horas.|
|`golf_category`     |Categoría de índice de golf que se expresa como una frase para las condiciones meteorológicas para jugar a golf|
|`phrase_nnchar`     |Frase meteorológica sensible de parte del día|
|`lunar_phrase`      |Código corto de tres caracteres para fases lunares|
|`uv_desc`           |Descripción de índice de UV, que complementa el valor de índice de UV proporcionando un nivel asociado de riesgo de daño de piel debido a la exposición|
|`wx_phrase`         |Descripción textual de las condiciones meteorológicas observadas en la estación de informes.|
|`pressure_desc`     |Frase que describe el cambio en la presión barométrica que se lee en la última hora.|
|`headline_text`     |Texto del titular de un suceso para la ubicación.|
|`event_desc`        |Descripción de un suceso.|
|`cntry_name`        |Nombre del país donde se ha producido un suceso, proporcionado en letras mayúsculas y minúsculas.|
*Tabla 4. Campos de respuesta traducidos*

## Manejo de campos de datos nulos o que faltan en la respuesta de API
{: #handling_null_or_missing}

Si un campo de datos es nulo porque no hay datos disponibles, las API REST devuelven los códigos de campo
apropiados con la palabra `null` o no devuelven el campo en absoluto. 

## Manejo de errores
{: #handling_errors}

Los siguientes códigos de error son comunes a todas las API:

|**Error** |**Descripción**                                    |
|----------|---------------------------------------------------|
|400       |Solicitud incorrecta. El servidor no ha entendido la solicitud debido a una sintaxis incorrecta. Este código de error se implementa para todas las API. La API rechaza la solicitud si se proporcionan parámetros no válidos.|
|401       |No autorizado. La solicitud precisa autenticación.|
|403       |Prohibido. El servidor ha entendido la solicitud pero se niega a cumplirla.|
|404       |No encontrado. Si un parámetro necesario no está presente en la solicitud de API, se devuelve el error MissingParameterException con el código de error 404.|
|500       |Error de servidor interno. El servidor ha encontrado una condición inesperada que le ha impedido cumplir la solicitud.|
*Tabla 5. Códigos de respuesta de error*

La respuesta de error es siempre la mismo. Se pueden devolver varios códigos de error en una respuesta.
Por
ejemplo, una respuesta de error JSON puede devolver lo siguiente:

```
{
  metadata: {
    transaction_id: "1411496413365:-1880721071"
  },
  success: false,
  errors: [
    {
      error: {
        code: "NDF-0001",
        message: "No se han encontrado datos para la consulta del producto."
      }
    }
}
```
