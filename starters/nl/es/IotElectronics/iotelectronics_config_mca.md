---

copyright:
  years: 2016

---


<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Configuración de conectividad de móvil y seguridad
{: #iot4e_configureMCA}

*Última actualización: 19 de septiembre de 2016*
{: .last-updated}

Habilite las comunicaciones móviles y la seguridad configurando {{site.data.keyword.amafull}}. Esta tarea es necesaria para utilizar la app para móvil de ejemplo y solo es necesario realizarla una vez.
{:shortdesc}

## Antes de empezar

Antes de empezar, debe realizar las tareas siguientes:
  - Despliegue una instancia del iniciador de {{site.data.keyword.iotelectronics}} en su organización de {{site.data.keyword.Bluemix_notm}}. Al desplegar una instancia del iniciador, se despliegan automáticamente las aplicaciones de componente y los servicios, incluido {{site.data.keyword.amafull}}.

  - El proceso de configuración varía ligeramente en función de la versión de la consola de {{site.data.keyword.Bluemix_notm}} que se utilice, por lo que se recomienda leer las instrucciones de la versión correspondiente.

  Puede ver la versión que está utilizando mediante una de las siguientes opciones:
    - [New {{site.data.keyword.Bluemix_notm}}](#configMCAnew). Si está utilizando la experiencia New {{site.data.keyword.Bluemix_notm}}, la opción **Ir a Classic Experience** aparece en la cabecera de sección del panel de control.
    - [Classic {{site.data.keyword.Bluemix_notm}}](#configMCAclassic). Si está utilizando la experiencia Classic {{site.data.keyword.Bluemix_notm}}, la opción **Probar New Bluemix** aparece en la cabecera de sección.

## Configuración de {{site.data.keyword.amashort}} en la experiencia New {{site.data.keyword.Bluemix_notm}}
{: #configMCAnew}

  1. Si acaba de desplegar el iniciador de {{site.data.keyword.iotelectronics}}, se mostrará la pestaña Iniciación de la app de inicio y deberá continuar en el siguiente paso de estas instrucciones. Si no se muestra la app de inicio, abra el panel de control de {{site.data.keyword.Bluemix_notm}} e inicie la aplicación de inicio de {{site.data.keyword.iotelectronics}} pulsando el título correspondiente.

    ![{{site.data.keyword.iotelectronics}} en el panel de control, New Experience](images/IoT4E_bm_dashboard.png "{{site.data.keyword.iotelectronics}} en el panel de control, New Experience")

  2. En la pestaña **Conexiones**, pulse el servicio de {{site.data.keyword.amashort}} para abrirlo.

    ![Cómo encontrar {{site.data.keyword.amashort}}.](images/IoT4E_Connections.png "Conexiones {{site.data.keyword.iotelectronics}} ")

  3. En la página **Autenticación de configuración**, localice el URL de su app de inicio de {{site.data.keyword.iotelectronics}} pulsando **Opciones móviles**. Copie el URL que se encuentra en el campo **Ruta**.

    ![{{site.data.keyword.amashort}} Opciones móviles](images/MCA_config_mobileoptions.png "Opciones móviles {{site.data.keyword.amashort}}")  

  4. En la **sección Personalizar de la página **Autenticación de configuración**, pulse **Configurar**.

       ![Configurar {{site.data.keyword.amashort}}.](images/MCA_config_pg.png "Página Autenticación de configuración {{site.data.keyword.amashort}}")  

  5. Introduzca las credenciales de autenticación siguientes y pulse **Guardar**:
    - **Nombre de reino**: escriba **myRealm**.
    - **URL del proveedor de identidad personalizado**: introduzca el URL que ha copiado antes para identificar la aplicación de inicio de {{site.data.keyword.iotelectronics}} en el formato siguiente: **https://<*myIoT4eStarterApp*>.mybluemix.net**
    - **URI de redirección de la aplicación web**: deje este campo en blanco.

      ![{{site.data.keyword.amashort}} Entrada de autenticación personalizada.](images/MCA_config_pg2.png "Entrada de autenticación personalizada {{site.data.keyword.amashort}}")  

  6. Vuelva a la pestaña Conexiones de la consola del iniciador de {{site.data.keyword.iotelectronics}} pulsando el nombre de la app de inicio, que está en la sección de cabecera.

   ![{{site.data.keyword.amashort}} ruta de navegación.](images/MCA_breadcrumb.png "Ruta de navegación {{site.data.keyword.amashort}}")

## Configuración de {{site.data.keyword.amashort}} en la experiencia Classic {{site.data.keyword.Bluemix_notm}}
{: #configMCAclassic}

1. En el panel de control de {{site.data.keyword.Bluemix_notm}}, inicie la aplicación de inicio de {{site.data.keyword.iotelectronics}} pulsando el mosaico correspondiente.

    ![{{site.data.keyword.iotelectronics}} en el panel de control, Classic.](images/IoT4E_bm_dashboard_c.png "{{site.data.keyword.iotelectronics}} en el panel de control, Classic")

2. En su instancia de {{site.data.keyword.iotelectronics}}, pulse el servicio de {{site.data.keyword.amashort}} para abrirlo.   

  ![Cómo encontrar {{site.data.keyword.amashort}}.](images/IoT4E_Connections_c.png "Conexiones {{site.data.keyword.iotelectronics}} ")

2. En la página **Autenticación de configuración**, localice el URL de su app de inicio de {{site.data.keyword.iotelectronics}} pulsando **Opciones móviles**. Copie el URL que se encuentra en el campo **Ruta**.

  ![{{site.data.keyword.amashort}} Opciones móviles](images/MCA_config_mobileoptions.png "Opciones móviles {{site.data.keyword.amashort}}")  

3. En la **sección Personalizar de la página **Autenticación de configuración**, pulse **Configurar**.

 ![Configurar {{site.data.keyword.amashort}}.](images/MCA_config_pg.png "Página Autenticación de configuración {{site.data.keyword.amashort}}")  

4. Introduzca las credenciales de autenticación siguientes y pulse **Guardar**:
   - **Nombre de reino**: escriba **myRealm**.
   - **URL del proveedor de identidad personalizado**: introduzca el URL que ha copiado antes para identificar la aplicación de inicio de {{site.data.keyword.iotelectronics}} en el formato siguiente: **https://<*myIoT4eStarterApp*>.mybluemix.net**
   - **URI de redirección de la aplicación web**: deje este campo en blanco.

    ![{{site.data.keyword.amashort}} Entrada de autenticación personalizada.](images/MCA_config_pg2.png "Entrada de autenticación personalizada {{site.data.keyword.amashort}}")  

5. Vuelva a la pestaña Conexiones de la consola de iniciador de {{site.data.keyword.iotelectronics}} como se indica a continuación:
  1. Visualice el menú pulsando la flecha doble junto a **Volver al panel de control** en la sección de cabecera.
  2. Pulse **Visión general** para volver a la consola de iniciador.  

    ![{{site.data.keyword.amashort}} ruta de navegación.](images/MCA_breadcrumb_c.png "Ruta de navegación {{site.data.keyword.amashort}}")
