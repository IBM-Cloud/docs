---

copyright:
  years: 2017
lastupdated: "2017-04-13"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Gestión de API
{: #manage_apis}

Después de integrar su API para que la gestione y supervise el sistema de gestión de API, puede ver y modificar los valores de la API. Si no ha integrado la API, debe integrarla siguiendo el procedimiento de [Creación de API desde acciones de {{site.data.keyword.openwhisk_short}}](manage_openwhisk_apis.html). 

Para gestionar los valores de la API, siga los pasos siguientes:

Si ha creado una API nueva, y ya está abierta en la interfaz, puede omitir los tres primeros pasos.

1. Seleccione la API que desea gestionar seleccionando una acción en el panel de control del servicio {{site.data.keyword.openwhisk_short}}, si la información sobre la API aún no se muestra. 
2. Seleccione el separador **API** si es necesario.
3. Seleccione la API que desea gestionar, si es necesario. Cuando se establezca una conexión, podrá ver y actualizar las selecciones siguientes: 
    * Resumen
    * Definición
    * Compartición
    * Explorador de API
4. Seleccione el graduador Exponer API gestionadas para activarlo y exponer sus API. Nota: algunos de los valores no se pueden definir si la API no está expuesta.   

## Resumen de valores correspondientes a las API
{: #overview_api}

El separador Resumen se selecciona de forma predeterminada cuando se selecciona una API y está dividido en dos secciones:
* Propiedades - En la sección Propiedades, puede ver la información siguiente:
    * Información básica sobre la API
	* Políticas de seguridad
	* Información sobre la tasa límite
    * Detalles del uso compartido
* Sección Análisis y registro - En la sección Análisis y registro, puede ver las siguientes estadísticas: 
	* Número de respuestas y tiempo medio de respuesta durante el último intervalo de tiempo especificado
    * Número de llamadas de API por minuto en formato gráfico
    * 100 últimas respuestas en la tabla Registro de respuestas
	
El gráfico *Respuestas* muestra una representación rápida del modo en que se recibe su API y un desglose del estado de las respuestas. Esto le puede ayudar a determinar si está recibiendo una mayoría de respuestas de error. Una mayoría de respuestas de error puede indicar que tiene más tráfico del que ha permitido en los valores de tasa. Puede ver un desglose numérico de las respuestas por código de respuesta pasando el puntero del ratón sobre el icono de información. Son comunes los siguientes códigos de respuesta: 
* 200  Correcto
* 201  Creado
* 302  Encontrado
* 304  No modificado
* 400  Solicitud incorrecta
* 401  No autorizado
* 403  Prohibido
* 500  Error interno del servidor
* 503  Servicio no disponible

La tabla Registro de respuestas contiene detalles individuales de las 100 últimas respuestas. Puede clasificar la información de acuerdo con las entradas de una columna seleccionando la cabecera de la columna. Puede buscar entradas específicas en la tabla Registro de respuestas mediante la barra *Buscar respuestas*. Para ver más información sobre un suceso, selecciónelo o seleccione **Ver detalles** en la lista del menú de opciones (tres puntos verticales) que hay junto a la entrada.


## Edición de los valores de la API
{: #settings_api}

En el separador **Definición**, puede actualizar la información básica sobre la API. Esta información incluye documentación, nombre y URL base. Utilice la sección Seguridad y limitación de tasa para especificar un límite de llamadas y de intervalo para asegurarse de que solo se realicen una determinada cantidad de llamadas por segundo, por minuto o por hora. También puede hacer que se necesite autenticación para crear llamadas de API, con el fin de evitar un uso no deseado de sus datos o para obtener estadísticas sobre las API. 

Para cambiar los valores correspondientes a una API, siga estos pasos: 

1. En el panel de control de gestión de API, pulse el separador **Definición**. 
2. Puede asignar un nombre o actualizar el nombre de la API e importar una definición de API en la sección Información de API. 
3. En la sección Seguridad y limitación de tasa, puede actualizar las políticas siguientes:
    * Requerir clave de API- Especifica si la llamada de API sólo se puede procesar si se especifica la clave de API correcta. El valor predeterminado no requiere una clave adicional.
    * Método de seguridad - Cuando la opción Clave de API está seleccionada, especifica si para procesar la API solo se necesita la API de clave o si se necesita tanto la clave de API como el secreto de API.
    * Ubicación de la clave y el secreto de API - En función del valor correspondiente al método, especifica cómo se incluye la seguridad de API en la llamada. Los nombres de invocación especifican cómo se identifica la información de seguridad. 
    * Limitar la tasa de llamadas de API - Establece el número de llamadas de API permitido durante un determinado intervalo de tiempo, con la opción de definirlo para cada clave. Tenga en cuenta que se utiliza un método burst-type (tipo de ráfaga) de limitación de tasa. La tasa media de llamadas de API se calcula durante el intervalo de tiempo total que especifique en la tasa. Si la tasa de llamadas de API durante un intervalo supera la tasa media de llamadas de API, podría haber un periodo de llamadas denegadas hasta alcanzar el límite de tiempo especificado en la tasa.    
    * Proveedor de OAuth - Garantiza que los usuarios con los parámetros de seguridad correctos puedan acceder a sus API, aplicando OAuth mediante credenciales de inicio de sesión social de proveedores como Google, Facebook, IBM y GitHub.
4. Habilitar CORS - CORS (Cross-origin Requests) permite algunas solicitudes limitadas procedentes de otro dominio. 
5. Pulse **Guardar**. 

## Compartición de API
{: #share_api}

Puede compartir sus API con otros usuarios dentro o fuera de la organización de {{site.data.keyword.Bluemix_notm}}. 

Cuando comparte API con otros, dentro o fuera de su organización de {{site.data.keyword.Bluemix_notm}}, puede crear claves para sus API. Cada API gestionada permite 5 claves que se pueden crear y a asignar a dicha API. Si envía una clave exclusiva a un individuo o empresa, puede realizar un seguimiento de algunas estadísticas sobre el modo en que se utiliza la API. Por ejemplo, puede realizar un seguimiento del número de llamadas a la API realizadas por dicha persona o empresa.

También puede limitar el número de llamadas a la clave, inhabilitar una clave o limitar las llamadas desde una clave. Este puede resultar útil durante las pruebas, el equilibrio de la carga de trabajo, la supervisión o para resolver algunas situaciones de seguridad.  

1. En el panel de control de gestión de API, pulse el separador **Compartición**. 
2. Dentro del área "Compartir dentro de la organización de {{site.data.keyword.Bluemix_notm}}", seleccione **Compartir API con todos los usuarios de la organización de Bluemix** si desea que la API esté disponible para todos los usuarios con acceso a su organización de {{site.data.keyword.Bluemix_notm}}. Esta opción debe estar seleccionada para generar una clave. 
3. Pulse **Crear clave de API** para crear una clave exclusiva para la API. Aparece el recuadro de diálogo Crear clave de API. La clave API se genera automáticamente.
4. Utilice la API clave para determinar qué usuario accede a la API mediante el envío al usuario de una clave exclusiva. La pasarela puede determinar qué clave (cliente) genera la llamada.
5. Pulse el icono **Menú** (tres puntos verticales) que hay junto a la clave para editar o suprimir esta clave de API. 

En la sección Compartición fuera de la organización de {{site.data.keyword.Bluemix_notm}}, puede compartir su API con usuarios que no tengan una cuenta de {{site.data.keyword.Bluemix_notm}}. Este método para compartir proporciona un enlace directo para ver información acerca de la API en el Explorador de API. La API contiene un botón para ejecutar la API en la vista del Explorador de API. Para solicitar un enlace para la API, siga los pasos siguientes:

1. En la sección "Compartición fuera de la organización de {{site.data.keyword.Bluemix_notm}}". Pulse **Crear clave de API**. Aparece el recuadro de diálogo Crear clave de API. Tenga en cuenta que el usuario tiene un secreto que usted no puede controlar. 
2. Especifique un nombre exclusivo para la clave de API. 
3. Seleccione **Crear clave**. 
4. Envíe el enlace del portal de la API al cliente que no tiene cuenta de {{site.data.keyword.Bluemix_notm}}. La clave y el secreto de la API (si se utiliza) se incluyen en el enlace, por lo que puede determinar qué clave ha generado el enlace.
  
El enlace a la documentación de la API abre la API en el separador **Explorador de API**. 

## Visualización y prueba con el Explorador de API
{: #explore_api}

Seleccione el separador Explorador de API para ver el HTML generado a partir del documento Swagger.  

El Explorador de API muestra todas las acciones de la API y la documentación que se aplica a la API. Puede ver las operaciones y las acciones y sus descripciones y probar la API desde la interfaz de usuario. También puede descargar el documento Swagger para reutilizar su contenido.

Para probar la API, siga los pasos siguientes:
1. *Ejemplos* está seleccionado de forma predeterminada. Muestra un ejemplo del código correspondiente a la API seleccionada.
2. Cambie el formato del ejemplo, si es necesario, seleccionando un lenguaje en el menú que se encuentra junto al lenguaje especificado. 
3. Seleccione **Probarlo**.
4. Seleccione **Llamar operación**. 

Se muestra la respuesta a la solicitud.    
