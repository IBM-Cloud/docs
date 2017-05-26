---

copyright:
  years: 2015, 2016
lastupdated: "2017-02-24"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Installationskonventionen
{: #installation_conventions}

## Konventionen für die Installation von Zellen
{: cell_installation_conventions}

WebSphere Application Server in Bluemix-Zellen werden unter Verwendung einer standardisierten Verzeichnisstruktur installiert und konfiguriert. Die folgende Liste enthält die wichtigsten Einstellungen.  Eine vollständige Liste der Einstellungen finden Sie in der Datei /etc/virtualimage.properties.

* IHS_HOME=/opt/IBM/WebSphere/HTTPServer
* IHS_INSTALL_ROOT=/opt/IBM/WebSphere/HTTPServer
* PLG_HOME=/opt/IBM/WebSphere/Plugins
* PROFILES_HOME=/opt/IBM/WebSphere/Profiles
* WAS_HOME=/opt/IBM/WebSphere/AppServer
* WAS_INSTALL_ROOT=/opt/IBM/WebSphere/AppServer
* WCT_HOME=/opt/IBM/WebSphere/Toolbox

## Konventionen für die Installation von Liberty-Verbünden

Ein Liberty-Verbund wird unter Verwendung einer standardisierten Verzeichnisstruktur installiert und konfiguriert. Die folgende Liste enthält die wichtigsten Einstellungen.  Eine vollständige Liste der Einstellungen finden Sie in der Datei /etc/virtualimage.properties.

* IHS_HOME=/opt/IBM/WebSphere/HTTPServer
* IHS_INSTALL_ROOT=/opt/IBM/WebSphere/HTTPServer
* PLG_HOME=/opt/IBM/WebSphere/Plugins
* PROFILES_HOME=/opt/IBM/WebSphere/Profiles
* WLP_HOME=/opt/IBM/WebSphere/Liberty

**Anmerkung**:
* Mithilfe von [Installation Manager](http://www.ibm.com/support/knowledgecenter/SSDV2W_1.8.3/com.ibm.cic.agent.ui.doc/helpindex_imic.html){: new_window} im Verzeichnis /home/virtuser/IBM/Installation Manager können Wartungen durchgeführt werden. Da die zugrunde liegenden Binärdateien als Benutzer virtuser installiert werden, müsen Sie sicherstellen, dass alle Fixpacks und vorläufigen Fixes ebenfalls als virtuser installiert werden.
* Stellen Sie sicher, dass das Starten und Stoppen von Servern über die Befehlszeile mit der WebSphere-Verwaltungs-ID und nicht als Benutzer virtuser durchgeführt werden.
