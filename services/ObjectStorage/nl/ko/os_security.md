---

copyright:
  years: 2014, 2016
lastupdated: "2016-11-04"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 파일 보호 {: #understanding-authentication}


## 서비스 신임 정보 이해 {: #understanding-credentials}

서비스 신임 정보는 서비스에 필요한 인증과 보안을 제공하는 데 사용됩니다. 신임 정보 세트는 인스턴스가 프로비저닝될 때 자동으로 생성됩니다. Swift 클라이언트는 다음 표에 있는 환경 변수에서 인증 정보를 가져옵니다. 

<table>
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
    <td> 엔드포인트 URL입니다. `/v3`가 URL의 끝에 추가되었는지 확인하십시오. </td>
  </tr>
</table>

표 1: 인증 변수와 설명

####  UI에 서비스 신임 정보 추가
1. 서비스 인스턴스 대시보드의 **서비스 신임 정보** 탭에서 **새 신임 정보**를 클릭하고 이름을 지정하십시오. 
2. (*선택사항*) **인라인 구성 매개변수 추가** 텍스트 필드에 작성할 역할에 대한 신임 정보를 입력하십시오. 이 정보는 JSON 페이로드로 형식화되어야 합니다. {{site.data.keyword.objectstorageshort}} 사용자 역할에 대한 자세한 정보는 [액세스 유형](../os_security.html#access-types)을 참조하십시오. 
    - 관리 사용자 작성: `{"role":"admin"}`
    - 비관리 사용자 작성: `{"role":"member"}`
3. **추가**를 클릭하십시오.


## 액세스 유형 {: #access-types}

서비스에 대한 액세스는 사용자 역할 및 컨테이너 액세스 제어 목록에 의해 제어됩니다. {{site.data.keyword.objectstorageshort}} 사용자는 관리자 또는 비관리자일 수 있습니다. 액세스 제어 목록은 컨테이너 레벨에서 관리자에 의해 사용될 수 있으며 서비스 인스턴스, 스토리지 계정 또는 프로젝트 레벨에 대해 사용할 수 없습니다.

<table>
  <tr>
    <th> 관리 사용자(admin) </th>
    <th> 비관리 사용자(member) </th>
  </tr>
  <tr>
    <td> 액세스 제어 관리 </td>
    <td> 기본적으로 서비스 또는 해당 컨테이너에 대한 액세스가 없음 </td>
  </tr>
  <tr>
    <td> 컨테이너를 작성하고 삭제할 수 있음 </td>
    <td> 컨테이너 읽기/쓰기 ACL을 기반으로 하여 조치를 수행할 수 있음 </td>
  </tr>
  <tr>
    <td> 컨테이너에 대해 읽고 쓸 수 있음 </td>
    <td> admin에 의해 결정된 대로 조치를 수행할 수 있음 </td>
  </tr>
</table>

표 2: 정의된 사용자 역할

{{site.data.keyword.Bluemix_notm}} 사용자 인터페이스, Cloud Foundry API 또는 Cloud Foundry CLI를 통해 {{site.data.keyword.objectstorageshort}} 사용자를 관리할 수 있습니다.




## 읽기 액세스 권한 부여 {: #read-access}

admin 역할을 가진 {{site.data.keyword.objectstorageshort}} 사용자는 다른 사용자의 컨테이너에 대한 읽기 액세스 권한을 부여하고 읽기 ACL 조합을 조작할 수 있습니다. 

<table>
  <tr>
    <th> 권한 </th>
    <th> 읽기 ACL 옵션 </th>
  </tr>
  <tr>
    <td> 계정 소속에 상관없이 모든 참조자 읽기 </td>
    <td> <code> .r,*` </code> </td>
  </tr>
  <tr>
    <td> 모든 참조자 및 목록에 대한 읽기 및 나열 </td>
    <td> <code>.r:*,.rlistings</code> </td>
  </tr>
  <tr>
    <td> 특정 프로젝트의 지정된 사용자에 대한 읽기 및 나열 </td>
    <td> <code> project_id:user_id </code> </td>
  </tr>
  <tr>
    <td> 모든 프로젝트의 지정된 사용자에 대한 읽기 및 나열 </td>
    <td> <code> *:user_id </code> </td>
  </tr>
  <tr>
    <td> 지정된 프로젝트의 모든 사용자에 대한 읽기 및 나열 </td>
    <td> <code> project_id:* </code> </td>
  </tr>
  <tr>
    <td> 모든 프로젝트의 모든 사용자에 대한 읽기 및 나열 </td>
    <td> <code> *:* </code> </td>
  </tr>
</table>

표 3: 옵션별 읽기 액세스 권한



1. 신임 정보를 인증하십시오. UI의 서비스 신임 정보 탭에 있는 신임 정보를 사용하거나 새 신임 정보를 생성할 수 있습니다. 새 신임 정보 생성에 대한 자세한 정보는 [서비스 신임 정보 생성](insert link here)을 참조하십시오. 출력으로 {{site.data.keyword.objectstorageshort}} URL과 인증 토큰을 수신합니다.
    Swift 명령:

    ```
  export OS_USER_ID=<user_id>
  export OS_PASSWORD=<password>
  export OS_TENANT_ID=<project_id>
  export OS_AUTH_URL=https://identity.open.softlayer.com/v3
  export OS_REGION_NAME=<region>
  export OS_IDENTITY_API_VERSION=3
  export OS_AUTH_VERSION=3

  swift auth
    ```
    {: codeblock}

      cURL 명령: 

    ```
    curl -i -H "X-Auth-User: <user_id>" -H "X-Auth-Key: <password>" <auth_url>
    ```
    {: pre}

2. 다음 명령을 실행하여 읽기 액세스 권한을 부여하십시오.
    Swift 명령:

    ```
    swift post <container_name> --read-acl "<user_id>:<project_id>"
    ```
    {: pre}

      cURL 명령: 

    ```
  curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Read: <tenant_id>:<project_id>" -H "X-Auth-Token: <OS_AUTH_TOKEN>"
  ```
    {: pre}
    **참고**: 액세스 제어 목록을 구분하려면 쉼표(,)를 사용하십시오.


3. 읽기 ACL 값을 확인하십시오. Swift 명령:

    ```
  swift stat <container_name>
  ```
    {: pre}
    cURL 명령:
```
    curl -i <OS_STORAGE_URL> -I -H "X-Auth-Token:<OS_AUTH_TOKEN>"
    ```
    {: pre}

    다음 예제 출력에서 읽기 액세스 권한이 부여된 것을 확인할 수 있습니다. 

    ```
    HTTP/1.1 204 No Content
    Content-Length: 0
    X-Container-Object-Count: 1
    Accept-Ranges: bytes
    X-Storage-Policy: standard
    X-Container-Read: c727d7e248b448f6b268f31a1bd8691e:3c5b516655e4479881d3d216895faedb
    X-Container-Bytes-Used: 31512
    X-Timestamp: 1462818314.11220
    Content-Type: text/plain; charset=utf-8
    X-Trans-Id: txad7fe001da274b9ba39a6-005772e4d6
    Date: Tue, 28 Jun 2016 20:57:58 GMT
    ```
    {: screen}



## 쓰기 액세스 권한 부여 {: #write-access}

admin 역할을 가진 {{site.data.keyword.objectstorageshort}} 사용자는 다른 사용자의 컨테이너에 대한 쓰기 액세스 권한을 부여하고 쓰기 ACL 조합을 조작할 수 있습니다. 

<table>
  <tr>
    <th> 권한 </th>
    <th> 쓰기 ACL 옵션 </th>
  </tr>
  <tr>
    <td> 특정 프로젝트의 지정된 사용자에 대한 쓰기 </td>
    <td> <code> project_id:user_id </code> </td>
  </tr>
  <tr>
    <td> 모든 프로젝트의 지정된 사용자에 대한 쓰기 </td>
    <td> <code> *:user_id </code> </td>
  </tr>
  <tr>
    <td> 지정된 프로젝트의 모든 사용자에 대한 쓰기 </td>
    <td>  <code> project_id:* </code> </td>
  </tr>
  <tr>
    <td> 모든 프로젝트의 모든 사용자에 대한 쓰기 </td>
    <td>  <code> *:* </code> </td>
  </tr>
</table>

표 4: 옵션별 쓰기 액세스 권한



1. 사용자가 작성한 서비스 신임 정보 내에 있는 정보를 사용하여 신임 정보를 인증하십시오. 출력으로 {{site.data.keyword.objectstorageshort}} URL과 인증 토큰을 수신합니다.
    Swift 명령:

    ```
    export OS_USER_ID="<user_id>"
    export OS_PASSWORD="<password>"
    export OS_TENANT_ID=<project_id>
    export OS_AUTH_URL=https://identity.open.softlayer.com/v3
    export OS_REGION_NAME=<region>
    export OS_IDENTITY_API_VERSION=3
    export OS_AUTH_VERSION=3

    swift auth
    ```
    {: codeblock}

      cURL 명령: 

    ```
    curl -i -H "X-Auth-User:< user_id>" -H "X-Auth-Key:< password>" https://identity.open.softlayer.com/v3
    ```
    {: pre}

2. 다음 명령을 실행하여 쓰기 액세스 권한을 부여하십시오.
    Swift 명령:

    ```
    swift post <container_name> --write-acl "<user_id>:<project_id>"
    ```
    {: pre}

      cURL 명령: 

    ```
  curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Write: <user_id>: <project_id>" -H "X-Auth-Token:<OS_AUTH_TOKEN>"

  ```
    {: pre}

    **참고**: 액세스 제어 목록을 구분하려면 쉼표(,)를 사용하십시오. 

3. 쓰기 ACL 값을 확인하십시오. Swift 명령:

    ```
  swift stat <container_name>
  ```
    {: pre}

      cURL 명령: 

    ```
    curl -i <OS_STORAGE_URL> -I -H "X-Auth-Token:<OS_AUTH_TOKEN>"
    ```
    {: pre}



## 액세스 제거 {: #removing-access}

컨테이너에서 읽기 ACL 제거:
* Swift 명령:

    ```
  swift post <container_name> --read-acl “”
  ```
    {: pre}

*    cURL 명령: 

    ```
  curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Read: " -H "X-Auth-Token: <OS_AUTH_TOKEN>"
  ```
    {: pre}

컨테이너에서 쓰기 ACL 제거:

* Swift 명령:

    ```
  swift post <container_name> --write-acl “”
  ```
    {: pre}

*    cURL 명령: 

    ```
  curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Write: " -H "X-Auth-Token: <OS_AUTH_TOKEN>"
  ```
    {: pre}

ACL을 제거했는지 여부 확인:

* Swift 명령:

    ```
  swift stat <container_name>
  ```
    {: pre}

  다음 예제 출력에서는 읽기 ACL과 쓰기 ACL을 공백으로 표시하며 이는 액세스 권한이 제거되었음을 의미합니다. 

  ```
         Account: AUTH_c727d7e248b448f6b268f31a1bd8691e
       Container: Test
         Objects: 1
           Bytes: 31512
        Read ACL:
       Write ACL:
         Sync To:
        Sync Key:
   Accept-Ranges: bytes
X-Storage-Policy: standard
     X-Timestamp: 1462818314.11220
      X-Trans-Id: txf04968bc9ef8431982b77-005772e34b
    Content-Type: text/plain; charset=utf-8

  ```
  {: screen}

*   cURL 명령: 
  ```
  curl -i <OS_STORAGE_URL> -I -H "X-Auth-Token: <OS_AUTH_TOKEN>"
  ```
  {: pre}
