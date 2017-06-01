---

copyright:
  years: 2017
lastupdated: "2017-05-16"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 임시 환경에서 리소스 영구 삭제
{: #destroying}

{{site.data.keyword.bplong}}를 사용하여 리소스를 영구 삭제할 수 있습니다. 리소스를 영구 삭제하면 환경과 모든 관련 리소스가 해체됩니다.  
{:shortdesc}

**경고**: 리소스를 영구 삭제하면 조치를 되돌릴 수 없습니다. 프로덕션 환경에서는 리소스를 영구 삭제하는 것을 권장하지 않습니다. 리소스 영구 삭제는 테스트나 QA와 같은 임시 환경에서 유용할 수 있습니다.

리소스를 영구 삭제하기 전에 다음 가이드라인을 고려하십시오. 
* 트래픽이 리소스로 향하지 않게 하십시오.
* 필요할 수 있는 모든 데이터가 백업되었는지 확인하십시오. 


## GUI를 사용하여 리소스 영구 삭제
{: #gui}

{{site.data.keyword.bpshort}} 대시보드를 사용하여 임시 환경을 작성하고 해체할 수 있습니다.
{:shortdesc}

1. **{{site.data.keyword.bpshort}}** 대시보드에서 **환경** 탭을 선택하십시오.

2. 제거할 특정 환경의 행을 클릭하십시오. 

3. 옵션 메뉴에서 **리소스 영구 삭제** 또는 **환경 삭제**를 선택하십시오. 삭제 및 영구 삭제 조치는 모두 되돌릴 수 없습니다. 활성 리소스가 있는지 여부에 따라 어느 옵션을 선택할지 결정하십시오.
  * 활성 리소스를 중지하고 제거하려면 **리소스 영구 삭제**를 선택하십시오. 영구 삭제 전에 플랜을 실행하여 환경과 연관된 리소스를 제거해도 괜찮은지 확인하는 것이 좋습니다.
  * {{site.data.keyword.bpshort}} 서비스에서 환경 구성을 제거하려면 **환경 삭제**를 선택하십시오. 일반적으로 이 옵션은 환경이 배치되지 않았으며 활성 리소스가 없는 경우 사용됩니다. 활성 리소스에 대해 이 옵션을 선택하면 더 이상 {{site.data.keyword.bpshort}} 서비스를 사용하여 환경에 변경사항을 배치하거나 추적할 수 없습니다. 활성 리소스는 해당 서비스 대시보드에서 개별적으로 관리해야 합니다.
  
  화면에 표시되는 프롬프트를 따라 선택사항을 확인하십시오. 


## CLI를 사용하여 리소스 영구 삭제
{: #cli}

{{site.data.keyword.bpshort}} CLI를 사용하여 임시 환경을 작성하고 해체할 수 있습니다.
{:shortdesc}

1. `destroy` 명령을 실행하여 환경과 리소스를 해체하십시오.

  ```
  bx schematics action destroy --id ENVIRONMENT_ID
  ```
  {: codeblock}
  
2. 선택사항: 서비스에서 구성을 제거하려면 `delete` 명령을 실행하십시오.

  ```
  bx schematics environment delete --id ENVIRONMENT_ID
  ```
  {: codeblock}


## API를 사용하여 리소스 영구 삭제
{: #api}

{{site.data.keyword.bpshort}} API를 사용하여 임시 환경을 작성하고 해체할 수 있습니다.
{:shortdesc}

1. `PUT v1/environments/<environment_ID>/destroy` 호출을 실행하여 리소스를 영구 삭제하십시오.

  ```
  curl -X PUT \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/destroy \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>' \
    -H 'content-type: application/json'
  ```
  {: codeblock}

2. 선택사항: {{site.data.keyword.bpshort}} 서비스에서 구성을 제거하려면 `DELETE v1/environments/<environment_ID>` 호출을 실행하십시오.

  ```
  curl -X DELETE \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID> \
    -H 'accept: text/plain' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}
