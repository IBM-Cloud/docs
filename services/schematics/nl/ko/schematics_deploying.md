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

# 환경에 리소스 배치
{: #deploying}

{{site.data.keyword.bplong}}를 사용하여 소스 코드에서 직접 최신 코드 변경사항을 배치할 수 있습니다. 환경을 배치할 때는 구성 파일을 통해 정의한 리소스를 배치합니다. 그런 다음 {{site.data.keyword.bpshort}}에서 환경의 라이프사이클, 오케스트레이션 및 프로비저닝을 관리할 수 있습니다.
{:shortdesc}

## GUI를 사용하여 환경에 배치
{: #gui}

그래픽 보기를 사용하여 환경을 배치하려는 경우에는 {{site.data.keyword.bpshort}} 대시보드를 사용할 수 있습니다.
{:shortdesc}


### 전제조건
{: #gui-prereq}

* Terraform 구성을 소스 제어에 저장하십시오. 구성은 HCL(HashiCorp Configuration Language) 또는 JSON 구문으로 작성할 수 있습니다. HCL 구문 및 구성 작성 방법에 관한 가이드라인은 <a href="https://www.terraform.io/docs/configuration/index.html">Terraform 구성 문서 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 참조하십시오. 사용 가능한 리소스는 <a href="https://ibm-bluemix.github.io/tf-ibm-docs/">{{site.data.keyword.IBM_notm}} 클라우드 제공자 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 참조하십시오. 

구성을 저장한 후 다음을 수행하십시오.

1. **{{site.data.keyword.bpshort}}** 대시보드에서 **환경**을 선택하십시오.

2. **환경 작성**을 클릭하여 환경을 추가하거나 배치하려는 기존 환경이 있는 행을 선택하십시오.

3. **플랜**을 클릭하여 환경을 배치할 때 프로비저닝되는 리소스를 미리볼 수 있습니다. 플랜을 실행할 때 {{site.data.keyword.bpshort}}에서는 소스 제어에서 최신 버전의 구성과 환경 세부사항의 변수를 추출합니다. 플랜 출력에서는 Terraform 상태 파일에 따라 배치된 내용과 구성을 비교합니다. 플랜이 환경에 적용되거나 플랜이 취소되기 전에는 환경이 잠겨 환경을 변경할 수 없습니다. 

4. **최근 활동** 섹션에서 로그를 보고 플랜 출력을 검사하십시오. 플랜 출력에서는 오류 존재 여부와 서비스에서 작성, 변경 또는 영구 삭제하려는 리소스를 보여줍니다.

5. 플랜을 시작할 준비가 되면 **적용**을 클릭하십시오. 활동 로그를 모니터하여 가장 최근의 실행에서 플랜이 성공적으로 적용되었는지 확인할 수 있습니다. 


## CLI를 사용하여 환경에 배치
{: #cli}

{{site.data.keyword.Bluemix_notm}} CLI용 {{site.data.keyword.bpshort}} 플러그인을 사용하여 환경에 업데이트를 배치할 수 있습니다.
{:shortdesc}

### 전제조건
{: #cli-prereq}

* Terraform 구성을 소스 제어에 저장하십시오. 
* 아직 수행하지 않은 경우 [{{site.data.keyword.Bluemix_notm}} CLI 저장소](http://clis.ng.bluemix.net/ui/home.html)에서 운영 체제에 적합한 {{site.data.keyword.Bluemix_notm}} CLI를 설치하십시오.

{{site.data.keyword.Bluemix_notm}} CLI에 로그인한 후 다음을 수행하십시오.

1. 다음 명령을 실행하여 {{site.data.keyword.bpshort}} CLI 플러그인을 설치하십시오.
  
  ```
  bx plugin install schematics -r Bluemix
  ```
  {: codeblock}

  설치에 성공하면 {{site.data.keyword.bpshort}} 플러그인이 `bx plugin list`에 표시됩니다. 

2. 구성에서 환경을 작성하십시오. 환경을 작성할 때 최신 코드를 추출할 수 있도록 서비스가 소스 제어를 가리키게 합니다. 
  
  ```
  bx schematics environment create --file FILE_NAME
  ```
  {: codeblock}
  
  <table summary="environment create 명령 설명">
  <caption>표 1. environment create 명령 설명.
  </caption>
  <thead>
  <th colspan="1">명령</th>
  <th colspan="1">수행 사항</th>
  </thead>
  <tbody>
  <tr>
  <td>--file FILE_NAME</td>
  <td>환경에 대한 세부사항이 저장된 JSON 파일.
  <p>
  <p>예제 JSON:
  <pre>{
      "description": "(Optional) Description of the environment",
      "frozen": false,
      "name": "Name of the environment",
      "sourceurl": "The GitHub URL that points to the Terraform configuration",
      "tags": ["(Optional) metadata_tag_1", "(Optional) metadata_tag_2"],
      "terraformversion": "0.9",
      "variablestore": [{
          "name": "(Optional) variable_1",
          "secure": false,
          "value": "Visible value"
      },
      {
          "name": "(Optional) variable_2_secret",
          "secure": true,
          "value": "Secured value"
      }]
  }</pre>
  </td>
  </tr>
  </tbody></table>
  
  리턴된 `ID` 값을 기록해 두십시오. `ID`는 환경에 지정되어 후속 명령에 사용되는 고유 ID입니다.
  
3. `plan` 명령을 실행하여 환경이 어떻게 변경되는지 미리보십시오. plan 명령은 배치된 사항과 비교하여 어떤 리소스가 얼마나 변경될지 보여주지만, 해당 변경사항은 `apply` 명령을 실행하기 전에는 적용되지 않습니다.
  
  ```
  bx schematics action plan --id ENVIRONMENT_ID
  ```
  {: codeblock}
  
  <table summary="plan 명령 설명">
  <caption>표 2. plan 명령 실행.
  </caption>
  <thead>
  <th colspan="1">명령</th>
  <th colspan="1">수행 사항</th>
  </thead>
  <tbody>
  <tr>
  <td>--id ENVIRONMENT_ID</td>
  <td>실행 플랜을 실행할 특정 환경입니다. 환경 ID의 값을 검색해야 하는 경우 <code>bx schematics list</code>를 실행할 수 있습니다.
  </td>
  </tbody></table>
  
  `activity_id`가 플랜에 지정되고 활동 로그에 기록됩니다. 

4. Terraform 플랜 출력을 보려면 활동 로그를 검색하십시오.

  ```
  bx schematics activity log --id ACTIVITY_ID
  ```
  {: codeblock}

  <table summary="log 명령 설명">
  <caption>표 3. log 명령 설명.
  </caption>
  <thead>
  <th colspan="1">명령</th>
  <th colspan="1">수행 사항</th>
  </thead>
  <tbody>
  <tr>
  <td>--id ACTIVITY_ID</td>
  <td>로그를 보려는 특정 활동입니다. 활동 ID의 값을 검색해야 하는 경우 <code>bx schematics activity list --id ENVIRONMENT_ID</code>를 실행할 수 있습니다.
  </td>
  </tbody></table>
  
5. `apply` 명령을 실행하여 환경에 리소스를 배치하십시오.
  
  ```
  bx schematics action apply --id ENVIRONMENT_ID
  ```
  {: codeblock}
  
  <table summary="apply 명령 설명">
  <caption>표 4. apply 명령 설명.
  </caption>
  <thead>
  <th colspan="1">명령</th>
  <th colspan="1">수행 사항</th>
  </thead>
  <tbody>
  <tr>
  <td>--id ENVIRONMENT_ID</td>
  <td>업데이트를 배치하려는 특정 환경입니다. 환경 ID의 값을 검색해야 하는 경우 <code>bx schematics list</code>를 실행할 수 있습니다.
  </td>
  </tbody></table>
  
6. 배치가 성공적인지 확인하기 위해 적용 출력을 모니터하십시오. 

  ```
  bx schematics activity log --id ACTIVITY_ID
  ```
  {: codeblock}

  배치에 성공하면 출력의 끝에 다음 행이 리턴됩니다.
  
  ```
  Apply complete! Resources: N added, N changed, N destroyed.
  ```
  {: screen}
  
## API를 사용하여 환경에 배치
{: #api}

{{site.data.keyword.bpshort}} API를 사용하여 프로그래밍 방식으로 환경을 배치할 수 있습니다.
{:shortdesc}

<a href="https://us-south.schematics.bluemix.net/swagger-api/">{{site.data.keyword.bpshort}} API <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>에 대한 호출은 다음 기본 엔드포인트를 가리킵니다.

```
https://us-south.schematics.bluemix.net
```
{: codeblock}

### 전제조건
{: #api-prereq}

* Terraform 구성을 소스 제어에 저장하십시오. 

다음 단계를 완료하여 환경에 리소스를 배치하십시오.

1. 인증 헤더에서 사용할 IAM OAuth 토큰을 생성하십시오. 명령을 수행하면 UAA 토큰과 IAM 토큰을 출력합니다.
  
  ```
  bx iam oauth-tokens
  ```
  {: codeblock}
  
  예제 출력:
  ```
  IAM token:  Bearer eyJraWQ...
  ```
  {: screen}
    
  `Bearer eyJraWQ...` 출력은 IAM 토큰의 예이며, 일부가 생략되어 있습니다. API 호출 헤더에 전체 토큰을 포함시키십시오.
  
2. `POST v1/environments` 호출을 실행하여 환경을 작성하십시오.

  ```
  curl -X POST \
    https://us-south.schematics.bluemix.net/v1/environments \
    -H 'accept: text/plain' \
    -H 'authorization: bearer <IAM_token>' \
    -H 'content-type: application/json' \
    -d '{
    "description": "(Optional) Description of the environment",
    "frozen": false,
    "name": "Name of the environment",
    "sourceurl": "The GitHub URL that points to the Terraform configuration",
    "tags": [
      "(Optional) metadata_tag_1",
      "(Optional) metadata_tag_2"
    ],
    "terraformversion": "0.9",
    "variablestore": [{
        "name": "(Optional) variable_1",
        "secure": false,
        "value": "Visible value"
    },
    {
        "name": "(Optional) variable_2_secret",
        "secure": true,
        "value": "Secured value"
    }]
  }'
  ```
  {: codeblock}
    
  문제가 없을 경우 응답에서 다음 출력을 리턴합니다.
  ```
  {
    "id": "Environment ID",
    "name": "Environment name",
    "description": "Description of the environment",
    "account": "{{site.data.keyword.Bluemix_notm}} account GUID",
    "owner": "The IBMid of the user who created the environment",
    "creationtime": "YYYY-MM-DDTHH:MM:SSZ",
    "status": "CREATED",
    "frozen": false,
    "sourceurl": "The GitHub URL that points to the configuration",
    "statefile": "The reference to the Terraform state file",
    "terraformversion": "0.9",
    "tags": [
      "metadata_tag_1",
      "metadata_tag_2"
    ],
    "variablestore": [
      {
        "name": "(Optional) variable_1",
        "value": "Visible value"
      }
    ]
  }
  ```
  {: screen}
    
  리턴된 `id` 값을 기록해 두십시오. `id`는 환경에 지정되어 후속 호출에 사용되는 고유 ID입니다.
  
3. 구성을 적용할 때 환경에 배치되는 리소스를 미리보려면 `POST v1/environments/<environment_ID>/plan` 호출을 실행하십시오. 플랜은 저장소의 마스터 분기에서 환경 구성을 추출합니다.
  
  ```
  curl -X POST \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/plan \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>' \
    -H 'content-type: application/json'
  ```
  {: codeblock}
  
  문제가 없을 경우 응답에서 `activityid`를 리턴합니다. 활동 ID 값은 플랜 및 적용 출력 등의 로그를 보는 데 필요합니다.
  ```
  {
    "activityid": "<activity_ID>"
  }
  ```
  {: screen}

4. `GET v1/environments/<environment_ID>/activities/<activity_ID>/log` 호출을 실행하여 플랜 출력을 보십시오.

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/activities/<activity_ID>/log \
    -H 'accept: text/html' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}

5. `PUT v1/environments/<environment_ID>/apply/` 호출을 실행하여 환경을 배치하십시오.
  
  ```
  curl -X PUT \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/apply \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>' \
    -H 'content-type: application/json'
  ```
  {: codeblock}
  
6. 적용 출력을 보기 위해 `GET v1/environments/<environment_ID>/activities/<activity_ID>/log` 호출을 실행하여 배치를 모니터하십시오.

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/activities/<activity_ID>/log \
    -H 'accept: text/html' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}

  배치에 성공하면 출력의 끝에 다음 행이 리턴됩니다.
  
  ```
  Apply complete! Resources: N added, N changed, N destroyed.
  ```
  {: screen}
