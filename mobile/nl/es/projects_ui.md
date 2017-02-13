---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Utilización de un iniciador de IU para crear un proyecto
{: #projects_ui}

Puede utilizar un [iniciador de IU](starters.html#UI_Starter) en el panel de control de {{site.data.keyword.Bluemix}} Mobile para crear un proyecto en el entorno de {{site.data.keyword.Bluemix_notm}}. Este procedimiento no se aplica a los proyectos que utilizan los Iniciadores de código. Consulte [Creación de un proyecto con un Iniciador de código](projects_code.html) para obtener instrucciones para los Iniciadores de código.
{:shortdesc}

Complete los pasos siguientes para crear un proyecto con un Iniciador de IU:

1. Cree un nuevo proyecto de panel de control de Mobile en {{site.data.keyword.Bluemix_notm}}.

 Empiece con el separador *Guía de inicio* tras seleccionar el catálogo de Mobile. Hay descripciones de iniciadores seleccionados que puede utilizar y las formas distintas de crear un proyecto que depende de cuánta ayuda necesite. Si sólo desea comenzar con la mínima ayuda, seleccione **Crear proyecto**.

 Si ya tiene proyectos, puede seleccionar el separador *Proyectos* mientras se encuentra en el separador *Guía de inicio*. Desde la vista **Proyectos** del panel de control de {{site.data.keyword.Bluemix_notm}} Mobile, puede seleccionar un proyecto con el que trabajar, utilizar las *Acciones* para un proyecto para suprimirlo o descargar el código para el mismo, o crear un nuevo proyecto. Si el proyecto ha empezado desde un Iniciador de IU, también puede abrirlo en el Creador de IU directamente desde el menú *Acciones*. 

	1. En la Consola de {{site.data.keyword.Bluemix_notm}}, seleccione **Mobile** tras expandir el menú con las tres líneas junto al logotipo de {{site.data.keyword.Bluemix_notm}}. 
	
	2. Seleccione **Crear proyecto**. 

	  De forma alternativa, puede seleccionar el separador **Proyectos** para ver los proyectos que ya se encuentran en el entorno móvil y crear un proyecto nuevo pulsando **Crear proyecto**. 

	3. Seleccione el iniciador que coincide mejor con el tipo de aplicación que desea crear y seleccione **Crear proyecto**. Estos son **Iniciadores de IU** e **Iniciadores de código**. Consulte [Iniciadores](starters.html) para obtener más información sobre los iniciadores y cómo utilizarlos. 
	
	4. Especifique un nombre para el proyecto y seleccione **Crear**.
	
2. Realice las selecciones en la pantalla **Visión general del proyecto**.  La pantalla **Visión general del proyecto** muestra información sobre el proyecto y las prestaciones opcionales que puede añadir al mismo, como por ejemplo {{site.data.keyword.mobilepushshort}}.   

	1. Opcional: Seleccione **Añadir** para añadir una de las prestaciones listadas al proyecto. Edite el **Nombre de servicio** para el servicio y pulse **Crear**. Cuando añade un servicio al proyecto, enlaza con la página de {{site.data.keyword.Bluemix_notm}} correspondiente a dicho servicio. Configure el servicio especificando la información necesaria para el mismo.
	
	2. Opcional: Repita el paso *a* para cualquier prestación adicional que desee añadir al proyecto. 

3. Diseñe la interfaz de usuario utilizando el Creador de IU.

   **Nota:** Dado que los Iniciadores de código no tienen una interfaz de usuario personalizable, el separador *Diseño* no está disponible.

    1. Seleccione **Creador de IU** en el menú de navegación para personalizar el diseño de la aplicación. 
	
		**Consejo:** para ver una breve visión general del creador de IU, seleccione **Mostrar cómo funciona** en el panel de navegación después de seleccionar el creador de IU. 
	
	2. Personalice el diseño de la aplicación desde el separador **Pantallas**.
	
	3. Añada pantallas nuevas seleccionando **Crear pantalla**. Asigne un nombre a la pantalla nueva para que sea más fácil su consulta en la aplicación. Puede seleccionar entre los siguientes tipos de pantallas: 
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
	     
		**Aviso:** Si importa datos que no coinciden con la estructura de los datos predeterminados, active el control deslizante *Sustituir esquema*. Un ejemplo sería un archivo .csv que tiene menos columnas que los datos que se proporcionan con el iniciador.
		 
	6. Seleccione **Navegación** para personalizar las acciones de navegación en la app. Esto es opcional ya que las acciones de navegación para muchas de las pantallas se crean automáticamente en función de las relaciones de las pantallas. Puede cambiar la pantalla de destino seleccionando la pantalla o el campo *desde* el que desea ir en la lista de elementos Menú. Luego seleccione la pantalla *a* la que desea ir en el campo Pantalla de destino.  
		 
	7. Seleccione **Acceso de usuarios** en la navegación para modificar los requisitos de acceso del proyecto. Puede activar y desactivar el acceso de usuarios con el conmutador. Cuando el acceso de usuarios esté activado, puede establecer el tiempo de espera de usuarios inactivo y las credenciales de usuarios que pueden acceder a la aplicación.
	
	8. Seleccione **Valores** en el menú de navegación para modificar la información global y los colores para el proyecto. Esta pantalla es donde se especifica la clave de la API de Google, si es necesario para las prestaciones que ha añadido a su proyecto. Esta pantalla también es donde añade su identificador de paquete exclusivo registrado con la Apple Store o la Google Play Store.
	
		Si desea añadir el IBM MobileFirst Foundation SDK al proyecto, active el conmutador.
		
	9. Si ha alternado el conmutador para añadir IBM MobileFirst Platform Foundation a su proyecto en la pantalla *Valores*, se mostrará una selección **Foundation** en la navegación. Seleccione **Foundation** y complete la información necesaria específica para IBM MobileFirst Platform Foundation.
	
	10. Seleccione **Publicar** en el menú de navegación para especificar la información final para crear la aplicación móvil. Puede especificar el identificador de paquetes para iOS y el identificador de aplicaciones para Android.
	
		Si está creando una aplicación de iOS, debe obtener el Identificador de paquetes, el Certificado de distribución como un archivo `.p12` y el Perfil de suministro como un archivo `.mobileprovision` desde el portal de suministro de Apple. El árbol debería crearse al mismo tiempo y con el mismo sistema con el que piensa utilizarlo al publicar la aplicación en la Apple Store. El Certificado de distribución y el Perfil de suministro deben basarse en el Identificador de paquetes.
4. Vuelva a la pantalla *Visión general del proyecto* para recuperar el código para la aplicación y pruébela. Puede descargar el código directamente para los sistemas operativos iOS o Android, o escaneando un código QR para el sistema operativo Android. 


