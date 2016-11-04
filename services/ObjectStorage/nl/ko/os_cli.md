---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}
# {{site.data.keyword.objectstorageshort}} 사용 시작 {: #using-object-storage}
*마지막 업데이트 날짜: 2016년 10월 19일*
{: .last-updated}

# Swift CLI를 사용하여 {{site.data.keyword.objectstorageshort}}에 액세스 {: #using-swift-cli}


{{site.data.keyword.objectstorageshort}} 서비스는 OpenStack Swift를 기반으로 하며 호환 가능한 클라이언트 애플리케이션을 사용하여 서비스에 액세스할 수 있습니다. 이 절에서는 Python Swift 클라이언트({{site.data.keyword.objectstorageshort}} API와 해당 확장기능의 명령행 인터페이스(CLI))를 사용하여 컨테이너와 파일 관련 작업을 수행하는 방법을 설명합니다.
{: shortdesc}

## Swift 클라이언트 설치 {: #install-swift-client}

다음 [필수 소프트웨어](http://docs.openstack.org/user-guide/common/cli_install_openstack_command_line_clients.html#install-the-prerequisite-software){: new_window}를 아직 설치하지 않은 경우 설치를 수행하십시오. 
* Python 2.7 이상
* 설치 도구 패키지
* pip 패키지

Python Swift 클라이언트를 설치하려면 다음 명령을 실행하십시오. 
  ```
sudo pip install python-swiftclient
```
  {: pre}

Python Keystone 클라이언트를 설치하려면 다음 명령을 실행하십시오. 
  ```
sudo pip install python-keystoneclient
```
  {: pre}




## 클라이언트 설정 {: #setup-swift-client}

Swift 클라이언트를 설정하려면 인증 정보를 `export`해야 합니다. UI에 있는 신임 정보를 사용하거나 [새 신임 정보 생성](../ObjectStorage/os_cli.html#generating-cli)을 수행할 수 있습니다. 

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
  {: codeblock}




## {{site.data.keyword.objectstorageshort}} 서비스 신임 정보 생성 {: #generating-cli}

Swift CLI를 사용하여 서비스 신임 정보를 생성하기 위해 다음 단계를 사용할 수 있습니다. 

1. 개발자 역할을 사용하여 {{site.data.keyword.Bluemix_notm}}에 로그인하십시오. 관리할 서비스 인스턴스의 영역 내에 위치해야 합니다.
      ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```
      {: pre}
2. 서비스 신임 정보를 생성하십시오. `service-key-name`은 신임 정보에 지정하는 이름입니다. Cloud Foundry 명령 또는 cURL 명령을 사용할 수 있습니다.
    Cloud Foundry 명령:
      ```
  cf create-service-key "<object_storage_service_instance_name>" <service-key-name> -c '{"role":"<object_storage_role>"}'
  ```
      {: pre}
      예제 Cloud Foundry 명령:
      ```
  cf create-service-key "Object-Storage-AclTest" GeorgeKey -c '{"role":"member"}'

  ```
      {: screen}
  cURL 명령:
  ```
  curl "https://api.ng.bluemix.net/v2/service_keys" -d '{   "service_instance_guid": "<service_instance_guid>",   "name": "<user_name>", "role": "member"}' -X POST -H "Authorization: <bearer_token>" -H "Content-Type: " -H "Cookie: "
  ```
      {: pre}
3. 작성한 서비스 키의 신임 정보 유효성을 검증하십시오.
      Cloud Foundry 명령:
      ```
  cf service-key <service_key_name> <member_name>
  ```
      {: pre}
      Object-Storage-Acl-Test 인스턴스의 예제 멤버 서비스 키:
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
  cURL 명령:
  ```
  curl "https://api.ng.bluemix.net/v2/service_instances/b9656309-d994-4dec-a71f-8eac6e2fc7dc/service_keys" -X GET  -H "Authorization: <bearer_token>" -H "Cookie: "
  ```
      {: pre}




## CLI를 통해 컨테이너에 오브젝트 저장 {: #storing-cli}

1. {{site.data.keyword.Bluemix_notm}}에 로그인하십시오. {{site.data.keyword.objectstorageshort}}의 인스턴스에 대해 작업하기 위해 올바른 조직과 영역에 있는지 확인하십시오. 
    ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```
    {: pre}
2. 다음 명령을 실행하여 새 컨테이너를 작성하십시오. 이때 사용자가 *container_name* 변수를 설정합니다. 
    ```
swift post <container_name>
```
    {: pre}
3. (*선택사항*) 컨테이너가 작성되었는지 확인하려면 다음 명령을 실행하여 컨테이너를 나열하십시오. 
    ```
swift list
```
    {: pre}
4. 다음 명령을 실행하여 컨테이너에 파일을 업로드하십시오. 
    ```
swift upload <container_name> <file_name>
```
    {: pre}
    **참고**: 5GB를 초과하는 파일을 업로드하려면 추가 단계가 필요합니다. 자세한 정보는 [대형 파일에 대한 작업](../ObjectStorage/os_large_files.html#large-files)의 내용을 참조하십시오.
5. (*선택사항*) 업로드에 성공했는지 확인하려면 다음 명령을 실행하여 컨테이너의 컨텐츠를 표시하십시오. 
    ```
swift list <container_name>
```
    {: pre}

**참고**: 동일한 이름의 파일을 업로드하면 {{site.data.keyword.objectstorageshort}}에서 저장된 파일을 새 파일로 바꿉니다. 파일을 다운로드하여 편집하는 경우 파일에 다른 이름을 지정하거나 업로드하기 전에 [오브젝트 버전화 설정](../ObjectStorage/os_versioning.html#work-with-object-versioning)을 수행하여 파일의 두 버전을 모두 유지하십시오. 



## Swift CLI를 사용하여 오브젝트 다운로드 {: #downloading-cli}

1.  {{site.data.keyword.Bluemix_notm}}에 로그인하십시오. {{site.data.keyword.objectstorageshort}}의 인스턴스에 대해 작업하기 위해 올바른 조직과 영역에 있는지 확인하십시오. 
    ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```
    {: pre}
2. 다음 명령을 실행하여 파일을 다운로드하십시오. 
    ```
swift download <container_name> <file_name>
```
    {: pre}




## CLI를 통해 오브젝트와 컨테이너 삭제 {: #deleting-cli}

1.  {{site.data.keyword.Bluemix_notm}}에 로그인하십시오. {{site.data.keyword.objectstorageshort}}의 인스턴스에 대해 작업하기 위해 올바른 조직과 영역에 있는지 확인하십시오. 
    ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```
    {: pre}
2. 다음 명령을 실행하여 파일을 삭제하십시오. 
    ```
swift delete <container_name> <file_name>
```
    {: pre}
    **참고**: [오브젝트를 삭제할 특정 시간](../ObjectStorage/os_deletion.html#schedule-object-deletion)을 스케줄링할 수 있습니다.
3. 컨테이너를 삭제하려면 다음 명령을 실행하십시오. 
    ```
    swift delete <container_name>
    ```
    {: pre}
    **주의**: 컨테이너를 삭제하면 컨테이너에 저장된 모든 오브젝트가 삭제됩니다.





## 디렉토리에 대한 작업 {: #directory-cli}

#### Swift CLI를 사용하여 컨테이너에 디렉토리 추가

Swift에는 실제 디렉토리 구조가 없지만 이름을 지정하여 디렉토리 레이아웃을 표시합니다. 디렉토리 이름을 지정하면 상대 경로의 일부로 모든 파일 이름에 첨부됩니다. 

1. 컨테이너에 디렉토리를 추가하려면 다음 명령을 실행하십시오. 
    ```
swift upload <container_name> <directory_name>
```
    {: pre}

#### 디렉토리 다운로드
디렉토리 구조를 다운로드하려면 `-prefix` 매개변수를 사용하여 다운로드하려는 디렉토리 또는 디렉토리 구조를 표시하십시오. 

1. 디렉토리를 다운로드하려면 다음 명령을 실행하십시오. 
    ```
swift download <container_name> --prefix <directory>
```
    {: pre}
