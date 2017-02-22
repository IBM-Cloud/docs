---

copyright:
  years: 2014, 2017
lastupdated: "2017-01-17"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# CLI를 구성하여 Swift 및 Cloud Foundry 명령 사용

Swift 또는 Cloud Foundry 명령을 사용하여 {{site.data.keyword.objectstorageshort}} 서비스와 상호작용하려면 필수 소프트웨어를 설치해야 합니다.
{: shortdesc}


## Swift 클라이언트 설치 {: #install-swift-client}

다음 필수 소프트웨어가 없는 경우 설치하십시오. 
* Python 2.7 이상
* setuptools 패키지
* pip 패키지
* Cloud Foundry CLI


Python Swift 클라이언트를 설치하려면 다음 명령을 실행하십시오. 
```
pip install python-swiftclient
```
{: pre}

Python Keystone 클라이언트를 설치하려면 다음 명령을 실행하십시오. 
```
pip install python-keystoneclient
```
{: pre}

필수 소프트웨어에 관한 자세한 정보는 [Openstack 문서](http://docs.openstack.org/user-guide/common/cli_install_openstack_command_line_clients.html#install-the-prerequisite-software){: new_window}를 참조하십시오. 


## 클라이언트 설정 {: #setup-swift-client}

Swift 클라이언트를 구성하려면 인증 정보를 `export`해야 합니다. Cloud Foundry 또는 URL 명령을 사용한 CLI를 통해 또는 {{site.data.keyword.Bluemix_notm}} UI를 통해서 [신임 정보를 생성](/docs/services/ObjectStorage/os_credentials.html)할 수 있습니다. 클라이언트는 다음 표에 있는 환경 변수에서 정보를 가져옵니다. 

<table>
<caption> 표 1. 환경 변수 및 설명</caption>
  <tr>
    <th> 환경 변수 </th>
    <th> 설명 </th>
  </tr>
  <tr>
    <td> <code>OS_USER_ID</code> </td>
    <td> {{site.data.keyword.objectstorageshort}} 사용자 ID입니다. </td>
  </tr>
  <tr>
    <td> <code>OS_PASSWORD</code> </td>
    <td> {{site.data.keyword.objectstorageshort}} 인스턴스의 비밀번호입니다. </td>
  </tr>
  <tr>
    <td> <code>OS_PROJECT_ID</code> </td>
    <td> 프로젝트 ID입니다. </td>
  </tr>
  <tr>
    <td> <code>OS_REGION_NAME</code> </td>
    <td> 오브젝트가 저장되는 지역입니다. 댈러스 지역과 런던 지역에서 {{site.data.keyword.objectstorageshort}}를 사용할 수 있습니다. </td>
  </tr>
  <tr>
    <td> <code>OS_AUTH_URL</code> </td>
    <td> 엔드포인트 URL입니다. <code>/v3</code>가 URL의 끝에 추가되었는지 확인하십시오. </td>
  </tr>
</table>



인증 정보를 내보내려면 신임 정보를 입력하고 다음 명령을 실행하십시오. 
```
export OS_USER_ID=
export OS_PASSWORD=
export OS_PROJECT_ID=
export OS_AUTH_URL=
export OS_REGION_NAME=
export OS_IDENTITY_API_VERSION=
export OS_AUTH_VERSION=

swift auth
    ```
{: codeblock}


예:
```
export OS_USER_ID=24a20b8e4e724f5fa9e7bfdc79ca7e85
export OS_PASSWORD=*******
export OS_PROJECT_ID=383ec90b22ff4ba4a78636f4e989d5b1
export OS_AUTH_URL=https://identity.open.softlayer.com/v3
export OS_REGION_NAME=dallas
export OS_IDENTITY_API_VERSION=3
export OS_AUTH_VERSION=3

swift auth
    ```
{: screen}
