---



copyright:

  years: 2015，2017

lastupdated: "2011-01-12"


---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Auto-Scaling CLI
{: #autoscalingcli}


{{site.data.keyword.Bluemix_notm}}용 {{site.data.keyword.autoscaling}} CLI를 사용하여 {{site.data.keyword.autoscaling}} 서비스를 구성할 수 있습니다. {{site.data.keyword.autoscaling}} CLI는 Linux64, Win64 및 OSX를 지원하며, Auto Scaling RESTful API와 비슷한 기능을 제공합니다.
{: shortdesc}

시작하기 전에 {{site.data.keyword.Bluemix_notm}} CLI를 설치하십시오. 지시사항은 [{{site.data.keyword.Bluemix_notm}} CLI 다운로드 ![외부 링크 아이콘](../../../icons/launch-glyph.svg)](http://plugins.ng.bluemix.net/ui/home.html){: new_window}를 참조하십시오. 

## {{site.data.keyword.Bluemix_notm}} CLI 플러그인 추가

{{site.data.keyword.Bluemix_notm}} CL를 설치하고 나면 {{site.data.keyword.autoscaling}} CLI 플러그인을 추가할 수 있습니다.

저장소를 추가하고 플러그인을 설치하려면 다음 단계를 완료하십시오.
1. {{site.data.keyword.Bluemix_notm}} CLI 플러그인 저장소를 추가하려면 다음 명령을 실행하십시오. 
```
bluemix plugin repo-add bluemix-plugin-repo https://plugins.ng.bluemix.net
```
2. {{site.data.keyword.autoscaling}} CLI 플러그인을 설치하려면 다음 명령을 실행하십시오. 
```
bluemix plugin install auto-scaling -r bluemix-plugin-repo
```

## Auto-Scaling 정책 연결

Auto-Scaling 정책을 특정 앱에 연결할 수 있습니다. 다음 명령을 실행하십시오.

```
bx as policy-attach <APP_NAME> -p <policy_file>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;APP_NAME&gt;</dt>
<dd class="pd">Auto-Scaling 정책을 연결할 앱의 이름입니다.</dd>
<dt class="pt dlterm">&lt;policy_file&gt;</dt>
<dd class="pd">Auto-Scaling 정책을 설명하는 JSON 파일의 이름입니다. 자세한 정보는 <a href="https://new-console.{DomainName}/apidocs/48" target="_blank">{{site.data.keyword.autoscaling}} RESTful API 문서</a>를 참조하십시오.</dd>
</dl>


## Auto-Scaling 정책 생성

명령행 인터페이스에서 질문에 답변하여 Auto-Scaling 정책을 생성할 수 있습니다. 입력 내용에 따라 Auto-Scaling 정책 정의를 포함한 JSON 파일이 사용자가 입력한 이름으로 저장됩니다. 파일 이름을 입력하지 않은 경우, 정책 내용이 파일에 저장되지 않은 채 명령행에 바로 인쇄됩니다. 다음 명령을 실행하십시오.

```
bx as policy-create
```
{: codeblock}


## Auto-Scaling 정책 표시

앱의 Auto-Scaling 정책을 표시할 수 있습니다. 정책의 내용이 명령행에 바로 인쇄됩니다. 다음 명령을 실행하십시오.

```
bx as policy-show <APP_NAME> [--json]
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;APP_NAME&gt;</dt>
<dd class="pd">Auto-Scaling 정책을 표시할 앱의 이름입니다. 기본적으로 JSON 구조는 사용자가 읽을 수 있는 출력으로 변환됩니다.</dd>
</dl>

**팁:** **--json** 옵션을 사용하면 원본 JSON 응답이 출력됩니다.


## Auto-Scaling 정책 분리

앱에서 Auto-Scaling 정책을 제거할 수 있습니다. 다음 명령을 실행하십시오.

```
bx as policy-detach <APP_NAME>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;APP_NAME&gt;</dt>
<dd class="pd">Auto-Scaling 정책을 분리할 앱의 이름입니다. </dd>
</dl>


## Auto-Scaling 정책의 사용 여부 설정

특정 앱에 대한 Auto-Scaling 정책의 사용 여부를 설정할 수 있습니다. 다음 명령을 실행하십시오.

```
bx as policy-enable|policy-disable <APP_NAME>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;APP_NAME&gt;</dt>
<dd class="pd">Auto-Scaling 정책의 사용 여부를 설정할 앱의 이름입니다. </dd>
</dl>


## 앱의 Auto-Scaling 히스토리 표시

특정 앱의 Auto-Scaling 활동 히스토리를 표시할 수 있습니다. Auto-Scaling 히스토리 레코드의 테이블이 명령행 인터페이스에 표시됩니다.

```
bx as history-show <APP_NAME>  [--start-date=<start_timestamp>]  [--end-date=<end_timestamp>]  [--json]
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;APP_NAME&gt;</dt>
<dd class="pd">Auto-Scaling 정책의 히스토리를 표시할 앱의 이름입니다.
<dt class="pt dlterm">&lt;start_timestamp&gt;</dt>
<dd class="pd">히스토리 범위가 시작되는 시점의 시간소인입니다. 지원되는 형식은 `yyyy-MM-ddTHH:mm:ss+/-hhmm, yyyy-MM-ddTHH:mm:ssZ`입니다. 기본적으로 시간소인은 현재 시간보다 50시간 이전 시간으로 설정됩니다. 시간소인 형식에 대한 자세한 정보는 <a href="https://www.w3.org/TR/NOTE-datetime" target="_blank">W3C 날짜 및 시간 형식 표준</a>을 참조하십시오.
<dt class="pt dlterm">&lt;end_timestamp&gt;</dt>
<dd class="pd">히스토리 범위가 끝나는 시점의 시간소인입니다. 지원되는 형식은 `yyyy-MM-ddTHH:mm:ss+/-hhmm, yyyy-MM-ddTHH:mm:ssZ`입니다. 기본적으로 시간소인은 현재 시간으로 설정됩니다. 시간소인 형식에 대한 자세한 정보는 <a href="https://www.w3.org/TR/NOTE-datetime" target="_blank">W3C 날짜 및 시간 형식 표준</a>을 참조하십시오.
</dl>



**팁:** **--json** 옵션을 사용하면 원본 JSON 응답이 출력됩니다.

# rellinks
{: rellinks}
## general
{: general}
* [{{site.data.keyword.autoscaling}} 서비스](/docs/services/Auto-Scaling/index.html)
* [{{site.data.keyword.Bluemix_notm}} CLI ![외부 링크 아이콘](../../../icons/launch-glyph.svg)](http://plugins.ng.bluemix.net/ui/home.html){: new_window}
* [W3C 날짜 및 시간 형식 표준 ![외부 링크 아이콘](../../../icons/launch-glyph.svg)](https://www.w3.org/TR/NOTE-datetime){: new_window}
