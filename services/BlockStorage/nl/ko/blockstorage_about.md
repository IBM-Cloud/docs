{:new_window: target="_blank"}


# {{site.data.keyword.blockstorageshort}} 정보
{: #about-block-storage}

마지막 업데이트 날짜: 2016년 8월 1일
{: .last-updated}

## 볼륨 
{: #using-volumes-concept}

IBM {{site.data.keyword.blockstorageshort}}를 사용하여 볼륨을 작성하고 이 볼륨을 가상 서버에 연결할 수 있습니다. 기본적으로 IBM {{site.data.keyword.virtualmachinesshort}}에는 지속적 스토리지가 없으며 다시 시작되는 경우 기본 이미지로 되돌아갑니다. {{site.data.keyword.blockstorageshort}}는 가상 서버에 지속적 스토리지를 제공합니다. Block Storage 볼륨의 데이터는 가상 서버의 라이프사이클 이상으로 지속됩니다. {{site.data.keyword.blockstorageshort}}는 OpenStack Cinder를 사용하여 볼륨 라이프사이클을 관리합니다.

{{site.data.keyword.blockstorageshort}} 볼륨은 {{site.data.keyword.blockstorageshort}} 서비스 인스턴스를 통해 작성합니다. 다음과 같은 방법으로 가상 서버에 볼륨을 연결할 수 있습니다.
  

* 사용자가 제공하는 특정 디바이스를 지정하십시오. 
* 시스템이 사용 가능한 디바이스 이름을 자동으로 선택할지 지정하십시오. 

가상 서버는 {{site.data.keyword.blockstorageshort}} 서비스와 관계없이 지정된 디바이스를 사용하여 직접 I/O 오퍼레이션을 수행합니다. 

## 스냅샷 
{: #using-snapshots-concept}

볼륨의 블록 레벨 스냅샷을 작성할 수도 있습니다. 볼륨이 연결되어 있는 동안에는 스냅샷을 작성할 수 없으므로 결과 스냅샷은 충돌 일치(crash-consistent)가 됩니다.  

다음 단계

볼륨을 작성하십시오. 자세한 정보는 [볼륨 작성](../BlockStorage/blockstorage_creatingvolume.html)을 참조하십시오. 
