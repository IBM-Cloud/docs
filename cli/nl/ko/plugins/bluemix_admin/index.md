---

copyright:

  years: 2015, 2017

lastupdated: "2017-02-20"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# {{site.data.keyword.Bluemix_notm}} 관리 CLI
{: #bluemixadmincli}


{{site.data.keyword.Bluemix_notm}} 관리 CLI 플러그인에 Cloud Foundry 명령행 인터페이스를 사용하여 {{site.data.keyword.Bluemix_notm}} 로컬 또는 {{site.data.keyword.Bluemix_notm}} 데디케이티드 환경을 관리할 수 있습니다. 예를 들어, LDAP 레지스트리에서 사용자를 추가할 수 있습니다. {{site.data.keyword.Bluemix_notm}} 퍼블릭 계정 관리에 대한 정보를 찾는 경우 [관리](/docs/admin/adminpublic.html#administer)를 참조하십시오.

시작하기 전에 cf 명령행 인터페이스를 설치하십시오. {{site.data.keyword.Bluemix_notm}} 관리
CLI 플러그인에는 cf 버전 6.11.2 이상이 필요합니다. [Cloud Foundry 명령행 인터페이스 다운로드 ![외부 링크 아이콘](../../../icons/launch-glyph.svg)](https://github.com/cloudfoundry/cli/releases){: new_window}

**제한사항:** Cloud Foundry 명령행 인터페이스는
Cygwin에서는 지원되지 않습니다. Cygwin 명령행 창 외의
명령행 창에서 Cloud Foundry 명령행 인터페이스를 사용하십시오.

**참고**: {{site.data.keyword.Bluemix_notm}} 관리 CLI는 {{site.data.keyword.Bluemix_notm}} 로컬 및 {{site.data.keyword.Bluemix_notm}} 데디케이티드 환경에만 사용됩니다. {{site.data.keyword.Bluemix_notm}} 퍼블릭에서 지원되지 않습니다.

## {{site.data.keyword.Bluemix_notm}} 관리 CLI 플러그인 추가

cf 명령행 인터페이스가 설치된 후에
{{site.data.keyword.Bluemix_notm}} 관리 CLI
플러그인을 추가할 수 있습니다.

**참고**: 이전에 {{site.data.keyword.Bluemix_notm}} 관리 플러그인을 설치한 경우, 최신 업데이트를 가져오려면 이 플러그인을 설치 제거하고 저장소를 삭제한 후 다시 설치해야 할 수도 있습니다.

저장소를 추가하고 플러그인을 설치하려면 다음 단계를 완료하십시오.

<ol>
<li>{{site.data.keyword.Bluemix_notm}} 관리 플러그인 저장소를 추가하려면 다음 명령을 실행하십시오.<br/><br/>
<code>
cf add-plugin-repo BluemixAdmin https://console.&lt;subdomain&gt;.bluemix.net/cli
</code><br/><br/>
</li>
<li>{{site.data.keyword.Bluemix_notm}} 관리 CLI 플러그인을 설치하려면 다음 명령을 실행하십시오.<br/><br/>
<code>
cf install-plugin BluemixAdminCLI -r BluemixAdmin
</code>
</li>
</ol>

플러그인을 설치 제거해야 하는 경우 다음 명령을 사용한 후 업데이트된 저장소를 추가하고 최신 플러그인을 설치할 수 있습니다. 

* 플러그인 설치 제거: `cf uninstall-plugin BluemixAdminCLI`
* 플러그인 저장소 제거: `cf remove-plugin-repo BluemixAdmin`


## {{site.data.keyword.Bluemix_notm}} 관리 CLI 플러그인 사용

{{site.data.keyword.Bluemix_notm}} 관리 CLI 플러그인을 사용하여 사용자 추가 및 제거, 조직에서 사용자 지정 및 지정 취소, 기타 관리 태스크를 수행할 수 있습니다. 

명령 목록을 보려면 다음 명령을
실행하십시오.

```
cf plugins
```
{: codeblock}

명령에 대한 추가 도움말을 보려면 `-help` 옵션을 사용하십시오.

### {{site.data.keyword.Bluemix_notm}}에 연결 및 로그인

관리 CLI 플러그인을 사용하려면 (아직 그렇게 하지 않은 경우) 먼저 연결하여
로그인해야 합니다. 

<ol>
<li>{{site.data.keyword.Bluemix_notm}} API 엔드포인트에 연결하려면 다음 명령을 실행하십시오.<br/><br/>
<code>
cf ba api https://console.&lt;subdomain&gt;.bluemix.net
</code>
<dl class="parml">
<dt class="pt dlterm">&lt;subdomain&gt;</dt>
<dd class="pd">{{site.data.keyword.Bluemix_notm}} 인스턴스 URL의 하위 도메인입니다.<br />
</dd>
</dl>
<p>관리 콘솔의 리소스 및 정보 페이지에서 올바른 URL을 확인할 수
있습니다. URL은 **API URL** 필드의 API 정보 섹션에
표시됩니다.</p>
</li>
<li>다음 명령으로 {{site.data.keyword.Bluemix_notm}}에 로그인하십시오.<br/><br/>
<code>
cf login
</code>
</li>
</ol>

## 사용자 관리
{: #admin_users}

### 사용자 추가
{: #admin_add_user}

사용자 환경의 사용자 레지스트리에서 {{site.data.keyword.Bluemix_notm}} 환경에 사용자를 추가하려면
다음 명령을 사용하십시오.

```
cf ba add-user <user_name> <organization> <first_name> <last_name>
```
{: codeblock}

**참고**: 특정 조직에 사용자를 추가하려면 **users.write** 권한이 있는 **관리자**(또는 **수퍼유저**)여야 합니다. 조직 관리자인 경우 **enable-managers-add-users** 명령을 실행하는 수퍼유저가 조직에 사용자를 추가하는 기능을 제공할 수 있습니다. 자세한 정보는 [관리자를 사용하여 사용자 추가](index.html#clius_emau)를 참조하십시오.

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">LDAP 레지스트리 내의 사용자 이름입니다.</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">사용자를 추가할 {{site.data.keyword.Bluemix_notm}} 조직의 이름 또는 GUID입니다.</dd>
<dt class="pt dlterm">&lt;first_name&gt;</dt>
<dd class="pd">조직에 추가할 사용자의 이름입니다.</dd>
<dt class="pt dlterm">&lt;last_name&gt;</dt>
<dd class="pd">조직에 추가할 사용자의 성입니다.</dd>
</dl>

**팁:** 긴 **ba add-user** 명령어에 대한
별명으로 **ba au**를 사용할 수도 있습니다.

<!-- staging-only commands start. Live for interconnect -->

### 사용자 검색
{: #admin_search_user}

사용자를 검색하려면, 선택적 검색 필터 매개변수(이름, 권한, 조직 및 역할)와 함께
다음 명령을 사용하십시오.

```
cf ba search-users -name=<user_name_value> -permission=<permission_value> -organization=<organization_value> -role=<role_value>
```
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">&lt;user_name_value&gt;</dt>
<dd class="pd">{{site.data.keyword.Bluemix_notm}} 내의 사용자 이름입니다.</dd>
<dt class="pt dlterm">&lt;permission_value&gt;</dt>
<dd class="pd">사용자에게 지정된 권한입니다. 예를 들어, 수퍼유저, 카탈로그, 사용자 및 보고서입니다. 지정되는 사용자 권한에 대한 자세한 정보는 [권한](/docs/admin/index.html#permissions)을 참조하십시오. 동일한 조회에 조직 매개변수가 있으면 이 매개변수를 사용할 수 없습니다. </dd>
<dt class="pt dlterm">&lt;organization_value&gt;</dt>
<dd class="pd">사용자가 속한 조직 이름입니다. 동일한 조회에 권한 매개변수가 있으면 이 매개변수를 사용할 수 없습니다. </dd>
<dt class="pt dlterm">&lt;role_value&gt;</dt>
<dd class="pd">사용자에게 지정된 조직 역할입니다. 예를 들어, 조직의 관리자, 청구 관리자 또는 감사자입니다. 이 매개변수와 함께 조직을 지정해야 합니다. 역할에 대한 자세한 정보는 [사용자 역할](/docs/admin/users_roles.html#userrolesinfo)을 참조하십시오. </dd>

</dl>

**팁:** 긴 **ba search-users** 명령어에 대한
별명으로 **ba su**를 사용할 수도 있습니다.

### 사용자의 권한 설정
{: #admin_setperm_user}

지정된 사용자의 권한을 설정하려면 다음 명령을 사용하십시오.

```
cf ba set-permissions <user_name> <permission> <access>
```
{: codeblock}

**참고**: 한 번에 하나의 권한을 설정할 수 있습니다. 

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">{{site.data.keyword.Bluemix_notm}} 내의 사용자 이름입니다.</dd>
<dt class="pt dlterm">&lt;permission&gt;</dt>
<dd class="pd">사용자의 권한을 설정합니다. 권한은 관리(사용 가능한 대체는 수퍼유저), 로그인(사용 가능한 대체는 기본), 카탈로그(읽기 또는 쓰기 액세스 권한), 보고서(읽기 또는 쓰기 액세스 권한) 또는 사용자(읽기 또는 쓰기 액세스 권한)입니다. </dd>
<dt class="pt dlterm">&lt;access&gt;</dt>
<dd class="pd">카탈로그, 보고서 또는 사용자 권한의 경우 <code>read</code> 또는 <code>write</code>로 액세스 레벨을 설정해야 합니다. </dd>
</dl>

**팁:** 긴 **ba set-permissions** 명령어에 대한
별명으로 **ba sp**를 사용할 수도 있습니다.

<!-- staging-only commands end -->

### 사용자 제거
{: #admin_remov_user}

{{site.data.keyword.Bluemix_notm}} 환경에서 사용자를 제거하려면 다음 명령을 사용하십시오.

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

### 관리자가 사용자를 추가하도록 설정
{: #clius_emau}

{{site.data.keyword.Bluemix_notm}} 환경에 **수퍼유저** 권한이 있는 경우 조직 관리자가 관리하는 조직에 사용자를 추가하도록 설정할 수 있습니다. 관리자가 사용자를 추가할 수 있도록 하려면 다음 명령을 사용하십시오.

```
cf ba enable-managers-add-users
```
{: codeblock}

**팁:** 긴 **ba enable-managers-add-users** 명령어의
별명으로 **ba emau**를 사용할 수도 있습니다. 

### 관리자가 사용자를 추가하도록 설정 제거
{: #clius_dmau}

조직 관리자가 **enable-managers-add-users** 명령을 사용하여 {{site.data.keyword.Bluemix_notm}} 환경에서 관리하는 조직에 사용자를 추가하도록 설정된 경우 및 **수퍼유저** 권한이 있는 경우 이 설정을 제거할 수 있습니다. 관리자가 사용자를 추가할 수 없도록 하려면 다음 명령을 사용하십시오.

```
cf ba disable-managers-add-users
```
{: codeblock}

**팁:** 긴 **ba disable-managers-add-users** 명령어의
별명으로 **ba emau**를 사용할 수도 있습니다. 

## 조직 관리
{: #admin_orgs}

### 조직 추가
{: #admin_add_org}

조직을 추가하려면 다음 명령을 사용하십시오. 

```
cf ba create-org <organization> <manager>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">추가할 {{site.data.keyword.Bluemix_notm}} 조직의 이름 또는 GUID입니다. </dd>
<dt class="pt dlterm">&lt;manager&gt;</dt>
<dd class="pd">조직 관리자의 사용자 이름입니다. </dd>
</dl>

**팁:** 긴 **ba create-org** 명령어에 대한
별명으로 **ba co**를 사용할 수도 있습니다.

### 조직 삭제
{: #admin_delete_org}

조직을 삭제하려면 다음 명령을 사용하십시오. 

```
cf ba delete-org <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">삭제할 {{site.data.keyword.Bluemix_notm}} 조직의 이름 또는 GUID입니다. </dd>
</dl>

**팁:** 긴 **ba delete-org** 명령어에 대한
별명으로 **ba do**를 사용할 수도 있습니다.

### 조직에 사용자 지정
{: #admin_ass_user_org}

{{site.data.keyword.Bluemix_notm}} 환경에 있는 사용자를 특정 조직에 지정하려면
다음 명령을 사용하십시오.

```
cf ba set-org <user_name> <organization> [<role>]
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">{{site.data.keyword.Bluemix_notm}} 내의 사용자 이름입니다.</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">사용자를 지정할 {{site.data.keyword.Bluemix_notm}} 조직의 이름 또는 GUID입니다.</dd>
<dt class="pt dlterm">&lt;role&gt;</dt>
<dd class="pd">{{site.data.keyword.Bluemix_notm}}
사용자 역할 및 설명에 대해서는 [역할](/docs/admin/users_roles.html)을
참조하십시오.</dd>
</dl>

**팁:** 긴 **ba set-org** 명령어에 대한
별명으로 **ba so**를 사용할 수도 있습니다.

### 조직에서 사용자 지정 취소
{: #admin_unass_user_org}

{{site.data.keyword.Bluemix_notm}} 환경에 있는 사용자를 특정 조직에서 지정 취소하려면
다음 명령을 사용하십시오.

```
cf ba unset-org <user_name> <organization> [<role>]
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">{{site.data.keyword.Bluemix_notm}} 내의 사용자 이름입니다.</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">사용자를 지정할 {{site.data.keyword.Bluemix_notm}} 조직의 이름 또는 GUID입니다.</dd>
<dt class="pt dlterm">&lt;role&gt;</dt>
<dd class="pd">{{site.data.keyword.Bluemix_notm}} 사용자 역할 및 설명에 대해서는
[역할 지정](/docs/admin/users_roles.html)을
참조하십시오.</dd>
</dl>

**팁:** 긴 **ba unset-org** 명령어에 대한
별명으로 **ba uo**를 사용할 수도 있습니다.

#### 역할 지정

<dl class="parml">
<dt class="pt dlterm">OrgManager</dt>
<dd class="pd">조직 관리자입니다. 조직 관리자는 다음 조치를 수행할 수 있는 권한을 가집니다.
<ul>
<li>조직 내 영역 작성 또는 삭제</li>
<li>조직으로 사용자 초대 및 사용자 관리</li>
<li>조직의 도메인 관리</li>
</ul>
</dd>
<dt class="pt dlterm">BillingManager</dt>
<dd class="pd">청구 관리자입니다. 청구 관리자는 조직에 대한 런타임 및 서비스 사용 정보를
볼 수 있습니다.</dd>
<dt class="pt dlterm">OrgAuditor</dt>
<dd class="pd">조직 감사자입니다. 조직 감사자는 영역 내의 애플리케이션 및 서비스 컨텐츠를
볼 수 있습니다.</dd>
</dl>

### 조직에 할당량 설정
{: #admin_set_org_quota}

특정 조직에 사용 할당량을 설정하려면 다음 명령을 사용하십시오. 

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


### 조직의 컨테이너 할당량 찾기
{: #admin_find_containquotas}

조직의 컨테이너 할당량을 찾으려면 다음 명령을 사용하십시오. 

```
cf bluemix-admin containers-quota <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">Bluemix의 조직 이름 또는 ID. 이 매개변수는 필수입니다. </dd>
</dl>

**팁:** 긴 **bluemix-admin containers-quota** 명령어의 별명으로
**ba cq**를 사용할 수도 있습니다.

### 조직의 컨테이너 할당량 설정
{: #admin_set_containquotas}

조직의 컨테이너 할당량을 설정하려면 하나 이상의 옵션을 포함하여 다음 명령을 사용하십시오.

```
cf bluemix-admin set-containers-quota <organization> <options>
```
{: codeblock}

**참고**: 여러 옵션을 포함할 수 있지만 적어도 하나는 포함해야 합니다.

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">Bluemix의 조직 이름 또는 ID. 이 매개변수는 필수입니다. </dd>
<dt class="pt dlterm">&lt;options&gt;</dt>
<dd class="pd">값이 정수여야 하는 다음 옵션 중 하나 이상을 포함합니다.
<ul>
<li>floating-ips-max &lt;value&gt;</li>
<li>floating-ips-space-default &lt;value&gt;</li>
<li>memory-max &lt;value&gt;</li>
<li>memory-space-default &lt;value&gt;</li>
<li>image-limit &lt;value&gt;</li>
</ul>
</dd>
</dl>

**팁:** 긴 옵션 이름의 별명으로 다음 단축 이름을
사용할 수도 있습니다.
<dl class="parml">
<dt class="pt dlterm">floating-ips-max &lt;value&gt;</dt>
<dd class="pd"><strong>fim</strong></dd>
<dt class="pt dlterm">floating-ips-space-default &lt;value&gt;</dt>
<dd class="pd"><strong>fisd</strong></dd>
<dt class="pt dlterm">memory-max &lt;value&gt;</dt>
<dd class="pd"><strong>mm</strong></dd>
<dt class="pt dlterm">memory-space-default &lt;value&gt;</dt>
<dd class="pd"><strong>msd</strong></dd>
<dt class="pt dlterm">image-limit &lt;value&gt;</dt>
<dd class="pd"><strong>il</strong></dd>
</dl>

선택적으로 올바른 JSON 오브젝트에 특정 구성 매개변수를 포함하는 파일을 제공할 수 있습니다. **-file** 옵션을 사용하면 이 옵션이 우선 적용되고 다른 옵션은 무시됩니다. 옵션을 설정하는 대신에 파일을 제공하려면 다음 명령을 사용하십시오.

```
cf bluemix-admin set-containers-quota <organization> <-file path_to_JSON_file>
```
{: codeblock}

JSON 파일의 형식은 다음 예제와 같습니다. 

```
{
  "floating_ips_max": 10,
  "floating_ips_space_default": 0,
  "ram_max": 4096,
  "ram_space_default": 0,
  "image_limit": 10
}
```
{: codeblock}

**팁:** 긴 **bluemix-admin set-containers-quota** 명령어의 별명으로
**ba scq**를 사용할 수도 있습니다.

## 영역 관리
{: #admin_spaces}

### 조직에 영역 추가

조직에 영역을 추가하려면 다음 명령을 사용하십시오.

```
cf bluemix-admin create-space <organization> <space_name>
```

{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">영역을 추가할 조직의 이름 또는 GUID입니다.</dd>
<dt class="pt dlterm">&lt;space_name&gt;</dt>
<dd class="pd">조직에서 작성할 영역의 이름입니다.</dd>
</dl>

**팁:** 긴 **ba create-space** 명령어에 대한
별명으로 **ba cs**를 사용할 수도 있습니다.

### 조직에서 영역 삭제

조직에서 영역을 삭제하려면 다음 명령을 사용하십시오.

```
cf bluemix-admin delete-space <organization> <space_name>
```

{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">영역을 제거할 조직의 이름 또는 GUID입니다.</dd>
<dt class="pt dlterm">&lt;space_name&gt;</dt>
<dd class="pd">조직에서 제거할 영역의 이름입니다.</dd>
</dl>

**팁:** 긴 **ba delete-space** 명령어에 대한
별명으로 **ba cs**를 사용할 수도 있습니다.

### 역할과 함께 영역에 사용자 추가

지정된 역할과 함께 영역에 사용자를 작성하려면 다음 명령을 사용하십시오.

```
cf bluemix-admin set-space <organization> <space_name> <user_name> <role>
```

{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">사용자를 추가할 조직의 이름 또는 GUID입니다.</dd>
<dt class="pt dlterm">&lt;space_name&gt;</dt>
<dd class="pd">사용자를 추가할 영역의 이름입니다.</dd>
<dt class="pt dlterm">&lt;user_anme&gt;</dt>
<dd class="pd">추가할 사용자의 이름입니다.</dd>
<dt class="pt dlterm">&lt;role&gt;</dt>
<dd class="pd">지정할 사용자의 역할입니다. 값은 관리자, 개발자 또는 감사자입니다. 영역의
{{site.data.keyword.Bluemix_notm}} 사용자 역할 및 설명은 [역할 지정](/docs/admin/users_roles.html)을
참조하십시오.</dd>
</dl>

**팁:** 긴 **ba set-space** 명령어에 대한
별명으로 **ba ss**를 사용할 수도 있습니다.


### 영역에서 사용자의 역할 제거 

영역에서 사용자 역할을 제거하려면 다음 명령을 사용하십시오.

```
cf bluemix-admin unset-space <organization> <space_name> <user_name> <role>
```

{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">사용자를 추가할 조직의 이름 또는 GUID입니다.</dd>
<dt class="pt dlterm">&lt;space_name&gt;</dt>
<dd class="pd">사용자를 추가할 영역의 이름입니다.</dd>
<dt class="pt dlterm">&lt;user_anme&gt;</dt>
<dd class="pd">추가할 사용자의 이름입니다.</dd>
<dt class="pt dlterm">&lt;role&gt;</dt>
<dd class="pd">지정할 사용자의 역할입니다. 값은 관리자, 개발자 또는 감사자입니다. 영역의
{{site.data.keyword.Bluemix_notm}} 사용자 역할 및 설명은 [역할 지정](/docs/admin/users_roles.html)을
참조하십시오.</dd>
</dl>

**팁:** 긴 **ba unset-space** 명령어에 대한
별명으로 **ba us**를 사용할 수도 있습니다.

## 카탈로그 관리
{: #admin_catalog}

### 모든 조직에 대해 서비스 사용
{: #admin_ena_service_org}

모든 조직에 대해
{{site.data.keyword.Bluemix_notm}} 카탈로그에
서비스를 표시하도록 설정하려면 다음 명령을 사용하십시오. 

```
cf ba enable-service-plan <plan_identifier>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">사용할 서비스 플랜의 이름 또는 GUID입니다. 고유하지 않은 서비스 플랜 이름(예: "표준" 또는 "기본")을 입력하면 선택할 수 있는 서비스 플랜이 프롬프트됩니다. 서비스 플랜 이름을 식별하려면, 홈 페이지에서 서비스 카테고리를 선택한 후에 **추가**를 선택하여 해당 카테고리의 서비스를 보십시오. 서비스 이름을 클릭하여 세부사항 보기를 여십시오. 그러면 해당 서비스에 사용 가능한 서비스 플랜의 이름을 볼 수 있습니다.</dd>
</dl>

**팁:** 긴 **ba enable-service-plan** 명령어에 대한
별명으로 **ba esp**를 사용할 수도 있습니다.

### 모든 조직에 대해 서비스 사용 안함
{: #admin_dis_service_org}

모든 조직에 대해 {{site.data.keyword.Bluemix_notm}} 카탈로그에
서비스를 표시하지 않도록 설정하려면 다음 명령을 사용하십시오. 

```
cf ba disable-service-plan <plan_identifier>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">사용할 서비스 플랜의 이름 또는 GUID입니다. 고유하지 않은 서비스 플랜 이름(예: "표준" 또는 "기본")을 입력하면 선택할 수 있는 서비스 플랜이 프롬프트됩니다. 서비스 플랜 이름을 식별하려면, 홈 페이지에서 서비스 카테고리를 선택한 후에 **추가**를 선택하여 해당 카테고리의 서비스를 보십시오. 서비스 이름을 클릭하여 세부사항 보기를 여십시오. 그러면 해당 서비스에 사용 가능한 서비스 플랜의 이름을 볼 수 있습니다.</dd>
</dl>

**팁:** 긴 **ba disable-service-plan** 명령어에 대한
별명으로 **ba dsp**를 사용할 수도 있습니다.

### 조직에 대한 서비스 가시성 추가
{: #admin_addvis_service_org}

{{site.data.keyword.Bluemix_notm}} 카탈로그에서 특정 서비스를 볼 수 있는 조직을 조직 목록에서 추가할 수 있습니다. 조직이 {{site.data.keyword.Bluemix_notm}} 카탈로그에서
특정 서비스를 볼 수 있도록 허용하려면 다음 명령을 사용하십시오. 

```
cf ba add-service-plan-visibility <plan_identifier> <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">사용할 서비스 플랜의 이름 또는 GUID입니다. 고유하지 않은 서비스 플랜 이름(예: "표준" 또는 "기본")을 입력하면 선택할 수 있는 서비스 플랜이 프롬프트됩니다. 서비스 플랜 이름을 식별하려면, 홈 페이지에서 서비스 카테고리를 선택한 후에 **추가**를 선택하여 해당 카테고리의 서비스를 보십시오. 서비스 이름을 클릭하여 세부사항 보기를 여십시오. 그러면 해당 서비스에 사용 가능한 서비스 플랜의 이름을 볼 수 있습니다.</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">서비스의 가시성 목록에 추가할 {{site.data.keyword.Bluemix_notm}} 조직의 이름 또는 GUID입니다. </dd>
</dl>

**팁:** 긴 **ba add-service-plan-visibility** 명령어에 대한
별명으로 **ba aspv**를 사용할 수도 있습니다.

### 조직에 대한 서비스 가시성 제거
{: #admin_remvis_service_org}

{{site.data.keyword.Bluemix_notm}} 카탈로그에서
특정 서비스를 볼 수 있는 조직을 조직 목록에서 제거할 수 있습니다. {{site.data.keyword.Bluemix_notm}} 카탈로그에서
조직에 대한 서비스의 가시성을 제거하려면
다음 명령을 사용하십시오. 

```
cf ba remove-service-plan-visibility <plan_identifier> <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">사용으로 설정할 서비스 플랜의 이름 또는 GUID입니다. 고유하지 않은 서비스 플랜 이름(예: "표준" 또는 "기본")을 입력하면 선택할 수 있는 서비스 플랜이 프롬프트됩니다. 서비스 플랜 이름을 식별하려면, 홈 페이지에서 서비스 카테고리를 선택한 후에 **추가**를 선택하여 해당 카테고리의 서비스를 보십시오. 서비스 이름을 클릭하여 세부사항 보기를 여십시오. 그러면 해당 서비스에 사용 가능한 서비스 플랜의 이름을 볼 수 있습니다.</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">서비스의 가시성 목록에서 제거할 {{site.data.keyword.Bluemix_notm}} 조직의 이름 또는 GUID입니다. </dd>
</dl>

**팁:** 긴 **ba remove-service-plan-visibility** 명령어에 대한
별명으로 **ba rspv**를 사용할 수도 있습니다.

### 조직에 대한 서비스 가시성 편집
{: #admin_editvis_service_org}

{{site.data.keyword.Bluemix_notm}} 카탈로그에서
특정 조직이 볼 수 있는 서비스의 목록을 편집하고 대체할 수도 있습니다. 단일 조직 또는 여러 조직에 대해 표시되는 기존 서비스를 모두 대체하려면
다음 명령을 사용하십시오. 

```
cf ba edit-service-plan-visibilities <plan_identifier> <organization_1> <optional_organization_2>
```
{: codeblock}

**참고:** 이 명령은 지정된 조직에 대해 표시되는 기존 서비스를 명령에서 지정하는 서비스로 대체합니다. 

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">사용할 서비스 플랜의 이름 또는 GUID입니다. 고유하지 않은 서비스 플랜 이름(예: "표준" 또는 "기본")을 입력하면 선택할 수 있는 서비스 플랜이 프롬프트됩니다. 서비스 플랜 이름을 식별하려면, 홈 페이지에서 서비스 카테고리를 선택한 후에 **추가**를 선택하여 해당 카테고리의 서비스를 보십시오. 서비스 이름을 클릭하여 세부사항 보기를 여십시오. 그러면 해당 서비스에 사용 가능한 서비스 플랜의 이름을 볼 수 있습니다.</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">가시성을 추가할 {{site.data.keyword.Bluemix_notm}} 조직의 이름 또는 GUID입니다. 명령에 추가로 조직 이름 또는 GUID를 입력하여 둘 이상의 조직에 대해
서비스의 가시성을 사용으로 설정할 수 있습니다. </dd>
</dl>

**팁:** 긴 **ba edit-service-plan-visibility** 명령어에 대한
별명으로 **ba espv**를 사용할 수도 있습니다.

## 보고서 관리
{: #admin_add_report}

### 보고서 추가
{: #admin_add_report}

보안 보고서를 추가하려면 다음 명령을 사용하십시오. 

```
cf ba add-report <category> <date> <PDF|TXT|LOG> <RTF>
```
{: codeblock}

**참고**: 보고서 권한에 대해 쓰기 액세스 권한이 있는 경우, 새 카테고리를 작성하고 사용자에 대한 허용된 형식으로 보고서를 추가할 수 있습니다. `category` 매개변수에 대해 새 카테고리 이름을 입력하거나 새 보고서를 기존 카테고리에 추가하십시오. 

<dl class="parml">
<dt class="pt dlterm">&lt;category&gt;</dt>
<dd class="pd">보고서의 카테고리입니다. 이름에 공백이 있는 경우 이름을 따옴표 안에
넣으십시오. </dd>
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

### 보고서 삭제
{: #admin_del_report}

보안 보고서를 삭제하려면 다음 명령을 사용하십시오. 

```
cf ba delete-report <category> <date> <name>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;category&gt;</dt>
<dd class="pd">보고서의 카테고리입니다. 이름에 공백이 있는 경우 이름을 따옴표 안에
넣으십시오. </dd>
<dt class="pt dlterm">&lt;date&gt;</dt>
<dd class="pd"><samp class="ph codeph">YYYYMMDD</samp> 형식의 보고서 날짜입니다. </dd>
<dt class="pt dlterm">&lt;name&gt;</dt>
<dd class="pd">보고서의 이름입니다. </dd>
</dl>

**팁:** 긴 **ba delete-report** 명령어에 대한
별명으로 **ba dr**을 사용할 수도 있습니다.

### 보고서 검색
{: #admin_retr_report}

보안 보고서를 검색하려면 다음 명령을 사용하십시오. 

```
cf ba retrieve-report <search>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;search&gt;</dt>
<dd class="pd">보고서의 파일 이름입니다. 이름에 공백이 있는 경우 이름을 따옴표 안에
넣으십시오. </dd>
</dl>

**팁:** 긴 **ba retrieve-report** 명령어에 대한 별명으로 **ba rr**을 사용할 수도 있습니다.

## 리소스 메트릭 정보 보기
{: #cliresourceusage}

메모리, 디스크 및 CPU 사용량을 포함하여 리소스 메트릭 정보를 확인할 수 있습니다. 실제 및 예약 리소스의 사용량을 포함하여 사용 가능한 실제 및 예약 리소스의 요약을 볼 수 있습니다. 또한 DEA(Droplet Execution Agent) 및 셀(Diego 아키텍처) 사용량 데이터와 히스토리 메모리 및 디스크 사용량도 볼 수 있습니다. 기본적으로 매주 및 내림차순으로 메모리 및 디스크 사용량의 데이터 히스토리가 표시됩니다. 리소스 메트릭 정보를 보려면 다음 명령을 사용하십시오.

```
cf ba resource-metrics <monthly> <weekly>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;monthly&gt;</dt>
<dd class="pd">한 달에 한 번 메모리 및 디스크 공간의 히스토리 데이터가 표시됩니다.</dd>
<dt class="pt dlterm">&lt;weekly&gt;</dt>
<dd class="pd">한 주에 한 번 메모리 및 디스크 용량의 히스토리 데이터가 표시됩니다. 이는 기본값입니다.</dd>
</dl>

**팁:** 긴 **ba resource-metrics** 명령어의 별명으로
**ba rsm**을 사용할 수도 있습니다. 


## 서비스 브로커 관리
{: #admin_servbro}

### 서비스 브로커 나열
{: #clilistservbro}

서비스 브로커를 나열하려면 다음 명령을 사용하십시오. 

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

### 서비스 브로커 추가
{: #cliaddservbro}

서비스 브로커를 추가하여
{{site.data.keyword.Bluemix_notm}} 카탈로그에 사용자 정의 서비스를 추가하려면 다음 명령을 사용하십시오.

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

### 서비스 브로커 삭제
{: #clidelservbro}

서비스 브로커를 삭제하여 {{site.data.keyword.Bluemix_notm}} 카탈로그에서
사용자 정의 서비스를 제거하려면 다음 명령을 사용하십시오.

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

### 서비스 브로커 업데이트
{: #cliupdservbro}

서비스 브로커를 업데이트하려면 다음 명령을 사용하십시오. 

```
cf ba update-service-broker <broker_name> <user_name> <password> <broker_url>
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

**팁:** 긴 **ba update-service-broker** 명령어에 대한
별명으로 **ba usb**를 사용할 수도 있습니다.


## 애플리케이션 보안 그룹 관리
{: #admin_secgro}

애플리케이션 보안 그룹(ASG)에 대해 작업하려면 로컬 또는 데디케이티드 환경의 전체 액세스 관리자여야 합니다. 환경의 모든 사용자는 명령으로 대상이 되는 조직의 사용 가능한 ASG를 나열할 수 있습니다. 그러나 ASG의 작성, 업데이트 또는 바인드를 수행하려면 {{site.data.keyword.Bluemix_notm}} 환경의 관리자여야 합니다. 

ASG는 {{site.data.keyword.Bluemix_notm}} 환경에서 애플리케이션의 아웃바운드 트래픽을 제어하는 가상 방화벽 역할을 합니다. 각 ASG는 네트워크 안팎으로 특정 트래픽과 통신을 허용하는 규칙의 목록으로 구성됩니다. 하나 이상의 ASG를 특정 보안 그룹 세트(예: 글로벌 액세스를 적용하는 데 사용되는 그룹 세트)에 바인딩하거나 {{site.data.keyword.Bluemix_notm}} 환경에서 조직 내의 영역에 바인딩할 수 있습니다. 

{{site.data.keyword.Bluemix_notm}}는 처음에 외부 네트워크에 대한 모든 액세스가 제한된 상태로 설정됩니다. IBM에서 작성한 두 보안 그룹(`public_networks`, `dns`)을 사용하면 이들 그룹을 기본 Cloud Foundry 보안 그룹 세트에 바인딩할 때 외부 네트워크에 대한 글로벌 액세스가 가능합니다. 글로벌 액세스를 적용하는 데 사용되는 Cloud Foundry의 두 보안 그룹 세트는 **기본 스테이징** 그룹 세트와 **기본 실행** 그룹 세트입니다. 이 그룹 세트는 모든 실행 중인 앱 또는 모든 스테이징 앱에 대한 트래픽을 허용하는 규칙을 적용합니다. 이 두 개의 보안 그룹 세트에 바인딩하지 않으려면 Cloud Foundry 그룹 세트에서 바인드를 해제한 후 특정 영역에 보안 그룹을 바인딩할 수 있습니다. 자세한 정보는 [애플리케이션 보안 그룹 바인딩 ![외부 링크 아이콘](../../../icons/launch-glyph.svg)](https://docs.cloudfoundry.org/adminguide/app-sec-groups.html#binding-groups){: new_window}을 참조하십시오. 

**참고**: 보안 그룹 관련 작업을 수행할 수 있는 다음 명령은 Cloud Foundry 1.6 버전을 기반으로 합니다. 필수 필드 및 선택 필드를 포함하여 자세한 정보는 [애플리케이션 보안 그룹 작성 ![외부 링크 아이콘](../../../icons/launch-glyph.svg)](https://docs.cloudfoundry.org/adminguide/app-sec-groups.html#creating-groups){: new_window}에 대한 Cloud Foundry 정보를 참조하십시오. 

### 보안 그룹 나열
{: #clilissecgro}

* 보안 그룹을 모두 나열하려면 다음 명령을 사용하십시오. 

```
cf ba security-groups
```
{: codeblock}

**팁:** 긴 **ba security-groups** 명령어의 별명으로
**ba sgs**를 사용할 수도 있습니다. 

* 특정 보안 그룹에 대한 세부사항을 표시하려면 다음 명령을 사용하십시오.

```
cf ba security-groups <security-group>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Security group&gt;</dt>
<dd class="pd">보안 그룹의 이름</dd>
</dl>

**팁:** `security-group` 매개변수가 있는 긴 **ba security-groups**
명령어의 별명으로 **ba sg**를 사용할 수도 있습니다. 


### 보안 그룹 작성
{: #clicreasecgro}

보안 그룹 및 출력 트래픽을 정의하는 규칙 작성에 대한 자세한 정보는 [애플리케이션 보안 그룹 작성 ![외부 링크 아이콘](../../../icons/launch-glyph.svg)](https://docs.cloudfoundry.org/adminguide/app-sec-groups.html#creating-groups){: new_window}을 참조하십시오. 

보안 그룹을 작성하려면 다음 명령을 사용하십시오. 

```
cf ba create-security-group <security-group> <path-to-rules-file>
```
{: codeblock}

작성하는 각 보안 그룹의 이름에 접두부 `adminconsole_`이 추가되어 IBM에서 작성한 보안 그룹과 구별됩니다. 

<dl class="parml">
<dt class="pt dlterm">&lt;Security group&gt;</dt>
<dd class="pd">보안 그룹의 이름</dd>
<dt class="pt dlterm">&lt;Path to rules file&gt;</dt>
<dd class="pd">규칙 파일의 절대 또는 상대 경로</dd>
</dl>

**팁:** 긴 **ba create-security-group** 명령어의
별명으로 **ba csg**를 사용할 수도 있습니다. 

### 보안 그룹 업데이트
{: #cliupdsecgro}

보안 그룹을 업데이트하려면 다음 명령을 사용하십시오. 

```
cf ba update-security-group <security-group> <path-to-rules-file>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Security group&gt;</dt>
<dd class="pd">보안 그룹의 이름</dd>
<dt class="pt dlterm">&lt;Path to rules file&gt;</dt>
<dd class="pd">규칙 파일의 절대 또는 상대 경로</dd>
</dl>

**팁:** 긴 **ba update-security-group** 명령어의
별명으로 **ba usg**를 사용할 수도 있습니다. 

### 보안 그룹 삭제
{: #clidelsecgro}

보안 그룹을 삭제하려면 다음 명령을 사용하십시오. 

```
cf ba delete-security-group <security-group>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Security group&gt;</dt>
<dd class="pd">보안 그룹의 이름</dd>
</dl>

**팁:** 긴 **ba delete-security-group** 명령어의
별명으로 **ba dsg**를 사용할 수도 있습니다. 


### 보안 그룹 바인딩
{: #clibindsecgro}

보안 그룹 바인딩에 대한 자세한 정보는 [애플리케이션 보안 그룹 바인딩 ![외부 링크 아이콘](../../../icons/launch-glyph.svg)](https://docs.cloudfoundry.org/adminguide/app-sec-groups.html#binding-groups){: new_window}을 참조하십시오. 

* 기본 스테이징 보안 그룹 세트를 바인드하려면 다음 명령을 사용하십시오.

```
cf ba bind-staging-security-group <security-group>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Security group&gt;</dt>
<dd class="pd">보안 그룹의 이름</dd>
</dl>

**팁:** 긴 **ba bind-staging-security-group** 명령어의
별명으로 **ba bssg**를 사용할 수도 있습니다. 

* 기본 실행 보안 그룹 세트를 바인드하려면 다음 명령을 사용하십시오.

```
cf ba bind-running-security-group <security-group>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Security group&gt;</dt>
<dd class="pd">보안 그룹의 이름</dd>
</dl>

**팁:** 긴 **ba bind-running-security-group** 명령어의
별명으로 **ba brsg**를 사용할 수도 있습니다. 

* 보안 그룹을 영역에 바인드하려면 다음 명령을 사용하십시오. 

```
cf ba bind-security-group <security-group> <org> <space>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Security group&gt;</dt>
<dd class="pd">보안 그룹의 이름</dd>
<dt class="pt dlterm">&lt;Org&gt;</dt>
<dd class="pd">보안 그룹을 바인딩할 대상 조직의 이름</dd>
<dt class="pt dlterm">&lt;Space&gt;</dt>
<dd class="pd">보안 그룹을 바인딩할 대상 조직 내의 영역 이름</dd>
</dl>

**팁:** 긴 **ba bind-security-group** 명령어의
별명으로 **ba bsg**를 사용할 수도 있습니다. 

### 보안 그룹 바인드 해제
{: #cliunbindsecgro}

보안 그룹 바인딩 해제에 대한 자세한 정보는 [애플리케이션 보안 그룹 바인딩 해제 ![외부 링크 아이콘](../../../icons/launch-glyph.svg)](https://docs.cloudfoundry.org/adminguide/app-sec-groups.html#unbinding-groups){: new_window}를 참조하십시오. 

* 기본 스테이징 보안 그룹 세트에서 바인드 해제하려면 다음 명령을 사용하십시오.

```
cf ba unbind-staging-security-group <security-group>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Security group&gt;</dt>
<dd class="pd">보안 그룹의 이름</dd>
</dl>

**팁:** 긴 **ba unbind-staging-security-group** 명령어의
별명으로 **ba ussg**를 사용할 수도 있습니다. 

* 기본 실행 보안 그룹 세트에서 바인드 해제하려면 다음 명령을 사용하십시오.

```
cf ba unbind-running-security-group <security-group>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Security group&gt;</dt>
<dd class="pd">보안 그룹의 이름</dd>
</dl>

**팁:** 긴 **ba bind-running-security-group** 명령어의
별명으로 **ba brsg**를 사용할 수도 있습니다. 

* 보안 그룹을 영역에서 바인드 해제하려면 다음 명령을 사용하십시오. 

```
cf ba unbind-security-group <security-group> <org> <space>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Security group&gt;</dt>
<dd class="pd">보안 그룹의 이름</dd>
<dt class="pt dlterm">&lt;Org&gt;</dt>
<dd class="pd">보안 그룹을 바인딩할 대상 조직의 이름</dd>
<dt class="pt dlterm">&lt;Space&gt;</dt>
<dd class="pd">보안 그룹을 바인딩할 대상 조직 내의 영역 이름</dd>
</dl>

**팁:** 긴 **ba unbind-staging-security-group** 명령어의
별명으로 **ba usg**를 사용할 수도 있습니다. 

## 빌드팩 관리
{: #admin_buildpack}

### 빌드팩 나열
{: #clilistbuildpack}

앱 카탈로그 쓰기 권한이 있는 경우, 빌드팩을 나열할 수 있습니다. 모든 빌드팩을 나열하거나 특정 빌드팩을 보려면 다음 명령을 사용하십시오.

```
cf ba buildpacks <buildpack_name>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;buildpack_name&gt;</dt>
<dd class="pd">보기 위한 특정 빌드팩을 지정하는 선택적 매개변수입니다.</dd>
</dl>

**팁:** 긴 **ba buildpacks** 명령어의
별명으로 **ba lb**를 사용할 수도 있습니다. 

### 빌드팩 작성 및 업로드
{: #clicreupbuildpack}

앱 카탈로그 쓰기 권한이 있는 경우, 빌드팩을 작성 및 업로드할 수 있습니다. .zip 파일 유형이 있는 압축된 파일을 업로드할 수 있습니다. 빌드팩을 업로드하려면 다음 명령을 사용하십시오. 

```
cf ba create-buildpack <buildpack_name> <file_path> <position>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;buildpack_name&gt;</dt>
<dd class="pd">업로드할 빌드팩의 이름입니다.</dd>
<dt class="pt dlterm">&lt;file_path&gt;</dt>
<dd class="pd">빌드팩 압축 파일의 경로입니다.</dd>
<dt class="pt dlterm">&lt;position&gt;</dt>
<dd class="pd">빌드팩 자동 삭제 중에 빌드팩이 선택되는 순서입니다.</dd>
</dl>

**팁:** 긴 **ba create-buildpack** 명령어의
별명으로 **ba cb**를 사용할 수도 있습니다. 

### 빌드팩 업데이트
{: #cliupdabuildpack}

앱 카탈로그 쓰기 권한이 있는 경우, 기존 빌드팩을 업데이트할 수 있습니다. 빌드팩을 업데이트하려면 다음 명령을 사용하십시오. 

```
cf ba update-buildpack <buildpack_name> <position> <enabled> <locked>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;buildpack_name&gt;</dt>
<dd class="pd">업데이트할 빌드팩의 이름입니다.</dd>
<dt class="pt dlterm">&lt;position&gt;</dt>
<dd class="pd">빌드팩 자동 삭제 중에 빌드팩이 선택되는 순서입니다.</dd>
<dt class="pt dlterm">&lt;enabled&gt;</dt>
<dd class="pd">빌드팩이 스테이징에 사용되는지를 표시합니다.</dd>
<dt class="pt dlterm">&lt;locked&gt;</dt>
<dd class="pd">업데이트를 방지하기 위해 빌드팩이 잠기는지를 표시합니다.</dd>
</dl>

**팁:** 긴 **ba update-buildpack** 명령어의
별명으로 **ba ub**를 사용할 수도 있습니다. 

### 빌드팩 삭제
{: #clidelbuildpack}

앱 카탈로그 쓰기 권한이 있는 경우, 기존 빌드팩을 삭제할 수 있습니다. 빌드팩을 삭제하려면 다음 명령을 사용하십시오. 

```
cf ba delete-buildpack <buildpack_name>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;buildpack_name&gt;</dt>
<dd class="pd">삭제할 빌드팩의 이름입니다.</dd>
</dl>

**팁:** 긴 **ba delete-buildpack** 명령어의
별명으로 **ba db**를 사용할 수도 있습니다. 
