{:new_window: target="_blank"} 

# {{site.data.keyword.blockstorageshort}}(베타) 시작하기

*마지막 업데이트 날짜: 2016년 7월 15일*
{: .last-updated}

{{site.data.keyword.blockstoragefull}}에서는 지속적 스토리지가 필요한 경우 트랜잭션이 많은 워크로드와 런타임의 블록 레벨 스토리지에 대한 액세스를 제공합니다.

IBM {{site.data.keyword.blockstorageshort}} for {{site.data.keyword.Bluemix_notm}}를 사용하여 가상 서버에 연결할 수 있는 {{site.data.keyword.blockstorageshort}} 볼륨을 작성할 수 있습니다. Block Storage 볼륨의 데이터는 가상 서버의 라이프사이클 이상으로 지속됩니다. IBM {{site.data.keyword.blockstorageshort}}에서는 OpenStack Cinder를 사용하여 볼륨 라이프사이클을 관리합니다. 

{{site.data.keyword.blockstorageshort}} 볼륨은 IBM {{site.data.keyword.blockstorageshort}} 서비스 인스턴스를 통해 작성합니다. 사용자가 제공하는 특정 디바이스의 가상 서버에 볼륨을 연결하거나 시스템이 사용 가능한 디바이스 이름을 자동으로 선택할 수 있습니다. 가상 서버는 {{site.data.keyword.blockstorageshort}} 서비스와 관계없이 지정된 디바이스를 사용하여 직접 I/O 오퍼레이션을 수행합니다. 

또한 볼륨의 블록 레벨 스냅샷을 작성할 수 있습니다. {{site.data.keyword.blockstorageshort}} 서비스에서는 볼륨이 연결되어 있는 동안 스냅샷 작성을 허용하지 않으므로 결과 스냅샷은 crash-consistent 상태가 됩니다.  


## {{site.data.keyword.blockstorageshort}} 서비스 인스턴스 작성 방법
사용자 영역에 {{site.data.keyword.blockstorageshort}} 서비스의 인스턴스를 작성하려면 다음 단계를 수행하십시오. 
 
1.	{{site.data.keyword.Bluemix_notm}} **카탈로그** 탭으로 이동하여 검색 상자에 **{{site.data.keyword.blockstorageshort}}**를 입력하거나 **서비스**로 이동하여 **스토리지**를 선택하십시오. **{{site.data.keyword.blockstorageshort}}** 서비스를 클릭하십시오.  
2.	영역과 서비스 이름을 입력하십시오. 플랜을 선택하고 **작성**을 클릭하십시오.
 	
{{site.data.keyword.blockstorageshort}} 서비스는 바인딩되지 않은 컨텍스트에서만 지원됩니다.  

사용자 영역에 {{site.data.keyword.blockstorageshort}} 서비스의 인스턴스가 작성됩니다. 서비스 인스턴스 아이콘을 클릭하여 언제든 {{site.data.keyword.blockstorageshort}} UI를 열어 볼륨을 관리할 수 있습니다. 



## {{site.data.keyword.blockstorageshort}} 사용자 인터페이스(UI) 사용 {: #using-block-storage-ui}
{{site.data.keyword.blockstorageshort}} 그래픽 사용자 인터페이스에서는 창의 맨 위에서 스토리지 볼륨, 스냅샷, 볼륨과 스냅샷의 총 스토리지 이용량에 대한 상위 레벨 개요를 제공합니다.  

헤더에는 최근 UI를 새로 고친 날짜 및 시간이 포함됩니다. 필요한 경우 새로 고치기 아이콘(둥근 화살표 아이콘)을 사용하여 UI를 수동으로 새로 고칠 수 있습니다.  

입력한 문자열을 기반으로 볼륨을 찾으려면 검색 막대를 사용하십시오. 입력된 검색 문자열과 일치하는 볼륨만 표시하도록 사용자가 입력할 때 테이블이 필터링됩니다. 

개요 아래에는 볼륨과 스냅샷의 두 탭이 있습니다. 볼륨 탭이 기본적으로 선택되어 있습니다. 이 탭의 테이블에는 사용 가능한 볼륨과 연결된 볼륨에 대한 자세한 정보가 나열되어 있습니다. 테이블의 각 행은 볼륨의 가장 중요한 특성을 표시합니다. 행을 펼치면 추가 특성이 표시됩니다. 또한 연결된 볼륨은 볼륨이 연결된 디바이스 및 가상 서버 인스턴스를 표시합니다. 

스냅샷 탭에는 비슷한 특성과 동작을 가진 스냅샷의 테이블이 표시됩니다.  

새 볼륨을 작성하거나 기존 볼륨을 조작하려면 테이블 위에 있는 작성 아이콘을 사용하십시오. 스냅샷에서 볼륨을 작성하는 경우 조치 드롭 다운 목록도 사용할 수 있습니다.




## 가상 서버에 볼륨 연결 {: #attaching-detaching-volume}
볼륨은 특정 디바이스 이름을 가진 디바이스로 가상 서버에서 연결되거나 분리됩니다. 가상 서버가 볼륨의 데이터를 지속할 수 있으려면 가상 서버에 볼륨을 연결해야 합니다. 

볼륨을 연결하려면 다음 단계를 수행하십시오.  

1.	사용 가능한 볼륨 목록에서 볼륨을 선택하십시오. 
2.	**연결**을 클릭하십시오. 
3.	연결 대화 상자의 드롭 다운 목록에서 가상 서버의 인스턴스를 선택하십시오.  
4.	선택적으로 이 볼륨을 연결하는 데 사용할 디바이스를 지정하십시오. 디바이스를 지정하지 않으면 시스템은 가상 서버에서 첫 번째로 사용 가능한 디바이스를 자동 선택합니다. 
5.	**연결**을 클릭하여 정보를 제출하고 대화 상자를 닫으십시오. 

가상 서버 인스턴스에 대한 정보와 함께 연결된 볼륨 테이블에 볼륨이 나열됩니다.
이제 가상 서버에서 디바이스를 사용하여 데이터를 지속할 수 있습니다.  


# 관련 링크 
{: #rellinks}

## API 참조 
{: #api}
* [OpenStack Block Storage(Cinder) API v2](http://developer.openstack.org/api-ref-blockstorage-v2.html){: new_window}

