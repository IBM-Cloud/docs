---

copyright:
  years: 2014, 2016
lastupdated: "2016-12-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}



# 액세스 관리

액세스 제어 목록을 사용하여 서비스 액세스를 관리할 수 있습니다. [관리자](/docs/services/ObjectStorage/os_access_types.html)는 서비스 인스턴스 관리 시 액세스를 제거할 뿐 아니라 읽기 및 쓰기 액세스를 부여할 수 있습니다.
{: shortdesc}


Swift CLI 또는 Bluemix UI를 사용하여 액세스 제어 목록을 관리할 수 있습니다. 액세스 관리는 서비스를 구성하고 오브젝트 저장이 시작된 후에 가능합니다. 액세스 관리 시 주의해야 할 몇 가지 사항이 있습니다. 
  * 컨테이너를 작성하는 사용자는 자동적으로 해당 컨테이너에 대한 관리 권한이 부여됩니다. 
  * 액세스 제어 목록은 서비스 인스턴스, 스토리지 계정 또는 프로젝트 레벨에 사용할 수 없습니다. 액세스는 컨테이너 레벨에서만 관리할 수 있습니다. 
  * 컨테이너에 대한 액세스가 [제거](/docs/services/ObjectStorage/os_remove_access.html)되었는지 확인하십시오. 
