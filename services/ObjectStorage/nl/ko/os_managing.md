---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# 오브젝트 관리

Swift CLI, API 또는 Bluemix UI를 사용하여 오브젝트와 컨테이너를 관리할 수 있습니다.
{: shortdesc}

오브젝트를 관리하려면 우선 서비스 인스턴스를 [인증](/docs/services/ObjectStorage/os_authenticate.html)하고 서비스 신임 정보를 [생성](/docs/services/ObjectStorage/os_credentials.html)한 후에 Swift CLI를 [구성](/docs/services/ObjectStorage/os_configuring.html)했는지 확인하십시오. 

오브젝트를 관리할 때는 다음과 같은 점을 유념하십시오. 
  * 저장 가능한 데이터 용량에는 제한이 없지만 개별 업로드 시 5GB의 제한이 있습니다. 5GB를 초과하는 파일을 업로드해야 하는 경우에는 [대형 오브젝트 저장](/docs/services/ObjectStorage/os_large_files.html)에 있는 단계를 따르십시오. 
  * Swift에는 실제 디렉토리 구조가 없지만 [기존 디렉토리](/docs/services/ObjectStorage/os_directories.html)를 명령에 추가할 수 있습니다. 
  * 실수로 데이터를 겹쳐써서 데이터가 손상되는 일이 발생하지 않도록 [오브젝트 버전화 설정](/docs/services/ObjectStorage/os_versioning.html)을 수행하십시오. 
  * 오브젝트를 삭제할 [시간을 스케줄링](/docs/services/ObjectStorage/os_deletion.html)할 수 있습니다. 
