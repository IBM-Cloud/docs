---

copyright:
  years: 2017
lastupdated: "2017-03-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Conexión de servidores IBM UrbanCode Deploy a Delivery Insights
{: #connect_ucd}

Para ver datos de un servidor IBM UrbanCode Deploy en Delivery Insights, es necesario instalar un parche en el servidor y, a continuación, conectar dicho servidor a DevOps Connect.
{:shortdesc}

## Antes de empezar 

- Consulte los [requisitos previos](uc_insights_prereqs.html), incluyendo la configuración de una instancia de DevOps Connect.
- El servidor IBM UrbanCode Deploy debe ser de la versión 6.2 o posterior. 

## Procedimiento


1. Instale el parche en el servidor IBM UrbanCode Deploy. Todas las versiones de IBM UrbanCode Deploy requieren un parche para comunicarse con DevOps Connect. 
  1. Descargue el parche correcto para su versión de IBM UrbanCode Deploy accediendo a la siguiente página y descargando el parche correcto: [http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/](http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/)

  1. Extraiga el archivo. Contendrá uno o varios de los archivos de parche que se deben añadir al servidor. 

  1. Detenga el servidor. Consulte [Inicio y detención del servidor](https://www.ibm.com/support/knowledgecenter/SS4GSP_6.2.3/com.ibm.udeploy.install.doc/topics/run_server.html).

  1. Coloque los archivos de parche en la carpeta <code><em>datos_aplicación</em>/patches</code>, donde <code><em>datos_aplicación</em></code> es la carpeta de los datos de aplicación del servidor. La carpeta de datos de aplicación predeterminada es `/opt/ibm-ucd/server/appdata` en Linux y `C:\Program Files\ibm-ucd\server\appdata` en Windows. En sistemas de alta disponibilidad, la carpeta de datos de aplicación corresponde siempre a una unidad de red compartida a la que cada servidor puede acceder. 

  1. Opcional: Mientras el servidor está detenido, para aumentar el rendimiento de la importación de datos desde este servidor, ejecute los siguientes mandatos SQL en la base de datos:
  
  ```
  create index rt_cpr_submitted_time on MyUCDDatabase.rt_app_process_request(submitted_time); 
  create index rt_cpr_submitted_time on MyUCDDatabase.rt_comp_process_request(component_id, submitted_time);
  ```
  Utilice el nombre de su base de datos en lugar de `MyUCDDatabase`.
  <!-- Ross says that this will not be necessary for versions 6.2.4.1 and later if he gets his code changes in. -->

  1. Inicie el servidor.  

    **Nota:** Es posible que tenga que esperar más que lo que suele hacer para que se inicie el servidor IBM UrbanCode Deploy. Si el servidor finalmente no se inicia, o si no está funcionando correctamente, suprima los archivos de parche y reinicie el servidor. Los archivos de parche no afectan de forma permanente al servidor.

1. Algunas versiones de IBM UrbanCode Deploy requieren un parche adicional en el servidor para conectarse a DevOps Connect. Si está utilizando IBM UrbanCode Deploy versión 6.2 a 6.2.1.2, debe instalar el siguiente parche adicional en el servidor: 
  1. Descargue el parche: [http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/ucd-6.2.1.1-WI149200-CLI-Updates-for-UCSync.jar](http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/ucd-6.2.1.1-WI149200-CLI-Updates-for-UCSync.jar). 
  1. Detenga el servidor. 
  1. Coloque el archivo de parche en la carpeta <code><em>datos_aplicación</em>/patches</code>. 
  1. Inicie el servidor. 

1. Cree una integración entre DevOps Connect y el servidor IBM UrbanCode Deploy:   
  **Importante:** La primera vez que se ejecuta la integración, DevOps Connect recupera datos de los últimos 90 días. Si tiene una gran cantidad de datos de despliegue, este proceso puede tardar mucho tiempo. Para recuperar datos de menos de 90 días, consulte [Resolución de problemas](uc_insights_connect_ucd.html#troubleshooting).
  1. En IBM UrbanCode Deploy, cree una señal de autenticación. Consulte [Señales](https://www.ibm.com/support/knowledgecenter/SS4GSP_6.2.3/com.ibm.udeploy.admin.doc/topics/security_token.html).
  1. En DevOps Connect, pulse **Integraciones**, y, a continuación, pulse **Añadir nueva**.
  1. Especifique un nombre y una descripción para la integración. La ubicación predeterminada de DevOps Connect es `https://hostname:8443/`, donde `hostname` es el nombre de host del sistema que aloja DevOps Connect.
  1. En la lista **Tipo de integración**, seleccione **IBM UrbanCode Deploy for Cloud Reporting**.
  1. En el campo **URI de servidor**, especifique el URL público del servidor IBM UrbanCode Deploy, por ejemplo, `https://my_UCD.example.com:8447`.
  1. En el campo **Señal de autenticación**, especifique o pegue la señal de autenticación que IBM UrbanCode Deploy haya generado. 
  1. En el campo **Usuario de administración**, especifique una lista separada por campos de IBMid para otorgarles acceso a la interfaz DevOps Connect.
  1. Opcional: Pulse **Ejecutar integración** para ejecutar la integración de forma inmediata. De forma predeterminada, las integraciones se ejecutan cada minuto.
  1. Pulse **Guardar**.

  ![Configuración de la integración en DevOps Connect](images/uc_insights_dc_integration.gif)

Ahora sus datos están sincronizados con Delivery Insights. Podrá crear y ver informes que se basan en estos datos.

## Resolución de problemas
{: #troubleshooting}

Si muchas solicitudes de proceso de componentes y aplicaciones se almacenan en la base de datos del servidor IBM UrbanCode Deploy, se pueden producir errores durante el proceso de recuperación. Un mensaje similar al siguiente texto se registra en el registro de salida del servidor: 

`ORA-01652: no es posible extender el segmento temp en 128 en el espacio de tablas TEMP`

Para solucionar este comportamiento, edite el archivo `plugin.properties` para que el plugin reduzca el número de días de datos útiles a recuperar. El archivo `plugin.properties` se encuentra en el directorio `~/.ibm/cloud-sync/plugins/settings/reporting-ucd-plugin/` en el sistema en donde se instaló DevOps Connect. Edite la línea siguiente para eliminar el signo de almohadilla (#) y reducir el número de días:

`#numDaysToRetrieve=90`

Por ejemplo, cambie la línea al texto siguiente para recuperar sólo los últimos 30 días de datos:

`numDaysToRetrieve=30`

Guarde el archivo, y, a continuación, ejecute la integración de nuevo. Consulte los registros del servidor para asegurarse de que ya no se produce el error. 
