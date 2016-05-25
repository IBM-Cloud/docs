---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Uso de las API REST de Insights for Weather
{: #rest_apis}

*Última actualización: 06 de abril de 2016*

Puede utilizar las [API REST de Insights for Weather](https://twcservice.{APPDomain}/rest-api/){:new_window}
para recuperar datos sobre el tiempo. Puede probar las operaciones de la API y ver de forma instantánea los resultados para acelerar el proceso de creación de aplicaciones. 

En la documentación de referencia, pulse **Listar operaciones** para ver los
detalles de cada operación.
Cuando se especifican parámetros y se pulsa **Probar**,
es posible que se le solicite que proporcione las credenciales.
Debe proporcionar el nombre de usuario y la
contraseña de las variables de entorno `VCAP_SERVICES`.
Puede encontrar esta información
abriendo la aplicación y pulsando **Variables de entorno** en la tabla de contenido.

**Nota:** Cada región es independiente. No es posible utilizar las credenciales de servicio facilitadas en una región para autenticarse en un servicio de otra región.
Si no se introducen las credenciales correctas, aparece un mensaje que indica que no está autorizado. 

Con estas API de Insights for Weather, puede recuperar datos indicando una geolocalización como coordenadas de longitud y latitud.
Puede utilizar las siguientes API.

|**API**                                  |**Descripción**              |
|-----------------------------------------|-----------------------------|
|`GET /v2/forecast/daily/10day`           |Devuelve previsiones del tiempo para el día actual y para los siguientes nueve días de una geolocalización. La previsión de cada día puede contener una previsión para el día y una para la noche. Estos segmentos son objetos independientes
en las respuestas JSON. Los datos de la previsión diaria no están disponibles a partir de las 3:00 PM hora local. A las 3:00 PM, hora local, la aplicación ya no debe mostrar la previsión del día.|
|`GET /v2/forecast/hourly/24hour`         |Devuelve una previsión por horas del día actual y de las siguientes 24 horas de una geolocalización. Los datos de previsión por hora pueden contener previsiones por hora hasta un máximo de 24
para cada ubicación. Debe descartar todas las previsiones por hora anteriores para una ubicación cuando
se reciben datos nuevos. |
|`GET /v2/observations/current`           |Devuelve las condiciones del tiempo actuales para una geolocalización. Estas observaciones recientes se mantienen en la base de datos
hasta 10 minutos en estaciones de informes específicas y 24 horas de observaciones por estación. Los datos
de observaciones recientes se actualizan continuamente y se sustituyen por una metodología
de primero en entrar, primero en salir (rotando los datos con la observación más reciente y moviendo las
observaciones más antiguas al almacenamiento de archivado) basándose
en la indicación de fecha/hora de las observaciones.|
|`GET /v2/observations/timeseries/24hour` |Devuelve las
observaciones actuales y hasta 24 horas de observaciones anteriores, a partir de la fecha y hora actuales,
para una geolocalización. Las observaciones meteorológicas se
recopilan de los dispositivos físicos desplegados en todo el mundo
y las observaciones meteorológicas actuales.|
*Tabla 1. Resumen de la API Insights for Weather*

## Observaciones de series de tiempo
{: #time_series}

Los datos de observaciones meteorológicas de serie temporal proporcionan información sobre la temperatura,
las precipitaciones, los vientos, la presión barométrica, la visibilidad, la radiación ultravioleta (UV) y
otros elementos de observación relacionados, incluyendo la estación de observación, la fecha/hora de observación,
los códigos de iconos meteorológicos y las frases. La diferencia entre las observaciones de series temporales
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

## Construcción de URL
{: #url_construction}

Las API de Insights for Weather utilizan una estructura de URL común y parámetros de consulta para solicitar y filtrar datos sobre el tiempo.
Los URL que se pasan a las API de Insights for Weather se construyen de este modo: 

```
https://twcservice.mybluemix.net/api/weather/v2/<product group>/&format={format type}&geocode={latitude,longitude}&language={language code}&units={units code}

```

|**Atributo**     |**Descripción**                                    |
|------------------|---------------------------------------------------|
|`nombre de host`        |Vía de acceso de URL alojado (por ejemplo
`https://twcservice.mybluemix.net:443/api/weather`)|
|`versión`         |Iteración actual (por ejemplo, "v2")|
|`grupo de productos`   |Producto (por ejemplo, "observations" o "forecast")|
|`geocódigo`         |Latitud y longitud opcionales, por ejemplo, "45.4214,75.6919" representa Ottawa, Canadá. Si proporciona una coordenada de geocódigo, la API devuelve datos para la ubicación disponible más
cercana. Se utilizan puntos como separadores decimales y se utilizan comas para separar los valores de
latitud y longitud. Si proporciona un geocódigo, los valores de latitud y longitud reales que se utilizan
se devuelven en los metadatos de la respuesta.|
|`idioma`        |Idioma en el que devolver la respuesta. El valor predeterminado es en-US. El
idioma de traducción predeterminado o solicitado se devuelve en el parámetro de idioma en los metadatos
de la respuesta.|
|`unidades`           |Unidades opcionales en las que se debe devolver la respuesta. La API soporta las unidades de medida English (e), Metric (m) y UK-Hybrid (h). Si proporciona las unidades de medida, pero no
proporciona un valor, la API devuelve los datos en la unidad de medida que corresponde
al código de idioma. La unidad de medida predeterminada o solicitada se devuelve en el parámetro de unidades
en los metadatos de la respuesta.|
*Tabla 2. Detalles de URL*

## Unidades de medida
{: #units_measure}

Cuando se utilizan las API de Insights for Weather, no es necesario pasar de forma explícita una unidad de medida. Las API
de Insights for Weather toman como valor predeterminado la unidad de medida que está asociada con el código de idioma en el URL. No obstante,
si desea proporcionar una unidad de medida que es diferente del valor predeterminado, puede pasar una
unidad de medida que altere temporalmente el valor predeterminado.

* Para en-US o en, el código de unidad de medida predeterminado es English/Imperial. El código de unidad es "e".
* Para en-GB, la unidad de medida predeterminada es Hybrid-UK. El código de unidad es "h".
* Para todo lo demás, la unidad de medida predeterminada es Metric. El código de unidad es "m".

## Traducción de idiomas
{: #language_translation}

Las API de Insights for Weather traducen las frases y la unidad de medida. Cuando se formatea una solicitud de URL,
debe proporcionar un idioma válido.
Se traducen los campos siguientes:

|**Campo**           |**Descripción**                                    |
|--------------------|---------------------------------------------------|
|`narrative`         |Previsión narrativa para el periodo de 24 horas|
|`dow`               |Día de la semana|
|`wind_phrase`       |Frase que describe la dirección y la velocidad del viento en una parte del día de 12 horas|
|`wdir_cardinal`     |Promedio de dirección del viento durante el día en notación cardinal |
|`daypart_name`      |Nombre de una parte del día de 12 horas que no incluye nombres de día en las primeras 48 horas|
|`temp_phrase`       |Frase corta que contiene la temperatura alta o baja prevista para el periodo de previsión de 12 horas|
|`shortcast`         |Parte de previsión narrativa meteorológica abreviada sensible |
|`long_daypart_name` |Marco de tiempo con nombre para la previsión meteorológica válida en un formato expandido.
El marco de tiempo con nombre puede ser para periodos de 12 o de 24 horas.|
|`golf_category`     |Categoría de índice de golf que se expresa como una frase para las condiciones meteorológicas para jugar a golf
|
|`phrase_nnchar`     |Frase meteorológica sensible de parte del día|
|`lunar_phrase`      |Código corto de tres caracteres para fases lunares|
|`uv_desc`           |Descripción de índice de UV, que complementa el valor de índice de UV proporcionando un nivel asociado de riesgo de daño de piel debido a la exposición|
|`sky_cover`         | Cubierta de cielo descriptiva que se basa en el porcentaje de cubierta de nubes
|
|`ptend_desc`        | Texto descriptivo de tendencia de presión en las últimas 3 horas|
*Tabla 3. Campos de respuesta traducidos*

## Manejo de campos de datos nulos o que faltan en la respuesta de API
{: #handling_null_or_missing}

Si un campo de datos es nulo porque no hay datos disponibles, las API de Insights for Weather devuelven los códigos de campo
apropiados con la palabra "null" o no devuelven el campo en absoluto. 

## Manejo de errores
{: #handling_errors}

Los siguientes códigos de error son comunes a todas las API:

|**Error** |**Descripción**                                    |
|----------|---------------------------------------------------|
|400       |Solicitud incorrecta. El servidor no ha entendido la solicitud debido a una sintaxis incorrecta. Este código
de error se implementa para todas las API. La API rechaza la solicitud si se proporcionan
parámetros no válidos.|
|401       |No autorizado. La solicitud precisa autenticación.|
|403       |Prohibido. El servidor ha entendido la solicitud pero se niega a cumplirla.|
|404       |No encontrado. Si un parámetro necesario no está presente en la solicitud de API, se devuelve el error MissingParameterException con el código de error 404. |
|405       |Método no permitido. Por ejemplo, enviar un POST en lugar de un GET.|
|406       |No aceptable. Por ejemplo, no aceptar respuestas comprimidas gzip.|
|408       |Tiempo de espera de solicitud excedido. El cliente no ha producido la solicitud durante el tiempo que
el servidor estaba dispuesto a esperar.|
|500       |Error de servidor interno. El servidor ha encontrado una condición inesperada que le ha impedido
cumplir la solicitud.|
|502-504   |Servicio no disponible o problema de pasarela. Estos códigos de error se devuelven si el servicio no
está disponible temporalmente.|
*Tabla 4. Código de respuesta de error*

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
