---

copyright:
  years: 2016, 2017
lastupdated: "2016-12-15"

---
{:new_window: target="_blank"}

# Guía de aprendizaje: Iniciador de IU del Catálogo de almacenamiento
{: #tutorial_store_catalog}

El Iniciador de IU del Catálogo de almacenamiento de {{site.data.keyword.Bluemix}} proporciona una estructura de aplicaciones de ventas básica que puede personalizar, y le proporciona puntos de integración para cada servicio de {{site.data.keyword.Bluemix_notm}} Mobile.


## Requisitos
{: #tutorial_requirements}

* Una cuenta de [Bluemix ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](http://bluemix.net "icono de enlace externo")


## Guía de inicio
{: #tutorial_gs}

Para comenzar a utilizar rápidamente el Iniciador de IU del Catálogo de almacenamiento, siga estos pasos:

1. Cree un proyecto de panel de control de Mobile en {{site.data.keyword.Bluemix_notm}}.

   1. Desde la página **Guía de inicio** del panel de control de Mobile, pulse **Crear proyecto**.

      De forma alternativa, puede pulsar **Crear proyecto** en la página **Proyectos**.

   2. Seleccione **Iniciadores de IU**, si aún no lo ha seleccionado.

   3. Seleccione **Almacenar catálogo** y pulse **Crear proyecto**.

   4. Especifique el nombre de proyecto y pulse **Crear**.

2. Opcional: Añada la función de {{site.data.keyword.mobilepushshort}}. 

   1. Pulse **Añadir** para **{{site.data.keyword.mobilepushshort}}** en la página **Visión general del proyecto**.

      De forma alternativa, puede pulsar **Crear** en la página **{{site.data.keyword.mobilepushshort}}**. 

   2. Especifique el nombre del servicio y pulse **Crear**.

   3. Para iOS, [configure el servicio de notificación Push de Apple ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](/docs/services/mobilepush/t_push_provider_ios.html "icono de enlace externo"){: new_window}.

   4. Para Android, [configure Google Cloud Messaging ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](/docs/services/mobilepush/t_push_provider_android.html "icono de enlace externo"){: new_window}.

3. Opcional: Añada otras funciones.

   1. Pulse **Añadir** para la función en la página **Visión general del proyecto**.

   2. Especifique el nombre del servicio y pulse **Crear**.

   3. Siga las instrucciones suministradas con el servicio para configurarlo.

4. Diseñe la aplicación.

   1. Seleccione **Creador de IU** en el menú de navegación para personalizar el diseño de la aplicación.
   
		**Consejo:** para ver una breve visión general del creador de IU, seleccione **Mostrar cómo funciona** en el panel de navegación después de seleccionar el creador de IU.

   2. Seleccione el separador **Diseño** en la navegación.

      Hay un espacio de trabajo para el diseño de la aplicación y una vista simulada del aspecto de la misma.

   3. Opcionalmente, añada pantallas nuevas seleccionando **Crear pantalla**. Ponga un nombre a la pantalla nueva para que sea más fácil su consulta en la aplicación. Se crearán pantallas nuevas en el mismo nivel que la pantalla principal, independientemente de lo seleccionado en el árbol. Puede seleccionar desde los siguientes tipos de pantallas:
      * Menú
      * Lista
      * Correlación
      * Personalizada
      * Gráfica	   

   4. Puede cambiar el título del menú de la aplicación seleccionando el recuadro de texto *Menú* en la sección **Diseño** de la interfaz y sustituyendo el contenido en el campo **Datos a visualizar**. Visualice las actualizaciones en la sección del dispositivo simulada.

      Actualice los elementos de diseño seleccionando cada uno de ellos y actualizando la información, según sea necesario. Estos elementos se muestran en un formato de árbol. Puede cambiar el orden o la ubicación de los elementos de menú arrastrando un elemento a una nueva ubicación. Todos los elementos secundarios del elemento también se moverán con el elemento principal. La información textual de los elementos de árbol que se muestra en los campos **Datos a visualizar** hace referencia al contenido de la hoja de cálculo del origen de los datos. *No cambie estos elementos en la vista **Diseño** porque se sobrescriben mediante el contenido de los Orígenes de datos identificados en la vista de **Datos**.*

		Un elemento identificado en el árbol como un *Formulario* es independiente y se puede modificar en línea. No hace referencia a la información de un Origen de datos.

   5. Seleccione **Datos** en la navegación para ver los datos que utiliza la aplicación. Hay información predeterminada en la plantilla; sin embargo, puede cambiar el origen de los datos seleccionando **Crear nuevo**. Puede hacer referencia a más de un origen de datos, por lo que proporcione un nombre para cada uno de los que utilice. Puede seleccionar desde las siguientes opciones de origen de datos:
      * Cloud
      * Local
      * Cloudant
      * Google Sheet
      * Excel Online
      * Google Drive

      También puede importar, exportar o modificar el contenido que se encuentra en la tabla, si es local, utilizando los botones y seleccionando el contenido en la tabla.

	  Aviso: Si importa datos que no coinciden con la estructura de los datos predeterminados, active el control deslizante *Sustituir esquema*. Un ejemplo sería un archivo .csv que tiene menos columnas que los datos que se proporcionan con el iniciador.
	  
   6. Seleccione **Navegación** para personalizar las acciones de navegación en la app. Esto es opcional ya que las acciones de navegación para muchas de las pantallas se crean automáticamente en función de las relaciones de las pantallas. Puede cambiar la pantalla de destino seleccionando la pantalla o el campo *desde* el que desea ir en la lista de elementos Menú. Luego seleccione la pantalla *a* la que desea ir en el campo Pantalla de destino.  

   7. Seleccione **Acceso de usuarios** en la navegación para modificar los requisitos de acceso del proyecto. Puede activar y desactivar el acceso de usuarios con el conmutador. Cuando el acceso de usuarios esté activado, puede establecer el tiempo de espera de usuarios inactivo y las credenciales de usuarios que pueden acceder a la aplicación.

   8. Seleccione **Valores** en el menú de navegación para modificar la información global y los colores para el proyecto. Esta pantalla es donde se especifica la clave de la API de Google, si es necesario para los servicios que ha añadido a su proyecto. Esta pantalla también es donde añade su identificador de paquete exclusivo registrado con la Apple Store o la Google Play Store.

      Si desea añadir el IBM MobileFirst Foundation SDK al proyecto, active el conmutador.

   9. Si ha alternado el conmutador para añadir IBM MobileFirst Platform Foundation a su proyecto en la pantalla *Valores*, se mostrará una selección **Foundation** en la navegación. Seleccione **Foundation** y complete la información necesaria específica para IBM MobileFirst Platform Foundation.

   10. Seleccione **Publicar** en el menú de navegación para especificar la información final necesaria para crear la aplicación móvil. Puede especificar el identificador de paquetes para iOS y el identificador de aplicaciones para Android.

       Si está creando una aplicación de iOS, debe obtener el Identificador de paquetes, el Certificado de distribución como un archivo *.p12* y el Perfil de suministro como un archivo *.mobileprovision* desde el portal de suministro de Apple. El árbol debería crearse al mismo tiempo y con el mismo sistema con el que piensa utilizarlo al publicar la aplicación en la Apple Store. El Certificado de distribución y el Perfil de suministro deben basarse en el Identificador de paquetes. 	

5. Descargue el proyecto.

   1. Pulse **Código** y seleccione la plataforma o el lenguaje de programación preferidos.

   2. Para Android, puede elegir entre las siguientes opciones una vez que se genere el código:

      * Descargar código

      * Descargar APK

      * Descargar con código QR

   3. Para iOS, puede elegir la siguiente opción una vez que se genere el código:

      * Descargar código

6. Ejecute la app en su dispositivo o simulador.


## Qué hacer a continuación
{: #tutorial_next}

[¡Pruébelo!![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](http://console.{DomainName}/mobile/create-project?starter=fb5e31a9-1186-4d46-939e-2f620f35b83b "icono de enlace externo"){: new_window}


### Guías de aprendizaje del Iniciador de IU
{: #tutorials_UI}

* [Guía de aprendizaje: Catálogo de almacenamiento](tutorial_store_catalog.html)


### Guías de aprendizaje del Iniciador de código
{: #tutorials_Code}

* [Guía de aprendizaje: Basic](tutorial.html)
* [Guía de aprendizaje: Cloudant Sync](tutorial_cloudant_synd.html)
* [Guía de aprendizaje: {{site.data.keyword.openwhisk_short}}](tutorial_openwhisk.html)
* [Guía de aprendizaje: {{site.data.keyword.visualrecognitionshort}}](tutorial_visual_recognition.html)
* [Guía de aprendizaje: Lenguaje Watson](tutorial_watson_language.html)
* [Guía de aprendizaje: Weather](tutorial_weather.html)

