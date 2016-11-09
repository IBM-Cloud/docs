---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 오브젝트 버전화에 대한 작업 {: #work-with-object-versioning}

*마지막 업데이트 날짜: 2016년 10월 19일*
{: .last-updated}

오브젝트 버전화를 사용하면 파일 이름을 바꾸지 않고 오브젝트의 개별 버전을 유지할 수 있습니다. 그러면 각 오브젝트의 히스토리를 보고 변경이 이루어진 경우를 계속 추적할 수 있습니다.
{: shortdesc}


### 오브젝트 버전화 설정 {: #setting-up-versioning}

`X-Versions-Location` 매개변수를 사용하여 컨테이너에서 각 오브젝트의 버전을 설정할 수 있습니다. 이를 수행하려면, 다음과 같이 추가 컨테이너를 작성하여 오브젝트의 이전 버전을 유지하십시오. 

Swift 클라이언트를 통해 또는 cURL 명령을 사용하여 오브젝트 버전화를 설정할 수 있습니다. 
* Swift 클라이언트를 사용 중인 경우 다음 명령을 실행하십시오. 

    ```
    swift post <container_name> -H "X-Versions-Location:<backup_container_name>"
    ```
    {: pre}
    
* cURL을 사용 중인 경우에는 다음과 같이 설정할 수 있습니다. 

    ```
    curl -i -X PUT -H "X-Auth-Token: <token>" -H "X-Versions-Location:<backup_container_name>" https://<object-storage_url>/<container_name>
    ```
    {: pre}
    
**참고**: 백업 컨테이너의 오브젝트는 다음과 같은 형식으로 이름이 자동 지정됩니다. `<Length><Object_name>/<Timestamp>`.
<table>
  <tr>
    <th> 속성 </th>
    <th> 설명 </th>
  </tr>
  <tr>
    <td> `Length` </td>
    <td> 오브젝트 이름의 길이입니다. 3자의 영(0)으로 채워진 16진수입니다. </td>
  </tr>
  <tr>
    <td> `Object_name` </td>
    <td> 오브젝트 이름입니다. </td>
  </tr>
  <tr>
    <td> `Timestamp` </td>
    <td> 오브젝트의 버전이 처음 업로드된 때를 나타내는 시간소인입니다. </td>
  </tr>
</table>

### 오브젝트 버전화 사용 안함 {: #disabling-versioning}

Swift 클라이언트를 통해 또는 cURL 명령을 사용하여 버전화를 사용 안함으로 설정할 수 있습니다. 

* Swift 클라이언트를 사용하려면 다음 명령을 실행하십시오. 

    ```
    swift post <container_name> -H "X-Remove-Versions-Location:"
    ```
    {: pre}
    
* 다음 cURL 명령을 실행하여 버전화를 사용 안함으로 설정하십시오. 

    ```
    cURL -i -X POST -H "X-Auth-Token: <token>" -H "X-Remove-Versions-Location: anyvalue" https://<object-storage_url>/<container_name>
    ```
    {: pre}


### 오브젝트 버전화 튜토리얼 {: #versioning-tutorial}
<!--- SHAWNA: This needs more background information. What are they doing? Why are they doing it? What is the outcome? --->

다음 튜토리얼을 사용하여 오브젝트 버전화의 전체 라이프사이클을 이해할 수 있습니다. 

1. `container_one` 컨테이너를 작성하십시오. 

    ```
    swift post container_one
    ```
    {: pre}
    
3. 이름이 `container_two`인 두 번째 컨테이너를 작성하십시오. 

    ```
    swift post container_two
    ```
    {: pre}
    
2. 버전화를 설정하십시오. 

    ```
swift post container_one -H "X-Versions-Location:container_two"
```
    {: pre}
    
4. 처음으로 기본 컨테이너에 오브젝트를 업로드하십시오. 

    ```
    swift upload container_one object
    ```
    {: pre}
    
7. 오브젝트의 새 버전을 container_one에 업로드하십시오. 파일의 새 버전을 업로드하는 경우 이전 버전은 버전화 설정 시 지정한 백업 컨테이너로 자동으로 이동합니다. 

    ```
    swift upload container_one object
    ```
    {: pre}
    
8. 컨테이너에서 파일의 새 버전을 보려면 container_on의 오브젝트를 나열하십시오. 

    ```
    swift list container_one
    ```
    {: pre}
    
9. container_two의 오브젝트를 나열하십시오. 파일의 이전 버전이 이 컨테이너에 저장됨을 확인할 수 있습니다. 

    ```
    swift list container_two
    ```
    {: pre}
    
10. container_one에서 오브젝트를 삭제하십시오. 오브젝트를 삭제하면 백업 컨테이너에 있는 이전 버전이 자동으로 기본 컨테이너로 이동합니다. 

    ```
    swift delete container_one object
    ```
    {: pre}
    
11. 두 컨테이너를 모두 나열하십시오. `container_one`에 원래 파일이 있고 `container_two`가 비어 있음을 확인할 수 있습니다. 

    ```
    swift list container_one
    swift list container_two
    ```
    {: pre}
