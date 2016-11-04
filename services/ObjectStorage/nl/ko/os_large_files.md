---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 대형 파일에 대한 작업 {: #large-files}
*마지막 업데이트 날짜: 2016년 10월 19일*
{: .last-updated}

오브젝트 업로드는 한 번의 업로드에서 최대 크기 5GB로 제한됩니다. 그러나 오브젝트를 작은 오브젝트로 세그먼트화하면 5GB보다 큰 오브젝트를 업로드할 수 있습니다. 세그먼트화된 오브젝트가 업로드되면 원래 오브젝트에 세그먼트를 병합하는 데 Manifest 파일도 필요합니다. 이를 수행하는 방법은 DLO(Dynamic Large Objects)와 SLO(Static Large Objects) 두 가지입니다.
{: shortdesc}

### DLO(Dynamic Large Objects): {: #dynamic}

다음 두 가지 방법으로 DLO를 처리할 수 있습니다. 
  * Swift 클라이언트가 자동으로 모든 작업을 처리하도록 함
  * Swift API를 사용하여 사용자가 직접 수행

#### Swift 클라이언트를 사용하여 DLO(Dynamic Large Objects) 처리

Swift 클라이언트에서는 `-segment-size` 매개변수를 사용하여 오브젝트를 작은 조각으로 분할합니다. 클라이언트는 파일을 업로드할 대상 컨테이너의 이름을 사용하여 새 컨테이너를 작성하고 세그먼트 번호(`<container_name>_segments`)로 접미부를 추가합니다. 세그먼트는 병렬로 업로드됩니다. 모든 세그먼트가 업로드되면 원래 파일 이름의 Manifest 파일에 하나의 병합된 오브젝트로 다운로드됩니다. 

1. {{site.data.keyword.Bluemix_notm}}에 로그인하고 업로드할 준비가 되면 다음 명령을 실행하여 파일을 세그먼트화하십시오. 

    ```
swift upload <container_name> <file_name> --segment-size <size_in_bytes>
```
    {: pre}

#### Swift API를 사용하여 DLO(Dynamic Large Objects) 처리

오브젝트가 5GB 이하가 되도록 오브젝트를 직접 세그먼트화한 후 Swift API를 통해 업로드할 수 있습니다. 업로드할 때 Manifest를 업로드하기 전에 모든 세그먼트를 업로드하는 것이 중요합니다. 모든 세그먼트 업로드가 완료되기 전에 오브젝트를 다운로드하면 다운로드된 오브젝트가 일치하지 않습니다. 다음 단계를 완료하여 대형 파일을 업로드할 수 있습니다. 

1. 원래 오브젝트를 이루도록 병합할 순서대로 세그먼트를 이름순으로 정렬하십시오. 
2. Manifest 파일을 보유하고 있는 컨테이너와 다른 컨테이너에 세그먼트를 업로드하십시오. 열 번째 세그먼트가 업로드된 후 업로드 조절이 시작되며 업로드 시간이 매우 증가합니다. 이와 같은 이유로 세그먼트 크기는 파일 크기를 10으로 나눈 값보다 작지 않은 것이 좋습니다. 

    ```
    curl -i -X PUT --data-binary @segment1 -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_name>/<object_name>/000001
    curl -i -X PUT --data-binary @segment2 -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_name>/<object_name>/000002
    ```
    {: pre}
    
3. 헤더 `X-Object-Manifest`를 해당 `<container>/prefix>` 값으로 설정하여 비어 있는 Manifest 파일을 업로드하십시오. 

    ```
    curl -i -X PUT -H "X-Auth-Token: <token>" -H "X-Object-Manifest: <container_name>/<object_name>/" https://<object-storage_url>/<manifest_container_name>/<object_name>
    ```
    {: pre}
    
    **참고**: Manifest 파일은 비어 있어야 합니다. 그렇지 않으면 파일의 컨텐츠를 세그먼트 중 하나로 간주하며 정렬된 이름의 제어를 받는 병합 순서로 정렬합니다.
4. 오브젝트를 다운로드하십시오. 다운로드 결과 전체 오브젝트를 받습니다. Manifest 파일을 업데이트하지 않아도 세그먼트를 추가하거나 제거할 수 있습니다. 올바른 접두부가 있는 세그먼트는 오브젝트의 일부로 남습니다. Manifest를 삭제해도 세그먼트는 삭제되지 않습니다. 

    ```
    curl -i -O -H "X-Auth-Token: <token>" https://<object-storage_url>/<manifest_container_name>/<object_name>
    ```
    {: pre}


### SLO(Static Large Objects) {: #static}

SLO(Static Large Objects)에서는 세그먼트와 Manifest 파일을 사용하지만 사용자에게 보다 많은 제어를 허용합니다. SLO를 사용하면 세그먼트가 동일한 컨테이너에 있지 않아도 되며 각 세그먼트를 임의의 컨테이너에 주어진 이름으로 저장할 수 있습니다. 그러나 세그먼트는 최소한 1MB여야 합니다. 올바른 Manifest가 업로드되면 헤더 “X-Static-Large-Object”가 자동으로 추가되고 true로 설정되지만 Manifest 파일의 헤더를 설정할 필요는 없습니다.
{: shortdesc}

Manifest 파일은 세그먼트의 세부사항을 제공하는 JSON 문서이며 모든 세그먼트가 업로드된 후 업로드되어야 합니다. Manifest의 각 세그먼트에서 사용할 수 있도록 제공되는 데이터를 실제 세그먼트의 메타데이터와 비교합니다. 일치하지 않는 항목이 있는 경우 Manifest가 업로드되지 않습니다. 

<table>
  <tr>
    <th> 속성 </th>
    <th> 설명 </th>
  </tr>
  <tr>
    <td> path </td>
    <td> 세그먼트의 위치와 이름입니다. container_name/object_name으로 지정됩니다. </td>
  </tr>
  <tr>
    <td> etag </td>
    <td> 오브젝트가 업로드되는 경우 PUT 요청에서 제공합니다. 오브젝트에 대한 HEAD를 수행하여 찾을 수도 있습니다. </td>
  </tr>
  <tr>
    <td> size_bytes </td>
    <td> 오브젝트 크기(바이트)입니다. </td>
  </tr>
</table>

*표 1: 병합 순서로 정렬된 Manifest 파일의 JSON 속성*

다음 단계를 완료하여 대형 파일을 업로드할 수 있습니다. 

1. 다음 명령을 실행하여 세그먼트를 업로드하십시오. 열 번째 세그먼트가 업로드된 후 업로드 조절이 시작되며 업로드 시간이 매우 증가합니다. 이와 같은 이유로 세그먼트 크기는 파일 크기를 10으로 나눈 값보다 작지 않은 것이 좋습니다. 

    ```
    curl -i -X PUT --data-binary @segment1 -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_one>/<segment>
    curl -i -X PUT --data-binary @segment2 -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_two>/<segment>
    curl -i -X PUT --data-binary @segment3 -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_one>/<segment>
    ```
    {: pre}
    
2. 다음과 같이 Manifest를 빌드하십시오. 

    ```
    [
        {
            "path": "<container_one>/<segment>",
            "etag": "e0ed3b751eb8d4b2c648d2dd78576e36",
            "size_bytes": 801882690
        },
        {
            "path": "container_two/<segment>",
            "etag": "65a301e71c82cbd325a5efe5877e1a24",
            "size_bytes": 1048576
        },
        {
            "path": "<container_one>/<segment>",
            "etag": "aea8b7462d527ad5ed0cfc22ea161062",
            "size_bytes": 138257
        }
    ]
    ```
    {: pre}
    
3. Manifest를 업로드하십시오. 이를 수행하려면 다음 명령을 실행하여 조회 `multipart-manifest=put`을 Manifest 이름에 추가해야 합니다. 

    ```
    curl -i -X PUT --data-binary @object_name -H "X-Auth-Token: <token>" https://<object-storage_url>/container_two/<object_name>?multipart-manifest=put
    ```
    {: pre}
    
4. 오브젝트를 다운로드하십시오. 

    ```
    curl -O -X GET -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_two>/<object_name>
    ```
    {: pre}
    
다음은 SLO(Static Large Objects)에 대한 작업 수행 시 필요한 몇몇 명령입니다. 

* Manifest 파일의 컨텐츠를 다운로드하려면 조회 `multipart-manifest=get`을 명령에 추가해야 합니다. 사용자가 받는 컨텐츠는 업로드한 컨텐츠와 동일하지 않습니다. 

    ```
    curl -O -X GET -H "X-Auth-Token:<token>" https://<object-storage_url>/<container_two>/<object_name>?multipart-manifest=get
    ```
    {: pre}
    
* Manifest를 삭제하려면 다음 명령을 실행하십시오. 

    ```
    curl -i -X DELETE -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_two>/<object_name>
    ```
    {: pre}
    
* Manifest와 모든 세그먼트를 삭제하려면 조회 `multipart-manifest=delete`를 Manifest 이름 뒤에 추가하십시오. 

    ```
    curl -i -X DELETE -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_two>/<object_name>?multipart-manifest=delete
    ```
    {: pre}

**참고**: 오브젝트에 세그먼트를 추가하거나 오브젝트에서 세그먼트를 제거하려면 새 세그먼트 목록이 있는 새 Manifest 파일을 업로드해야 합니다. Manifest 이름을 동일하게 유지할 수 있습니다. 
