---

copyright:

  years: 2015, 2017
lastupdated: "2017-05-10"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Gestión de claves de API
{: #manapikey}

Una clave de interfaz de programación de aplicaciones (clave de API) es un código que se pasa en una llamada en un programa informático a una interfaz de programación de aplicaciones (API) para identificar el programa que realiza la llamada, su desarrollador o su usuario para el sitio web. Las claves de API se utilizan para realizar un seguimiento y un control sobre la forma la que se utiliza la API, por ejemplo, para impedir un uso malintencionado o abusivo de la misma (tal como quizás se defina este uso en los términos del servicio).  La clave de API a menudo actúa a la vez como un identificador exclusivo y como una señal secreta para la autenticación, y habitualmente tiene un conjunto de derechos de acceso en la API asociada. Las claves de API se pueden basar en un sistema de UUID (Universally Unique Identifier) para asegurarse de que son únicas para cada usuario. 

Como usuario de {{site.data.keyword.Bluemix_notm}}, podría desear utilizar una clave de API al habilitar un programa o script sin distribuir su contraseña al script. Otra ventaja en la utilización de una clave de API, es que un usuario o una organización pueden crear varias claves de API para distintos programas y que es posible suprimirlas de forma independiente si están en riesgo sin interferir con otras claves de API o incluso el usuario. Además, como [usuario federado](/docs/admin/adminpublic.html#federatedid), se puede utilizar una clave de API para iniciar una sesión. Para obtener más información sobre la utilización de una clave de API para iniciar una sesión, consulte la documentación del mandato [`bluemix login` de la CLI de {{site.data.keyword.Bluemix_notm}}](/docs/cli/reference/bluemix_cli/bx_cli.html#bluemix_login) y el [mandato `cf login` de la CLI de cf](/docs/cli/reference/cfcommands/index.html#cf_login).  

Utilice la ventana Claves de API de Bluemix para gestionar sus claves de API de {{site.data.keyword.Bluemix_notm}}.
Vaya a **Gestionar** &gt; **Seguridad** &gt; **Claves de API de Bluemix** para ver una lista de sus claves de API con descripciones y fechas. 
Desde esta página se pueden crear, editar o suprimir claves de API. 

Siga estos pasos para crear una clave de API: 

1. Vaya a **Gestionar** &gt; **Seguridad** &gt; **Claves de API de Bluemix**. 
2. Pulse **Crear una clave de API**.
3. Especifique un nombre y una descripción para su clave de API. 
4. Pulse **Crear una clave de API**.
5. A continuación, pulse **Mostrar** para visualizar, copiar y guardar la clave de API para más tarde, o pulse **Descargar clave de API**. 

**Nota**: La clave de API únicamente está disponible para ser mostrada o descargada en el momento de su creación. Si se pierde la clave de API, deberá crear una nueva clave de API. 

Siga estos pasos para editar una clave de API: 

1. Vaya a **Gestionar** &gt; **Seguridad** &gt; **Claves de API de Bluemix**. 
2. Desde el menú **Acciones** de una clave de API que aparezca listada en la tabla, pulse **Editar nombre y descripción ** 
3. Actualice la información de su clave de API. 
4. Pulse **Actualizar clave de API**.

Siga estos pasos para suprimir una clave de API:  

1. Vaya a **Gestionar** &gt; **Seguridad** &gt; **Claves de API de Bluemix**. 
2. Desde el menú **Acciones** de una clave de API que aparezca en la lista en la tabla, pulse **Suprimir**.
3. A continuación, confirme la supresión pulsando **Suprimir clave**.

También puede utilizar la CLI de {{site.data.keyword.Bluemix_notm}} para gestionar sus claves de API listando sus claves, creando claves, actualizando claves o suprimiendo claves. Consulte la sección del mandato [`bluemix iam api-keys`](/docs/cli/reference/bluemix_cli/bx_cli.html#bluemix_iam) para obtener más información. 

