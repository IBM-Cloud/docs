---

copyright:
  años: 2015,2016

---

{:new_window: target=_"blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Iniciación a {{site.data.keyword.iotrtinsights_full}}
{: #gettingstartedtemplate}
*Última actualización: 11 de febrero de 2016*

Con {{site.data.keyword.iotrtinsights_full}} en Bluemix ({{site.data.keyword.iotrtinsights_short}}), puede realizar analíticas en datos en tiempo real desde los dispositivos Internet of Things, y obtener perspectivas sobre su estado y el estado general de las operaciones.
{:shortdesc}

Antes de poder empezar a utilizar {{site.data.keyword.iotrtinsights_short}}, debe configurar el servicio {{site.data.keyword.iot_full}} ({{site.data.keyword.iot_short}}) para conectar el motor de analíticas a los dispositivos. Puede utilizar un servicio {{site.data.keyword.iot_short}} existente o crear uno nuevo. Para empezar a configurar y a ejecutar rápidamente, puede desplegar la aplicación telefónica Internet of Things y su servicio de {{site.data.keyword.iot_short}} asociado en la organización.

Para empezar a configurar y a ejecutar rápidamente este servicio, siga estos pasos:
1. Despliegue el servicio {{site.data.keyword.iotrtinsights_short}} en la organización Bluemix.
  1. Desde el panel de control de la cuenta de Bluemix, pulse **Utilizar servicios o API**.
  2. Localice la sección Internet of Things del catálogo de servicios y seleccione **{{site.data.keyword.iotrtinsights_short}}**.
  3. En la página {{site.data.keyword.iotrtinsights_short}}, verifique las selecciones de Añadir servicio:  
    - Espacio - Verifique que está desplegando el servicio en el mismo espacio en que ha desplegado el servicio de {{site.data.keyword.iot_short}}.
    - App - Déjela desenlazada.
    - Nombre de servicio - Cambie opcionalmente el nombre de servicio a algo que sea fácil de recordar. Este nombre se muestra en el mosaico de {{site.data.keyword.iotrtinsights_short}} IoT en el panel de control de Bluemix.
    - Plan seleccionado - Seleccione Gratuito o un plan de compra que sea adecuado a sus necesidades.  
    > **Importante:** Con el plan de {{site.data.keyword.iotrtinsights_short}} gratuito, solo puede desplegar una instancia del servicio por organización.
  4. Pulse **Utilizar** para desplegar {{site.data.keyword.iotrtinsights_short}} en los servicios de Bluemix.
2. Opcional: Utilice su teléfono como un dispositivo IoT con {{site.data.keyword.iotrtinsights_short}} IoT.
Utilice la aplicación telefónica Internet of Things para configurar rápidamente su teléfono inteligente para que actúe como un dispositivo IoT que puede utilizar para verificar el entorno de {{site.data.keyword.iotrtinsights_short}} y comenzar a definir las analíticas en tiempo real en los datos. Para obtener más información sobre la aplicación Internet of Things Phone, consulte el proyecto [aplicación telefónica Internet of Things](https://github.com/ibm-messaging/IoT-html5-phone).

  Para crear la aplicación y conectar el teléfono a {{site.data.keyword.iot_full}}:
  1. Pulse el botón de abajo para iniciar el proceso de despliegue:
  [![Desplegar en un icono de Bluemix.](images/deploy_to_bluemix.png "Desplegar en un icono de Bluemix")](https://bluemix.net/deploy?repository=https://github.com/ibm-messaging/iot-html5-phone "Desplegar el Teléfono de IoT en Bluemix")  
  > **Nota:** El despliegue de la aplicación telefónica de Internet of Things también despliega un servicio {{site.data.keyword.iot_short}} (*iot-phone-iotf-service*) que se enlaza automáticamente a la aplicación telefónica. Añada esta {{site.data.keyword.iot_short}} como un origen de datos para probar la aplicación telefónica Internet of Things. También crea un servicio Cloudant NoSQL DB (*iot-phone-cloudant-cloudantNoSQLDB*) que utilizará la aplicación.

  2. Pulse **Aprobar** si se le solicita que apruebe por sí mismo el acceso para IBM Single Sign On Service (OAuth Consent).  
  >**Consejo:** Si no tiene una cuenta de Bluemix, puede registrarse para activar la cuenta de prueba gratuita de Bluemix.
  2. Cambie el campo APP NAME a algo fácil de recordar; llamaremos a esto *aplicación telefónica* en el resto de estas instrucciones. Este nombre se mostrará en un mosaico de aplicaciones del panel de control de Bluemix y forma parte del URL que se utilizará al conectar el teléfono a {{site.data.keyword.iot_short}}.
  2. Pulse **Desplegar**.
  2. Una vez que se haya completado el proceso de despliegue y que vea un mensaje 'Success', vuelva al panel de control de Bluemix. El mosaico *aplicación telefónica* y el mosaico *iot-phone-iotf-service* se añadirán a la cuenta.
  1. Desde el panel de control de Bluemix, pulse el mosaico *aplicación telefónica*.
  2. Desde el teléfono, abra un navegador y vaya a la URL Rutas que aparece debajo del nombre de la aplicación. Cuando se le solicite, especifique un ID de dispositivo de su elección para identificar el teléfono como un dispositivo en los paneles de control de {{site.data.keyword.iot_short}} y de {{site.data.keyword.iotrtinsights_short}} IoT.
  3. Pulse **Conectar** para conectar el teléfono al *iot-phone-iotf-service* de {{site.data.keyword.iot_short}}.
  La vista se renueva para visualizar los datos que se envían desde el teléfono a su {{site.data.keyword.iot_short}}.
2. Cree y configurar un servicio de Internet of Things.  
> **Consejo:** Si ha desplegado la aplicación telefónica Internet of Things, el *iot-phone-iotf-service* ya se ha creado y puede omitir este paso.  

  1. Inicie la sesión en la organización Bluemix y seleccione el espacio en el que desea desplegar {{site.data.keyword.iotrtinsights_short}} IoT.
  2. Desde el Panel de control de Bluemix, pulse **Utilizar servicios o API**.
  3. Localice la sección Internet of Things del catálogo de servicios y seleccione **Internet of Things**.
  4. En la página {{site.data.keyword.iot_full}}, verifique las selecciones Añadir servicio y pulse **Utilizar** para añadir {{site.data.keyword.iot_short}} a los servicios de Bluemix.
  Una vez que se haya desplegado el servicio de {{site.data.keyword.iot_short}}, se le dirigirá a la página de gestión de servicio.
3. Localice las claves de la API de conexión.
Si ha creado un nuevo servicio {{site.data.keyword.iot_short}}, ahora debe crear claves de API para conectar los dos servicios. Si está utilizando un servicio existente, puede utilizar las claves existentes.  
  1. Desde el panel de control de Bluemix, pulse el mosaico Internet of Things.  
  >**Nota:** Si está utilizando la aplicación telefónica Internet of Things, pulse el mosaico *iot-phone-iotf-service*.  

  1. Pulse **Iniciar panel de control** para abrir el panel de control de {{site.data.keyword.iot_full}}.
  2. Vaya a **Acceder > Claves de API**.
  3. Pulse **Generar clave de API**.
  3. Tome nota de la clave de API, de la señal de autenticación y del ID de organización que se visualiza en la parte superior del panel de control de {{site.data.keyword.iot_short}}.
  Utilice esta información en {{site.data.keyword.iotrtinsights_short}} IoT para conectar los servicios.
4. Conecte el servicio {{site.data.keyword.iot_short}} y el servicio {{site.data.keyword.iotrtinsights_short}} IoT.
  1. Desde el panel de control de Bluemix, pulse el mosaico {{site.data.keyword.iotrtinsights_short}} IoT.  
  2. En la página de servicio, pulse **Añadir un origen de datos**.
  2. En la página Gestionar orígenes de datos de la consola de {{site.data.keyword.iotrtinsights_short}}, pulse **Añadir nuevo origen de datos**.
  3. Otorgue al origen de datos un nombre descriptivo y proporcione la información siguiente que ha recopilado anteriormente:
    - ID de organización
    - Clave de API
    - Señal de autenticación
  4. Pulse ![Crear icono.](images/create.png "Crear icono") para crear el origen de datos y conectarse a él.
4. Empiece utilizando {{site.data.keyword.iotrtinsights_short}}.
Ahora puede empezar a utilizar {{site.data.keyword.iotrtinsights_short}} añadiendo usuarios, conectando los dispositivos, configurando paneles de control para ver datos de dispositivos relevantes y configurando alertas.
>**Selección de la instancia de {{site.data.keyword.iotrtinsights_short}}:** Si se le ha otorgado acceso a cualquier instancia adicional de {{site.data.keyword.iotrtinsights_short}} como un operador o administrador, puede conmutar rápidamente entre estas instancias. En la consola de {{site.data.keyword.iotrtinsights_short}}, pulse el nombre de usuario y seleccione la instancia a la que desee acceder.   

# rellinks
## muestras
* [aplicación telefónica Internet of Things](https://github.com/ibm-messaging/IoT-html5-phone)
* [recetas de Internet of Things de developerWorks](https://developer.ibm.com/recipes/)
* [Creación de apps con la aplicación de inicio Internet of Things](https://www.ng.bluemix.net/docs/starters/IoT/iot500.html#iot500)

## api
* [Documentación de la API](https://iotrti-prod.mam.ibmserviceengage.com/apidoc/)

## general
* [Acerca de](iotrtinsights_overview.html)   
* [Novedades de Servicios de Bluemix](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category)
* [Iniciación a {{site.data.keyword.iot_full}}](https://www.ng.bluemix.net/docs/services/IoT/index.html)
* [dW Answers en IBM developerWorks](https://developer.ibm.com/answers/topics/iot-real-time/)
