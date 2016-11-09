---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# {{site.data.keyword.objectstorageshort}} 인스턴스 바인드 해제 및 디프로비저닝 {: #deprovisioning-object-storage}

*마지막 업데이트 날짜: 2016년 10월 19일*
{: .last-updated}


### 인스턴스 바인드 해제
Cloud Foundry 앱에서 {{site.data.keyword.objectstorageshort}}가 더 이상 필요하지 않지만 저장된 데이터를 유지하려는 경우 앱에서 서비스의 인스턴스를 바인드 해제할 수 있습니다. 

**주의**: {{site.data.keyword.objectstorageshort}} 인스턴스를 {{site.data.keyword.Bluemix_notm}} 애플리케이션에서 바인드 해제하거나 서비스 키를 삭제하면 해당 인스턴스의 모든 신임 정보가 삭제되며 이를 복원할 수 없습니다. 

1. {{site.data.keyword.Bluemix_notm}} 콘솔에서 앱 세부사항을 여십시오. 
2. {{site.data.keyword.objectstorageshort}} 인스턴스를 선택하고 **서비스 바인드 해제**를 클릭하십시오. 
3. **제거**를 클릭하십시오. 
4. **다시 스테이징**을 클릭하십시오. 



### 인스턴스 디프로비저닝

더 이상 필요하지 않은 {{site.data.keyword.objectstorageshort}}의 바인드 해제된 인스턴스가 있는 경우 인스턴스를 삭제할 수 있습니다. 

**주의**: {{site.data.keyword.objectstorageshort}} 인스턴스를 디프로비저닝하면 클라우드 프로젝트가 삭제됩니다. 디프로비저닝된 인스턴스의 모든 컨테이너와 오브젝트가 삭제되며 이를 복원할 수 없습니다. 

1. {{site.data.keyword.Bluemix_notm}} 콘솔에서 앱 세부사항을 여십시오. 
2. {{site.data.keyword.objectstorageshort}} 인스턴스를 선택하고 **삭제**를 클릭하십시오. 
3. **다시 스테이징**을 클릭하십시오. 
