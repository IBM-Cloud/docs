---

copyright:
  years: 2016, 2017
lastupdated: "2017-05-02"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Habilitación de SMS y mensajería de voz
{: #supportedcloud}

{{site.data.keyword.iotinsurance_full}} da soporte a la integración con Twilio para habilitar SMS y mensajería de voz. Twilio es una aplicación de terceros, que puede instalar en su panel de control de {{site.data.keyword.Bluemix_notm}}.
{: shortdesc}

## Requisitos previos
Para habilitar la mensajería de voz, debe tener una cuenta de Twilio autorizada y un número de teléfono de origen de Twilio. Si utiliza una cuenta gratuita de Twilio, también debe autorizar un número de teléfono para recibir llamadas o mensajes. Para obtener más información, consulte la [documentación de Twilio ![Icono de enlace externo](../../icons/launch-glyph.svg)](https://support.twilio.com/hc/en-us/articles/223136107-How-does-Twilio-s-Free-Trial-work-){:new_window}.

## Creación y configuración de una instancia de Twilio
1. Cree una instancia de Twilio en la misma organización y espacio de {{site.data.keyword.Bluemix_notm}} en la que ha instalado {{site.data.keyword.iotinsurance_short}}.
    1. Inicie la sesión en [{{site.data.keyword.Bluemix_notm}}](https://console.ng.bluemix.net).
    2. Seleccione el separador **Catálogo**.
    3. Localice la sección Móvil del catálogo de servicios y pulse **Twilio**.

    **Consejo:** Pulse [aquí ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.ng.bluemix.net/catalog/services/twilio/){: new_window} para ir directamente a la página de Twilio.
    {: tip}

    4. En la página de Twilio, proporcione sus credenciales y enlace la aplicación, como se indica a continuación:

      1. Escriba `Twilio-00` como nombre de servicio. **Importante:** Debe utilizar `Twilio-00` para conectarse correctamente a {{site.data.keyword.iotinsurance_short}}.

      2. Escriba sus credenciales de Twilio.

      3. En el menú **Conectar a**, seleccione la aplicación iot4i-action-engine para enlazar la instancia de Twilio con {{site.data.keyword.iotinsurance_short}}.

      4. Pulse **Crear**.  

    La aplicación de Twilio se instala en su entorno. Un mensaje le solicita que vuelva a transferir o reinicie la aplicación iot4i-action-engine para habilitar el enlace. Puede reiniciar ahora o esperar hasta que haya añadido la variable de entorno en el paso siguiente.

2. Cree una variable de entorno denominada TWILIO_FROM_NUMBER para el componente iot4i-action-engine.
    1. Desde el panel de control de Bluemix, abra la aplicación iot4i-action-engine.
    2. Seleccione **Tiempo de ejecución** y, a continuación, pulse **Variables de entorno**.
    3. En la sección **Definido por el usuario**, pulse **Añadir**.
    4. En a columna Nombre, escriba `TWILIO_FROM_NUMBER` y en la columna Valor escriba su número de voz y que permita SMS de Twilio.
    5. Pulse **Guardar**.

3. Reinicie la aplicación Iot4i-action-engine pulsando el icono Reiniciar situado junto al botón Rutas.

## Adición de las acciones de SMS y voz a una cobertura

Para añadir funciones de SMS y voz a una cobertura, debe añadir las acciones siguientes en la definición de cobertura:
  - `send-sms`
  - `phone-call`

Para ver un ejemplo de una cobertura que contiene una lista de acciones, consulte el [ejemplo de creación de una cobertura de muestra ![Icono de enlace externo](../../icons/launch-glyph.svg)](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/blob/master/bl/shield.js){:new_window}. En el ejemplo, las acciones de SMS y voz pueden añadirse a la lista de acciones que contiene las acciones `email` y `pushios`.

Para obtener más información sobre la creación de coberturas, consulte [Utilización del kit de herramientas de cobertura](iotinsurance_shield_toolkit.html).
