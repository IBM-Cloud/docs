---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-28"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 安装约定
{: #installation_conventions}

## 单元安装约定
{: cell_installation_conventions}

WebSphere Application Server for Bluemix 单元已安装，并且已遵循标准化目录结构进行配置。以下列表记录了一些重要的设置。请参阅 /etc/virtualimage.properties，以获取设置的完整列表。

* IHS_HOME=/opt/IBM/WebSphere/HTTPServer
* IHS_INSTALL_ROOT=/opt/IBM/WebSphere/HTTPServer
* PLG_HOME=/opt/IBM/WebSphere/Plugins
* PROFILES_HOME=/opt/IBM/WebSphere/Profiles
* WAS_HOME=/opt/IBM/WebSphere/AppServer
* WAS_INSTALL_ROOT=/opt/IBM/WebSphere/AppServer
* WCT_HOME=/opt/IBM/WebSphere/Toolbox

## Liberty 集合安装约定

Liberty 集合已安装，并且已遵循标准化目录结构进行配置。以下列表记录了一些重要的设置。请参阅 /etc/virtualimage.properties，以获取设置的完整列表。

* IHS_HOME=/opt/IBM/WebSphere/HTTPServer
* IHS_INSTALL_ROOT=/opt/IBM/WebSphere/HTTPServer
* PLG_HOME=/opt/IBM/WebSphere/Plugins
* PROFILES_HOME=/opt/IBM/WebSphere/Profiles
* WLP_HOME=/opt/IBM/WebSphere/Liberty

**注**：
* 通过使用安装在 /home/virtuser/IBM/Installation Manager 目录中的 [Installation Manager](http://www.ibm.com/support/knowledgecenter/SSDV2W_1.8.3/com.ibm.cic.agent.ui.doc/helpindex_imic.html){: new_window} 可应用维护。因为以 virtuser 身份安装了底层二进制，请确保以 virtuser 身份安装所有修订包和临时修订。
* 确保使用 WebSphere 管理标识而非以 virtuser 身份从命令行启动和停止服务器
