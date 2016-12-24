---

copyright:
  years: 2014, 2016
lastupdated: "2016-12-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# {{site.data.keyword.objectstorageshort}} 인스턴스 바인드 해제 및 디프로비저닝 {: #deprovisioning-object-storage}

{{site.data.keyword.objectstorageshort}}를 Cloud Foundry 애플리케이션에 바인드했으나 더 이상 스토리지가 필요하지 않은 경우, 인스턴스의 바인드를 해제하고 디프로비저닝할 수 있습니다.
{: shortdesc}


## 인스턴스 바인드 해제
Cloud Foundry 앱에서 {{site.data.keyword.objectstorageshort}}가 더 이상 필요하지 않지만 저장된 데이터를 유지하려는 경우 앱에서 서비스의 인스턴스를 바인드 해제할 수 있습니다. 

**주의**: {{site.data.keyword.objectstorageshort}} 인스턴스를 {{site.data.keyword.Bluemix_notm}} 애플리케이션에서 바인드 해제하거나 서비스 키를 삭제하면 해당 인스턴스의 모든 신임 정보가 삭제되며 이를 복원할 수 없습니다. {{site.data.keyword.objectstorageshort}} 계정은 {{site.data.keyword.objectstorageshort}} 인스턴스가 디프로비저닝될 때까지 삭제되지 않습니다. 새 서비스 키를 리바인드하거나 작성하여 새 클라우드 신임 정보를 생성할 수 있습니다.

1. 앱에 바인드된 서비스를 표시하려면 Cloud Foundry 애플리케이션의 연결 탭을 클릭하십시오. 
2. 바인드 해제할 서비스를 찾고 서비스 타일의 메뉴 단추를 클릭하십시오. 
3. **서비스 바인드 해제**를 선택하십시오. 
4. **서비스 인스턴스 삭제** 상자를 선택 취소하고 **확인**을 클릭하십시오. 
5. 변경사항이 적용되도록 **다시 스테이징**을 클릭하십시오. 



## 인스턴스 디프로비저닝

더 이상 필요하지 않은 {{site.data.keyword.objectstorageshort}}의 인스턴스가 있는 경우 인스턴스를 삭제할 수 있습니다. 

**주의**: {{site.data.keyword.objectstorageshort}} 인스턴스를 디프로비저닝하면 클라우드 프로젝트 및 Swift 계정이 삭제됩니다. 디프로비저닝된 인스턴스의 모든 컨테이너와 오브젝트가 삭제되며 이를 복원할 수 없습니다. 

1. 앱에 바인드된 서비스를 표시하려면 Cloud Foundry 애플리케이션의 연결 탭을 클릭하십시오. 
2. 바인드 해제할 서비스를 찾고 서비스 타일의 메뉴 단추를 클릭하십시오. 
3. **서비스 삭제**를 선택하십시오. 
4. 확인을 위해 **삭제**를 클릭하십시오. 
5. 변경사항이 적용되도록 **다시 스테이징**을 클릭하십시오. 
