---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Flujos Decahose y PowerTrack {: #decahose_powertrack}

{{site.data.keyword.twittershort}}
proporciona acceso a los flujos de datos
Twitter Decahose y PowerTrack, basados en la inscripción de plan
{{site.data.keyword.Bluemix_notm}}. 
Ambos
flujos proporcionan feeds en tiempo real y diferentes características
para que se ajusten a sus necesidades.
{:shortdesc}

El flujo de datos Decahose es una muestra aleatoria del 10% de Twitter Firehose. Los tuits provienen de Twitter en tiempo real y la secuencia la determinan los algoritmos de muestreo de Twitter. Para la mayoría de los análisis estadísticos, una muestra aleatoria del 10% es lo suficientemente precisa. Los datos Decahose se indexan para un periodo de 2 años, de modoe que las respuestas de consultas pueden no devolver tuits con más de dos años de antigüedad. El acceso a Decahose está disponible en el Plan gratuito y el Plan de entrada, mientras
que el acceso al flujo de datos PowerTrack es exclusivo para usuarios
del Plan de entrada.

El flujo PowerTrack ofrece la ventaja añadida del filtrado de
tuits de entrada, basados en un filtro definido por el usuario
basado en reglas conocido como seguimiento. Como
usuario Plan de entrada, puede crear hasta 1.000 reglas por cuenta. Para un filtrado avanzado, se pueden combinar varios seguimientos para
formar un seguimiento agregado. Las siguientes
secciones describen los estados del seguimiento, las propiedades y
las acciones soportadas que puede realizar en los seguimientos, como
edición, supresión, etc.

**Nota**: La indexación del flujo de datos PowerTrack se limita a un
millón de tuits por mes de calendario. Una vez que se alcanza el límite, se detiene la indexación para el mes. Al principio del mes
siguiente, puede volver a activar los seguimientos; no se activan
automáticamente. Para maximizar el uso del flujo, se recomienda
encarecidamente una gestión adecuada de los seguimientos. Por
ejemplo, los seguimientos redundantes se pueden convertir en inactivos.

## Tipos de seguimiento {: #track_types}

Los usuarios del Plan de entrada pueden crear
seguimientos personalizables para filtrar mensajes recopilados en el
flujo de datos PowerTrack.  {{site.data.keyword.twittershort}}
soporta los dos tipos de seguimiento siguientes.

<dl>
<dt>Regla</dt>
<dd>Todos los mensajes recopilados en este seguimiento coinciden con
al menos una de las reglas asociadas con el seguimiento. Puede
añadir, editar y suprimir reglas dentro de este tipo de seguimiento.

La sintaxis de reglas
[GNIP PowerTrack](http://support.gnip.com/apis/powertrack2.0/rules.html) completa se admite dentro de
los seguimientos basados en reglas. Todas las consultas deben ajustarse al   {{site.data.keyword.twittershort}} [Lenguaje de consulta](twitter_rest_apis.html#querylanguage "Lenguaje de consulta").
</dd>

<dt>Agregado</dt>
<dd>Una combinación de dos o más seguimientos de agregados o reglas. Los
seguimientos agregados se utilizan para la agrupación
arbitraria de varios seguimientos. Puede añadir y suprimir
seguimientos individuales desde un tipo de seguimiento agregado. Las reglas individuales no se pueden añadir a seguimientos
agregados; utilice un seguimiento de reglas en su lugar para ello. Los seguimientos agregados no tienen estado, pero sus seguimientos de
reglas constituyentes son
**Activos** o **Inactivos**.</dd>
</dl>

## Propiedades de seguimiento {: #track_properties}
Los seguimientos contienen las siguientes propiedades. Algunas propiedades no se aplican a los seguimientos agregados o basados en reglas. Por ejemplo, la propiedad de reglas no se aplica a
seguimientos agregados.

<dl>
<dt>createdDate</dt>
<dd>Indica cuándo se ha creado el seguimiento; se especifica como `AAAAMMDDHHMM`.</dd>

<dt>endDate</dt>
<dd>Indica cuándo el seguimiento dejará de recopilar mensajes. El valor especificado debe estar en el futuro y cumplir con uno de los siguientes formatos: `AAAA-MM-DD` o `AAAA-MM-DDTHH:MM:SSZ`. Si se especifica
una fecha en el pasado se devolverá un error HTTP 400.

Esta propiedad no se aplica a seguimientos agregados.</dd>

<dt>id</dt>
<dd>Una referencia de ID exclusivo que se asigna a un seguimiento
después de la creación. El ID se representa en un formato de serie
GUID (por ejemplo, 3F2504E0-4F89-41D3-9A0C-0305E82C3301) para
seguimientos agregados y de reglas.</dd>

<dt>name</dt>
<dd>Nombre descriptivo del seguimiento. La exclusividad de esta propiedad no se garantiza.</dd>

<dt>rules</dt>
<dd>Una matriz de reglas, incluidas palabras clave de consultas y
otros parámetros que definen los filtros de seguimiento. Esta propiedad se aplica a seguimientos basados en reglas, pero no
se aplica a seguimientos agregados.</dd>

<dt>state</dt>
<dd>Debe ser **Activo** o
**Inactivo**. Un seguimiento activo recopila mensajes, mientras que un seguimiento inactivo no. Puede cambiar el
estado de un seguimiento en cualquier momento.

Esta propiedad no se aplica a seguimientos agregados.</dd>

<dt>trackIds</dt>
<dd>Una matriz de ID de seguimiento. Esta propiedad se aplica
únicamente a
seguimientos agregados.</dd>

<dt>type</dt>
<dd>Indica si el tipo de seguimiento es **Regla** o **Agregado**.

Para obtener más información sobre las propiedades del
seguimiento, incluidas las operaciones del seguimiento y el esquema
de modelo, consulte la documentación de la API de REST {{site.data.keyword.twittershort}}.</dd>
</dl>

