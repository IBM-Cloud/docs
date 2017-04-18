---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-28"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Convenios de instalación
{: #installation_conventions}

## Convenios de instalación de células
{: cell_installation_conventions}

Una célula de WebSphere Application Server for Bluemix se instala y configura siguiendo una estructura de directorios estandarizada. En la lista siguiente se indican algunos de los valores importantes.  Consulte el archivo /etc/virtualimage.properties para obtener una lista completa de valores.

* IHS_HOME=/opt/IBM/WebSphere/HTTPServer
* IHS_INSTALL_ROOT=/opt/IBM/WebSphere/HTTPServer
* PLG_HOME=/opt/IBM/WebSphere/Plugins
* PROFILES_HOME=/opt/IBM/WebSphere/Profiles
* WAS_HOME=/opt/IBM/WebSphere/AppServer
* WAS_INSTALL_ROOT=/opt/IBM/WebSphere/AppServer
* WCT_HOME=/opt/IBM/WebSphere/Toolbox

## Convenios de instalación de Liberty Collective

Se instala un Liberty Collective y se configura siguiendo una estructura de directorios estandarizada. En la lista siguiente se indican algunos de los valores importantes.  Consulte el archivo /etc/virtualimage.properties para obtener una lista completa de valores.

* IHS_HOME=/opt/IBM/WebSphere/HTTPServer
* IHS_INSTALL_ROOT=/opt/IBM/WebSphere/HTTPServer
* PLG_HOME=/opt/IBM/WebSphere/Plugins
* PROFILES_HOME=/opt/IBM/WebSphere/Profiles
* WLP_HOME=/opt/IBM/WebSphere/Liberty

**Nota**:
* El mantenimiento puede aplicarse utilizando el [gestor de instalación](http://www.ibm.com/support/knowledgecenter/SSDV2W_1.8.3/com.ibm.cic.agent.ui.doc/helpindex_imic.html){: new_window} instalado en el directorio /home/virtuser/IBM/Installation Manager. Dado que los binarios subyacentes se han instalado como virtuser, asegúrese de que todos los fixpacks y arreglos temporales se instalen como virtuser.
* Asegúrese de que los servidores se inician y detienen desde la línea de mandatos utilizando el ID administrativo de WebSphere, no el usuario virtuser.
