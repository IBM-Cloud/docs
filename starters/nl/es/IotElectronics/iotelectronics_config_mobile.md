---

copyright:
  years: 2016

---


<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Utilización de la app para móvil
{: #iot4e_using_mobile}
*Última actualización: 19 de septiembre de 2016*
{: .last-updated}

Empiece a utilizar la app para móvil de {{site.data.keyword.iotelectronics_full}} para ver cómo puede recibir alertas, enviar mandatos y comprobar el estado de los dispositivos conectados.
{:shortdesc}

## Antes de empezar

Antes de utilizar la app para móvil, debe completar las siguientes tareas:
  - Despliegue una instancia del iniciador de {{site.data.keyword.iotelectronics}} en su organización de {{site.data.keyword.Bluemix_notm}}. Al desplegar una instancia del iniciador, se despliegan automáticamente las aplicaciones de componente y los servicios del iniciador.
  - [Habilite las comunicaciones móviles y la seguridad](iotelectronics_config_mca.html) configurando {{site.data.keyword.amafull}}.

## Iniciación a la aplicación para móvil
Para empezar con la aplicación para móvil, realice las tareas siguientes:
1. [Descargue la aplicación para móvil](#iot4e_downloadmobile) a su dispositivo móvil.
2. [Conecte la aplicación para móvil al entorno de {{site.data.keyword.iotelectronics}}](#iot4e_connecting_mobile) y registre los dispositivos.


 ### Descarga de la app para móvil
 {: #iot4e_downloadmobile}
 Para obtener la app para móvil, descárguela e instálela en el teléfono desde la tienda Apple App.  En el teléfono, abra la open la App Store y busque "ibm iot". Elija **IBM IoT for Electronics** e instálela.

 Como alternativa puede instalarla en el teléfono utilizando [iTunes](https://itunes.apple.com/us/app/ibm-iot-for-electronics/id1103404928?ls=1&mt=8).


### Conexión de la aplicación para móvil
{: #iot4e_connecting_mobile}

Para conectar la aplicación para móvil a su entorno y registrar sus dispositivos, realice las siguientes tareas:

1. Abra la aplicación de inicio de {{site.data.keyword.itoelectronics}}. Para obtener instrucciones, consulte [Apertura de la aplicación de inicio](iot4ecreatingappliances.html#iot4e_openAppMain).

2. Seleccione **Controlar de forma remota los dispositivos conectados**.

    ![{{site.data.keyword.iotelectronics}} experiencia iniciador](images/IoT4E_remotely_option.png "Experiencia iniciador {{site.data.keyword.iotelectronics}}")

3. Cree una o varias arandelas desplazándose a la sección con la etiqueta **A continuación, elija o añada una nueva arandela simulada** y pulsando a continuación el icono +. Se crea una nueva arandela.

    ![Añadir arandela](images/IoT4E_add_washer.png "Añadir arandela")

4.	Desplácese por el código QR de conexión y explórelo utilizando el dispositivo móvil. El código QR de Conexión se encuentra en la sección con la etiqueta **Para conectar la app con el entorno, se le solicitará que explore este código QR**.

  ![Código QR de conexión.](images/iot4e_mobile_connect_QR.png "Código QR de conexión {{site.data.keyword.iotelectronics}} ")

5. En el dispositivo móvil, escriba sus credenciales de inicio de sesión. El ID de usuario y la contraseña pueden tener cualquier longitud. Recuerde las credenciales de inicio de sesión para sesiones futuras. Ahora su dispositivo móvil está registrado en el entorno de {{site.data.keyword.iotelectronics}} y puede registrar dispositivos individuales.

6. En el sistema, desplácese hasta una arandela simulada y púlsela para visualizar sus datos y el código QR de dispositivo.

  ![Seleccione una arandela.](images/IoT4E_mobile_washer_QR.png "Seleccione una arandela.")

7.	Utilice el dispositivo móvil para explorar el código QR de la arandela. Ahora la arandela está registrada y el estado correspondiente se muestra en el teléfono móvil.

#### Qué hacer a continuación
Ahora puede ver alertas y controlar la arandela mediante el dispositivo móvil. Siga estos pasos para probarlo:
  - En el sistema, seleccione un problema con la arandela, como la anomalía de la placa o la vibración fuerte. El problema envía una alerta al teléfono móvil.
  - En el dispositivo móvil, pulse **Iniciar arandela** para iniciar la máquina. Puede ver el cambio de estado de la arandela en el sistema a medida que avanza por los ciclos correspondientes.
