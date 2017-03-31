---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-10"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Configuración de la conectividad móvil y la seguridad
{: #iot4e_configureMCA}

Habilite las comunicaciones móviles y la seguridad configurando {{site.data.keyword.amafull}}. Esta tarea es necesaria para usar la app móvil de muestra y solo debe hacerse una vez.
{:shortdesc}

Antes de empezar, debe desplegar una instancia del iniciador de {{site.data.keyword.iotelectronics}} en su organización {{site.data.keyword.Bluemix_notm}}. Al desplegar una instancia del iniciador se despliega automáticamente las aplicaciones y los servicios del componente, incluido {{site.data.keyword.amafull}}.

1. En el panel de control {{site.data.keyword.Bluemix_notm}}, abra la aplicación {{site.data.keyword.iotelectronics}}.

   **Consejo:** La aplicación se encuentra en la sección Aplicaciones del panel de control de {{site.data.keyword.Bluemix_notm}}. Asegúrese de pulsar el nombre y no la ruta.

    ![{{site.data.keyword.iotelectronics}} en el panel de control](images/IoT4E_bm_dashboard.svg "{{site.data.keyword.iotelectronics}} en el panel de control")

2. Copie el URL de la app web {{site.data.keyword.iotelectronics}} pulsando con el botón derecho en **Ver app** y seleccionando **Copiar ubicación del enlace**.

3. En el separador **Conexiones**, pulse el servicio {{site.data.keyword.amashort}} para abrirlo.

3. En la página Autenticación de {{site.data.keyword.amashort}}, habilite la autenticación pulsando **Activado**.

4. En la sección **Personalizado**, especifique las siguientes credenciales de autenticación:

    - **Nombre de reino**: `myRealm`

    - **URL de proveedor de identidad personalizado**: pegue el URL de la aplicación API que ha copiado en el primer paso del siguiente formato:   **https://<*myIoT4eStarterApp*>.mybluemix.net**.

    **Importante:** asegúrese de que el URL utiliza el protocolo de seguridad `https` aunque el valor que haya copiado utilice `http`.

    - **URI de redirección de su aplicación web**: deje este campo en blanco.

   ![Configurar {{site.data.keyword.amashort}}.](images/MCA_config_pg.svg "Página de autenticación de {{site.data.keyword.amashort}}")

5. Guarde los valores. Ahora puede volver a la consola de servicio de {{site.data.keyword.iotelectronics}} o a su consola de {{site.data.keyword.Bluemix_notm}}.
