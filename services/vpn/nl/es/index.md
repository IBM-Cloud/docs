---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Iniciación a {{site.data.keyword.vpn_short}}
{: #vpn}  
*Última actualización: 09 de mayo de 2016*

El servicio {{site.data.keyword.vpn_full}} para Bluemix&reg; está disponible para acceder a IBM Containers (contenedores de Docker) dentro del entorno de nube de IBM Bluemix. Puede utilizar el entorno de nube de IBM Bluemix como extensión de su centro de datos corporativo. También se puede conectar a los servidores de SoftLayer utilizando el servicio IBM VPN.
{:shortdesc}

Antes de empezar, compruebe que tiene un contenedor de IBM Docker listo para utilizar. Consulte [IBM Containers for Bluemix](https://www.ng.bluemix.net/docs/containers/container_index.html) para obtener más información sobre como crear y gestionar IBM Containers.  

Para empezar, seleccione el mosaico de instancia de servicio **Red privada virtual** en el panel de control de Bluemix. Efectúe los pasos siguientes:

1. Configure la pasarela de {{site.data.keyword.vpn_short}} seleccionando **CREAR PASARELA**. Se creará una pasarela predeterminada. Si es necesario, edite la configuración de pasarela como se muestra en los pasos siguientes.  
{: #gateway}  

  1. Seleccione **EDITAR**.  
  2. Especifique el nombre de la pasarela.  
  3. Seleccione el contenedor y el grupo de contenedores con el que desea utilizar el servicio VPN. **Note:** Las subredes privadas del contenedor y del grupo de contenedores están preseleccionadas, de modo que puede acceder a ellas a través de la conexión de VPN. 
  4. Seleccione **GUARDAR**.  

 Puede utilizar las políticas predeterminadas IKE e IPSec o configurar políticas personalizadas. Si desea utilizar las políticas predeterminadas, vaya al paso 4.

2. Configure la política de IKE seleccionando el separador **Políticas de IKE e IPSec**.
  1. Seleccione **AÑADIR NUEVA**.  
  2. Especifique los detalles siguientes:
	* **Nombre**: Nombre de la política IKE.
	* **Algoritmo de autorización**: sha1; no se puede cambiar.  
	* **Algoritmo de cifrado**: Selecciónelo en la lista desplegable. Valores: aes-128 (predeterminado), aes-192, aes-256, 3des
	* **Tiempo de vida de clave**: Valor de tiempo de vida (en segundos) de la asociación de seguridad de IKE. Rango: 60-86400. Valor predeterminado: 86400
	* **PFS**: Identificador de grupo Diffie-Hellman (DH). Valores: Group2, Group5, Group14. Valor predeterminado: Group2
	* **Modalidad de negociación**: Main; no se puede cambiar.
	* **Versión**: IKEV1; no se puede cambiar.
  3. Seleccione **GUARDAR**.

3. Configure la política IPSec:
  1. Seleccione **AÑADIR NUEVA**.  
  2. Especifique los detalles siguientes:
  	* **Nombre**: Nombre de la política IPSec.  
  	* **Algoritmo de autorización**: sha1; no se puede cambiar.  
  	* **Algoritmo de cifrado**: Selecciónelo en la lista desplegable. Valores: aes-128 (predeterminado), aes-192, aes-256, 3des
  	* **Tiempo de vida de clave**: Valor de tiempo de vida (en segundos) de la asociación de seguridad. Rango: 60-86400. Valor predeterminado: 3600
  	* **PFS**: Identificador de grupo Diffie-Hellman (DH). Valores: Group2, Group5, Group14. Valor predeterminado: Group2
  	* **Protocolo de transformación**: ESP; no se puede cambiar.
  	* **Modalidad de encapsulación**: Tunnel; no se puede cambiar.
  3. Seleccione **GUARDAR**.  

4. Proporcione la información para establecer una conexión entre su centro de datos o pasarela de VPN de servidor de SoftLayer y la pasarela de IBM VPN.  
{: #site}  

  1. Seleccione el separador **Dispositivo de pasarela**.
  2. Seleccione **Crear conexión** en la sección **Conexiones de sitios**.
  3. Especifique los detalles de conexiones de sitios siguientes:  
  	* **Nombre**: Nombre de la conexión.  
  	* **Descripción**: Descripción de la conexión (opcional).  
  	* **Serie de clave compartida previamente**: Clave compartida previamente (secreta) que se utilizará para la autenticación.
  	* **Estado de administración**: Estado de la conexión de VPN. Selecciónelo en la lista desplegable: ACTIVO O INACTIVO. Valor predeterminado: ACTIVO  
  	* **IP de pasarela de cliente**: Dirección de IP de punto final remoto del túnel de VPN.  
  	* **Subred de cliente**: Dirección de subred remota en formato CIDR. Seleccione el signo más para añadir otra subred. 
  4. (Opcional) Configure los siguientes parámetros de **Opciones avanzadas**:  
  	* **Política IKE**: Seleccione la política IKE.  
  	* **Intervalo de estado activo**: Intervalo de estado activo en segundos. Enviar mensajes de estado activo en el intervalo configurado para comprobar el estado activo del igual. Valor predeterminado: 15. Rango: 5-86399
  	* **Acción sobre igual inactivo**: Acción a realizar cuando el igual se detecta como inactivo.  
    	Valores: 
  		* hold (valor predeterminado): La asociación de seguridad (SA) se pone en espera. 
  		* clear: La SA se suprime.
  		* disabled: La SA se inhabilita.
  		* restart: La SA se renegocia.
  		* restart-by-peer: Todas las SA con el igual inactivo se renegocian.  
  	* **Política IPSec**: Seleccione la política IPSec.
  	* **Tiempo de espera de estado activo**: valor de tiempo de espera en segundos tras el cual la sesión se termina. Valor predeterminado: 120. Rango: 6-86400. El valor de intervalo de estado activo debe ser superior que el valor de intervalo de estado activo.
  5. Seleccione **GUARDAR**.

  **Nota:** Cuando la conexión se está estableciendo, el estado de conexión se muestra como ***pending create***. Cuando vea este estado, actualice la ventana varias veces para ver el estado activo de la conexión.

**Importante:** Si utiliza una aplicación web, debe enlazar la aplicación web al contenedor de Docker que esté utilizando. Este enlace es necesario para que el tráfico pase por el túnel VPN de IPSec.

**Importante** Actualmente, el servicio IBM VPN opera en modalidad de respuesta. Para iniciar la conexión VPN, un paquete de datos debe fluir de la pasarela IBM VPN a su centro de datos local o servidor de SoftLayer. Una vez se ha establecido la conexión VPN, el tráfico puede fluir en cualquier dirección entre puntos finales de la conexión VPN.

 
# rellinks
## ejemplos 
{: #samples}  
* [Ejemplo de configuración de pasarela strongSwan local](vpn_onpremises.html#strongswan){: new_window}
* [Ejemplo de configuración de pasarela Vyatta local](vpn_onpremises.html#vyatta){: new_window}
* [Ejemplo de configuración del servicio de dispositivo de pasarela (Gaas) SoftLayer local](vpn_onpremises.html#gaas){: new_window}
* [Ejemplo de configuración de Cisco ASA local](vpn_onpremises.html#cisco){: new_window}

## api  
{: #api}  
* [API RESTful de IBM VPN](https://new-console.ng.bluemix.net/apidocs/101){: new_window}

## general  
{: #general}  
* [Interfaz de línea de mandatos de IBM VPN](../../cli/plugins/vpn/index.html){: new_window}
* [Preguntas frecuentes de IBM VPN](vpn_faq.html#vpn_faq){: new_window}
* [Hoja de precios de IBM Bluemix](https://console.{DomainName}/pricing/){: new_window}
* [Requisitos previos de IBM Bluemix](https://developer.ibm.com/bluemix/support/#prereqs)
