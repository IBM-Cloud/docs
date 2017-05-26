---

copyright:
  years: 2015, 2016
lastupdated: "2017-02-24"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 安裝慣例
{: #installation_conventions}

## Cell 安裝慣例
{: cell_installation_conventions}

WebSphere Application Server in Bluemix Cell 是遵循標準化目錄結構所安裝及配置。下列清單記錄一些重要的設定。如需完整的設定清單，請參閱 /etc/virtualimage.properties。

* IHS_HOME=/opt/IBM/WebSphere/HTTPServer
* IHS_INSTALL_ROOT=/opt/IBM/WebSphere/HTTPServer
* PLG_HOME=/opt/IBM/WebSphere/Plugins
* PROFILES_HOME=/opt/IBM/WebSphere/Profiles
* WAS_HOME=/opt/IBM/WebSphere/AppServer
* WAS_INSTALL_ROOT=/opt/IBM/WebSphere/AppServer
* WCT_HOME=/opt/IBM/WebSphere/Toolbox

## Liberty Collective 安裝慣例

Liberty Collective 是遵循標準化目錄結構所安裝及配置。下列清單記錄一些重要的設定。如需完整的設定清單，請參閱 /etc/virtualimage.properties。

* IHS_HOME=/opt/IBM/WebSphere/HTTPServer
* IHS_INSTALL_ROOT=/opt/IBM/WebSphere/HTTPServer
* PLG_HOME=/opt/IBM/WebSphere/Plugins
* PROFILES_HOME=/opt/IBM/WebSphere/Profiles
* WLP_HOME=/opt/IBM/WebSphere/Liberty

**附註**：
* 利用 /home/virtuser/IBM/Installation Manager 目錄中所安裝的 [Installation Manager](http://www.ibm.com/support/knowledgecenter/SSDV2W_1.8.3/com.ibm.cic.agent.ui.doc/helpindex_imic.html){: new_window}，可套用維護。因為是以 virtuser 身分安裝基礎二進位，所以請確保以 virtuser 身分安裝所有修正套件及臨時修正程式。
* 確定使用 WebSphere 管理 ID 而非以 virtuser 身分從指令行啟動及停止伺服器
