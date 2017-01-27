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

# 오브젝트 다운로드

저장된 오브젝트를 다운로드하여 UI나 CLI를 통해 편집하거나 검토할 수 있습니다.
{: shortdesc}


## UI에서 오브젝트 다운로드 {: #downloading-ui}

1. 실수로 데이터를 겹쳐써서 데이터가 손상되는 일이 발생하지 않도록 [오브젝트 버전화 설정](/docs/services/ObjectStorage/os_versioning.html)을 수행하십시오. 오브젝트를 버전화하지 않으려면 다운로드하기 전에 디렉토리나 파일 이름을 바꾸십시오. 
2. 서비스 인스턴스 대시보드에서 다운로드할 파일이 있는 컨테이너를 선택합니다. 
3. 파일을 선택합니다.
4. **조치** 드롭 다운 메뉴에서 **파일 다운로드**를 선택합니다. 


## Swift CLI를 사용하여 오브젝트 다운로드 {: #downloading-cli}

1.  {{site.data.keyword.Bluemix_notm}}에 로그인되어 있지 않는 경우 {{site.data.keyword.objectstorageshort}}의 인스턴스가 있는 조직 및 영역에 로그인하십시오.

```
cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
```
{: pre}

2. 실수로 데이터를 겹쳐써서 데이터가 손상되는 일이 발생하지 않도록 [오브젝트 버전화 설정](/docs/services/ObjectStorage/os_versioning.html)을 수행하십시오. 오브젝트 버전화를 원하지 않는 경우에는 저장소의 기존 파일을 나열하여 필요에 따라 디렉토리 또는 파일의 이름을 바꾼 후 다운로드하십시오.

3. 다음 명령을 실행하여 파일을 다운로드하십시오. 

```
swift download <container_name> <file_name>
```
{: pre}
