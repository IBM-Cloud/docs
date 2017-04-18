---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Utilización de las API REST de Insights for Twitter
{: #rest_apis}

El servicio {{site.data.keyword.twittershort}} consta de las API RESTful para buscar y consumir contenido de Twitter. La tabla [Lenguaje de consulta](twitter_rest_apis.html#querylanguage){: new.window} lista los términos de consulta soportados por las API de servicio. Los ejemplos se proporcionan para demostrar cómo se pueden construir las consultas.
{:shortdesc}

## Documentación de API REST {: #rest_api}
La documentación de la API REST se crea con Swagger, que permite probar las operaciones de la API y ver al instante los resultados para que ayudarle a crear sus aplicaciones en menos tiempo.
Actualmente están disponibles las operaciones de API siguientes:

* Búsqueda: encuentra tuits en Decahose o el flujo PowerTrack filtrado.
* Número total: devuelve el número de tuits basándose en una consulta especificada.
* Comprobar: determina si una lista de mensajes cumple las políticas de Twitter y los usuarios de Twitter.
* Seguimientos: proporciona a los usuarios del Plan de entrada un surtido de puntos finales para
gestionar filtros PowerTrack.

Para obtener más información sobre las API REST y sus recursos, consulte la referencia de [REST API](https://cdeservice.{APPDomain}/rest-api/){: new_window}. Seleccione la región en la que se encuentra la aplicación. Cada región es independiente; no puede
utilizar credenciales de servicio que le se suministran en una región para autenticarse en
un servicio en otra región.

En la documentación de referencia, pulse **List Operations** para ver los detalles de cada operación. Después de pulsar el botón **Try it out!** es posible que se le solicite que proporcione credenciales. Es necesario proporcionar el nombre de usuario y la contraseña de las variables de entorno **VCAP_SERVICES**. Para localizar esta información, abra la aplicación y pulse **Variables de entorno** en la tabla de contenido.

**Nota**: si no se especifican las credenciales apropiadas se genera un mensaje"No autorizado" en el cuerpo de respuesta.

**Importante**: los seguimientos activos que se crean con la característica **Try it out!** recopila tuits de Twitter, que cuentan de cara a la bonificación mensual. Cuando ya no se
necesitan los seguimientos, cambie el estado a
**Inactivo** o simplemente suprima el seguimiento.


## Lenguaje de consulta {: #querylanguage}

Con {{site.data.keyword.twittershort}} puede efectuar búsquedas en el contenido de Twitter mediante un amplio conjunto de parámetros y filtros de consulta para generar unos resultados más precisos.

En las consultas están soportados los operadores booleanos siguientes. 

| **Operador**        | **Descripción**                                                                                                                   | **Ejemplos**      |
|---------------------|-----------------------------------------------------------------------------------------------------------------------------------|-------------------|
| término1 **AND** término2 | Devuelve los tuits que contienen tanto término1 como término2. El espacio en blanco entre los dos términos se trata como si fuese AND, por lo que el operador se puede omitir. | `#ibm twitter`      |
| término1 **OR** término2  | Devuelve los tuits que contienen término1 o término2.    | `#money OR revenue` |
| -término1              | Devuelve los tuits que no contienen término1.  |`ibm -apple`  |

*Tabla 1. Operadores booleanos*

Prioridad de operador: "-" tiene prioridad sobre "AND", y "AND" tiene prioridad sobre "OR". Debe utilizar paréntesis para indicar explícitamente la prioridad de los operadores. Por ejemplo, `large animals` -(`giraffes` OR `bears`) busca tuits que contienen los términos "large" y "animals", pero excluye los tuits que contienen "giraffes" y "bears".

En la tabla siguiente se indican los términos de consulta soportados actualmente.

| **Término** 	| **Descripción** 	| **Ejemplos** 	|
|----------------------------------------------	|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------	|---------------------------------------------	|
| palabra
clave 	| Encuentra los tuits que contienen la palabra clave en el cuerpo. La búsqueda no distingue entre mayúsculas y minúsculas. 	| análisis 	|
| "exact phrase match" 	| Encuentra los tuits que contienen la secuencia de palabras clave exacta. 	| "IBM and analytics" 	|
| `#hashtag` 	| Encuentra los tuits que tienen la etiqueta hash *#hashtag*. 	| `#insight2015` 	|
| `bio_lang:language` 	| Encuentra los tuits de los usuarios cuyos valores de idioma del perfil coinciden con el código de idioma especificado.  Consulte `lang:` para obtener una lista de idiomas soportados. 	| `bio_lang:en` 	|
| `bio_location:"location"` 	| Encuentra los tuits de los usuarios cuyos valores de ubicación del perfil coinciden con la referencia `location` especificadaq. 	| `bio_location:"New York"` 	|
| `country_code:country-code` 	| Encuentra los tuits cuyo lugar o ubicación etiquetado coincida con el código de país especificado. </br>**Para ver una lista de códigos de país soportados, consulte  **: http://en.wikipedia.org/wiki/ISO_3166-1 	| `country_code:us` 	|
| `followers_count: lowerLimit,upperLimit` 	| Encuentra los tuits de los usuarios que tienen un número de seguidores comprendido dentro del rango especificado. El valor upperLimit es opcional y ambos límites están incluidos. 	| `followers_count:500` 	|
| `friends_count: lowerLimit,upperLimit` 	| Encuentra los tuits de los usuarios que siguen a un número de usuarios comprendido dentro del rango especificado. El valor upperLimit es opcional y ambos límites están incluidos. 	| `friends_count:1000,3000` 	|
| `from:twitterHandle` 	| Encuentra los tuits de los usuarios con el nombre de usuario preferido *twitterHandle*. No debe contener el símbolo &commat;. 	| `from:alexlang11` 	|
| `has:children` 	| Encuentra los tuits de los usuarios que tienen hijos. 	| `has:children` 	|
| `is:married` 	| Encuentra los tuits de los usuarios que están casados. 	| `is:married` 	|
| `is:verified` 	| Encuentra los tuits en los que el autor ha sido verificado por Twitter. 	| `analytics is:verified` 	|
| `lang:language-code` 	| Encuentra los tuits en un idioma determinado. La lista de códigos de idioma soportados es esta: <ul><li>`ar` (Árabe)</li><li>`zh` (Chino)</li><li>`da` (Danés)</li><li>`dl` (Neerlandés)</li><li>`en` (Inglés)</li><li>`fi` (Finlandés)</li><li>`fr` (Francés)</li><li>`de` (Alemán)</li><li>`el` (Griego)</li><li>`he` (Hebreo)</li><li>`id` (Indonesio)</li><li>`it` (Italiano)</li><li>`ja` (Japonés)</li><li>`ko` (Coreano)</li><li>`no` (Noruego)</li><li>`fa` (Persa)</li><li>`pl` (Polaco)</li><li>`pt` (Portugués)</li><li>`ru` (Ruso)</li><li>`es` (Español)</li><li>`sv` (Sueco)</li><li>`th` (Tailandés)</li><li>`tr` (Turco)</li><li>`uk` (Ucraniano)</li></ul>    | `lang:de` (para localizar tuits en alemán) 	|
| `listed_count: lowerLimit,upperLimit` 	| Encuentra los tuits en los que la lista de Twitter del autor esté comprendido en el rango especificado. El valor upperLimit es opcional y ambos límites están incluidos. 	| `listed_count:1000,3000` 	|
| `point_radius:[longitude latitude radius]` 	| Encuentra los tuits enviados desde una zona geográfica, especificada por sus coordenadas de longitud y latitud y por un radio. </br></br>Todas las coordenadas se representan en grados decimales. El valor `longitude` debe estar comprendido entre -180 y +180, mientras que `latitude` debe estar comprendido entre -90 y +90. Si se especifica un valor fuera de los rangos soportados, se devolverá un error. Los
valores deben especificarse como números de coma flotante; los
enteros no se admiten. </br></br>El radio del área circundante debe especificarse en millas
(mi) o en kilómetros (km). 	| `point_radius:[41.128611 -73.707778 5.0mi]` 	|
| `posted:startTime  posted:startTime,endTime` 	| Encuentra los tuits que se han publicado en el momento indicado por "startTime" o más tarde. El valor "endTime" es opcional y ambos límites están incluidos. Las indicaciones de fecha y hora deben tener uno de los formatos siguientes:  </br>"aaaa-mm-dd" o "aaaa-mm-ddTHH:MM:SSZ" </br>  El huso horario se basa en UTC (Hora
universal coordinada). Cuando especifica horas, minutos y segundos,
la hora debe aparecer entre "T" y "Z", segúne el formato recomendado. 	| `posted:2014-12-01,2014-12-12` 	|
| `sentiment:sentiment-value` 	| Encuentra los tuits con un sentimiento determinado. Los valores soportados son: </br><dl>positive</dl> <dlentry>El tuit contiene más frases relacionadas con sentimientos positivos que negativos.</dlentry> </br></br><dl>negative</dl> <dlentry>El tuit contiene más frases relacionadas con sentimientos negativos que positivos.</dlentry>  </br></br><dl>neutral</dl>  <dlentry>El tuit no contiene indicaciones de sentimientos o está en un idioma en el que no se ofrece la detección de sentimientos.</dlentry> </br></br><dl>ambivalent</dl>  <dlentry>El tuit contiene la misma cantidad de frases con sentimientos positivos que con sentimientos negativos.</dlentry> 	| `sentiment:positive` 	|
| `statuses_count: lowerLimit,upperLimit` 	| Encuentra los tuits de los usuarios que han publicado un número de estados que está comprendido en el rango especificado. El valor upperLimit es opcional y ambos límites están incluidos. 	| `statuses_count:1000,3000` 	|
| `time_zone:timeZone` 	| Encuentra los tuits de los usuarios cuyos valores del perfil coinciden con el huso horario especificado. 	| `time_zone:"Eastern Time (US & Canada)"` 	|
| `time_zone:city` 	| Encuentra los tuits de los usuarios cuyos valores del perfil
coinciden con la ciudad especificada. 	| `time_zone:"Dublin"` 	|
*Tabla 2. Términos de consulta*

Todos los términos de consulta soportados se pueden combinar con los operadores booleanos descritos anteriormente. Por ejemplo,

`ibm -apple followers_count:500`
