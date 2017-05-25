---

copyright:
  years: 2015, 2016
lastupdated: "2017-02-24"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 설치 규칙
{: #installation_conventions}

## 셀 설치 규칙
{: cell_installation_conventions}

WebSphere Application Server in Bluemix 셀은 표준화된 디렉토리 구조에 따라 설치되고 구성됩니다. 다음 목록은 몇 가지 중요한 설정을 표시합니다. 설정의 전체 목록은 /etc/virtualimage.properties를 참조하십시오.

* IHS_HOME=/opt/IBM/WebSphere/HTTPServer
* IHS_INSTALL_ROOT=/opt/IBM/WebSphere/HTTPServer
* PLG_HOME=/opt/IBM/WebSphere/Plugins
* PROFILES_HOME=/opt/IBM/WebSphere/Profiles
* WAS_HOME=/opt/IBM/WebSphere/AppServer
* WAS_INSTALL_ROOT=/opt/IBM/WebSphere/AppServer
* WCT_HOME=/opt/IBM/WebSphere/Toolbox

## Liberty Collective 설치 규칙

표준화된 디렉토리 구조를 따라 Liberty Collective가 설치되어 구성됩니다.
다음 목록은 몇 가지 중요한 설정을 표시합니다. 설정의 전체 목록은 /etc/virtualimage.properties를 참조하십시오.

* IHS_HOME=/opt/IBM/WebSphere/HTTPServer
* IHS_INSTALL_ROOT=/opt/IBM/WebSphere/HTTPServer
* PLG_HOME=/opt/IBM/WebSphere/Plugins
* PROFILES_HOME=/opt/IBM/WebSphere/Profiles
* WLP_HOME=/opt/IBM/WebSphere/Liberty

**참고**:
* /home/virtuser/IBM/Installation Manager 디렉토리에 설치된 [Installation Manager](http://www.ibm.com/support/knowledgecenter/SSDV2W_1.8.3/com.ibm.cic.agent.ui.doc/helpindex_imic.html){: new_window}를 사용하여 유지보수를 적용할 수 있습니다. 기본 2진 파일을 virtuser로 설치하므로 모든 수정팩 및 임시 수정사항을 virtuser로 설치하는지 확인하십시오.
* virtuser가 아니라 WebSphere 관리 ID로 명령행에서 서버를 시작하고 중지하는 작업을 수행하도록 하십시오.
