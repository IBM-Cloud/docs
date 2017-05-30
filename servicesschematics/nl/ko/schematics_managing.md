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

# 환경의 리소스 관리
{: #managing}

{{site.data.keyword.bplong}}에서는 환경 관리가 간소화됩니다. 필요할 때마다 배치된 리소스를 수정하고 변경사항을 반복하여 재배치할 수 있습니다.

{:shortdesc}

환경에 대한 변경사항을 경량 프로세스를 통해 재배치할 수 있습니다. 할당된 리소스를 변경하려는 경우 선언 구문으로 원하는 출력만을 명시하여 구성 변경사항을 코딩합니다. {{site.data.keyword.bpshort}}에서는 배치하기 전에 변경사항을 미리볼 수 있습니다.


## GUI를 사용하여 리소스 업데이트
{: #gui}

그래픽 보기를 사용하여 환경의 리소스를 관리하려는 경우에는 {{site.data.keyword.bpshort}} 대시보드를 사용할 수 있습니다.
{:shortdesc}

GitHub에서 구성에 대한 코드 변경사항을 공개하거나 GUI에서 변수를 수정한 후, 다음 단계를 완료하여 환경에 업데이트를 배치하십시오.

1. **{{site.data.keyword.bpshort}}** 대시보드에서 **환경**을 선택하십시오.

2. 업데이트하려는 특정 환경의 행을 클릭하십시오.

3. **플랜**을 클릭하고 플랜 로그에서 오류를 검사하십시오. 사용자나 {{site.data.keyword.Bluemix_notm}} 계정의 다른 협업자가 플랜을 적용하거나 취소할 때까지 환경이 잠깁니다. 

4. **적용**을 클릭하여 업데이트를 배치하십시오. 


## CLI를 사용하여 리소스 업데이트
{: #cli}

{{site.data.keyword.bpshort}} CLI를 사용하여 프로그래밍 방식으로 환경의 리소스를 업데이트할 수 있습니다.
{:shortdesc}

GitHub에서 구성에 대한 코드 변경사항을 공개한 후, 다음 단계를 완료하여 환경에 업데이트를 배치하십시오.

1. `plan` 명령을 실행하십시오. {{site.data.keyword.bpshort}} CLI가 GitHub에서 업데이트된 환경 구성을 가져온 후, 리소스와 현재 배치 사이의 차이점을 보여주는 미리보기를 출력합니다.

  ```
  bx schematics action plan --id ENVIRONMENT_ID
  ```
  {: codeblock}

2. 활동 로그에서 플랜 출력을 확인하십시오.

  ```
  bx schematics activity log --id ACTIVITY_ID
  ```
  {: codeblock}

3. `apply` 명령을 실행하여 플랜을 배치하십시오. 

  ```
  bx schematics action apply --id ENVIRONMENT_ID
  ```
  {: codeblock}


## API를 사용하여 리소스 업데이트
{: #api}

{{site.data.keyword.bpshort}} API를 사용하여 프로그래밍 방식으로 환경의 리소스를 관리할 수 있습니다.
{:shortdesc}

GitHub에서 구성에 대한 코드 변경사항을 공개한 후, 다음 단계를 완료하여 환경에 업데이트를 배치하십시오.

1. `POST v1/environments/<environment_ID>/plan` 호출을 실행하십시오. {{site.data.keyword.bpshort}} API가 GitHub에서 업데이트된 환경 구성을 가져온 후, 이를 Terraform 상태 파일과 비교하여 리소스와 현재 배치 사이의 차이점을 표시합니다.

  ```
  curl -X POST \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/plan \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>' \
    -H 'content-type: application/json'
  ```
  {: codeblock}

  예제 응답:
  ```
  {
    "activityid": "<activity_ID>"
  }
  ```
  {: screen}

2. 활동 로그에서 플랜 출력을 확인하십시오.

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/activities/<activity_ID>/log \
    -H 'accept: text/html' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}

3. `PUT /v1/environments/<environment_ID>/apply` 호출을 실행하여 플랜을 배치하십시오. 

  ```
  curl -X PUT \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/apply \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>' \
    -H 'content-type: application/json' \
  ```
  {: codeblock}


## 환경에 대한 변경사항 감사
{: #auditing}

소스 제어 저장소의 버전 히스토리에서 구성을 감사할 수 있습니다. {{site.data.keyword.bpshort}}에서는 환경에 대한 배치를 모니터하거나 이전 배치와 관련된 로그를 볼 수 있도록 감사 로그를 확인하는 다음과 같은 옵션을 제공합니다.

### {{site.data.keyword.bpshort}} 대시보드
{: #auditing-gui}

1. 환경의 행을 선택하여 환경 세부사항 페이지에 액세스하십시오.

2. **최근 활동** 섹션을 모니터하십시오. 이전 플랜 및 배치의 히스토리 로그도 볼 수 있습니다.

### {{site.data.keyword.bpshort}} CLI
{: #auditing-cli}

1. 환경 ID를 검색하십시오.

  ```
  bx schematics environment list
  ```
  {: codeblock}

2. 환경의 활동 ID를 검색하십시오. 활동 ID는 계획, 적용, 영구 삭제 및 삭제 조치에 지정됩니다. 다음 명령은 환경에서 실행되는 모든 활동을 나열합니다.

  ```
  bx schematics activity list --id ENVIRONMENT_ID
  ```
  {: codeblock}

3. 누가, 언제 환경을 변경했는지와 같은 특정 활동에 대한 데이터를 검색하십시오.

  ```
  bx schematics activity show --id ACTIVITY_ID
  ```
  {: codeblock}

4. 선택사항: 플랜 또는 적용 출력 등의 자세한 로그를 보려면 `log` 명령을 실행하십시오. 

  ```
  bx schematics activity log --id ACTIVITY_ID
  ```
  {: codeblock}

### {{site.data.keyword.bpshort}} API
{: #auditing-api}

1. 환경 ID를 검색하십시오.

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}
  
  응답 본문에는 {{site.data.keyword.Bluemix_notm}} 계정의 모든 환경이 포함됩니다. 감사하려는 특정 환경의 `id` 값을 찾으십시오.

2. 환경에 대해 실행할 조치의 활동 ID를 검색하십시오.

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/activities \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}

3. 환경의 특정 활동을 가져오십시오. 

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/activities/<activity_ID> \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}

4. Terraform 출력의 자세한 로그를 검사하십시오.

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/activities/<activity_ID>/log \
    -H 'accept: text/html' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}
