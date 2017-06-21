---



copyright:

  years: 2015, 2017

lastupdated: "2017-04-19"



---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# 애플리케이션 업로드

{{site.data.keyword.Bluemix}}에 로그인한 후 `bluemix app push` 명령을 사용하여 애플리케이션을 업로드할 수 있습니다.
{:shortdesc}

시작하기 전에 다음을 수행해야 합니다.
  1. {{site.data.keyword.Bluemix}} 명령행 인터페이스를 설치하십시오.

  <a class="xref" href="http://clis.ng.bluemix.net/ui/home.html" target="_blank" title="(새 탭 또는 창에서 열림)"><img class="image" src="images/btn_bx_commandline.svg" alt="{{site.data.keyword.Bluemix}} 명령행 인터페이스 다운로드" /> </a>

  2. {{site.data.keyword.Bluemix}}에 연결하십시오.

  <pre class="pre"><code class="hljs">bluemix api https://api.<span class="keyword" data-hd-keyref="DomainName">DomainName</span></code></pre>

  3. {{site.data.keyword.Bluemix_notm}}에 로그인하십시오.

  <pre class="pre"><code class="hljs">bluemix login -u <var class="keyword varname" data-hd-keyref="user_ID">username</var> -o <var class="keyword varname" data-hd-keyref="org_name">org_name</var> -s <var class="keyword varname" data-hd-keyref="space_name">space_name</var></code></pre>

**bluemix app push** 명령이 실행되면 명령행 인터페이스는 빌드팩을 사용하여 애플리케이션을 빌드하고 실행하는 {{site.data.keyword.Bluemix_notm}} 환경에 작업 디렉토리를 제공합니다.

  1. 애플리케이션 디렉토리에서 애플리케이션 이름을 사용하여 **bluemix app push** 명령을 입력하십시오. 앱 이름은 {{site.data.keyword.Bluemix_notm}} 환경에서 고유해야 합니다. 

  <pre class="pre"><code class="hljs">bluemix app push <var class="keyword varname" data-hd-keyref="app_name">app_name</var> -m 512m</code></pre>

  {{site.data.keyword.Bluemix_notm}}에는 기본 제공 빌드팩이 포함됩니다. 일부 경우에는 기본 제공 빌드팩에 대해서도 -c 옵션을 제공하여 애플리케이션을 시작하는 데 사용되는 명령을 지정해야 합니다. 예를 들어, Node.js 애플리케이션을 푸시하려면 -c 옵션을 사용해야 합니다.

  <pre class="pre"><code class="hljs">bluemix app push <var class="keyword varname" data-hd-keyref="app_name">app_name</var> -c start_command</code></pre>

  또한 Node.js 애플리케이션에 유효한 package.json 파일이 포함되어야 합니다.

  모든 기타 외부 빌드팩은 -b 옵션을 사용하여 푸시해야 합니다. 예를 들어, 다음과 같습니다. 

  <pre class="pre"><code class="hljs">bluemix app push <var class="keyword varname" data-hd-keyref="app_name">app_name</var> -b buildpack_URL</code></pre>

  **팁:** **bluemix app push** 명령을 사용하면 명령이 현재 디렉토리에서 Bluemix로 모든 파일 및 디렉토리를 복사합니다. 애플리케이션 디렉토리에 필요한 파일만 있는지 확인하십시오.


  2. 애플리케이션을 변경하는 경우 `bluemix app push` 명령을 다시 입력하여 해당 변경사항을 업로드할 수 있습니다. 명령은 이전 옵션 및 프롬프트에 대한 사용자 응답을 사용하여 새 코드 비트로 애플리케이션의 실행 중인 인스턴스를 업데이트합니다.

{{site.data.keyword.Bluemix}} CLI가 해당 설치에서 cf cli를 번들화했습니다. `bluemix app push` 명령은 실제로 `cf push`를 호출하여 애플리케이션을 {{site.data.keyword.Bluemix_notm}}에 업로드하고 배치합니다. cf push에 대한 자세한 정보는 [cf 명령](/docs/cli/reference/cfcommands/index.html)을 참조하십시오. 빌드팩에 대한 정보는 [커뮤니티 빌드팩 사용](/docs/cfapps/byob.html)을 참조하십시오.
