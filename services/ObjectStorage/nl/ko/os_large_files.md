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


# 대형 오브젝트 저장 {: #large-files}

오브젝트 업로드는 한 번의 업로드에서 최대 크기 5GB로 제한됩니다. 그러나 더 큰 오브젝트를 작은 부분으로 세그먼트화하고 Manifest 파일을 사용하여 세그먼트를 연결할 수 있습니다. 오브젝트가 연결되면 최대 크기는 적용되지 않습니다.
{: shortdesc}

대형 오브젝트는 동적 또는 정적일 수 있습니다. 정적 대형 오브젝트(SLO)에서 세그먼트는 동일한 컨테이너에 있을 필요가 없습니다. 각 세그먼트는 임의의 컨테이너에 저장될 수 있으며 임의의 이름이 부여될 수 있습니다. 동적 대형 오브젝트에서 Swift 클라이언트는 컨테이너를 작성하며 번호 지정된 세그먼트는 컨테이너에 병렬로 업로드됩니다. 


## 동적 대형 오브젝트: {: #dynamic}

두 가지 방법으로 동적 대형 오브젝트를 업로드할 수 있습니다. 
  * Swift 클라이언트가 자동으로 모든 작업을 처리하도록 함
  * Swift API를 사용하여 사용자가 직접 수행

#### Swift 클라이언트를 사용하여 동적 대형 오브젝트 처리

Swift 클라이언트에서는 `-segment-size` 매개변수를 사용하여 오브젝트를 작은 조각으로 분할합니다. 클라이언트는 파일을 업로드할 대상 컨테이너의 이름을 사용하여 새 컨테이너를 작성하고 세그먼트 번호(`<container_name>_segments`)로 접미부를 추가합니다. 세그먼트는 병렬로 업로드됩니다. 모든 세그먼트가 업로드되면 원래 파일 이름의 Manifest 파일에 하나의 병합된 오브젝트로 다운로드됩니다. 

1. {{site.data.keyword.Bluemix_notm}}에 로그인하고 업로드할 준비가 되면 다음 명령을 실행하여 파일을 세그먼트화하십시오. 
    ```
swift upload <container_name> <file_name> --segment-size <size_in_bytes>
```
    {: pre}

#### Swift API를 사용하여 DLO(Dynamic Large Objects) 처리

오브젝트가 5GB 이하가 되도록 오브젝트를 직접 세그먼트화한 후 Swift API를 통해 업로드할 수 있습니다. 

**참고**: 업로드 시에 모든 세그먼트는 Manifest 파일 전에 업로드되어야 합니다. 모든 세그먼트가 업로드되기 전에 오브젝트가 다운로드된 경우, 다운로드된 오브젝트는 일관성 없이 연결됩니다. 

다음 단계를 완료하여 대형 파일을 업로드할 수 있습니다. 

1. 원래 오브젝트를 작성하기 위해 연결이 필요한 순서대로 이름별로 정렬하십시오. 
2. Manifest 파일을 보유하고 있는 컨테이너와 다른 컨테이너에 세그먼트를 업로드하십시오. 업로드에 대한 조절은 10번째 세그먼트가 업로드된 후에 시작되며, 업로드 시간을 상당히 늘립니다.   

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

    **참고**: Manifest 파일은 비어 있어야 합니다. 그렇지 않으면, 파일의 컨텐츠가 세그먼트 중 하나로 간주되며 정렬된 이름의 제어를 받는 연결의 순서로 정렬됩니다.
4. 오브젝트를 다운로드하십시오. 그 결과로 전체 오브젝트를 수신합니다. Manifest 파일을 업데이트하지 않아도 세그먼트를 추가하거나 제거할 수 있습니다. 올바른 접두부의 세그먼트는 오브젝트의 일부로 남습니다. Manifest를 삭제해도 세그먼트는 삭제되지 않습니다. 

    ```
    curl -i -O -H "X-Auth-Token: <token>" https://<object-storage_url>/<manifest_container_name>/<object_name>
    ```
    {: pre}


## 정적 대형 오브젝트 {: #static}

정적 대형 오브젝트는 세그먼트와 Manifest 파일을 사용하지만 사용자에게 보다 많은 제어를 허용합니다. SLO에서는 세그먼트가 동일한 컨테이너에 있을 필요가 없습니다. 각 세그먼트는 임의의 컨테이너에 저장될 수 있으며 임의의 이름이 부여될 수 있습니다. 그러나 세그먼트는 최소한 1MB여야 합니다. Manifest 파일의 헤더를 설정할 필요는 없지만, 올바른 Manifest가 업로드되면 헤더 “X-Static-Large-Object”가 자동으로 추가되고 true로 설정됩니다.
{: shortdesc}

Manifest 파일은 세그먼트의 세부사항을 제공하는 JSON 문서이며 모든 세그먼트가 업로드된 후 업로드되어야 합니다. Manifest의 각 세그먼트에 대해 제공되는 데이터는 실제 세그먼트의 메타데이터와 비교됩니다. 일치하지 않는 항목이 있는 경우에는 Manifest가 업로드되지 않습니다. 

<table>
<caption> 표.1 Manifest 파일의 JSON 속성 </caption>
  <tr>
    <th> 속성 </th>
    <th> 설명 </th>
  </tr>
  <tr>
    <td> <i> path </i> </td>
    <td> 세그먼트의 위치와 이름입니다. container_name/object_name으로 지정됩니다. </td>
  </tr>
  <tr>
    <td> <i> etag </i> </td>
    <td> 오브젝트가 업로드되는 경우 PUT 요청에서 제공합니다. 오브젝트에 대한 HEAD를 수행하여 찾을 수도 있습니다. </td>
  </tr>
  <tr>
    <td> <i> size_bytes </i> </td>
    <td> 오브젝트 크기(바이트)입니다. </td>
  </tr>
</table>



#### 대형 파일 업로드 방법

1. 다음 명령을 실행하여 세그먼트를 업로드하십시오. 업로드에 대한 조절은 10번째 세그먼트가 업로드된 후에 시작되며, 업로드 시간을 상당히 늘립니다.   

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

3. Manifest 이름에 조회 `multipart-manifest=put`을 추가하여 Manifest 파일을 업로드하십시오. 

    ```
    curl -i -X PUT --data-binary @object_name -H "X-Auth-Token: <token>" https://<object-storage_url>/container_two/<object_name>?multipart-manifest=put
    ```
    {: pre}

4. 오브젝트를 다운로드하십시오. 

    ```
    curl -O -X GET -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_two>/<object_name>
    ```
    {: pre}


#### 정적 대형 오브젝트 관련 작업 

다음 명령을 사용하여 파일을 관리할 수 있습니다. 

**참고**: 오브젝트에 대해 세그먼트를 추가하거나 제거하려면 세그먼트의 새 목록이 있는 새 Manifest 파일을 업로드하십시오. Manifest 이름을 동일하게 유지할 수 있습니다. 

* Manifest 파일의 컨텐츠를 다운로드하려면 조회 `multipart-manifest=get`을 명령에 추가해야 합니다. 사용자가 수신하는 컨텐츠는 업로드한 컨텐츠와 동일하지 않습니다. 

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
