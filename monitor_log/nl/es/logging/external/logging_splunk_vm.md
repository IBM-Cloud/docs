---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Ejemplo: Envío de secuencia de registros de aplicaciones de Cloud Foundry a Splunk
{: #splunk}

En este ejemplo, Jane, una desarrolladora, creará un servidor virtual utilizando IBM Virtual Servers Beta y una imagen Ubuntu. Jane intenta enviar una secuencia de registros de app de Cloud Foundry desde {{site.data.keyword.Bluemix_notm}} a Splunk.
{:shortdesc}

  1. Lo primero que hace Jane es configurar Splunk.

     a. Jane descarga Splunk Light desde el [sitio de descarga de Splunk Light ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://www.splunk.com/en_us/download/splunk-light.html){:new_window} y, a continuación, lo instala con el siguiente mandato. El software se instala en */opt/splunk*.

	    ```
        dpkg -i  ~/splunklight-6.3.0-aa7d4b1ccb80-linux-2.6-amd64.deb
        ```

     b. Jane instala y aplica los parches al complemento de tecnología syslog de RFC5424 para realizar la integración con {{site.data.keyword.Bluemix_notm}}. Para obtener más información sobre cómo instalar el complemento, consulte [las directrices de Cloud Foundry ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://docs.cloudfoundry.org/devguide/services/integrate-splunk.html){:new_window}.

	    Jane instala el complemento con los mandatos siguientes:

	    ```
        cd /opt/splunk/etc/apps
        tar xvfz ~/rfc5424-syslog_11.tgz
        ```

        A continuación, aplica los parches al complemento, sustituyendo */opt/splunk/etc/apps/rfc5424/default/transforms.conf* con el nuevo archivo *transforms.conf* que contiene el siguiente texto:


	    ```
        [rfc5424_host]
        DEST_KEY = MetaData:Host
        REGEX = <\d+>\d{1}\s{1}\S+\s{1}(\S+)
        FORMAT = host::$1

        [rfc5424_header]
        REGEX = <(\d+)>\d{1}\s{1}\S+\s{1}\S+\s{1}(\S+)\s{1}(\S+)\s{1}(\S+)
        FORMAT = prival::$1 appname::$2 procid::$3 msgid::$4
        MV_ADD = true
        ```
        {:screen}

     Una vez que Splunk está configurado, Jane debe abrir algunos puertos en la máquina Ubuntu para que acepte la obtención de los syslog entrantes (puerto 5140) y la interfaz de usuario web de Splunk (puerto 8000) porque de forma predeterminada el cortafuegos del servidor virtual de {{site.data.keyword.Bluemix_notm}} está activado. 

	    **Nota:** La configuración de iptable se realiza aquí a efectos de la evaluación que Jane está realizando y es temporal. Para configurar los parámetros del cortafuegos en el servidor virtual Bluemix en producción, consulte la documentación de [Grupos de seguridad de red ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://new-console.ng.bluemix.net/docs/services/networksecuritygroups/index.html){:new_window} para obtener información más detallada. 

	   ```
	   iptables -A INPUT -p tcp --dport 5140 -j ACCEPT
       iptables -A INPUT -p tcp --sport 5140 -j ACCEPT
       iptables -A INPUT -p tcp --dport 8000 -j ACCEPT
       iptables -A INPUT -p tcp --sport 8000 -j ACCEPT
	   ```
	   {:screen}

	   A continuación, Jane ejecuta Splunk utilizando el siguiente mandato: 

       ```
	   /opt/splunk/bin/splunk start --accept-license
       ```

  2. Jane configura los valores de Splunk para aceptar la obtención de syslog desde {{site.data.keyword.Bluemix_notm}}. Debe crear una entrada de datos para la obtención de syslog. 

     a. Desde la interfaz web de Splunk, Jane pulsa **Datos > Entrada de datos**. 
Se visualizará una lista de tipos de entrada a los que Splunk da soporte. 

     b. Selecciona **TCP**, porque la obtención de syslog utiliza el protocolo TCP. 

     c. En el panel de **TCP**, Jane especifica **5140** en el campo **Puerto**, deja los campos restantes en blanco y, a continuación, pulsa **Siguiente**.

     d. Desde la lista de **Tipo de origen**, selecciona **No categorizado > rfc5424_syslog**.

     e. Para el tipo de **Método**, selecciona **IP**.

     f. En el campo **Índice**, pulsa **Crear un nuevo índice**. Le otorga el nombre "bluemix" al nuevo índice y, a continuación, pulsa **Guardar**.

     g. Por último, en la ventana **Revisar**, confirma que los valores son correctos y pulsa **Enviar** para habilitar esta entrada de datos. 

  3. En {{site.data.keyword.Bluemix_notm}}, Jane crea un servicio de obtención de syslog y vincula el servicio a una app. 

     a. Jane crea un servicio de obtención de syslog utilizando el siguiente mandato desde la interfaz de línea de mandatos de cf: 

     ```
     cf cups splunk -l syslog://dummyhost:5140
     ```

     **Nota:** *dummyhost* no es el nombre real. Se utiliza para ocultar el nombre de host real. 

     b. Jane vincula el servicio de obtención de syslog a una app en su espacio y, a continuación, reconstruye la app. 

	 ```
     cf bind-service myapp splunk
     cf restage myapp
     ```


Jane prueba su app y, a continuación, escribe la siguiente serie de consulta en la interfaz web de Splunk: 

```
source="tcp:5140" index="bluemix" sourcetype="rfc5424_syslog"
```

Jane verá una secuencia de registros en su interfaz web de Splunk. A pesar de que la versión de Splunk que Jane instala es Splunk Light, todavía podrá retener hasta 500MB de registros al día. 

