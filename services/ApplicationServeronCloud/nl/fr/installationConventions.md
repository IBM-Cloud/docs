---

copyright:
  years: 2015, 2016
lastupdated: "2017-02-24"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Conventions d'installation
{: #installation_conventions}

## Conventions d'installation de la cellule
{: cell_installation_conventions}

Une cellule WebSphere Application Server in Bluemix doit être installée et configurée conformément à une structure de répertoire normalisée. La liste suivante répertorie quelques-uns des paramètres importants. Pour la liste complète des paramètres, voir /etc/virtualimage.properties.

* IHS_HOME=/opt/IBM/WebSphere/HTTPServer
* IHS_INSTALL_ROOT=/opt/IBM/WebSphere/HTTPServer
* PLG_HOME=/opt/IBM/WebSphere/Plugins
* PROFILES_HOME=/opt/IBM/WebSphere/Profiles
* WAS_HOME=/opt/IBM/WebSphere/AppServer
* WAS_INSTALL_ROOT=/opt/IBM/WebSphere/AppServer
* WCT_HOME=/opt/IBM/WebSphere/Toolbox

## Conventions d'installation de la collectivité Liberty

Une collectivité Liberty est installée et configurée conformément à une structure de répertoire normalisée. La liste suivante répertorie quelques-uns des paramètres importants. Pour la liste complète des paramètres, voir /etc/virtualimage.properties.

* IHS_HOME=/opt/IBM/WebSphere/HTTPServer
* IHS_INSTALL_ROOT=/opt/IBM/WebSphere/HTTPServer
* PLG_HOME=/opt/IBM/WebSphere/Plugins
* PROFILES_HOME=/opt/IBM/WebSphere/Profiles
* WLP_HOME=/opt/IBM/WebSphere/Liberty

**Remarque **:
* Vous pouvez appliquer la maintenance via l'utilitaire [Installation Manager](http://www.ibm.com/support/knowledgecenter/SSDV2W_1.8.3/com.ibm.cic.agent.ui.doc/helpindex_imic.html){: new_window} installé sous le répertoire /home/virtuser/IBM/Installation Manager. Etant donné que les fichiers binaires sous-jacents sont installés en tant que virtuser, prenez soin d'installer tous les groupes de correctifs et tous les correctifs temporaires en tant que virtuser.
* Prenez soin de démarrer et d'arrêter les serveurs depuis la ligne de commande en utilisant l'ID de l'administrateur WebSphere, et non pas en tant que virtuser
