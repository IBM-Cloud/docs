{:new_window: target="_blank"}


# {{site.data.keyword.blockstorageshort}} 정보
{: #about-block-storage}

마지막 업데이트 날짜: 2016년 9월 7일
{: .last-updated}

IBM {{site.data.keyword.blockstorageshort}} 서비스를 사용하면 가상 서버에 지속적 스토리지를 연결할 수 있습니다. 스토리지를 사용하려면 가상 서버에 블록 볼륨을 연결합니다. Block Storage 볼륨의 데이터는 가상 서버의 라이프사이클 이상으로 지속됩니다. 즉, 데이터를 변경하지 않고 서버 인스턴스에서 볼륨을 분리하고 다른 서버 인스턴스에 다시 연결할 수 있습니다. {{site.data.keyword.blockstorageshort}}는 OpenStack Cinder를 사용하여 볼륨 라이프사이클을 관리합니다. 

스토리지는 /dev/vdb 등과 같이 파티션 나누기, 포맷 및 마운트할 수 있는 블록 디바이스에서 액세스합니다. 삭제 전까지 데이터는 지속됩니다. 

## 볼륨 
{: #using-volumes-concept}

{{site.data.keyword.blockstorageshort}} 볼륨은 {{site.data.keyword.blockstorageshort}} 서비스 인스턴스를 통해 작성합니다. 다음과 같은 방법으로 가상 서버에 볼륨을 연결할 수 있습니다.
  

* 사용자가 제공하는 특정 디바이스를 지정하십시오. 
* 시스템이 사용 가능한 디바이스 이름을 자동으로 선택할지 지정하십시오. 

가상 서버는 {{site.data.keyword.blockstorageshort}} 서비스와 관계없이 지정된 디바이스를 사용하여 직접 I/O 오퍼레이션을 수행합니다. 

## 스냅샷 
{: #using-snapshots-concept}

볼륨의 블록 레벨 스냅샷을 작성할 수도 있습니다. 스냅샷은 특정 시점에 블록 스토리지 볼륨의 데이터를 캡처합니다. 스냅샷을 사용하여 데이터의 증분식 백업을 수행할 수 있습니다. 스냅샷은 원래 볼륨과 동일한 스토리지에 있습니다. 그러므로 스냅샷은 충분한 재해 복구 전략이 아닙니다.

**참고**: 볼륨이 서버 인스턴스에 연결된 동안 스냅샷을 작성할 수 없습니다. 

스냅샷에서 볼륨을 작성할 때, 새 볼륨은 스냅샷을 찍을 때 원래 볼륨의 상태와 동일한 상태로 작성됩니다. 

스냅샷에서 볼륨을 작성하면 다음과 같은 영향을 미칩니다.

* 기존 볼륨이 제거되지 않습니다.
* 관련 스냅샷을 찍은 후 작성, 수정 또는 삭제된 데이터가 새 볼륨에 포함되지 않습니다.

다음 단계

볼륨을 작성하십시오. 자세한 정보는 [볼륨 작성](../BlockStorage/blockstorage_creatingvolume.html)을 참조하십시오. 
