---

copyright:
  years: 2016
lastupdated: "2016-10-26"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


<!-- {{site.data.keyword.iotinsurance_full}}  {{site.data.keyword.iotinsurance_short}}  -->


# Instalación y conexión de la app para móvil de ejemplo
{: #iot4i_gettingstarted}

La app para móvil de ejemplo {{site.data.keyword.iotinsurance_full}} es una implementación de referencia para un cliente móvil de {{site.data.keyword.iotinsurance_short}}. Puede utilizar la app para registrar dispositivos nuevos en el sistema y recibir alertas para los dispositivos.
{:shortdesc}

**Requisitos previos:** Antes de comenzar, asegúrese de que se cumplan los siguientes requisitos previos:
  - Entorno de desarrollo integrado Apple Xcode 8 o superior.
  - Un dispositivo móvil iPhone con iOS 9.0 o superior.
  - CocoaPods instalado en su sistema. Consulte el [sitio web de CocoaPods](https://guides.cocoapods.org/using/getting-started.html).
  - Los [parámetros](#iot4i_mobileParam) necesarios para conectar la app para móvil de ejemplo a su instancia del servicio.

## Compilación de la app para móvil de ejemplo
{: #building_mobile}
Para probar la app para móvil de ejemplo, realice las siguientes tareas:

1. Clone el [repositorio de código fuente para la app móvil de ejemplo](https://github.com/ibm-watson-iot/ioti-mobile) en un sistema en el que esté instalado Xcode 7.3 o superior.
2. Instale los paquetes necesarios y genere el archivo IoT4I.xcworkspace ejecutando un mandato pod install de CocoaPods en su proyecto. CocoaPods debe estar instalado para realizar esta tarea.
3. Abra el proyecto en Xcode efectuando una doble pulsación en el archivo IoT4I.xcworkspace.
4. Conecte el iPhone al equipo y selecciónelo como destino de compilación.
5. Seleccione el archivo IoT4I en la lista de archivos para visualizar el recuadro de diálogo Identity.
6. En el recuadro de diálogo Identity en Xcode, realice los siguientes cambios:
  - Cambie el **Bundle Identifier** a un identificador único como, por ejemplo, **myIoT4Ibundle**.
  - Establezca **Team** con su nombre de equipo personal y, a continuación, pulse **Fix Issue**.
7. Para conectar su app a su instancia de {{site.data.keyword.iotinsurance_short}}, establezca los siguientes parámetros en el archivo **constants.swift**:  
    - [applicationRoute](#iot4i_mobileParam) = URL de su instancia de {{site.data.keyword.iotinsurance_short}}
    - [applicationId](#iot4i_mobileParam) = URL de su instancia de {{site.data.keyword.amashort}}
8. En su sistema, pulse la flecha para compilar y ejecutar el esquema actual. La app para móvil de ejemplo está instalada en su teléfono. Para obtener más información, consulte [Apple developer instructions for running apps on devices from Xcode](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/LaunchingYourApponDevices/LaunchingYourApponDevices.html).

  **Nota:** Si, al intentar compilar, se muestra un error que dice *Could not launch IoT4I because you have not yet verified that your Developer App certificate is trusted on your device*, selecciónese usted mismo como desarrollador de confianza tal como se indica a continuación:  
    1. En el teléfono, vaya a **Configuración > General > Gestión de dispositivos > su_ID_desarrollador**.
    2. Pulse el nombre de cuenta de su ID de desarrollador para establecer confianza para su ID de desarrollador.
    3. Cuando se le solicite, confirme que el ID de desarrollador es fiable.

## Habilitación de notificaciones push para la app para móvil.
{: #iot4i_pushNotification}

Realice las siguientes tareas para habilitar las notificaciones push para su dispositivo móvil. Debe tener una cuenta válida de desarrollador de Apple para utilizar el servicio de notificación push.

1. Inicie sesión en su cuenta de desarrollador de Apple en https://developer.apple.com/account.

2. Cree un archivo de certificado.
  1. Seleccione **Certificates, Identifiers & Profiles**.
  2. Seleccione Identifiers: App IDs.
  3. Pulse el botón Add (+) para crear un nuevo ID de app.
  4. Especifique una descripción para la App en **Description**.
  5. Seleccione **Explicit App ID** y especifique un ID de paquete como, por ejemplo, com.YourOrganizationName.iot4i.mobileApp).
  6. Seleccione (V) en **Push Notifications** y pulse **Continue > Register > Done**.

3. Cree un certificado de notificación push.
  1. Seleccione **Certificates: All**.
  2. Pulse el botón Add (+) para crear un nuevo certificado APN.
  3. En la página Add iOS Certificate, seleccione **Apple Push Notification service SSL (Sandbox)** y pulse **Continue**.
  4. Seleccione el ID de app que ha creado en el paso anterior y pulse **Continue**.
  5. Cree un archivo CSR siguiendo las instrucciones que se indican en la página y pulse **Continue**.
  6. Seleccione el archivo CSR que ha creado y pulse **Continue**.
  7. Descargue y ejecute el archivo de certificado.

4. Cree un perfil.
  1. Seleccione **Provisioning profile: Development**.
  2. Pulse el botón Add (+) para crear un nuevo perfil de desarrollo.
  3. Seleccione **iOS App Development** y pulse **Continue**.
  4. Seleccione el ID de app que ha creado antes.
  5. Seleccione **Developer Certificates: All** y pulse **Continue**.
  5. Seleccione **All development devices (testing devices)** y pulse **Continue**.
  6. Especifique un nombre de perfil y pulse **Continue**.
  7. Descargue y ejecute el perfil generado.

5. Cree un archivo PKCS (Public Key Cryptography Standards) 12 y añádalo al servicio {{site.data.keyword.mobilepushshort}}.
  1. Abra Acceso de cadena de claves y seleccione **Mis certificados**.
  2. Pulse con el botón derecho en **Apple Development IOS Push Service: (bundleID)** y exporte, guarde y especifique una contraseña para el archivo.
  3. En la consola de {{site.data.keyword.Bluemix_notm}}, abra el servicio {{site.data.keyword.mobilepushshort}}.
  4. Pulse **Configurar**.
  5. En la sección Certificado de notificaciones push de Apple, suba el archivo PKCS 12 y especifique la contraseña.
  6. En Xcode, cambie el identificador de paquete al que ha creado antes.
  7. Ejecute la app y otorgue permisos para el Servicio de notificaciones Push.

# Enlaces relacionados
{: #rellinks}

## Referencia de API
{: #api}
* [API de {{site.data.keyword.iotinsurance_short}}](https://iot4i-api-docs.mybluemix.net/){:new_window}
* [Ejemplos de API de {{site.data.keyword.iotinsurance_short}}](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/#iot-for-insurance-api-examples){:new_window}

## Enlaces relacionados
{: #general}
* [Documentación de {{site.data.keyword.iot_full}}](https://console.ng.bluemix.net/docs/services/IoT/index.html)
* [Foro de soporte para desarrolladores](https://developer.ibm.com/answers/search.html?f=&type=question&redirect=search%2Fsearch&sort=relevance&q=%2B[iot]%20%2B[bluemix])
* [Foro de soporte de Stack Overflow](http://stackoverflow.com/questions/tagged/ibm-bluemix)
