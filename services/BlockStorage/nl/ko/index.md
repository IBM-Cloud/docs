{:new_window: target="_blank"} 

# {{site.data.keyword.blockstorageshort}}(베타) 시작하기

마지막 업데이트 날짜: 2016년 7월 29일
{: .last-updated}

{{site.data.keyword.blockstoragefull}}는 지속적 스토리지가 필요한 트랜잭션 집중 워크로드 및 런타임에 블록 레벨 스토리지에 대한 액세스를 제공합니다. {{site.data.keyword.blockstorageshort}} 서비스를 사용하여 볼륨 라이프사이클을 관리하고 IBM Virtual Servers에 볼륨을 연결하며 Block Storage 볼륨의 스냅샷을 작성할 수 있습니다. 

시작하기 전에 다음 정보를 검토하십시오. 

* {{site.data.keyword.blockstorageshort}} 서비스는 바인딩되지 않은 컨텍스트에서만 지원됩니다.  
* Block Storage 볼륨을 연결하려면 IBM {{site.data.keyword.virtualmachinesshort}}가 작성되어 있어야 합니다. IBM {{site.data.keyword.virtualmachinesshort}}에서 Block Storage 볼륨을 사용하는 방법에 대해 자세히 보려면 [Block Storage 볼륨 및 IBM Virtual Servers](../../virtualmachines/vm_create.html#storage_BS)를 참조하십시오.  

{{site.data.keyword.blockstorageshort}}를 시작하려면 다음 단계를 완료하십시오. 

1. 볼륨을 작성하십시오. 
   
   a. {{site.data.keyword.blockstorageshort}} 서비스를 여십시오. 

   b. **작성**을 클릭하여 **볼륨 작성** 대화 상자를 시작하십시오. 

   c.	원하는 볼륨 크기를 입력하십시오. 소수는 허용되지 않습니다. 크기는 조직에 지정된 할당량에 따라 제한됩니다. 
   
   d.	이름을 입력하십시오. 이름은 표시 용도로만 사용됩니다.
   
   e. 선택적으로 볼륨에 대한 자세한 설명을 입력하십시오. 
   
   f.	**작성**을 클릭하여 정보를 제출하고 대화 상자를 닫으십시오. 

  볼륨을 작성하는 데 시간이 걸릴 수 있습니다. 

2. 가상 서버에 볼륨을 연결하십시오. 

   a. {{site.data.keyword.blockstorageshort}} 서비스를 여십시오. 
   
   b. 사용 가능한 볼륨 목록에서 볼륨을 선택하십시오. 
   
   c.	**연결**을 클릭하십시오. 
   
   d.	연결 대화 상자의 드롭 다운 목록에서 가상 서버의 인스턴스를 선택하십시오.  
   
   e.	선택적으로 이 볼륨을 연결하는 데 사용할 디바이스를 지정하십시오. 디바이스를 지정하지 않으면 시스템은 가상 서버에서 첫 번째로 사용 가능한 디바이스를 자동 선택합니다. 
   
   f.	**연결**을 클릭하여 정보를 제출하고 대화 상자를 닫으십시오. 
   
   가상 서버 인스턴스에 대한 정보와 함께 연결된 볼륨 테이블에 볼륨이 나열됩니다. 이제 가상 서버에서 디바이스를 사용하여 데이터를 지속할 수 있습니다.  
 
다음 단계

볼륨을 사용할 수 있도록 준비하십시오. 자세한 정보는 [볼륨 준비](../BlockStorage/blockstorage_preparingvolume.html)를 참조하십시오. 

# 관련 링크 
{: #rellinks}

## 튜토리얼 및 샘플
{:id="samples"}

* [How to Use IBM Block Storage for Bluemix with IBM Virtual Servers](https://developer.ibm.com/bluemix/2016/02/24/use-block-storage-for-bluemix-with-virtual-servers/){: new_window}
* [Getting Started with IBM Block Storage for Bluemix](https://developer.ibm.com/bluemix/2016/02/15/getting-started-with-block-storage/){: new_window}
* [IBM Block Storage for Bluemix Demo](https://www.youtube.com/watch?v=3gCIHYKU1rE&list=PLzpeuWUENMK2d3L5qCITo2GQEt-7r0oqm&index=45){: new_window}

## API 참조 
{: #api}
* [OpenStack Block Storage(Cinder) API v2](http://developer.openstack.org/api-ref-blockstorage-v2.html){: new_window}

