---

 

copyright:

  years: 2015，2016

 

---

{:shortdesc: .shortdesc} 
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#{{site.data.keyword.Bluemix_notm}}에서 앱 호스팅

*마지막 업데이트 날짜: 2016년 5월 9일*

<!--The whole topic is staging only -->

{{site.data.keyword.Bluemix}}에서는 애플리케이션을 작성할 수 있음은 물론 기존 애플리케이션을 호스팅할 수도 있습니다. 클라우드 준비 상태이면, 앱을 {{site.data.keyword.Bluemix_notm}}에 마이그레이션할 수 있습니다. {{site.data.keyword.Bluemix_notm}}에서는 애플리케이션을 실행할 수 있도록 다양한 방법을 제공합니다(예: Cloud Foundry, IBM Containers 및 Virtual Machines).

##앱 클라우드 준비 상태 만들기
{: #cloud-readyapps}

클라우드 준비 애플리케이션은 애플리케이션이 디자인되고 빌드될 때 클라우드 플랫폼 원칙을 따릅니다. 클라우드 준비 애플리케이션은 클라우드 플랫폼에서 제공하는 기능을 사용할 수 있습니다. 

애플리케이션에 다음 원칙이 모두 있는 경우 애플리케이션은 클라우드 준비 상태이며 {{site.data.keyword.Bluemix_notm}}에 마이그레이션할 수 있습니다. 애플리케이션에서 원칙이 위반되는 경우, 일반적으로는 원칙을 고수하도록 애플리케이션을 수정할 수 있습니다. 

* 특정 토폴로지에 직접 애플리케이션을 코딩하지 마십시오. 

  클라우드가 아닌 환경에서는 애플리케이션이 특정 배치 토폴로지를 사용할 수 있습니다. 그러나 애플리케이션 토폴로지는 클라우드 애플리케이션에서 변경될 수 있습니다. 클라우드 준비 애플리케이션 및 서비스가 즉각적 확장성 변경을 허용하기 때문입니다. 확장성 변경사항에는 애플리케이션의 인스턴스 수에 대한 수동 크기 조정 및 동적 스케일링이 포함됩니다. 

  애플리케이션이 확장성 변경사항의 영향을 받지 않도록 하려면, 가급적 애플리케이션을 Stateless 및 일반적이 되도록 빌드하십시오. 

* 로컬 파일 시스템이 영구적이라고 가정하지 마십시오. 

  클라우드에서 애플리케이션 인스턴스를 언제든지 이동, 삭제하거나 복제할 수 있으므로, 파일 시스템에 기록된 파일에 의존하지 마십시오. 애플리케이션이 애플리케이션 로그를 포함하여 빈번하게 사용되는 정보의 캐시로서 로컬 파일 시스템을 사용하는 경우, 인스턴스가 종료되고 다른 위치나 다른 VM에서 다시 시작될 때 해당 정보가 유실됩니다. 

  로컬 파일 시스템 대신 SQL 또는 NoSQL 데이터베이스와 같은 서비스에서 정보를 저장할 수 있습니다. 동적 클라우드 환경에서는 로그가 생성된 애플리케이션 인스턴스보다 오래 생존하는 서비스에서 로그를 사용 가능하게 하는 것도 중요합니다. 

* 애플리케이션의 세션 상태를 저장하지 마십시오. 

  시스템의 상태는 데이터베이스 및 공유 스토리지에 의해 정의되며, 각각의 개별 실행 중인 애플리케이션 인스턴스에 의해 정의되지는 않습니다. 어떤 종류의 Statefulness이건 애플리케이션의 확장성을 제한합니다. 서버의 중앙 집중화된 위치에 이를 저장함으로써 세션 상태의 영향을 최소화하도록 시도하십시오. 

  세션 상태를 완전히 제거할 수 없는 경우에는 애플리케이션 서버 외부의 가용성이 높은 저장소로 이를 푸시하십시오. 저장소에는 IBM WebSphere Extreme Scale, Redis, Memcached 또는 외부 데이터베이스가 포함됩니다. 

* 특정 인프라 종속성을 사용하지 마십시오. 

  이는 여러 Manifestation이 있는 일반 원칙입니다. 예를 들어, 애플리케이션이 사용하는 서비스에 특정 호스트 이름 또는 IP 주소가 할당되었다고 가정하지 마십시오. 서비스가 클라우드 환경에서 재배치되거나 재생성될 수 있으므로, 호스트 이름 및 IP 주소는 변경될 수도 있습니다. 

  환경 특정 종속성을 특성 파일의 세트로 추출하는 것은 개선사항이지만 이는 아직 부적합합니다. 최상의 방법은 외부 서비스 레지스트리를 사용하여 서비스 엔드포인트를 해결하거나, 전체 라우팅 기능을 가상 이름으로 서비스 버스 또는 로드 밸런서로 위임하는 것입니다. 

* 애플리케이션에서 인프라 API를 사용하지 마십시오. 

  인프라 API는 소프트웨어 스택의 여러 다른 계층을 참조할 수 있으므로 애플리케이션의 특정 인프라 API에 의존하는 경우 인프라를 변경하기가 더 어렵습니다. 

  대신 기존의 오픈 소스 또는 상용 제품에 의존하고, 애플리케이션 코드 외부에 있도록 PaaS 계층의 PaaS 솔루션을 남겨둘 수 있습니다. 

* 애매한 프로토콜을 사용하지 마십시오. 

  복원성을 위해 추가 구성이 필요한 애매한 프로토콜은 사용하지 마십시오. 

  표준 프로토콜을 기반으로 하는 애플리케이션은 플랫폼에 위임된 구성 항목으로 보다 복원성이 있습니다. 표준 프로토콜에는 HTTP, SSL, 표준 데이터베이스, 큐잉 및 웹 서비스 연결이 포함됩니다. 

* OS 특정 기능에 의존하지 마십시오. 

  OS 특정 기능을 이미 사용 중인 경우에는 호환성 라이브러리(예: Cygwin 및 Mono)를 사용하여 이 문제를 해결할 수 있습니다. Cygwin은 Windows 환경에서 Linux 도구 세트를 제공하는 호환성 라이브러리입니다. Mono는 Linux에서 Windows .NET 기능을 제공하는 호환성 라이브러리입니다.

  OS 특정 종속성을 피하십시오. 대신 미들웨어 인프라 또는 서비스 제공업체에서 제공하는 서비스를 사용하십시오. 

* 애플리케이션을 수동으로 설치하지 마십시오. 

  애플리케이션은 동적 클라우드 환경에서 자주 요청 시에 설치됩니다. 설치 프로세스는 스크립팅되어 있으면 안정적이어야 하며, 구성 데이터는 스크립트의 외부에 있어야 합니다. 

  최소한, 운영 체제와 무관한 스크립트의 균등 세트로서 애플리케이션 설치를 캡처하십시오. 상이한 자동화 기술에 적용될 수 있도록 애플리케이션 설치를 소형으로 포터블하게 유지하십시오. 또한 애플리케이션 설치에서 필요한 종속성을 최소화하십시오. 

클라우드 준비 애플리케이션에 대한 자세한 정보는 [12-요소 애플리케이션](http://12factor.net/){:new_window}을 참조하십시오. 

##앱 마이그레이션
{: #ht_hostapp}

애플리케이션을 클라우드 환경으로 완전히 이동하는 대신, 증분 방식으로 {{site.data.keyword.Bluemix_notm}}에 애플리케이션을 마이그레이션할 수 있습니다. 우선 애플리케이션의 일부를 마이그레이션한 후에, 클라우드 통합 서비스를 사용하여 기존 데이터 또는 SOR(System of Record)에 연결할 수 있습니다. 

클라우드 애플리케이션에서 백엔드 데이터 또는 서비스에 액세스해야 할 수 있습니다(예: SOR(System of Record)). {{site.data.keyword.Bluemix_notm}}에서는 Secure Gateway 서비스를 사용하여 {{site.data.keyword.Bluemix_notm}} 조직 및 엔터프라이즈 백엔드 네트워크 간의 보안 터널을 설정할 수 있습니다. 이 서비스를 사용하여 {{site.data.keyword.Bluemix_notm}}의 애플리케이션은 백엔드 네트워크의 데이터 및 서비스에 액세스할 수 있습니다. 세부사항은 [콘솔을 통해 Secure Gateway로 엔터프라이즈 백엔드 접속](https://developer.ibm.com/bluemix/2015/04/01/reaching-enterprise-backend-bluemix-secure-gateway/){:new_window}을 참조하십시오.

애플리케이션을 Cloud Foundry 애플리케이션으로서 {{site.data.keyword.Bluemix_notm}}에 배치하려면 {{site.data.keyword.Bluemix_notm}} 카탈로그에서 런타임을 선택하십시오. 런타임에는 자체 애플리케이션과 대체할 수 있는 스타터 Hello World 애플리케이션이 포함되어 있습니다. 원하는 런타임을 제공하는 스타터를 찾을 수 없는 경우에는 cf push 명령에서 –b 옵션을 사용하여 {{site.data.keyword.Bluemix_notm}}로 사용자 정의, Cloud Foundry 호환 가능 빌드팩을 가져올 수 있습니다. 세부사항은 [커뮤니티 빌드팩 사용](../cfapps/byob.html)을 참조하십시오.

{{site.data.keyword.Bluemix_notm}}에서 제공하는 다음의 도구 및 서비스를 사용할 수 있습니다. 

*표 1. {{site.data.keyword.Bluemix_notm}} 도구*

| 도구	| 방법 |
|:------|:--------|
|Cloud Foundry 명령행 인터페이스(cf cli)	|로컬 클라이언트에서 코드를 관리하고 Cloud Foundry 명령행 인터페이스를 사용하여 애플리케이션을 {{site.data.keyword.Bluemix_notm}}에 수동으로 푸시하십시오. 자세한 정보는 [앱 업로드](../starters/upload_app.html)를 참조하십시오. |
|Eclipse	|Eclipse에서 코드를 관리하고 {{site.data.keyword.Bluemix_notm}}용 IBM Eclipse 도구를 사용하여 애플리케이션을 푸시하십시오.|
|Git 통합	|GitHub에서 코드를 관리하고 Git를 {{site.data.keyword.Bluemix_notm}}로 통합하십시오. 다른 개발자과 협업할 수 있습니다. 애플리케이션은 코드의 변경사항을 커미트할 때 {{site.data.keyword.Bluemix_notm}}에 자동으로 배치됩니다. 애플리케이션을 수동으로 푸시할 필요가 없습니다. |
|{{site.data.keyword.Bluemix_notm}} DevOps Delivery Pipeline	|DevOps GitHub 저장소에서 코드를 관리하고 DevOps Delivery Pipeline을 사용하여 애플리케이션을 {{site.data.keyword.Bluemix_notm}}에 배치하십시오. |


Cloud Foundry 플랫폼이 애플리케이션 요구사항을 충족하지 않는 경우에는 보다 사용자 정의된 옵션으로 런타임이 설정, 구성되고 유지보수되는 VM 또는 컨테이너를 사용할 수 있습니다. 

##cf cli를 사용하여 앱 업로드
{: #ht_cfcli}

로컬 클라이언트에서 코드를 관리하고 Cloud Foundry 명령행 인터페이스를 사용하여 애플리케이션을 {{site.data.keyword.Bluemix_notm}}에 수동으로 업로드할 수 있습니다. 코드를 변경하는 경우에는 애플리케이션을 {{site.data.keyword.Bluemix_notm}}에 다시 푸시하여 업데이트된 코드를 실행해야 합니다. 

다음 단계를 수행하여 애플리케이션을 마이그레이션하십시오. 

<ol>
<li>Cloud Foundry 명령행 인터페이스를 설치하십시오. 최신 버전의 cf 명령행 인터페이스를 사용 중인지 확인하십시오. <ol>
<li>운영 체제의 설치 프로그램을 다운로드하십시오. </li>
<li>도구 마법사에 따라 명령행을 설치하십시오. </li>
<li>다음 명령을 사용하여 cf 명령행 인터페이스의 버전을 확인하십시오. <pre>cf -v</pre></li>
</ol>
</li>

<li>선택사항: 애플리케이션을 {{site.data.keyword.Bluemix_notm}}에 푸시하기 전에 배치 세부사항을 지정하고 저장하려는 경우에는 다음 단계를 수행하여 애플리케이션 Manifest를 추가할 수 있습니다.
<ol>
<li>애플리케이션의 작업 디렉토리로 이동하고 이름이 manifest.yml(기본 이름)인 파일을 작성하십시오.</li>
<li>Manifest 파일에서 배치 세부사항을 지정하십시오. 다음 예는 Java™ 애플리케이션에 대한 Manifest 파일을 표시합니다.
<pre class="pre codeblock"><code>applications:
- disk_quota: 1024M
  host: myjavatest
  name: MyJavaTest
  path: webStarterApp.war
  domain: mybluemix.net
  instances: 1
  memory: 512M</code></pre>
<p>이 파일에서 사용할 수 있는 지원 옵션에 대한 자세한 정보는 [애플리케이션 Manifest](../manageapps/depapps.html#appmanifest)를 참조하십시오. </p></li></ol>
</li>

<li>애플리케이션을 푸시하십시오. cf push 명령을 사용하여 애플리케이션을 업로드할 수 있습니다.
<ol>
<li>다음 명령을 실행하여 {{site.data.keyword.Bluemix_notm}}에 연결하고 로그인하십시오. 프롬프트가 나타나면 조직 및 영역을 선택하십시오.
<pre>cf login -a https://api.ng.bluemix.net</pre></li>
<li>애플리케이션 디렉토리에서 애플리케이션 이름과 함께 cf push 명령을 입력하십시오. 애플리케이션 이름은 {{site.data.keyword.Bluemix_notm}} 환경에서 고유해야 합니다.
<pre>cf push appname</pre></li>
<li>선택사항: 외부 빌드팩을 사용 중인 경우에는 cf push 명령에서 -b 옵션을 사용해야 합니다. 예:
<pre>cf push appname -b buildpack_URL</pre>
<p>세부사항은 커뮤니티 빌드팩 사용을 참조하십시오. </p>
</li></ol>
</li>

<li>선택사항: 애플리케이션을 변경하는 경우에는 cf push 명령을 다시 입력하여 해당 변경사항을 업로드해야 합니다. cf 명령행 인터페이스는 이전 옵션 및 프롬프트에 대한 사용자 응답을 사용하여 새 코드 비트로 애플리케이션의 실행 중인 인스턴스를 업데이트합니다. </li>
</ol>

**참고:**

* cf push 명령을 사용하는 경우에는 cf 명령행 인터페이스가 현재 디렉토리의 모든 파일 및 디렉토리를 {{site.data.keyword.Bluemix_notm}}에 복사합니다. 애플리케이션 디렉토리에 필요한 파일만 있는지 확인하십시오.
* 애플리케이션의 모든 인스턴스에 대해 조직에 충분한 메모리가 있는지 확인하십시오. 사용자 조직의 메모리 할당량을 보려면 cf org org_name을 사용하십시오.
* cf push에 대한 자세한 정보는 [cf commands](../cli/reference/cfcommands/index.html) 명령을 참조하십시오.

##데이터 마이그레이션 및 서비스 사용
{: #ht_service}

{{site.data.keyword.Bluemix_notm}}에 애플리케이션을 업로드한 후에는 {{site.data.keyword.Bluemix_notm}} 카탈로그에서 애플리케이션이 연결된 서비스를 선택하고 서비스 인스턴스를 작성하며 인스턴스를 애플리케이션에 바인드한 후에 애플리케이션을 다시 시작하십시오. 

애플리케이션의 VCAP_SERVICES 환경 변수는 {{site.data.keyword.Bluemix_notm}}의 서비스 인스턴스와 상호작용하는 방법에 대한 정보가 포함된 JSON 오브젝트입니다. 이 정보에는 서비스 인스턴스 이름, 신임 정보 및 서비스 인스턴스에 대한 연결 URL이 포함됩니다. 

{{site.data.keyword.Bluemix_notm}}에서 코드를 실행하려면, 서비스 연결에 대한 정보를 가져올 수 있도록 VCAP_SERVICES 변수를 구문 분석하기 위한 코드 로직을 추가해야 합니다. 환경 변수를 통해 서비스 인스턴스의 동적 지정된 호스트 및 포트를 가져올 수 있도록 애플리케이션을 수정하십시오. 다음 예는 Ruby 애플리케이션에서 Postgre SQL 서비스 인스턴스의 신임 정보를 가져오는 방법을 표시합니다. 

```
services = JSON.parse(ENV['VCAP_SERVICES'], :symbolize_names => true)

        url = services.values.map do |srvs|
          srvs.map do |srv|
            if srv[:credentials][:uri] =~ /^postgres/
              srv[:credentials][:uri]
            else
              []
            end
          end
        end.flatten!.first
```		
{:codeblock}

{{site.data.keyword.Bluemix_notm}}용 애플리케이션을 수정한 후에 애플리케이션이 로컬 환경에서 실행될 수 있도록 보장하려면, 모든 {{site.data.keyword.Bluemix_notm}} Cloud Foundry 애플리케이션에 대해 설정된 VCAP_SERVICES 환경 변수가 존재하는지 확인하십시오. 


# 관련 링크
{: #rellinks}

## 관련 링크
{: #general}

* [IBM Containers](../containers/container_cli_ov.html)
* [가상 머신](../virtualmachines/vm_index.html)
* [Delivery Pipeline 시작하기](../services/DeliveryPipeline/index.html)
* [IBM Eclipse Tools for Bluemix를 사용하여 앱 배치](../manageapps/eclipsetools/eclipsetools.html)
* [12-요소 앱](http://12factor.net/){:new_window}
* [콘솔을 통해 Bluemix Secure Gateway로 엔터프라이즈 백엔드 접속](https://developer.ibm.com/bluemix/2015/04/01/reaching-enterprise-backend-bluemix-secure-gateway/){:new_window}
