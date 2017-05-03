---

copyright:
  years: 2015, 2016
lastupdated: "2017-02-24"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Convenções de Instalação
{: #installation_conventions}

## Convenções de instalação da célula
{: cell_installation_conventions}

Uma célula do WebSphere Application Server no Bluemix é instalada e configurada seguindo uma estrutura de diretório padronizada. A lista a seguir indica algumas das configurações importantes.  Veja /etc/virtualimage.properties para obter uma lista completa das configurações.

* IHS_HOME=/opt/IBM/WebSphere/HTTPServer
* IHS_INSTALL_ROOT=/opt/IBM/WebSphere/HTTPServer
* PLG_HOME=/opt/IBM/WebSphere/Plugins
* PROFILES_HOME=/opt/IBM/WebSphere/Profiles
* WAS_HOME=/opt/IBM/WebSphere/AppServer
* WAS_INSTALL_ROOT=/opt/IBM/WebSphere/AppServer
* WCT_HOME=/opt/IBM/WebSphere/Toolbox

## Convenções de instalação do Liberty Collective

Um Liberty collective é instalado e configurado seguindo uma estrutura de diretório padronizada. A lista a seguir indica algumas das configurações importantes.  Veja /etc/virtualimage.properties para obter uma lista completa das configurações.

* IHS_HOME=/opt/IBM/WebSphere/HTTPServer
* IHS_INSTALL_ROOT=/opt/IBM/WebSphere/HTTPServer
* PLG_HOME=/opt/IBM/WebSphere/Plugins
* PROFILES_HOME=/opt/IBM/WebSphere/Profiles
* WLP_HOME=/opt/IBM/WebSphere/Liberty

**Nota**:
* A manutenção pode ser aplicada usando o [Installation Manager](http://www.ibm.com/support/knowledgecenter/SSDV2W_1.8.3/com.ibm.cic.agent.ui.doc/helpindex_imic.html){: new_window} instalado no diretório /home/virtuser/IBM/Installation Manager. Como os binários subjacentes são instalados como virtuser, assegure-se de que todos os fix packs e correções temporárias sejam instalados como virtuser.
* Assegure-se de que o início e a parada de servidores a partir da linha de comandos sejam executados como o ID administrativo do WebSphere, não como virtuser
