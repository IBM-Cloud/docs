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

# 오브젝트 저장

UI나 CLI를 사용하여 오브젝트를 스토리지에 업로드할 수 있습니다. 오브젝트 업로드는 한 번의 업로드에서 최대 크기 5GB로 제한됩니다. 그러나 대형 오브젝트를 작은 오브젝트로 세그먼트화하여 업로드할 수 있습니다.
{: shortdesc}


## UI를 통해 컨테이너에 오브젝트 저장 {: #storing-ui}

**참고**: 같은 이름의 파일을 업로드할 때 {{site.data.keyword.objectstorageshort}}에서 새 파일로 저장된 파일을 대체합니다. 파일을 다운로드하여 편집하는 경우, 파일 버전을 모두 보관하려면 업로드하기 전에 파일에 다른 이름을 지정하거나 [오브젝트 버전화를 설정](/docs/services/ObjectStorage/os_versioning.html)하십시오. 


1. 서비스 인스턴스 대시보드의 **조치** 드롭 다운 메뉴에서 컨테이너를 추가합니다. 
2. 컨테이너 이름을 지정하고 **작성**을 클릭합니다.
3. **조치** 드롭 다운 메뉴에서 **파일 추가**를 선택합니다. 대화 상자가 열립니다.
4. 업로드할 파일을 선택하고 **열기**를 클릭합니다. 



## CLI를 통해 컨테이너에 오브젝트 저장 {: #storing-cli}

1. {{site.data.keyword.Bluemix_notm}}에 로그인되어 있지 않는 경우 {{site.data.keyword.objectstorageshort}}의 인스턴스가 있는 조직 및 영역에 로그인하십시오.

  ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```
  {: pre}

2. 다음 명령을 실행하여 {{site.data.keyword.objectstorageshort}} 컨테이너를 작성하십시오. 이제 *container_name* 변수가 사용자에 의해 설정됩니다. 

  ```
swift post <container_name>
```
  {: pre}

**참고**: 오류 메시지가 수신되면 [필수 소프트웨어](/docs/services/ObjectStorage/os_configuring.html#install-swift-client)를 설치했는지 확인하십시오. 

3. 선택사항: 컨테이너가 작성되었는지 확인하려면 다음 명령을 실행하여 컨테이너를 나열하십시오. 

  ```
swift list
```
  {: pre}

4. 실수로 데이터를 겹쳐써서 데이터가 손상되는 일이 발생하지 않도록 [오브젝트 버전화 설정](/docs/services/ObjectStorage/os_versioning.html)을 수행하십시오. 오브젝트 버전화를 원하지 않는 경우에는 저장소의 기존 파일을 나열하여 필요에 따라 디렉토리 또는 파일의 이름을 바꾼 후 업로드하십시오.

5. 다음 명령을 실행하여 컨테이너에 파일을 업로드하십시오. 

  ```
swift upload <container_name> <file_name>
```
  {: pre}

  **참고**: 5GB를 초과하는 파일을 업로드하려면 [추가 단계가 필요](/docs/services/ObjectStorage/os_large_files.html)합니다. 

6. 선택사항: 업로드에 성공했는지 확인하려면 다음 명령을 실행하여 컨테이너의 컨텐츠를 표시하십시오. 

  ```
swift list <container_name>
```
  {: pre}
