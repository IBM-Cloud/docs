---

 

copyright:

  years: 2015, 2016

 

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# {{site.data.keyword.Bluemix_notm}} 관리 CLI
{: #bluemixadmincli}

*마지막 업데이트 날짜: 2016년 3월 3일*

{{site.data.keyword.Bluemix_notm}} 관리 CLI 플러그인과 함께
Cloud Foundry 명령행 인터페이스를 사용하여 {{site.data.keyword.Bluemix_notm}} Local 또는
{{site.data.keyword.Bluemix_notm}} Dedicated 환경의 사용자를
관리할 수 있습니다. 예를 들어,
LDAP 레지스트리에서 사용자를 추가할 수 있습니다.{{site.data.keyword.Bluemix_notm}} Public 계정 관리에 대한 정보를 찾는 경우 [관리](../../../admin/adminpublic.html#administer)를 참조하십시오.

시작하기 전에 cf 명령행 인터페이스를 설치하십시오. {{site.data.keyword.Bluemix_notm}} 관리
CLI 플러그인에는 cf 버전 6.11.2 이상이 필요합니다.[Cloud Foundry 명령행 인터페이스 다운로드](https://github.com/cloudfoundry/cli/releases){: new_window}

**제한사항:** Cloud Foundry 명령행 인터페이스는
Cygwin에서는 지원되지 않습니다. Cygwin 명령행 창 외의
명령행 창에서 Cloud Foundry 명령행 인터페이스를 사용하십시오.

## {{site.data.keyword.Bluemix_notm}} 관리
CLI 플러그인 추가

cf 명령행 인터페이스가 설치된 후에 {{site.data.keyword.Bluemix_notm}}
관리 CLI 플러그인을 추가할 수 있습니다.

**참고**: 이전에 {{site.data.keyword.Bluemix_notm}} 관리 플러그인을 설치한 경우, 최신 업데이트를 가져오려면 이 플러그인을 설치 제거하고 저장소를 삭제한 후 다시 설치해야 할 수도 있습니다.

저장소를 추가하고 플러그인을 설치하려면 다음 단계를 완료하십시오.

<ol>
<li>{{site.data.keyword.Bluemix_notm}} 관리 플러그인 저장소를 추가하려면 다음 명령을 실행하십시오. <br/><br/>
<code>
cf add-plugin-repo BluemixAdmin https://console.&lt;subdomain&gt;.bluemix.net/cli
</code><br/><br/>
<dl class="parml">
<dt class="pt dlterm">&lt;subdomain&gt;</dt>
<dd class="pd">{{site.data.keyword.Bluemix_notm}} 인스턴스 URL의 하위 도메인입니다.</dd>
</dl>
</li>
<li>{{site.data.keyword.Bluemix_notm}} 관리 CLI 플러그인을 설치하려면 <br/><br/>
<code>
cf install-plugin bluemix-admin-cli -r BluemixAdmin
</code> 명령을 실행하십시오.
</li>
</ol>

## {{site.data.keyword.Bluemix_notm}} 관리
CLI 플러그인 사용

{{site.data.keyword.Bluemix_notm}} 관리 CLI
플러그인을 사용하여 사용자 추가 및 제거, 조직에서 사용자 지정 및 지정 취소, 기타 관리 태스크를 수행할 수 있습니다. 명령 목록을 보려면 다음 명령을 실행하십시오.

```
cf plugins
```
{: codeblock}

명령에 대한 추가 도움말을 보려면 `-help` 옵션을 사용하십시오.

### {{site.data.keyword.Bluemix_notm}}에 연결 및 로그인

관리 CLI 플러그인을 사용하여 사용자를 관리하려면 (아직 그렇게 하지 않은 경우) 먼저 연결하여 로그인해야 합니다. 

<ol>
<li>{{site.data.keyword.Bluemix_notm}} API 엔드포인트에 연결하려면 <br/><br/>
<code>
cf ba api https://console.&lt;subdomain&gt;.bluemix.net
</code> 명령을 실행하십시오.
<dl class="parml">
<dt class="pt dlterm">&lt;subdomain&gt;</dt>
<dd class="pd">{{site.data.keyword.Bluemix_notm}} 인스턴스 URL의 하위 도메인입니다.<br />
</dd>
</dl>
<p>관리 콘솔의 자원 및 정보 페이지에서 올바른 URL을 확인할 수
있습니다. URL은
**API URL** 필드의 API 정보 섹션에 표시됩니다.</p>
</li>
<li><br/><br/>
<code>
cf login
</code> 명령을 사용하여 {{site.data.keyword.Bluemix_notm}}에 로그인하십시오.
</li>
</ol>

### 사용자 추가

LDAP 레지스트리에서
{{site.data.keyword.Bluemix_notm}} 환경에
사용자를 추가할 수 있습니다. 다음 명령을 입력하십시오. 

```
cf ba add-user <user_name> <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">LDAP 레지스트리 내의 사용자 이름입니다.</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">사용자를 추가할 {{site.data.keyword.Bluemix_notm}} 조직의
이름 또는 GUID입니다.</dd>
</dl>

**팁:** 긴 **ba add-user** 명령어에 대한
별명으로 **ba au**를 사용할 수도 있습니다.

<!-- staging-only commands start. Live for interconnect -->

### 사용자 검색

사용자를 검색할 수 있습니다. 다음 명령을 입력하십시오. 

```
cf ba search-users <user_name>
```
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">{{site.data.keyword.Bluemix_notm}} 내의 사용자 이름입니다.</dd>

</dl>

**팁:** 긴 **ba search-users** 명령어에 대한
별명으로 **ba su**를 사용할 수도 있습니다.

### 사용자의 권한 설정

지정된 사용자의 권한을 설정할 수 있습니다. 다음 명령을 입력하십시오. 

```
cf ba set-permissions <user_name> <permission> <access>
```
{: codeblock}

**참고**: 한 번에 하나의 권한을 설정할 수 있습니다. 

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">{{site.data.keyword.Bluemix_notm}} 내의 사용자 이름입니다.</dd>
<dt class="pt dlterm">&lt;permission&gt;</dt>
<dd class="pd">사용자의 권한을 설정합니다. 권한은 관리, 로그인, 카탈로그(읽기 또는 쓰기 액세스), 보고서(읽기 또는 쓰기 액세스) 또는 사용자(읽기 또는 쓰기 액세스)입니다.</dd>
<dt class="pt dlterm">&lt;access&gt;</dt>
<dd class="pd">카탈로그, 보고서 또는 사용자 권한의 경우 <code>read</code> 또는 <code>write</code>로 액세스 레벨을 설정해야 합니다. </dd>
</dl>

**팁:** 긴 **ba set-permissions** 명령어에 대한
별명으로 **ba sp**를 사용할 수도 있습니다.

<!-- staging-only commands end -->

### 사용자 제거

다음 명령을 입력하여
{{site.data.keyword.Bluemix_notm}} 환경에서
사용자를 제거할 수 있습니다. 

```
cf ba remove-user <user_name>
```
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">{{site.data.keyword.Bluemix_notm}} 내의 사용자 이름입니다.</dd>

</dl>

**팁:** 긴 **ba remove-user** 명령어에 대한
별명으로 **ba ru**를 사용할 수도 있습니다.

### 조직 추가 및 삭제

조직을 추가하고 삭제할 수 있습니다. 

* 조직을 추가하려면 다음 명령을 입력하십시오. 

```
cf ba create-organization <organization> <manager>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">추가할 {{site.data.keyword.Bluemix_notm}} 조직의 이름 또는 GUID입니다. </dd>
<dt class="pt dlterm">&lt;manager&gt;</dt>
<dd class="pd">조직 관리자의 사용자 이름입니다. </dd>
</dl>

**팁:** 긴 **ba create-organization** 명령어에 대한
별명으로 **ba co**를 사용할 수도 있습니다.

* 조직을 삭제하려면 다음 명령을 입력하십시오. 

```
cf ba delete-organization <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">삭제할 {{site.data.keyword.Bluemix_notm}} 조직의 이름 또는 GUID입니다. </dd>
</dl>

**팁:** 긴 **ba delete-organization** 명령어에 대한
별명으로 **ba do**를 사용할 수도 있습니다.

### 조직에 사용자 지정

{{site.data.keyword.Bluemix_notm}} 환경에서
사용자를 특정 조직에 지정할 수
있습니다. 다음 명령을 입력하십시오. 

```
cf ba set-org <user_name> <organization> [<role>]
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">{{site.data.keyword.Bluemix_notm}} 내의 사용자 이름입니다.</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">사용자를 지정할 {{site.data.keyword.Bluemix_notm}} 조직의
이름 또는 GUID입니다.</dd>
<dt class="pt dlterm">&lt;role&gt;</dt>
<dd class="pd">{{site.data.keyword.Bluemix_notm}}
사용자 역할 및 설명에 대해서는 [역할](../../../admin/adminpublic.html#orgsandspaces)을 참조하십시오.</dd>
</dl>

**팁:** 긴 **ba set-org** 명령어에 대한
별명으로 **ba so**를 사용할 수도 있습니다.

### 조직에서 사용자 지정 취소

{{site.data.keyword.Bluemix_notm}} 환경에서
사용자를 특정 조직에서 지정 취소할 수
있습니다. 다음 명령을 입력하십시오. 

```
cf ba unset-org <user_name> <organization> [<role>]
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">{{site.data.keyword.Bluemix_notm}} 내의 사용자 이름입니다.</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">사용자를 지정할 {{site.data.keyword.Bluemix_notm}} 조직의
이름 또는 GUID입니다.</dd>
<dt class="pt dlterm">&lt;role&gt;</dt>
<dd class="pd">{{site.data.keyword.Bluemix_notm}}
사용자 역할 및 설명에 대해서는 [역할](../../../admin/adminpublic.html#orgsandspaces)을 참조하십시오.</dd>
</dl>

**팁:** 긴 **ba unset-org** 명령어에 대한
별명으로 **ba uo**를 사용할 수도 있습니다.

### 역할

<dl class="parml">
<dt class="pt dlterm">OrgManager</dt>
<dd class="pd">조직 관리자입니다. 조직 관리자는 다음 조치를 수행할 수 있는 권한을 가집니다.<ul>
<li>조직 내 영역 작성 또는 삭제</li>
<li>조직으로 사용자 초대 및 사용자 관리</li>
<li>조직의 도메인 관리</li>
</ul>
</dd>
<dt class="pt dlterm">BillingManager</dt>
<dd class="pd">청구 관리자입니다. 청구 관리자는 조직에 대한 런타임 및 서비스 사용 정보를 볼 수 있습니다.</dd>
<dt class="pt dlterm">OrgAuditor</dt>
<dd class="pd">조직 감사자입니다. 조직 감사자는 영역 내의
애플리케이션 및 서비스 컨텐츠를 볼 수 있습니다.</dd>
</dl>

### 조직에 할당량 설정

특정 조직에 사용 할당량을 설정할 수 있습니다. 

```
cf ba set-quota <organization> <plan>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">할당량을 설정할 {{site.data.keyword.Bluemix_notm}} 조직의 이름 또는 GUID입니다. </dd>
<dt class="pt dlterm">&lt;plan&gt;</dt>
<dd class="pd">조직에 대한 할당량 플랜입니다. </dd>
</dl>

**팁:** 긴 **ba set-quota** 명령어에 대한
별명으로 **ba sq**를 사용할 수도 있습니다.

### 보고서 추가, 삭제 및 검색

보안 보고서를 추가, 삭제 및 검색할 수 있습니다. 
* 보고서를 추가하려면 다음 명령을 입력하십시오. 

```
cf ba add-report <category> <date> <PDF|TXT|LOG> <RTF>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;category&gt;</dt>
<dd class="pd">보고서의 카테고리입니다. 이름에 공백이 있는 경우 이름을 따옴표 안에 넣으십시오. </dd>
<dt class="pt dlterm">&lt;date&gt;</dt>
<dd class="pd"><samp class="ph codeph">YYYYMMDD</samp> 형식의 보고서 날짜입니다. </dd>
<dt class="pt dlterm">&lt;PDF|TXT|LOG&gt;</dt>
<dd class="pd">업로드할 보고서 PDF, 텍스트 파일 또는 로그 파일의 경로입니다. </dd>
<dt class="pt dlterm">&lt;RTF&gt;</dt>
<dd class="pd">PDF의 RTF(Rich Text Format) 버전을 포함시키는 옵션입니다. 이 옵션은 보고서 PDF의 경로를 포함시킨 경우에만
적용됩니다. RTF 버전은 색인 작성 및 검색에 사용됩니다. </dd>
</dl>

**팁:** 긴 **ba add-report** 명령어에 대한
별명으로 **ba ar**을 사용할 수도 있습니다.

* 보고서를 삭제하려면 다음 명령을 입력하십시오. 

```
cf ba delete-report <category> <date> <name>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;category&gt;</dt>
<dd class="pd">보고서의 카테고리입니다. 이름에 공백이 있는 경우 이름을 따옴표 안에 넣으십시오. </dd>
<dt class="pt dlterm">&lt;date&gt;</dt>
<dd class="pd"><samp class="ph codeph">YYYYMMDD</samp> 형식의 보고서 날짜입니다. </dd>
<dt class="pt dlterm">&lt;name&gt;</dt>
<dd class="pd">보고서의 이름입니다. </dd>
</dl>

**팁:** 긴 **ba delete-report** 명령어에 대한
별명으로 **ba dr**을 사용할 수도 있습니다.

* 보고서를 검색하려면 다음 명령을 입력하십시오. 

```
cf ba retrieve-report <category> <date> <name>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;category&gt;</dt>
<dd class="pd">보고서의 카테고리입니다. 이름에 공백이 있는 경우 이름을 따옴표 안에 넣으십시오. </dd>
<dt class="pt dlterm">&lt;date&gt;</dt>
<dd class="pd"><samp class="ph codeph">YYYYMMDD</samp> 형식의 보고서 날짜입니다. </dd>
<dt class="pt dlterm">&lt;name&gt;</dt>
<dd class="pd">보고서의 이름입니다. </dd>
</dl>

**팁:** 긴 **ba retrieve-report** 명령어에 대한
별명으로 **ba rr**을 사용할 수도 있습니다.

### 모든 조직에 대해 서비스 사용 또는 사용 안함

모든 조직에 대해 {{site.data.keyword.Bluemix_notm}} 카탈로그에
서비스를 표시하거나 표시하지 않을 수 있습니다. 

* 모든 조직에 대해 {{site.data.keyword.Bluemix_notm}} 카탈로그에
서비스를 표시하도록 설정하려면 다음 명령을 입력하십시오. 

```
cf ba enable-service-plan <plan_identifier>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">사용으로 설정할 서비스의 이름 또는 GUID입니다. 고유하지 않은 서비스 이름을 입력하면 선택할 수 있는
서비스 플랜이 프롬프트됩니다. </dd>
</dl>

**팁:** 긴 **ba enable-service-plan** 명령어에 대한
별명으로 **ba esp**를 사용할 수도 있습니다.

* 모든 조직에 대해 {{site.data.keyword.Bluemix_notm}} 카탈로그에
서비스를 표시하지 않도록 설정하려면 다음 명령을 입력하십시오. 

```
cf ba disable-service-plan <plan_identifier>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">사용 안함으로 설정할 서비스의 이름 또는 GUID입니다. 고유하지 않은 서비스 이름을 입력하면 선택할 수 있는
서비스 플랜이 프롬프트됩니다. </dd>
</dl>

**팁:** 긴 **ba disable-service-plan** 명령어에 대한
별명으로 **ba dsp**를 사용할 수도 있습니다.

### 조직에 대한 서비스 가시성 추가, 제거 및 편집

{{site.data.keyword.Bluemix_notm}} 카탈로그에서
특정 서비스를 볼 수 있는 조직의 목록에 조직을 추가하거나 제거할 수 있습니다. 또한
{{site.data.keyword.Bluemix_notm}} 카탈로그에서
특정 조직이 볼 수 있는 서비스의 목록을 편집하거나 대체할 수도 있습니다. 

* 조직이 {{site.data.keyword.Bluemix_notm}} 카탈로그에서
특정 서비스를 볼 수 있도록 허용하려면 다음 명령을 입력하십시오. 

```
cf ba add-service-plan-visibility <plan_identifier> <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">가시성을 추가할 서비스의 이름 또는 GUID입니다. 고유하지 않은 서비스 이름을 입력하면 선택할 수 있는
서비스 플랜이 프롬프트됩니다. </dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">서비스의 가시성 목록에 추가할 {{site.data.keyword.Bluemix_notm}} 조직의
이름 또는 GUID입니다. </dd>
</dl>

**팁:** 긴 **ba add-service-plan-visibility** 명령어에 대한
별명으로 **ba aspv**를 사용할 수도 있습니다.

* {{site.data.keyword.Bluemix_notm}} 카탈로그에서
조직에 대한 서비스의 가시성을 제거하려면 다음 명령을 입력하십시오. 

```
cf ba remove-service-plan-visibility <plan_identifier> <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">가시성을 제거할 서비스의 이름 또는 GUID입니다. 고유하지 않은 서비스 이름을 입력하면 선택할 수 있는
서비스 플랜이 프롬프트됩니다. </dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">서비스의 가시성 목록에서 제거할 {{site.data.keyword.Bluemix_notm}} 조직의
이름 또는 GUID입니다. </dd>
</dl>

**팁:** 긴 **ba remove-service-plan-visibility** 명령어에 대한
별명으로 **ba rspv**를 사용할 수도 있습니다.

* 단일 조직 또는 여러 조직에 대해 표시되는 기존 서비스를 모두 대체하려면
다음 명령을 사용하십시오. 

```
cf ba edit-service-plan-visibilities <plan_identifier> <organization_1> <optional_organization_2>
```
{: codeblock}

**참고:** 이 명령은
지정된 조직에 대해 표시되는 기존 서비스를 명령에서 지정하는 서비스로
대체합니다. 

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">표시할 서비스의 이름 또는 GUID입니다. 고유하지 않은 서비스 이름을 입력하면 선택할 수 있는
서비스 플랜이 프롬프트됩니다. </dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">가시성을 추가할 {{site.data.keyword.Bluemix_notm}} 조직의
이름 또는 GUID입니다. 명령에 추가로 조직 이름 또는 GUID를 입력하여 둘 이상의 조직에 대해 서비스의 가시성을 사용으로
설정할 수 있습니다. </dd>
</dl>

**팁:** 긴 **ba edit-service-plan-visibility** 명령어에 대한
별명으로 **ba espv**를 사용할 수도 있습니다.

### 서비스 브로커에 대한 작업

모든 서비스 브로커를 나열하거나 서비스 브로커를 추가 또는 삭제하거나 서비스 브로커를 업데이트하려면 다음 명령을 사용하십시오.

* 다음 명령을 입력하여 서비스 브로커를 나열할 수 있습니다. 

```
cf ba service-brokers <broker_name>
```
{: codeblock}

**참고**: 모든 서비스 브로커를 나열하려면 `broker_name` 매개변수 없이 명령을 입력하십시오. 

<dl class="parml">
<dt class="pt dlterm">&lt;broker_name&gt;</dt>
<dd class="pd">선택사항: 사용자 정의 서비스 브로커의 이름입니다. 특정 서비스 브로커에 대한 정보를 가져오려면 이 매개변수를 사용하십시오.</dd>
</dl>

**팁:** 긴 **ba service-brokers** 명령어에 대한
별명으로 **ba sb**를 사용할 수도 있습니다.

* 다음 명령을 입력하여 서비스 브로커를 추가할 수 있으며, 이로써 사용하는
{{site.data.keyword.Bluemix_notm}} 카탈로그에 사용자 정의 서비스를 추가할 수 있습니다. 

```
cf ba add-service-broker <broker_name> <user_name> <password> <broker_url>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;broker_name&gt;</dt>
<dd class="pd">사용자 정의 서비스 브로커의 이름입니다.</dd>
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">서비스 브로커에 액세스할 수 있는 계정의 사용자 이름입니다.</dd>
<dt class="pt dlterm">&lt;password&gt;</dt>
<dd class="pd">서비스 브로커에 액세스할 수 있는 계정의 비밀번호입니다.</dd>
<dt class="pt dlterm">&lt;broker_url&gt;</dt>
<dd class="pd">서비스 브로커의 URL입니다.</dd>
</dl>

**팁:** 긴 **ba add-service-broker** 명령어에 대한
별명으로 **ba asb**를 사용할 수도 있습니다.

* 다음 명령을 입력하여 서비스 브로커를 삭제할 수 있으며, 이로써
{{site.data.keyword.Bluemix_notm}} 카탈로그에서 해당 사용자 정의 서비스를 제거할 수 있습니다.

```
cf ba delete-service-broker <service_broker>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;service_broker&gt;</dt>
<dd class="pd">사용자 정의 서비스 브로커의 이름 또는 guid입니다.</dd>
</dl>

**팁:** 긴 **ba delete-service-broker** 명령어에 대한
별명으로 **ba dsb**를 사용할 수도 있습니다.

* 다음 명령을 입력하여 서비스 브로커를 업데이트할 수 있습니다.

`cf ba update-service-broker <broker_name> <user_name> <password> <broker_url>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;broker_name&gt;</dt>
<dd class="pd">사용자 정의 서비스 브로커의 이름입니다.</dd>
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">서비스 브로커에 액세스할 수 있는 계정의 사용자 이름입니다.</dd>
<dt class="pt dlterm">&lt;password&gt;</dt>
<dd class="pd">서비스 브로커에 액세스할 수 있는 계정의 비밀번호입니다.</dd>
<dt class="pt dlterm">&lt;broker_url&gt;</dt>
<dd class="pd">서비스 브로커의 URL입니다.</dd>
</dl>

**팁:** 긴 **ba update-service-broker** 명령어에 대한
별명으로 **ba usb**를 사용할 수도 있습니다.
