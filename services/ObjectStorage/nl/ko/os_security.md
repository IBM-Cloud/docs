---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}



# 액세스 관리

액세스 제어 목록을 사용하여 서비스 액세스를 관리할 수 있습니다. [관리 사용자](/docs/services/ObjectStorage/os_access_types.html)는 읽기 및 쓰기 액세스 권한은 물론 제거 액세스 권한을 부여할 수 있습니다.
{: shortdesc}

UI 또는 Swift CLI를 사용하여 액세스 권한을 관리하기 전에, 서비스를 구성하고 오브젝트 저장을 시작했는지 확인하십시오. 

액세스 제어 목록 관련 작업 중에는 다음과 같은 점을 유념하십시오. 
  * 컨테이너를 작성하는 사용자는 자동적으로 해당 컨테이너에 대한 관리 권한이 부여됩니다. 
  * 액세스 제어 목록은 서비스 인스턴스, 스토리지 계정 또는 프로젝트 레벨에 사용할 수 없습니다. 액세스 권한은 컨테이너 또는 오브젝트 레벨에서만 관리가 가능합니다. 
  * 컨테이너에 대한 액세스 권한이 [제거](/docs/services/ObjectStorage/os_remove_access.html)되었는지 확인하십시오. 
