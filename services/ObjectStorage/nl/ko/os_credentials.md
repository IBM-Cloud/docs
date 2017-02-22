---

copyright:
  years: 2014, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 서비스 신임 정보 생성 {: #credentials}

서비스 신임 정보는 서비스에 필요한 인증과 보안을 제공하는 데 사용됩니다. CLI나 {{site.data.keyword.Bluemix_notm}} UI를 사용하여 신임 정보를 새로 생성할 수 있습니다.
{: shortdesc}


## UI에서 신임 정보를 추가하려면 다음 단계를 수행하십시오. 

1. 서비스 인스턴스 대시보드의 **서비스 신임 정보** 탭에서 **새 신임 정보**를 클릭하고 이름을 지정하십시오. 
2. 선택사항: **인라인 구성 매개변수 추가** 텍스트 필드에서, 부여하려는 [액세스 유형](/docs/services/ObjectStorage/os_access_types.html)이 있는 역할의 신임 정보를 입력하십시오. 이 정보는 JSON 페이로드로 형식화되어야 합니다.
    - 관리 사용자 작성: `{"role":"admin"}`
    - 비관리 사용자 작성: `{"role":"member"}`
3. **추가**를 클릭하십시오.


## CLI에서 Cloud Foundry 명령을 사용하여 신임 정보를 추가하려면 다음 단계를 수행하십시오. 

1. {{site.data.keyword.Bluemix_notm}}에 로그인되어 있지 않는 경우 개발자 역할을 사용하여 로그인하십시오. 관리할 서비스 인스턴스의 영역 내에 위치해야 합니다.
  ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```
  {: pre}

2. 서비스 신임 정보를 생성하십시오. `service-key-name` 변수를 대체하여
신임 정보에 이름을 지정합니다. 선택적으로 [사용자 역할](/docs/services/ObjectStorage/os_access_types.html)도 지정할 수 있습니다.

  ```
  cf create-service-key "<service_instance_name>" <service-key-name> -c '{"role":"<user_role>"}'
  ```
  {: pre}

  예:
  ```
  cf create-service-key "Object-Storage-AclTest" GeorgeKey -c '{"role":"member"}'
  ```
  {: screen}

3. 작성한 키의 신임 정보 유효성을 검증하십시오. 

  ```
  cf service-keys <service_instance_name>
  ```
  {: pre}

  구성원 역할이 있는 사용자의 예제 인스턴스 키 Object-Storage-Acl-Test입니다. 

  ```
  {
    "auth_url": "https://identity.open.softlayer.com",
    "domainId": "8753ff40ac1a4f4a9f162ad8026b6ce0",
    "domainName": "757955",
    "password": "xxxxxxxx",
    "project": "object_storage_6046b6e2_ee53_4884_916f_89c65e4d408e",
    "projectId": "c727d7e248b448f6b268f31a1bd8691e",
    "region": "dallas",
    "role": "member",
    "userId": "3c5b516655e4479881d3d216895faedb",
    "username": "member_2afbeea1d58b1867f46c699553d1e4513e7df83a"
  }
  ```
  {: screen}



#### CLI에서 cURL 명령을 사용하여 신임 정보를 추가하려면 다음 단계를 수행하십시오. 

1. {{site.data.keyword.Bluemix_notm}}에 로그인되어 있지 않는 경우 개발자 역할을 사용하여 로그인하십시오. 관리할 서비스 인스턴스의 영역 내에 위치해야 합니다.

  ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```
  {: pre}

2. 다음 명령을 실행하여 서비스 신임 정보를 생성하십시오. 

  ```
  curl "https://api.ng.bluemix.net/v2/service_keys" -d '{   "service_instance_guid": "<service_instance_guid>",   "name: <service_instance_name>", "role: <user_role>"}' -X POST -H "Authorization: <bearer_token>" -H "Content-Type: <content_type" -H "Cookie: <cookie>"
  ```
  {: pre}

  <table>
  <caption> 표 1. cURL 서비스 신임 정보 변수 설명</caption>
    <tr>
      <th> 변수 </th>
      <th> 설명 </th>
    </tr>
    <tr>
      <td> <code>https://api.ng.bluemix.net/v2/service_keys</code> </td>
      <td> 서비스 키 엔드포인트입니다. </td>
    </tr>
    <tr>
      <td><i> service_instance_guid </i></td>
      <td> URL에 포함되어 있습니다. </td>
    </tr>
    <tr>
      <td><i> name </i></td>
      <td> 서비스 인스턴스 이름입니다. </td>
    </tr>
    <tr>
      <td><i> role </i></td>
      <td> <a href= /docs/services/ObjectStorage/os_constructing.html>사용자 역할</a>을 admin 또는 member로 지정하십시오. </td>
    </tr>
    <tr>
      <td><i> bearer_token </i></td>
      <td> Keystone으로 인스턴스를 인증할 때 수신한 토큰입니다. </td>
    </tr>
  </table>



3. 다음 명령을 실행하여 신임 정보 유효성을 검증하십시오. 

  ```
  curl "https://api.ng.bluemix.net/v2/service_instances/b9656309-d994-4dec-a71f-8eac6e2fc7dc/service_keys" -X GET  -H "Authorization: <bearer_token>" -H "Cookie: "
  ```
  {: screen}
