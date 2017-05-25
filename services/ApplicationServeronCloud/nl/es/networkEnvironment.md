---

copyright:
  years: 2015, 2016
lastupdated: "2017-02-24"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Entorno de red
{: #networkEnvironment}

Una vez suministrada la instancia de servicio de WebSphere Application Server en {{site.data.keyword.Bluemix_notm}}, puede acceder a VM de varias formas. Puede conectarse sobre una VPN segura para obtener SSH, puede utilizar la consola de administración de WebSphere tradicional y puede acceder por aplicación a VM. También puede conectar VM a Internet con una dirección IP pública. 

En el siguiente diagrama se muestran estos métodos de red: 

Figura 1. Vista de cliente con red multiarrendatario con IP pública

![Figura 1. Vista de cliente con red multiarrendatario con IP pública ](images/wasaas_multi_tenantPublicIP.gif)

## Acceso VPN
{: #vpnAccess}

Después de suministrar una instancia de servicio de WebSphere Application Server en {{site.data.keyword.Bluemix_notm}} desde el panel de control de servicio de la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}, puede descargar las credenciales VPN y establecer una conexión OpenVPN. Luego puede acceder a VM a través de SSH. También puede acceder a Liberty Admin Center, a la consola de administración de WebSphere tradicional y a las aplicaciones. 

## Acceso a Internet pública
{: #publicInternetAccess}

Si lo desea, puede solicitar una dirección IP pública para VM del servidor WebSphere pulsando **Gestionar IP pública** en el panel de control de servicio de la interfaz de usuario de {{site.data.keyword.Bluemix_notm}} y solicitando una IP pública. Este proceso reserva la dirección IP para este servidor. A continuación, pulse **Abrir IP** para abrir la conexión entre Internet y la instancia de servicio de WebSphere Application Server en {{site.data.keyword.Bluemix_notm}}. 

## Puertos IP públicos
{: #publicIPports}

Cuando abre el acceso a IP pública, la dirección IP se asocia a VM y se abren los puertos 80 y 443 en la pasarela. Sin embargo, de forma predeterminada, Liberty Core y los servidores WebSphere Base tradicionales no abren los puertos 80 y 443. Por el contrario, los puertos 80 y 443 se abren de forma predeterminada en IBM HTTP Server. Por lo tanto, es posible que tenga que configurar los servidores Liberty Core y WebSphere Base tradicional para el tráfico de las aplicaciones en el puerto 80/443 cuando utilice IP pública. 
* Para configurar el servidor Liberty Core, consulte [Configuración de Liberty Core Server para el acceso público](networkEnvironment.html#configureLibertyForPublicAccess).
* Para configurar el servidor WebSphere Base tradicional, añada una escucha de cadena de transporte de contenedor web en el puerto 80/443 tal como se describe en [Configuración de cadenas de transporte](http://www.ibm.com/support/knowledgecenter/SSEQTP_8.5.5//com.ibm.websphere.nd.doc/ae/trun_chain_transport.html){: new_window}.

## Puertos IP privados VPN
{: #privateIPports}

Se establece conexión con la dirección IP privada de VM a través de la conexión VPN. Solo se puede acceder a Liberty Admin Center (9080, 9443), a la consola de administración de WebSphere tradicional (9060, 9043), a SSH (22) y a los puertos que no son 80/443 a través de la conexión VPN, tal como se muestra en la Figura 1. Consulte los archivos **server.xml** e **ibm-web-bnd.xml** de ejemplo de Liberty Core para ver detalles sobre cómo separar Liberty Admin Center de los puertos de la aplicación. 

**Evite problemas:** para los servidores Liberty Core y WebSphere Base tradicional, los puertos del cortafuegos están preconfigurados cuando se suministra VM. Sin embargo, para configuraciones de Network Deployment donde el gestor de despliegue o el controlador colectivo está situado junto a IBM HTTP Server, es posible que tenga que abrir los puertos en el cortafuegos. Consulte [Puertos del cortafuegos](systemAccess.html#firewall_ports) para ver detalles. 

## Configuración del servidor Liberty Core para el acceso a IP pública
{: #configureLibertyForPublicAccess}

Tiene que configurar Liberty Core de modo que escuche el tráfico de la aplicación en los puertos 80/443 cuando utilice IP pública. 

De forma predeterminada, Liberty está configurado con Liberty Admin Center y las aplicaciones disponibles en el host virtual **default_host**, que está asociado a **defaultHttpEndpoint** en el puerto 9080 y 9443. Vuelva a configurar el servidor para separar Liberty Admin Center del host virtual de la aplicación y del punto final y haga que estén disponibles en distintos puertos. 

El siguiente fragmento de código es un ejemplo de ajustes en la configuración de server.xml: 

```    
    <!-- open port 9080/9443 for incoming http connections -->
    <httpEndpoint id="defaultHttpEndpoint"
        host="*"
        httpPort="9080"
        httpsPort="9443">
        <tcpOptions soReuseAddr="true"/>
    </httpEndpoint>

    <!-- define a new endpoint for public app traffic -->
    <httpEndpoint id="publicHttpEndpoint"
        host="*"
        httpPort="80"
        httpsPort="443">
        <tcpOptions soReuseAddr="true"/>
    </httpEndpoint>

    <!– restrict default_host to vpn so the Liberty Admin Center is not public -->
    <virtualHost id="default_host" allowFromEndpointRef="defaultHttpEndpoint">
      <hostAlias>*:9080</hostAlias>
      <hostAlias>*:9443</hostAlias>
    </virtualHost>

    <virtualHost id="external_host">
      <hostAlias>*:80</hostAlias>
      <hostAlias>*:443</hostAlias>
    </virtualHost>
```
{: codeblock}

Ahora asocie la aplicación con el host virtual **external_host** incluyendo el siguiente fragmento de código en el archivo **META-INF/ibm-web-bnd.xml** de la aplicación: 

```
    <?xml version="1.0" encoding="UTF-8"?>
    <web-bnd
        xmlns="http://websphere.ibm.com/xml/ns/javaee"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="http://websphere.ibm.com/xml/ns/javaee
        http://websphere.ibm.com/xml/ns/javaee/ibm-web-bnd_1_0.xsd"
        version="1.0">

        <virtual-host name="external_host" />
    </web-bnd>
```
{: codeblock}
