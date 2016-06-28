---

copyright:
  years: 2016

---


<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Utilización de la app para móvil
{: #iot4e_using_mobile}
*Última actualización: 14 de junio de 2016*

Empiece a utilizar la app para móvil de {{site.data.keyword.iotelectronics_full}} para ver cómo puede recibir alertas, enviar mandatos y comprobar el estado de los dispositivos conectados.
{:shortdesc}

Complete las siguientes tareas:
1. [Descargue la app para móvil](#iot4e_downloadmobile)
2. [Configure {{site.data.keyword.amafull}}](#iot4e_configureMCA)
3. [Conecte el dispositivo móvil con el entorno de {{site.data.keyword.iotelectronics}}](#iot4e_connecting_mobile)
4. [Registre y controle un dispositivo en el dispositivo móvil](#iot4e_adding_appliance)


 ## Descarga de la app para móvil
 {: #iot4e_downloadmobile}
Para obtener la app para móvil, descárguela e instálela en el teléfono desde la tienda Apple App. En el teléfono, abra la open la App Store y busque "ibm iot". Elija **IBM IoT for Electronics** e instálela. 

 Como alternativa puede instalarla en el teléfono utilizando [iTunes](https://itunes.apple.com/us/app/ibm-iot-for-electronics/id1103404928?ls=1&mt=8).

## Configuración de {{site.data.keyword.amashort}}
{: #iot4e_configureMCA}

Para poder conectarse a la app para móvil, debe configurar {{site.data.keyword.amafull}}.  

  1. En el separador **Conexiones** de {{site.data.keyword.iotelectronics}}, abra la aplicación {{site.data.keyword.amashort}}. (También puede acceder a la aplicación desde el panel de control de {{site.data.keyword.Bluemix_notm}}.)  

    ![Cómo encontrar {{site.data.keyword.amashort}}.](images/IoT4E_Connections.svg "Conexiones {{site.data.keyword.iotelectronics}} ")

  2. En la sección **Personalizado**, pulse **Configurar**.

   ![Configurar {{site.data.keyword.amashort}}.](images/MCA_config_pg.svg "{{site.data.keyword.amashort}} Configurar página de autenticación")  

  3. Especifique las siguientes credenciales de autenticación: 
    - **Nombre de reino**: escriba **myRealm**.
    - **URL**: escriba el URL para identificar la app de inicio de {{site.data.keyword.iotelectronics}} en el siguiente formato:**https://<*myIoT4eStarterApp*>.mybluemix.net**  

      **Sugerencia:** asegúrese de utilizar el prefijo `https://` segundo en el URL. Puede encontrar el URL de la app de inicio pulsando **Opciones móviles**.)


  ![{{site.data.keyword.amashort}} Entrada de autenticación personalizada.](images/MCA_config_pg2.svg "{{site.data.keyword.amashort}} Entrada de autenticación personalizada")  

  4. Guarde los datos.

## Conexión de la app para móvil con el entorno de {{site.data.keyword.iotelectronics}}
{: #iot4e_connecting_mobile}

Para ver los dispositivos simulados en la app para móvil, debe conectar la app para móvil con el entorno de {{site.data.keyword.iotelectronics}} Bluemix.

Para conectar la app para móvil, siga estos pasos:

  1. En el sistema, inicie la aplicación {{site.data.keyword.iotelectronics}} y pulse **Ver app** para visualizar la app de inicio.  

  ![{{site.data.keyword.iotelectronics}}  Página de Cómo empezar con Ver app resaltado.](images/IoT4E_getting_started.svg "{{site.data.keyword.iotelectronics}} Página de Cómo empezar con Ver app")  
  2. Seleccione **Controlar de forma remota los dispositivos conectados**.

  ![Seleccione la experiencia de la app de consumidor de {{site.data.keyword.iotelectronics}}.](images/IoT4E_consumer_app.svg "{{site.data.keyword.iotelectronics}} Experiencia de app de consumidor")

  3. Cree una o más arandelas. La app para móvil no puede conectarse hasta que se crea una arandela.

  4.	Desplácese por el código QR de conexión y explórelo utilizando el dispositivo móvil. El código QR de Conexión se encuentra en la sección con la etiqueta `Para conectar la app con el entorno, se le solicitará que explore este código QR`.

  ![Explore el código QR de conexión de {{site.data.keyword.iotelectronics}}.](images/iot4e_mobile_connect_QR.svg "{{site.data.keyword.iotelectronics}} Código QR de conexión")

  5. Escriba las credenciales de inicio de sesión. El ID de usuario y la contraseña pueden tener cualquier longitud. Recuerde las credenciales de inicio de sesión para sesiones futuras.  

## Registro y control de un dispositivo en el dispositivo móvil
{: #iot4e_adding_appliance}

Para ver el estado del dispositivo y recibir notificaciones, debe registrar el dispositivo utilizando la app para móvil.

Para registrar un dispositivo, realice los siguientes pasos:

  1. En el sistema, desplácese hasta una arandela simulada y púlsela para visualizar sus datos y el código QR de dispositivo. 

![Seleccione una arandela.](images/IoT4E_mobile_washer_QR.svg "Seleccione una arandela.")

  3.	Utilice el dispositivo móvil para explorar el código QR de la arandela para registrar la arandela en el teléfono móvil. Verá el estado de la arandela en el teléfono móvil.

  4. En el sistema, seleccione un problema con la arandela, como la anomalía de la placa o la vibración fuerte. El problema envía una alerta al teléfono móvil.
