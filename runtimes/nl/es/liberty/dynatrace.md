---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Utilización de Dynatrace
{: #using_dynatrace}

*Última actualización: 08 de abril de 2016*

Dynatrace es un servicio de otro proveedor que proporciona supervisión de la aplicación.

Para obtener más información acerca de lo que proporciona el servicio de Dynatrace, consulte [Supervisión de la aplicación Dynatrace](http://www.dynatrace.com/en/products/application-monitoring.html).

Cuando se habilita el servicio Dynatrace que se utilizará con la app de Liberty, siga estos pasos del proceso:

1. Adquiera y aloje el archivo jar del agente de Dynatrace para que el paquete de compilación de Liberty pueda descargarlo.
2. Configure una instancia del servidor de Dynatrace para que el agente de Dynatrace que se ejecuta con la app de Liberty pueda comunicarse con ella.
3. Configure la app de Liberty para que pueda descargar el agente de Dynatrace y conectarse con el servidor de Dynatrace.

## Alojamiento del agente de Dynatrace
{: #hosting_dynatrace_agent}
El agente de Dynatrace debe estar alojado en un servidor web, y el paquete de compilación de Liberty debe ser capaz de descargar el jar del agente desde dicho servidor. El servidor debe estar configurado con un archivo index.yml que especifique los detalles sobre el jar del agente. Complete los pasos que se muestran a continuación para configurar el agente de Dynatrace:
  1. Descargue el jar del agente de Dynatrace. Consulte [Instaladores de la plataforma del servidor de Dynatrace](https://community.dynatrace.com/community/display/EVAL/Step+1+-+Download+and+install+Dynatrace) en el sitio web de la comunidad de Dynatrace para obtener instrucciones sobre la descarga del jar del agente de Dynatrace. El archivo jar del agente apropiado para la ejecución en Bluemix es el **dynatrace-agent-unix.jar** versión **6.3.0+**.
  2. Aloje el archivo jar del agente en una ubicación desde la que el paquete de compilación de Liberty pueda descargarlo. Puede alojarlo en el mismo Bluemix utilizando cualquiera de los recursos del servidor disponibles, o puede alojarlo en alguna ubicación disponible de forma pública.
     * Asegúrese de que se proporciona un archivo index.yml en la ubicación de alojamiento. El archivo index.yml debe contener una entrada que conste del ID de versión del jar del agente seguido por dos puntos y el URL completo de la ubicación de ese jar de agente. Por ejemplo:
```
      ---
      6.3.0: https://my-dynatrace-agent.mybluemix.net/dynatrace-agent-6.3.0-unix.jar
```
{: #codeblock}
     * Al final del URL, el nombre del archivo jar debe ser **dynatrace-agent-version-unix.jar**. La versión debe ser **6.3.0** o **6.3.0_nnnn**, donde nnnn es el identificador de la microversión. Tenga en cuenta que este puede ser distinto del nombre de archivo jar que Dynatrace utiliza y, por lo tanto, podría solicitarle que cambie el nombre del jar.       
     * El archivo **dynatrace-agent-6.3.0-unix.jar** debe estar disponible en la ubicación especificada en el archivo index.yml. La ubicación para el archivo jar y el index.yml puede ser el mismo directorio.

## Configuración del recopilador de Dynatrace

A continuación, deberá configurar un recopilador de Dynatrace que es accesible en el agente de Dynatrace. También debe crear un servicio proporcionado por el usuario para pasar información para el agente de Dynatrace para que se conecte con el recopilador de Dynatrace. Consulte [Arquitectura de Dynatrace](https://community.dynatrace.com/community/display/DOCDT63/Architecture) para comprender mejor la relación entre componentes de Dynatrace.

  1. Configure un recopilador de Dynatrace.
    * Consulte el [sitio web de la comunidad de Dynatrace](https://community.dynatrace.com/community/display/EVAL/Step+3+-+Connect+Agent+to+Dynatrace) para obtener instrucciones sobre la descarga y configuración del recopilador de Dynatrace.
    * Asegúrese de que el recopilador se configura en una ubicación que sea accesible para el agente de Dynatrace que se ejecuta con la app en Bluemix.
  2. Cree un servicio proporcionado por el usuario que apunte al recopilador de Dynatrace en ejecución. <b>NOTA</b> El nombre del servicio proporcionado por el usuario debe contener <b>dynatrace</b>. Por ejemplo, utilice el mandato que aparece a continuación:
```
    $ cf cups my-dynatrace-collector -p '{"server":"DynatraceCollectorIPaddress","profile":"Monitoring"}'
```
{: #codeblock}
En este ejemplo, my-dynatrace-collector es el nombre proporcionado al servicio, DynatraceCollectorIPaddress es la dirección IP del recopilador de Dynatrace que ha configurado, y el perfil es el nombre de perfil de Dynatrace opcional asociado con esta app supervisada. El valor del perfil predeterminado es Monitoring. Puede especificar los parámetros opcionales como en el ejemplo que se indica a continuación.
```
    $ cf cups my-dynatrace-collector -p '{"server":"DynatraceCollectorIPaddress","profile":"Monitoring",
                                          "options" : {
                                                       "dynatrace-parameter-1": "value",
                                                       "dynatrace-parameter-2": "value"
                                         }}'
```
{: #codeblock}
Consulte [Sección establecimiento del agente de la configuración del agente](https://community.dynatrace.com/community/display/DOCDT62/Agent+Configuration) en el sitio web de la comunidad de Dynatrace para obtener más información sobre las opciones disponibles. Por ejemplo, utilizando la opción de exclusión, puede excluir las clases que supervisa Dynatrace. Consulte [Infraestructura del agente de DynaTrace](https://github.com/cloudfoundry/ibm-websphere-liberty-buildpack/blob/master/docs/framework-dynatrace-agent.md) para obtener más detalles sobre cómo configurar el servicio proporcionado por el usuario.
  3. Una vez que haya enviado la app a Bluemix, enlace el servicio proporcionado por el usuario que ha creado a la app. Por ejemplo, utilice el mandato
```
    $ cf bs myApp my-dynatrace-service
```
**Nota**: Debe volver a transferir la aplicación después de enlazar el servicio.

## Configuración de la app de Liberty
{: #configuring_liberty_app}

La app de Liberty que desea supervisar deben estar configurada para localizar el servidor en el que se encuentra el jar del agente que ha establecido previamente. Puede configurar la app con la variable de entorno de **JBP_CONFIG_DYNATRACEAGENT**. La variable de entorno de **JBP_CONFIG_DYNATRACEAGENT** indica al paquete de compilación desde dónde se debe descargar el agente de Dynatrace. Para establecer la variable de entorno, siga estos pasos:
<ol>
   <li> Establezca la variable **JBP_CONFIG_DYNATRACEAGENT** para que tenga el valor
   *"repository_root: URL_of_server_hosting_index.yml"*. Por ejemplo, después de enviar la aplicación, emita el siguiente mandato:
```
    $ cf se myApp JBP_CONFIG_DYNATRACEAGENT 'repository_root: https://my-dynatrace-agent-host.mybluemix.net'
```
{: #codeblock}
  En este ejemplo, *my-dynatrace-agent-host.mybluemix.net* es el URL del archivo index.yml alojado por el servidor que ha configurado previamente.
  </li>
  <li> Después de establecer la variable de entorno, vuelva a transferir la aplicación. El staging_task.log para la aplicación de Liberty emite un mensaje que indica que se ha descargado correctamente el agente de Dynatrace desde el servidor de alojamiento del agente. Por ejemplo:
```
    Descarga de dynatrace-agent-6.3.0-unix.jar 6.3.0 de https://my-dynatrace-agent-host.mybluemix.net/dynatrace-agent-6.3.0-unix.jar (17,8 s)
```
{: #codeblock}
</li>
<li>Para ver el staging_task.log, emita el siguiente mandato:
```
    $ cf files myAppName logs/staging_task.log
```
{: #codeblock}
</li>
</ol>

# rellinks
## general
* [Tiempo de ejecución de Liberty](index.html)
* [Visión general del perfil de Liberty](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
