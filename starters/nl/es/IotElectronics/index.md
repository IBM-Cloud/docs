---

copyright:
  years: 2016

---

{:new_window: target="_blank"}

{:shortdesc: .shortdesc}


# Creación de apps con el iniciador de {{site.data.keyword.iotelectronics}}
*Última actualización: 14 de junio de 2016*

{{site.data.keyword.iotelectronics_full}} es una solución integrada de extremo a extremo que permite a las apps comunicarse con, controlar, analizar y actualizar dispositivos conectados. El iniciador incluye una app de inicio que le permite crear y controlar dispositivos simulados y una app para móvil que le permite controlar estos dispositivos desde el dispositivo móvil.
{:shortdesc}

**Requisito previo**:  
Asegúrese de que ha desplegado el Iniciador de {{site.data.keyword.iotelectronics}} en la sección Contenedores modelo del catálogo de Bluemix. Si lo hace automáticamente se despliegan las aplicaciones de componentes y servicios del iniciador, incluido {{site.data.keyword.amafull}}.

Para empezar con {{site.data.keyword.iotelectronics}}, realice estas tareas tal como se describe en las secciones que siguien a continuación: 

1. Habilite las comunicaciones con la app para móvil de ejemplo configurando {{site.data.keyword.amashort}}.
2. Cree dispositivos simulados utilizando la aplicación web de iniciador  de {{site.data.keyword.iotelectronics}}.
3. Instale y conecte la app para móvil de ejemplo.

## Configuración de {{site.data.keyword.amashort}}
{: #configureMCA}
Para utilizar la app para móvil, debe configurar {{site.data.keyword.amashort}}, tal como se indica a continuación: 
1. En el panel de control de {{site.data.keyword.Bluemix_notm}}, abra [{{site.data.keyword.amashort}}](https://new-console.ng.bluemix.net/docs/services/mobileaccess/overview.html).
2. En la sección **Personalizado**, seleccione **Configurar**.
3. Especifique las siguientes credenciales de autenticación:
  - **Nombre de reino**: myRealm
  - **URL**: https://<*myIoT4eStarterApp*>.mybluemix.net  

    **Sugerencia:** asegúrese de utilizar el prefijo `https://` segundo en el URL. Puede encontrar el URL de la app de inicio pulsando **Opciones móviles**.)
4. Guarde los datos.

  Para obtener
instrucciones detalladas, consulte [Configuración
de {{site.data.keyword.amashort}}](iotelectronics_config_mobile.html#iot4e_configureMCA).

##Creación de dispositivos simulados
Para crear un dispositivo simulado, efectúe los pasos siguientes:
1. En el panel de control de {{site.data.keyword.Bluemix_notm}}, inicie la aplicación {{site.data.keyword.iotelectronics}}
2. Espere a que aparezca el mensaje de estado `La app está ejecutándose` y pulse **Ver app** para visualizar la app de inicio.
  
3. Seleccione **Controlar de forma remota los dispositivos conectados**
4. Desplácese a la sección con la etiqueta **A continuación, elija o añada una nueva arandela simulada** y pulse el botón Añadir (+). Se crea una nueva arandela.

## Instalación y conexión de la app para móvil de ejemplo
Para instalar y conectar la app para móvil de ejemplo, efectúe los pasos siguientes: 

*Nota*: debe tener un dispositivo iOS para utilizar la app para móvil de ejemplo.

1. En el teléfono, abra App Store y busque `ibm iot`. Elija  **IBM IoT for Electronics** y realice la instalación.
2. Conecte el teléfono con su organización explorando el código QR de conexión que ha encontrado en la app de inicio. 
3. Conecte el dispositivo simulado explorando el código QR de dispositivo encontrado en la app de inicio. 

  Para obtener instrucciones detalladas, consulte [Conexión de la app para móvil con el entorno de {{site.data.keyword.iotelectronics}}](iotelectronics_config_mobile.html#iot4e_connecting_mobile)

##Qué hacer a continuación
Vea lo que puede hacer con {{site.data.keyword.iotelectronics}}.

- Explorar la app de inicio para experimentar cómo una empresa de producción puede supervisar dispositivos conectados a {{site.data.keyword.iot_short_notm}}.
- Explorar la app para móvil para experimentar cómo pueden registrar e interactuar con sus dispositivos los propietarios de aplicaciones.

- Provocar manualmente una anomalía en el dispositivo para desencadenar alertas, notificaciones y acciones en el fabricante y el propietario del dispositivo.

- Asociar datos operativos con datos de usuario para entender cómo funcionan los productos y dispositivos y quién los hace funcionar. 


# Enlaces relacionados 
{: #rellinks}
## Documentación de la API
{: #api}
* [{{site.data.keyword.iotelectronics}}](http://ibmiotforelectronics.mybluemix.net/public/iot4eregistrationapi.html)
* [{{site.data.keyword.iotrtinsights_short}}](https://iotrti-prod.mam.ibmserviceengage.com/apidoc/)  
* [{{site.data.keyword.iot_short}}](https://developer.ibm.com/iotfoundation/recipes/api-documentation/)


## Componentes 
{: #general}

* [Documentación de {{site.data.keyword.iotelectronics_full}}](iotelectronics_overview.html)
* [{{site.data.keyword.iot_full}}](https://new-console.ng.bluemix.net/docs/services/IoT/index.html)
* [{{site.data.keyword.iotrtinsights_full}}](https://new-console.ng.bluemix.net/docs/services/iotrtinsights/iotrtinsights_overview.html)
* [{{site.data.keyword.amafull}}](https://new-console.ng.bluemix.net/docs/services/mobileaccess/overview.html)
* [{{site.data.keyword.sdk4nodefull}}](https://new-console.ng.bluemix.net/docs/runtimes/nodejs/index.html#nodejs_runtime)

## Ejemplos
{: #samples}
* [App para móvil de ejemplo](https://new-console.ng.bluemix.net/docs/starters/IotElectronics/iotelectronics_config_mobile.html)
