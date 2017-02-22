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


# 오브젝트 삭제 

더 이상 필요하지 않은 오브젝트나 컨테이너를 스토리지 인스턴스에서 삭제할 수 있습니다. 수동으로 삭제하거나, 오브젝트의 만료 [시간을 스케줄링](/docs/services/ObjectStorage/os_deletion.html#schedule-object-deletion)할 수 있습니다.
{: shortdesc}

**참고**: 컨테이너를 삭제하는 경우 해당 컨테이너에 저장된 모든 오브젝트가 삭제됩니다. 


## UI를 통해 오브젝트와 컨테이너 삭제 {: #deleting-ui}

1. 서비스 인스턴스 대시보드에서 더 이상 필요하지 않은 파일이 있는 컨테이너를 선택합니다. 
2. **조치** 드롭 다운 메뉴에서 **파일 삭제**를 선택합니다. 
3. 컨테이너가 더 이상 필요하지 않은 경우 **조치** 드롭 다운 메뉴에서 **컨테이너 삭제**를 선택하십시오. 



## CLI를 통해 오브젝트와 컨테이너 삭제 {: #deleting-cli}

1.  {{site.data.keyword.Bluemix_notm}}에 로그인되어 있지 않는 경우 {{site.data.keyword.objectstorageshort}}의 인스턴스가 있는 조직 및 영역에 로그인하십시오.
  ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```
  {: pre}

2. 선택사항: 파일 및 컨테이너를 삭제하기 전에 오브젝트의 백업이 있는지 확인하십시오. 

3. 다음 명령을 실행하여 파일을 삭제하십시오. 
  ```
swift delete <container_name> <file_name>
```
  {: pre}

4. 컨테이너를 삭제하려면 다음 명령을 실행하십시오. 
  ```
    swift delete <container_name>
    ```
  {: pre}



## 오브젝트 삭제 스케줄링 {: #schedule-object-deletion}


`X-Delete-At` 또는 `X-Delete-After` 헤더 중 하나를 사용하여 오브젝트의 삭제를 스케줄링할 수 있습니다.
{: shortdesc}

`X-Delete-At` 헤더는 오브젝트를 삭제하는 epoch 시간을 나타내는 정수를 취합니다. `X-Delete_After` 헤더는 오브젝트가 삭제된 후의 시간(초)을 나타내는 정수를 취합니다 

**참고:** 표시된 정확한 시간에 오브젝트가 실제로 삭제되지 않을 수 있습니다. 그러나 오브젝트는 사실상 지정된 시간에 만료됩니다. 해당 시간에는 오브젝트에 더 이상 접근할 수 없습니다. 실제 삭제는 Swift 클러스터에서 구성된 swift-object-expirer 디먼이 다음번에 실행될 때 발생합니다. 

#### Swift 명령 사용 방법:

* 특정 날짜 및 시간에 오브젝트를 삭제하도록 설정하려면, 다음 명령을 실행하십시오. 

    ```
    swift post -H "X-Delete-At:<epoch_time>" <container_name> <object_name>
    ```
    {: pre}

    예:
    오브젝트를 "2016/04/01 08:00:00"에 삭제하도록 설정하려면, 다음 명령을 실행하십시오. 

    ```
    swift post -H "X-Delete-At:1459515600" container1 file7
    ```
    {: screen}

* 특정 기간 후에 오브젝트를 삭제하도록 설정하려면, 다음 명령을 사용하십시오. 

    ```
    swift post -H "X-Delete-After:<number_of_seconds>" <container_name> <object_name>
    ```
    {: pre}

    예:
    지금부터 한 시간 후에 오브젝트를 삭제하도록 설정하려면, 다음 명령을 실행하십시오. 

    ```
    swift post -H "X-Delete-After:3600" container1 file7
    ```
    {: screen}

* 오브젝트에서 만기 시간을 제거하려면, 다음 명령을 사용하십시오. 

    ```
    swift post -H "X-Remove-Delete-After:<number_of_seconds>" <container_name> <object_name>
    ```
    {: pre}



#### cURL 명령 사용 방법:

* 오브젝트를 "2016/04/01 08:00:00"에 삭제하도록 설정하려면, 다음 명령을 사용하십시오. 

    ```
    cURL -X POST -H "X-Auth-Token: <token>" -H "X-Delete-At:<epoch_time>" https://<object-storage_url>/<container_name>/<object_name>
    ```
    {: pre}

* 지금부터 한 시간 후에 오브젝트를 삭제하도록 설정하려면, 다음 명령을 사용하십시오. 

    ```
    cURL -X POST -H "X-Auth-Token: <token>" -H "X-Delete-After:<number_of_seconds>" https://<object-storage_url>/<container_name>/<object_name>
    ```
    {: pre}

* 오브젝트에 헤더가 있는지 확인하려면, 다음 명령을 사용하십시오. 

    ```
    cURL -I -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_name>/<object_name>
    ```
    {: pre}

* 만기 시간을 제거하려면, 다음 명령을 사용하십시오. 

    ```
    cURL -X POST -H "X-Auth-Token: <token>" -H "X-Remove-Delete-At:<epoch_time>" https://<object-storage_url>/<container_name>/<object_name>
    ```
    {: pre}
