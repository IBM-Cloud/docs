---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

#Acceso al sistema
{: #system_access}
Estos temas incluyen métodos de creación y gestión de una instancia de servicio, junto con varias formas de acceder a los sistemas y configurar el acceso.
{: shortdesc}

*Última actualización: 8 de junio de 2016*
{: .last-updated}

## Uso de la API REST en WebSphere Application Server para {{site.data.keyword.Bluemix_notm}}
{: #restapi_usage}

Las instancias de WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} se crean, suministran, gestionan y suprimen de una de las siguientes formas:


* En el Panel de control de catálogo y servicio de {{site.data.keyword.Bluemix_notm}} en la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}.
* En la creación de una aplicación o script que utiliza nuestras API de RESTful.

Mediante el uso de las API REST compatible con Swagger 2.0, los clientes tienen acceso a la misma función como se ha proporcionado a través del portal y panel de control. Para obtener más información sobre las API REST y los recursos soportados, consultee WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} [Documentación de API REST](https://new-console.{DomainName}/apidocs/212){: new_window}.

**Nota:** después de crear una instancia de servicio, en función del tamaño de Camiseta que se crea, el servicio puede no estar listo inmediatamente para su uso. Se recomienda consultar el campo **Estado** del JSON devuelto para determinar el estado actual de la instancia de servicio.

**Nota:** de forma predeterminada, el URL base de API apunta a un punto final en la [Región EE.UU. sur](https://wasaas-broker.ng.bluemix.net/wasaas-broker/api/v1){: new_window}.  Si utiliza la Región de Gran Bretaña o Sídney, asegúrese de que la aplicación utiliza uno de los siguientes puntos finales:


* [Región de Gran Bretaña](https://wasaas-broker.eu-gb.bluemix.net/wasaas-broker/api/v1){: new_window}
* [Región de Sídney](https://wasaas-broker.au-syd.bluemix.net/wasaas-broker/api/v1){: new_window}


## Panel de control de servicio
{: #service_dashboard}

Después de crear la instancia de servicio, se le conducirá el panel de control de servicio. Siempre puede volver al panel de control de servicio pulsando el icono de servicio desde el panel de control de la organización.
Desde el panel de instrumentos de servicio puede acceder a:

*  Un enlace a esta documentación
*  Un enlace para descargar los archivos de configuración de OpenVPN necesarios.
*  La capacidad de iniciar y detener la máquina virtual. La VM se inicia al principio.
*  Al nombre de host.
*  Al usuario admin y a la contraseña admin.
*  A la clave SSH privada.
*  Al usuario admin y a la contraseña admin de WebSphere®.
*  A los URL del centro y de la consola de administración.

**Nota**: debido a una cantidad específica de recursos de cálculo, memoria y entrada y salida, los clientes tienen un cargo para VM acumuladas en el estado DETENIDO a una tasa reducida del 5%. Los clientes se gestionan en un número fijo de instancias DETENIDAS con no más de 10 direcciones IP o 64 GB de memoria.



## Configuración de openVPN para WebSphere Application Server para instancias de Bluemix
{: #setup_openvpn}

OpenVPN es necesario para acceder a cualquier máquina virtual de WebSphere Application Server on Bluemix. Debe instalarlo y ejecutarlo con privilegios de administrador.  

### Utilice estas instrucciones para configurar openVPN en Windows:

1. Desde el enlace [descargar openVPN Windows](http://swupdate.openvpn.org/community/releases/), descargue:
  * [openvpn-install-2.3.4-I001-x86_64.exe](https://swupdate.openvpn.org/community/releases/openvpn-install-2.3.4-I001-x86_64.exe){: new_window} para 64 bits o
  * [openvpn-install-2.3.4-I001-i686.exe](https://swupdate.openvpn.org/community/releases/openvpn-install-2.3.4-I001-i686.exe){: new_window} para 32 bits.
2. Asegúrese de que [ejecuta como administrador de Windows](https://technet.microsoft.com/en-us/magazine/ff431742.aspx){: new_window} e instale openVPN.
3. Descargue los archivos de configuración de VPN desde el enlace de descarga de OpenVPN de la instancia de WebSphere Application Server para Bluemix en el panel de instrumentos de servicios. Extraiga los cuatro archivos en el archivo comprimido en el directorio **{inicio OpenVPN}\config**.   Por ejemplo:

  <pre>  
    C:\Program Files\OpenVPN\Config
  </pre>
  {: codeblock}

4. Inicie el programa cliente openVPN "OpenVPN GUI". Asegúrese de que selecciona [Ejecutar como administrador de Windows](https://technet.microsoft.com/en-us/magazine/ff431742.aspx){: new_window} para iniciar el programa. Si no lo hace, no podrá conectarse.

### Utilice estas instrucciones para configurar openVPN en Linux:
1. Para instalar openVPN, siga estas [instrucciones](https://openvpn.net/index.php/access-server/docs/admin-guides/182-how-to-connect-to-access-server-with-linux-clients.html){: new_window}.
  * Si necesita descargar e instalar manualmente el gestor de paquetes de RPM, vaya a la [descarga de openVPN unix/linux](https://openvpn.net/index.php/access-server/download-openvpn-as-sw.html){: new_window}. Es posible que necesite ayuda del administrador de Linux.
3. Descargue los archivos de configuración de VPN desde el enlace de descarga de OpenVPN de la instancia de WebSphere Application Server para Bluemix en el panel de instrumentos de servicios. Extraiga los archivos en el directorio desde el que tiene previsto iniciar el cliente openVPN. Necesita los cuatro archivos en el mismo directorio.
3. Inicie el programa cliente openVPN.  Abra una ventana de terminal y vaya al directorio que contiene los archivos de configuración. Ejecute el mandato siguiente como usuario root:

  <pre>
      $ openvpn --config vt-wasaas-wasaas.ovpn
  </pre>
  {: codeblock}  

### Utilice las siguientes instrucciones para configurar openVPN en Mac:
1. Un método consiste en instalar [Tunnelblick](https://tunnelblick.net/){: new_window}, un producto de software de código abierto.
2. Extraiga los archivos de configuración de VPN desde el servicio de WebSphere. Tunnelblick le solicita la contraseña de administrador para Mac y añade la configuración al conjunto de VPN que puede utilizar para conectarse.
3. Conéctese a la red de VPN y, a continuación, podrá acceder a la máquina virtual. Después del primer acceso, Tunnelblick almacena en la memoria caché la configuración y puede conectarse desde [Tunnelblick](https://tunnelblick.net/){: new_window}. Puede colocar un icono en la barra de menús de la parte superior para un acceso más fácil.


## Utilización de SSH para acceder a WebSphere Application Server para máquinas virtuales de Bluemix
{: #using_ssh}

En estas instrucciones se da por supuesto que utiliza OpenSSH como cliente. OpenSSH está disponible normalmente en Linux o en Cygwin ejecutándose en Windows. También puede instalarse para ejecutarse desde un indicador de mandatos de Windows.

Para verificar la instalación de OpenSSH, introduzca este mandato:
  ```
      $ ssh -V
  ```
  {: codeblock}

La respuesta debería ser parecida a esta:
  ```
      OpenSSH_6.6p1, OpenSSL 1.0.1g 7 Apr 2014
  ```
  {: codeblock}

Utilice las instrucciones siguientes para configurar el acceso SSH a las VM de WebSphere Application Server para Bluemix:

1. Revise el mensaje de aviso que aparece la primera vez que se conecta, "La autenticidad del host  x.x.x.x no se puede establecer." Esto es normal. Cuando se le solicite, seleccione Sí. La clave pública ahora se instala en la VM para el usuario
"virtuser".
2. Inicie sesión en virtuser utilizando la clave privada. Para obtener mejores resultados, utilice el método de autenticación de clave privada.
3. Copie el contenido de la clave privada en un archivo.
4. Ejecute el mandato:

  <pre>
    $ ssh virtuser@169.53.246.xxx -i /path/privateKeyFileName
  </pre>
  {: codeblock}

5. Obtenga autoridad completa sysadmin cambiando del usuario virtuser al usuario root con este mandato:

  <pre>
    $ sudo su root
  </pre>
  {: codeblock}

6. Si experimenta problemas al acceder al sistema con la clave ssh privada, utilice la contraseña de usuario root proporcionada. Inicie sesión como usuario root ejecutando el mandato siguiente y especifique la contraseña.

 <pre>
    $ ssh root@169.53.246.x
  </pre>
  {: codeblock}

7. Tanto si accede al sistema con la clave SSH privada como si lo hace con la contraseña de root, cambie inmediatamente la contraseña de root.
8. Para simplificar los mandatos SSH, cree un archivo llamado "config" en el directorio %HOME%/.ssh. Por ejemplo:

  <pre>
   Host VM1
      Hostname 169.53.246.xxx
      User virtuser
      IdentityFile /path/privateKeyFileName
  </pre>
  {: codeblock}

9. Ejecute "ssh VM1" para conectarse como virtuser.

## Vías de acceso del sistema
{: #system_paths}

* Los mandatos del perfil de Liberty pueden emitirse desde */opt/IBM/WebSphere/Liberty/bin*.
* La ubicación del perfil de servidor del perfil de Liberty es */opt/IBM/WebSphere/Profiles/Liberty/servers/server1*.
* Los mandatos de WebSphere Application Server tradicional pueden emitirse desde */opt/IBM/WebSphere/AppServer/bin*.
* La ubicación del perfil de WebSphere Application Server tradicional para el servidor es  */opt/IBM/WebSphere/Profiles/DefaultAppSrv01/servers/server1*.

## Utilización de los enlaces del centro de administración y la consola de administración
{: #console_links}

Al pulsar en el enlace al centro de administración o a la consola de administración, puede recibir un aviso parecido a *Conexión no fiable*. El texto del mensaje exacto varía según el navegador, así como los pasos exactos para omitir o eliminar el aviso.

Puesto que está utilizando enlaces proporcionados por {{site.data.keyword.IBM}},
puede ignorar sin problemas el aviso y conectarse. Si el navegador ofrece almacenar una excepción de seguridad, si lo hace será la forma más fácil de impedir el aviso en el futuro.

Otra opción exportar el certificado de firmante entrante y, a continuación, importarlo al navegador como certificado raíz de confianza. Esta opción podría requerir que realizara una entrada en el archivo *hosts* que correlaciona la dirección IP de VM con el nombre común del emisor de certificado. Este nombre presenta el siguiente formato: <pureapplication.ibmcloud.com. Si ahora utiliza el nombre del host en lugar de la dirección IP en el URL, debería conectarse sin problemas. A continuación tendrá que acceder al centro de administración o a la consola de administración utilizando ese nombre de host en lugar de la dirección IP en el URL.

Por último, los clientes a menudo instalan sus propios certificados raíz para las aplicaciones que hacen externas. Para obtener más información, consulte el Knowledge Center de [WebSphere Application Server](http://www.ibm.com/support/knowledgecenter/SSEQTP_8.5.5/com.ibm.websphere.base.doc/ae/tsec_securecomm.html?cp=SSEQTP_8.5.5%2F1-11-2-6&lang=en){: new_window} o de [Liberty Core](http://www.ibm.com/support/knowledgecenter/SSD28V_8.5.5/com.ibm.websphere.wlp.core.doc/ae/twlp_sec_comm.html?lang=en){: new_window}.

## Puertos de cortafuegos
{: #firewall_ports}

Es probable que deba abrir puertos en el cortafuegos para permitir el acceso a aplicaciones y bases de datos.
  * En cada nodo de WebSphere Application Server para Bluemix, encontrará un archivo openFirewallPorts.sh de script en el directorio WAS_HOME/virtual/bin.
  * En cada host colectivo Liberty, encontrará un archivo openFirewallPorts.sh de script en el directorio WAS_HOME/virtual/bin.

Uso:
  ```
      $ openFirewallPorts.sh -ports <PUERTO>:<PROTOCOLO>,... -persist true|false
  ```
  {: codeblock}

* PUERTO es un número de puerto
* PROTOCOLO es TCP o UDP
* -persist es true o false

Para especificar varios puertos, sepárelos
con una coma ","

**Nota**: los parámetros sport y dport del puerto abierto se abren en los apartados INPUT y OUTPUT del cortafuegos. Debe ejecutar este script como raíz utilizando sudo. También puede
modificar iptables directamente.
