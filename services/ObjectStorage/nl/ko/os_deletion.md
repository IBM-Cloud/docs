---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 오브젝트 삭제 스케줄링 {: #schedule-object-deletion}
*마지막 업데이트 날짜: 2016년 10월 19일*
{: .last-updated}

오브젝트 삭제를 스케줄링할 수 있습니다. `X-Delete-At` 또는 `X-Delete-After` 헤더 중 하나를 이용하여 이를 수행할 수 있습니다.
{: shortdesc}

`X-Delete-At` 헤더는 오브젝트를 삭제하는 epoch 시간을 나타내는 정수를 사용합니다. `X-Delete_After` 헤더는 오브젝트가 삭제되고 난 후의 시간(초)을 나타내는 정수를 사용합니다. Swift 클라이언트를 사용하여 오브젝트 삭제를 스케줄링하려면 사용자 요구사항에 최적으로 맞는 다음 명령을 실행하십시오. 

* 특정 날짜 및 시간에 오브젝트를 삭제하도록 설정하려면 다음 명령을 실행하십시오. 
    
    ```
    swift post -H "X-Delete-At:<epoch_time>" <container_name> <object_name>
    ```
    {: pre}
    
    예:
    
    오브젝트를 "2016/04/01 08:00:00"에 삭제하도록 설정하려면 다음 명령을 실행하십시오. 
    
    ```
    swift post -H "X-Delete-At:1459515600" <container_name> <object_name>
    ```
    {: screen}
* 지금부터 1시간 안에 오브젝트를 삭제하도록 설정하려면, 다음 명령을 사용하십시오. 
    
    ```
    swift post -H "X-Delete-After:<number_of_seconds" <container_name> <object_name>
    ```
    {: pre}
    
    예:
    
    지금부터 한 시간 안에 오브젝트를 삭제하도록 설정하려면 다음 명령을 실행하십시오. 
    
    ```
swift post -H "X-Delete-After:3600" container object
```
    {: screen}
* 오브젝트에서 만기 시간을 제거하려면, 다음 명령을 사용하십시오. 
    
    ```
    swift post -H "X-Remove-Delete-After:<number_of_seconds>" container object
    ```
    {: pre}

스케줄링된 오브젝트 삭제에 cURL 명령을 사용하기 위해 사용자 요구사항에 최적으로 맞는 다음 명령을 실행할 수 있습니다. 시간의 표준은 Swift 클라이언트와 동일합니다. 

* 오브젝트를 "2016/04/01 08:00:00"에 삭제되도록 설정하려면, 다음 명령을 사용하십시오. 
   
   ```
   cURL -X POST -H "X-Auth-Token: <token>" -H "X-Delete-At:<epoch_time>" https://<object-storage_url>/<container_name/<object_name>
    ```
    {: pre}
    
* 지금부터 1시간 안에 오브젝트를 삭제하도록 설정하려면, 다음 명령을 사용하십시오. 
    
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

**참고:** 표시된 정확한 시간에 오브젝트가 실제로 삭제되지 않을 수 있습니다. 그러나 오브젝트는 사실상 지정된 시간에 만료됩니다. 이는 오브젝트에 더 이상 도달할 수 없음을 의미합니다. 다음 번에 Swift 클러스터에서 구성된 swift-object-expirer 디먼을 실행하면 실제로 삭제가 실행됩니다. 
