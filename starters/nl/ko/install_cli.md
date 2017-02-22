---



copyright:

  years: 2015，2017

lastupdated: "2017-01-12"


---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:prereq: .prereq}
{:download: .download}
{:pre: .pre}
{:app_name: data-hd-keyref="app_name"}
{:app_key: data-hd-keyref="app_key"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:host: data-hd-keyref="host"}
{:org_name: data-hd-keyref="org_name"}
{:route: data-hd-keyref="route"}
{:space_name: data-hd-keyref="space_name"}
{:service_name: data-hd-keyref="service_name"}
{:service_instance_name: data-hd-keyref="service_instance_name"}
{:user_ID: data-hd-keyref="user_ID"}

# 명령행 인터페이스를 사용하여 Cloud Foundry 앱 다운로드, 수정 및 재배치

Cloud Foundry 명령행 인터페이스를 사용하여 Cloud Foundry 애플리케이션 및 서비스 인스턴스를 다운로드, 수정 및 재배치하십시오.
{:shortdesc}

시작하기 전에 Cloud Foundry 명령행 인터페이스를 다운로드하여 설치하십시오.  

<p>
<a class="xref" href="https://github.com/cloudfoundry/cli/releases" target="_blank" title="(새 탭 또는 창에서 열림)"><img class="image" src="images/btn_cf_commandline.svg" alt="Cloud Foundry 명령행 인터페이스 다운로드" /> </a>
</p>

**제한사항:** 명령행 도구는 Cygwin에서 지원되지 않습니다. Cygwin 명령행 창 이외의 명령행 창에서 도구를 사용하십시오.
{:prereq}

명령행 인터페이스를 설치한 후 시작할 수 있습니다. 

  1. {: download} 앱에 대한 코드를 새 디렉토리에 다운로드하여 개발 환경을 설정하십시오. 
  
    <a class="xref" href="http://bluemix.net" target="_blank" title="(새 탭 또는 창에서 열림)"><img class="image" src="images/btn_starter-code.svg" alt="애플리케이션 코드 다운로드" /> </a>

  2. 코드가 있는 디렉토리로 변경하십시오. 

  <pre class="pre">cd <var class="keyword varname">your_new_directory</var></pre>

  3.  앱 코드를 적절히 변경하십시오. 예를 들어, {{site.data.keyword.Bluemix}} 샘플 애플리케이션을 사용 중이고 사용자 앱에 `src/main/webapp/index.html` 파일이 포함되어 있는 경우 이를 수정할 수 있으며 새로운 내용을 설명하기 위해 "Thanks for creating ..."을 편집할 수 있습니다. 앱을 {{site.data.keyword.Bluemix_notm}}에 다시 배치하기 전에 로컬로 실행되고 있는지 확인하십시오. 

    `manifest.yml` 파일에 주의하십시오. 앱을 다시 {{site.data.keyword.Bluemix_notm}}에 배치할 때 이 파일이 애플리케이션의 URL, 메모리 할당, 인스턴스 수 및 기타 중요한 매개변수 판별에 사용됩니다. Cloud Foundry 문서에서 [Manifest 파일의 자세한 정보 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html "외부 링크 아이콘"){: new_window}를 확인할 수 있습니다. 

    또한 해당하는 경우 빌드 지시사항과 같은 세부사항이 포함되어 있는 `README.md` 파일도 주의하십시오. 

    참고: 애플리케이션이 Liberty 앱인 경우 재배치 전에 먼저 빌드해야 합니다. 

  4. {{site.data.keyword.Bluemix_notm}}에 연결하고 로그인하십시오. 

  <pre class="pre">cf api https://api.<span class="keyword" data-hd-keyref="DomainName">DomainName</span></pre>

  <pre class="pre">cf login -u <var class="keyword varname" data-hd-keyref="user_ID">username</var> -o <var class="keyword varname" data-hd-keyref="org_name">org_name</var> -s <var class="keyword varname" data-hd-keyref="space_name">space_name</var></pre>

  연합 ID를 사용 중인 경우 `-sso` 옵션을 사용하십시오. 

  <pre class="pre">cf login -u <var class="keyword varname" data-hd-keyref="user_ID">username</var> -o <var class="keyword varname" data-hd-keyref="org_name">org_name</var> -s <var class="keyword varname" data-hd-keyref="space_name">space_name</var> -sso</pre>

  5. <var class="keyword varname">your_new_directory</var>에서 `cf push` 명령을 사용하여 {{site.data.keyword.Bluemix_notm}}에 앱을 재배치하십시오. `cf push` 명령에 대한 자세한 정보는 [애플리케이션 업로드](/docs/starters/upload_app.html)를 참조하십시오. 

  <pre class="pre">cf push <var class="keyword varname" data-hd-keyref="app_name">app_name</var></pre>

  6. https://<var class="keyword varname" data-hd-keyref="app_name">app_name</var>.<span class="keyword" data-hd-keyref="APPDomain">AppDomainName</span>을 브라우징하여 앱에 액세스하십시오. 
