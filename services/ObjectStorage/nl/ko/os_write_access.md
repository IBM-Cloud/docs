---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 쓰기 액세스 권한 부여 

[admin 역할](/docs/services/ObjectStorage/os_access_types.html)이 있는 {{site.data.keyword.objectstorageshort}} 사용자는 다른 사용자에 대한 쓰기 액세스 권한을 부여하고 쓰기 ACL 조합을 조작할 수 있습니다.
{: shortdesc}

<table>
<caption> 표 1. 옵션별 쓰기 액세스 권한</caption>
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
    <td> <code> &#42;:user_id </code> </td>
  </tr>
  <tr>
    <td> 지정된 프로젝트의 모든 사용자에 대한 쓰기 </td>
    <td>  <code> project_id:&#42; </code> </td>
  </tr>
  <tr>
    <td> 모든 프로젝트의 모든 사용자에 대한 쓰기 </td>
    <td>  <code> &#42;:&#42; </code> </td>
  </tr>
</table>



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

2. 다음 명령을 실행하여 쓰기 액세스를 부여하십시오.

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

3. 쓰기 ACL 값을 확인하십시오. 

    Swift 명령:

    ```
    swift stat <container_name>
    ```
    {: pre}

    cURL 명령: 

    ```
    curl -i <OS_STORAGE_URL> -I -H "X-Auth-Token:<OS_AUTH_TOKEN>"
    ```
    {: pre}
