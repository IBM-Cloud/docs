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

# {{site.data.keyword.Bluemix_notm}} CLI용 {{site.data.keyword.bpshort}} CLI 플러그인
{: #cli}

{{site.data.keyword.Bluemix}} CLI용 {{site.data.keyword.bpshort}} 명령을 참조하여 환경을 관리하고 {{site.data.keyword.Bluemix_notm}}에서 다른 오퍼레이션을 수행하십시오.
{: shortdesc}

CLI 명령을 사용하기 전에 다음을 수행하십시오.

* `bx login [--sso]`로 {{site.data.keyword.Bluemix_notm}}에 로그인하여 세션을 인증하십시오. 연합 ID를 사용하는 사용자의 경우 `--sso` 플래그를 사용하여 일회성 패스코드를 생성해야 합니다.

`bx schematics help`를 실행하여 명령 목록을 볼 수 있습니다.

<table id="manage_environments" summary="bx schematics environment 명령으로 환경 관리.">
<caption>표 1. 환경을 관리하는 데 사용 가능한 명령. 명령은 <code>bx schematics environment</code> 구문을 따름.
</caption>
 <thead>
 <th colspan="5">환경 관리</th>
 </thead>
 <tbody>
 <tr>
 <td>[bx schematics environment create](#environment-create)</td>
 <td>[bx schematics environment delete](#environment-delete)</td>
 <td>[bx schematics environment list](#environment-list)</td>
 <td>[bx schematics environment show](#environment-show)</td>
 <td>[bx schematics environment update](#environment-update)</td>
 </tr>
</tbody></table>
 
 <table id="update_resources" summary="환경에서 프로비저닝한 리소스를 bx schematics action 명령으로 업데이트.">
 <caption>표 2. 환경의 리소스를 업데이트하는 데 사용 가능한 명령. 명령은 <code>bx schematics action</code> 구문을 따름.
 </caption>
  <thead>
  <th colspan="5">리소스 업데이트</th>
  </thead>
  <tbody>
  <td>[bx schematics action apply](#action-apply)</td>
  <td>[bx schematics action destroy](#action-destroy)</td>
  <td>[bx schematics action plan](#action-plan)</td>
  </tr></tbody></table>
  
  <table id="audit_environment" summary="bx schematics activity 명령으로 환경에서 실행한 활동 감사.">
  <caption>표 3. 환경에서 실행한 활동을 감사하는 데 사용 가능한 명령. 명령은 <code>bx schematics activity</code> 구문을 따름.
  </caption>
   <thead>
   <th colspan="5">환경 감사</th>
   </thead>
   <tbody>
   <td>[bx schematics activity list](#activity-list)</td>
   <td>[bx schematics activity log](#activity-log)</td>
   <td>[bx schematics activity planfile](#activity-planfile)</td>
   <td>[bx schematics activity show](#activity-show)</td>
   </tr></tbody></table>

## bx schematics environment create
{: #environment-create notoc}

구성에서 {{site.data.keyword.Bluemix_notm}}에 환경을 작성합니다.

```
bx schematics environment create --file FILE_NAME [--json]
```
{: codeblock}

### 매개변수

<dl>
<dt>--file FILE_NAME</dt>
<dd>환경에 대한 세부사항을 전달하는 데 사용하는 JSON 파일입니다.
<p>
<p>사용 가능한 모든 값이 있는 예제 JSON:
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
}</pre></dd>
<dt>--json</dt>
<dd>JSON 형식으로 출력을 인쇄합니다.</dd>
</dl>

## bx schematics environment delete
{: #environment-delete notoc}

{{site.data.keyword.Bluemix_notm}}에서 환경 구성을 제거합니다. 이 명령은 실행 중인 리소스가 없는 환경에서만 사용하는 것이 좋습니다. 실행 중인 리소스가 있는 환경을 삭제하는 경우, 개별 서비스 대시보드에서 각 리소스를 관리해야 합니다.

```
bx schematics environment delete --id ENVIRONMENT_ID [--force]
```
{: codeblock}

### 매개변수

<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>환경의 고유 ID입니다. <code>bx schematics environment list</code>를 실행하여 이 값을 검색할 수 있습니다.</dd>
<dt>--force</dt>
<dd>예/아니오 확인 없이 명령을 강제로 진행합니다.</dd>
</dl>

## bx schematics environment list
{: #environment-list notoc}

{{site.data.keyword.Bluemix_notm}} 계정에 있는 모든 기존 환경 목록을 검색합니다.

```
bx schematics environment list [--count VALUE] [--offset VALUE] [--json] 
```
{: codeblock}

### 매개변수
<dl>
<dt>--count VALUE</dt>
<dd>리턴에서 제한할 환경 수입니다.</dd>
<dt>--offset VALUE</dt>
<dd>환경 목록의 오프셋입니다.</dd>
<dt>--json</dt>
<dd>JSON 형식으로 출력을 인쇄합니다.</dd>
</dl>

## bx schematics environment show
{: #environment-show notoc}

기존 환경에 대한 세부사항을 검색합니다.

```
bx schematics environment show --id ENVIRONMENT_ID [--json]
```
{: codeblock}

### 매개변수
<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>환경의 고유 ID입니다. <code>bx schematics environment list</code>를 실행하여 이 값을 검색할 수 있습니다.</dd>
<dt>--json</dt>
<dd>JSON 형식으로 출력을 인쇄합니다.</dd>
</dl>
  
## bx schematics environment update
{: #environment-update notoc}

환경 이름 또는 GitHub URL과 같은 기존 환경에 대한 세부사항을 업데이트합니다. 환경에 할당된 리소스 수를 업데이트하려면 [bx schematics action plan](#action-plan)을 참조하십시오.

```
bx schematics environment update --id ENVIRONMENT_ID --file FILE_NAME [--json]
```
{: codeblock}

### 매개변수
<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>환경의 고유 ID입니다. <code>bx schematics environment list</code>를 실행하여 이 값을 검색할 수 있습니다.</dd>
<dt>--file FILE_NAME</dt>
<dd>환경에 대한 세부사항을 전달하는 데 사용하는 JSON 파일입니다. 허용된 값이 있는 예제 JSON 스니펫을 보려면 [bx schematics environment create](#environment-create)를 참조하십시오.</dd>
<dt>--json</dt>
<dd>JSON 형식으로 출력을 인쇄합니다.</dd>
</dl>

## bx schematics action apply
{: #action-apply notoc}

환경 구성을 배치합니다. `apply` 명령은 GitHub 저장소에 저장된 구성을 스캔하고 실행합니다.

```
bx schematics action apply --id ENVIRONMENT_ID [--force] [--json]
```
{: codeblock}

### 매개변수
<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>환경의 고유 ID입니다. <code>bx schematics environment list</code>를 실행하여 이 값을 검색할 수 있습니다.</dd>
<dt>--force</dt>
<dd>예/아니오 확인 없이 명령을 강제로 진행합니다.</dd>
<dt>--json</dt>
<dd>JSON 형식으로 적용 출력을 인쇄합니다.</dd>
</dl>

## bx schematics action destroy
{: #action-destroy notoc}

환경과 리소스를 영구 삭제합니다. `destroy` 명령은 실행 중인 리소스를 포함하여 사용자의 환경을 해체합니다. 일반적으로 이 조치는 일정 기간 동안만 활성화가 필요한 QA 환경과 같은 임시 환경에서만 사용합니다. 프로덕션 환경을 영구 삭제하는 것은 권장되지 않습니다. `destroy` 조치는 되돌릴 수 없으므로 주의하여 사용해야 합니다.

```
bx schematics action destroy --id ENVIRONMENT_ID [--force] [--json]
```
{: codeblock}

### 매개변수
<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>환경의 고유 ID입니다. <code>bx schematics environment list</code>를 실행하여 이 값을 검색할 수 있습니다.</dd>
<dt>--force</dt>
<dd>예/아니오 확인 없이 명령을 강제로 진행합니다.</dd>
<dt>--json</dt>
<dd>JSON 형식으로 영구 삭제 출력을 인쇄합니다.</dd>
</dl>
</dl>

## bx schematics action plan
{: #action-plan notoc}

배치된 구성과 환경 구성을 비교합니다. `plan` 명령은 GitHub 저장소에서 구성을 스캔하고 이를 배치된 환경에 연관된 상태 파일과 비교하여 차이점을 찾습니다. 플랜 출력에는 `apply` 명령으로 환경 구성을 배치하는 경우 추가되거나 제거되는 리소스가 표시됩니다. 

```
bx schematics action plan --id ENVIRONMENT_ID [--file FILE_NAME] [--json]
```
{: codeblock}

### 매개변수
<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>환경의 고유 ID입니다. <code>bx schematics environment list</code>를 실행하여 이 값을 검색할 수 있습니다.</dd>
<dt>--file FILE_NAME</dt>
<dd>플랜 조치의 매개변수를 전달하는 데 사용하는 선택적 JSON 파일입니다. 환경의 Terraform 구성에 대한 특정 Git 분기를 참조하도록 <code>sourcesha</code> 매개변수를 전달할 수 있습니다. Git 분기는 <code>refs/heads/BRANCH_NAME</code>과 같은 헤드 참조로 지정해야 합니다. 매개변수가 지정되지 않은 경우, 기본값은 마스터 분기의 헤드인 <code>refs/heads/master</code>입니다.
<p>
<p>값이 지정된 예제 JSON 스니펫:
<pre>{
  "sourcesha": "refs/heads/BRANCH_NAME"
}</pre></dd>
<dt>--json</dt>
<dd>JSON 형식으로 플랜 출력을 인쇄합니다.</dd>
</dl>

## bx schematics activity list
{: #activity-list notoc}

환경에서 실행한 Terraform 활동의 데이터를 나열합니다.

```
bx schematics activity list --id ENVIRONMENT_ID [--count VALUE] [--offset VALUE] [--json]
```
{: codeblock}

### 매개변수
<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>환경의 고유 ID입니다. <code>bx schematics environment list</code>를 실행하여 이 값을 검색할 수 있습니다.</dd>
<dt>--count VALUE</dt>
<dd>리턴할 활동의 수입니다.</dd>
<dt>--offset VALUE</dt>
<dd>목록의 오프셋입니다.</dd>
<dt>--json</dt>
<dd>JSON 형식으로 플랜 출력을 인쇄합니다.</dd>
</dl>

## bx schematics activity log
{: #activity-log notoc}

환경에서 실행하는 조치의 자세한 활동 로그를 봅니다.

```
bx schematics activity log --id ACTIVITY_ID
```
{: codeblock}

### 매개변수
<dl>
<dt>--id ACTIVITY_ID</dt>
<dd>특정 활동에 대한 세부사항을 리턴하는 플래그입니다. <code>bx schematics activity list --id ENVIRONMENT_ID</code> 명령을 사용하여 환경별 활동 ID 목록을 검색할 수 있습니다.</dd>
</dl>

## bx schematics activity planfile
{: #activity-planfile notoc}

환경의 플랜 파일을 봅니다.

```
bx schematics activity planfile --id ACTIVITY_ID
```
{: codeblock}

### 매개변수
<dl>
<dt>--id ACTIVITY_ID</dt>
<dd>특정 활동에 대한 세부사항을 리턴하는 플래그입니다. <code>bx schematics activity list --id ENVIRONMENT_ID</code> 명령을 사용하여 환경별 활동 ID 목록을 검색할 수 있습니다.</dd>
</dl>

## bx schematics activity show
{: #activity-show notoc}

환경에서 실행한 특정 활동에 대한 세부사항을 검색합니다.

```
bx schematics activity show --id ACTIVITY_ID [--json]
```
{: codeblock}

### 매개변수
<dl>
<dt>--id ACTIVITY_ID</dt>
<dd>특정 활동에 대한 세부사항을 리턴하는 플래그입니다. <code>bx schematics activity list --id ENVIRONMENT_ID</code> 명령을 사용하여 환경별 활동 ID 목록을 검색할 수 있습니다.</dd>
<dt>--json</dt>
<dd>JSON 형식으로 플랜 출력을 인쇄합니다.</dd>
</dl>
