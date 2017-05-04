---



copyright:

  years: 2015，2017

lastupdated: "2017-01-12"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# CLI 및 개발 도구
{: #cli}

{{site.data.keyword.Bluemix_short}}를 통해 통합 명령행 인터페이스 및 CLI 플러그인과 같은 강력한 도구를 이용할 수 있습니다. 각각의 CLI를 다운로드하여 {{site.data.keyword.Bluemix_notm}} 인터페이스에 사용 가능합니다.
{:shortdesc}

## ![](./images/CLI.svg) 명령행 인터페이스
{: #downloads}

{{site.data.keyword.Bluemix_notm}} 인터페이스를 지원하는 명령행 인터페이스를 다운로드하여 설치하십시오. 

Cloud Foundry cf 명령행 도구는 모든 {{site.data.keyword.Bluemix_notm}} CLI 도구의 전제 조건입니다. {{site.data.keyword.Bluemix_notm}} 명령행 도구는 Cloud Foundry 애플리케이션 이외에 {{site.data.keyword.Bluemix_notm}} 환경을 관리하는 확장된 경험을 제공합니다.

두 CLI 도구는 모두 기본적으로 443 포트를 사용합니다. CLI 도구 및 {{site.data.keyword.Bluemix_notm}} 환경 간에 HTTP 프록시가 있는 경우에는 실제 HTTP 프록시 url 및 포트(있는 경우)로 `http-proxy` 환경 변수를 구성해야 합니다. 세부사항은 [Using the CLI with an HTTP Proxy Server ![외부 링크 아이콘](../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/cf-cli/http-proxy.html){: new_window}를 참조하십시오. 


| *{{site.data.keyword.Bluemix_notm}}: bx* | *Cloud Foundry: cf* |
|---------------------|---------------|
| [CLI 다운로드](http://clis.ng.bluemix.net/)  <br> [문서 보기](/docs/cli/reference/bluemix_cli/index.html)|  [CLI 다운로드 ![외부 링크 아이콘](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/cli/releases){: new_window}  <br> [문서 보기](/docs/cli/reference/cfcommands/index.html) |
{: caption="표 1. CLI 다운로드" caption-side="top"}


## ![](./images/CLI_Plugin.svg) 명령행 인터페이스 플러그인

더 많은 명령으로 {{site.data.keyword.Bluemix_notm}} 명령행 인터페이스를 간편하게 확장합니다. {{site.data.keyword.Bluemix_notm}} 명령행 인터페이스 플러그인에 액세스하려면 [CLI 플러그인 저장소![외부 링크 아이콘](../icons/launch-glyph.svg)](https://plugins.ng.bluemix.net/)를 참조하십시오. 

### {{site.data.keyword.Bluemix_notm}} 명령행 인터페이스 확장: bx
{: cli_bluemix_ext}

* {{site.data.keyword.Bluemix_notm}} 레지스트리에서 {{site.data.keyword.Bluemix_notm}} CLI 플러그인을 설치하려면 플러그인 레지스트리 엔드포인트를 설정하십시오. 

```
bluemix plugin repo-add bluemix-bx https://plugins.ng.bluemix.net
```
{: codeblock}

* 그런 다음, 다음 명령을 실행하여 플러그인을 설치하십시오.

```
bluemix plugin install plugin_name -r bluemix-bx
```
{: codeblock}


| *{{site.data.keyword.activedeployshort}} CLI* | *{{site.data.keyword.autoscaling}} CLI* | *IBM Bluemix 컨테이너 서비스*  |
|-----|-----|-----|
| 플러그인 이름: active-deploy<br> [문서 보기](/docs/services/ActiveDeploy/cli.html#cli) | 플러그인 이름: auto-scaling <br> [문서 보기](/docs/cli/plugins/auto-scaling/index.html) |  플러그인 이름: container-service  <br> [문서 보기](/docs/containers/cs_cli_devtools.html) |
{: caption="표 2. 플러그인" caption-side="top"}

|  *사설 네트워크 피어링* | *VPN*  |
|-----|-----|
| 플러그인 이름: private-network-peering  <br> [문서 보기](/docs/cli/plugins/pnp/index.html) |플러그인 이름: VPN <br> [문서 보기](/docs/cli/plugins/bx_vpn/index.html) |
{: caption="표 3. 플러그인" caption-side="top"}


### Cloud Foundry 명령행 인터페이스 확장: cf
{: cli_cf_ext}

* {{site.data.keyword.Bluemix_notm}} 레지스트리에서 cf CLI 플러그인을 설치하려면 플러그인 레지스트리 엔드포인트를 설정하십시오. 

```
cf add-plugin-repo bluemix-cf https://plugins.ng.bluemix.net
```
{: codeblock}

* 그런 다음, 다음 명령을 실행하여 플러그인을 설치하십시오.

```
cf install-plugin plugin_name -r bluemix-cf
```
{: codeblock}


| *Active Deploy* | *관리 콘솔* |
|-----------------|-----------------|
| 플러그인 이름: active-deploy<br>  [문서 보기](/docs/services/ActiveDeploy/cli.html#cli) |  플러그인 이름: bluemix-admin<br> [문서 보기](/docs/cli/plugins/bluemix_admin/index.html) |
{: caption="표 4. 플러그인" caption-side="top"}


| *{{site.data.keyword.IBM}} Containers for {{site.data.keyword.Bluemix_notm}}* | *VPN* |
|-----------------|-----------------|
| 플러그인 이름: ibm-containers<br> [문서 보기](https://www.{DomainName}/docs/containers/container_cli_cfic.html#container_cli_cfic) | 플러그인 이름: VPN <br> [문서 보기](/docs/cli/plugins/vpn/index.html) |
{: caption="표 5. 플러그인" caption-side="top"}


## ![](./images/Integrated_Dev_Tools.svg) 통합 개발 도구

즐겨찾기 {{site.data.keyword.Bluemix_notm}} 서비스를 통합하기 위해 플러그인을 다운로드하고 설치합니다.

| *{{site.data.keyword.jazzhub_short}}* | *Liberty for Java* | *MobileFirst* | *{{site.data.keyword.rules_short}}* | *Eclipse Tools for Bluemix* |
|-------------|----------|----------|----------|----------|
| [Egit Eclipse 플러그인 ![외부 링크 아이콘](../icons/launch-glyph.svg)](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_egit){: new_window} <br> [RTC Eclipse 플러그인 ![외부 링크 아이콘](../icons/launch-glyph.svg)](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_rtc){: new_window} | [Liberty Eclipse 플러그인 ![외부 링크 아이콘](../icons/launch-glyph.svg)](https://developer.ibm.com/wasdev/downloads/liberty-profile-using-eclipse/){: new_window} | [Eclipse 플러그인 ![외부 링크 아이콘](../icons/launch-glyph.svg)](https://marketplace.eclipse.org/content/ibm-mobilefirst-platform-studio){: new_window} | [Rules Designer Eclipse 플러그인 ![외부 링크 아이콘](../icons/launch-glyph.svg)](/docs/services/rules/index.html#rulov002) | [Bluemix Eclipse 플러그인 ![외부 링크 아이콘](../icons/launch-glyph.svg)](https://console.ng.bluemix.net/docs/manageapps/eclipsetools/eclipsetools.html){: new_window} |
{: caption="표 6. 플러그인" caption-side="top"}
