---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# インストール規則
{: #installation_conventions}

## セルのインストール規則
{: cell_installation_conventions}

WebSphere Application Server for Bluemix セルは、標準化されたディレクトリー構造に従ってインストールおよび構成されます。以下のリストは、いくつかの重要な設定に言及しています。これらの設定の完全なリストについては、/etc/virtualimage.properties を参照してください。

* IHS_HOME=/opt/IBM/WebSphere/HTTPServer
* IHS_INSTALL_ROOT=/opt/IBM/WebSphere/HTTPServer
* PLG_HOME=/opt/IBM/WebSphere/Plugins
* PROFILES_HOME=/opt/IBM/WebSphere/Profiles
* WAS_HOME=/opt/IBM/WebSphere/AppServer
* WAS_INSTALL_ROOT=/opt/IBM/WebSphere/AppServer
* WCT_HOME=/opt/IBM/WebSphere/Toolbox

## Liberty 集合のインストール規則

Liberty 集合は、標準化されたディレクトリー構造に従ってインストールおよび構成されます。以下のリストは、いくつかの重要な設定に言及しています。これらの設定の完全なリストについては、/etc/virtualimage.properties を参照してください。

* IHS_HOME=/opt/IBM/WebSphere/HTTPServer
* IHS_INSTALL_ROOT=/opt/IBM/WebSphere/HTTPServer
* PLG_HOME=/opt/IBM/WebSphere/Plugins
* PROFILES_HOME=/opt/IBM/WebSphere/Profiles
* WLP_HOME=/opt/IBM/WebSphere/Liberty

**注**:
* 保守は、/home/virtuser/IBM/Installation Manager ディレクトリーにインストールされている [Installation Manager](http://www.ibm.com/support/knowledgecenter/SSDV2W_1.8.3/com.ibm.cic.agent.ui.doc/helpindex_imic.html){: new_window} を使用して適用できます。基礎のバイナリーは virtuser としてインストールされているため、すべてのフィックスパックおよび暫定修正は virtuser としてインストールするようにしてください。
* コマンド・ラインからのサーバーの始動および停止は、virtuser ではなく、WebSphere 管理 ID として実行するようにしてください。
