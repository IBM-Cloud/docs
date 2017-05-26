---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-24"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Installation conventions
{: #installation_conventions}

## Cell Installation Conventions
{: cell_installation_conventions}

A WebSphere Application Server in Bluemix cell is installed and configured following a standardized directory structure. The following list notes a few of the important settings.  See /etc/virtualimage.properties for a full list of the settings.

* IHS_HOME=/opt/IBM/WebSphere/HTTPServer
* IHS_INSTALL_ROOT=/opt/IBM/WebSphere/HTTPServer
* PLG_HOME=/opt/IBM/WebSphere/Plugins
* PROFILES_HOME=/opt/IBM/WebSphere/Profiles
* WAS_HOME=/opt/IBM/WebSphere/AppServer
* WAS_INSTALL_ROOT=/opt/IBM/WebSphere/AppServer
* WCT_HOME=/opt/IBM/WebSphere/Toolbox

## Liberty Collective Installation Conventions

A Liberty collective is installed and configured following a standardized directory structure. The following list notes a few of the important settings.  See /etc/virtualimage.properties for a full list of the settings.

* IHS_HOME=/opt/IBM/WebSphere/HTTPServer
* IHS_INSTALL_ROOT=/opt/IBM/WebSphere/HTTPServer
* PLG_HOME=/opt/IBM/WebSphere/Plugins
* PROFILES_HOME=/opt/IBM/WebSphere/Profiles
* WLP_HOME=/opt/IBM/WebSphere/Liberty

**Note**:
* Maintenance can be applied by using the [Installation Manager](http://www.ibm.com/support/knowledgecenter/SSDV2W_1.8.3/com.ibm.cic.agent.ui.doc/helpindex_imic.html){: new_window} installed in the /home/virtuser/IBM/Installation Manager directory. Since the underlying binaries are installed as virtuser, ensure that all fix packs and interim fixes are installed as virtuser.
* Ensure that starting and stopping servers from the command line is performed as the WebSphere Administrative ID, not as virtuser
