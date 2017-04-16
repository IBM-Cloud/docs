---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-28"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Convenzioni di installazione
{: #installation_conventions}

## Convenzioni di installazione della cella
{: cell_installation_conventions}

Una cella WebSphere Application Server for Bluemix cell iiene installata e configurata rispettando una struttura di directory standardizzata. Il seguente elenco annota alcune importanti impostazioni.  Consulta /etc/virtualimage.properties per un elenco completo di impostazioni.

* IHS_HOME=/opt/IBM/WebSphere/HTTPServer
* IHS_INSTALL_ROOT=/opt/IBM/WebSphere/HTTPServer
* PLG_HOME=/opt/IBM/WebSphere/Plugins
* PROFILES_HOME=/opt/IBM/WebSphere/Profiles
* WAS_HOME=/opt/IBM/WebSphere/AppServer
* WAS_INSTALL_ROOT=/opt/IBM/WebSphere/AppServer
* WCT_HOME=/opt/IBM/WebSphere/Toolbox

## Convenzioni di installazione del collettivo Liberty

Un collettivo Liberty viene installato e configurato rispettando una struttura di directory standardizzata. Il seguente elenco annota alcune importanti impostazioni.  Consulta /etc/virtualimage.properties per un elenco completo di impostazioni.

* IHS_HOME=/opt/IBM/WebSphere/HTTPServer
* IHS_INSTALL_ROOT=/opt/IBM/WebSphere/HTTPServer
* PLG_HOME=/opt/IBM/WebSphere/Plugins
* PROFILES_HOME=/opt/IBM/WebSphere/Profiles
* WLP_HOME=/opt/IBM/WebSphere/Liberty

**Nota**:
* La manutenzione può essere applicata utilizzando l'[Installation Manager](http://www.ibm.com/support/knowledgecenter/SSDV2W_1.8.3/com.ibm.cic.agent.ui.doc/helpindex_imic.html){: new_window} installato nella directory /home/virtuser/IBM/Installation Manager. Poiché i file binari sottostanti sono installati come virtuser, accertati che tutti i fix pack e tutte le correzioni temporanee siano installati come virtuser.
* Assicurati che l'avvio e l'arresto dei server dalla riga di comando siano eseguiti come ID amministrativo WebSphere, non come virtuser
