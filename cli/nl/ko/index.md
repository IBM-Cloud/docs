---



copyright:

  years: 2015, 2017

lastupdated: "2017-02-14"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# 다운로드
{: #cli}

{{site.data.keyword.Bluemix_short}}를 통해 통합 명령행 인터페이스 및 CLI 플러그인과 같은 강력한 도구를 이용할 수 있습니다. 각각의 CLI를 다운로드하여 {{site.data.keyword.Bluemix_notm}} 인터페이스에 사용 가능합니다.
{:shortdesc}

## ![](./images/CLI.svg) 명령행 인터페이스
{: #downloads notoc}

명령행 도구를 다운로드하고 설치하여 {{site.data.keyword.Bluemix_notm}} 경험을 지원하십시오.

{{site.data.keyword.Bluemix_notm}} CLI는 명령행 경험을 제공하여 {{site.data.keyword.Bluemix_notm}} 환경을 관리합니다. 또한 Cloud Foundry 애플리케이션 및 서비스 관리를 위해 Cloud Foundry 명령행 인터페이스 cf를 설치에 포함합니다. 

두 CLI 도구는 모두 기본적으로 443 포트를 사용합니다. CLI 도구 및 {{site.data.keyword.Bluemix_notm}} 환경 간에 HTTP 프록시가 있는 경우에는 실제 HTTP 프록시 url 및 포트(있는 경우)로 `HTTP_PROXY` 환경 변수를 구성해야 합니다. 세부사항은 [Using the CLI with an HTTP Proxy Server ![외부 링크 아이콘](../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/cf-cli/http-proxy.html){: new_window}를 참조하십시오. 

[{{site.data.keyword.Bluemix_notm}} CLI 다운로드 ![외부 링크 아이콘](../icons/launch-glyph.svg)](http://clis.ng.bluemix.net/){: new_window} <br> 
[문서 보기](/docs/cli/reference/bluemix_cli/index.html)

## ![](./images/CLI_Plugin.svg) 명령행 인터페이스 플러그인
{: #cliplugins notoc}

더 많은 명령으로 {{site.data.keyword.Bluemix_notm}} 명령행 인터페이스를 간편하게 확장합니다. {{site.data.keyword.Bluemix_notm}} 명령행 인터페이스 플러그인에 액세스하려면 [CLI 플러그인 저장소![외부 링크 아이콘](../icons/launch-glyph.svg)](https://plugins.ng.bluemix.net/){: new_window}를 참조하십시오. 

### {{site.data.keyword.Bluemix_notm}} 명령행 인터페이스 확장: bx
{: #cli_bluemix_ext notoc}


{{site.data.keyword.Bluemix_notm}} cli 도구를 설치하면 [CLI 플러그인 저장소 ![외부 링크 아이콘](../icons/launch-glyph.svg)](https://plugins.ng.bluemix.net/){: new_window}가 기본적으로 저장소 별명 `Bluemix`로 미리 구성됩니다. 사용 가능한 플러그인을 직접 설치할 수 있습니다.

```
bluemix plugin install plugin_name -r Bluemix
```

| *{{site.data.keyword.activedeployshort}} CLI* | *{{site.data.keyword.autoscaling}} CLI* | *IBM Bluemix 컨테이너 서비스*  |
|-----|-----|-----|
| 플러그인 이름: active-deploy<br> [문서 보기](/docs/services/ActiveDeploy/cli.html#cli) | 플러그인 이름: auto-scaling <br> [문서 보기](/docs/cli/plugins/auto-scaling/index.html) | 플러그인 이름: container-service  <br> [문서 보기](/docs/containers/cs_cli_devtools.html) |
{: caption="표 2. 플러그인" caption-side="top"}

|  *사설 네트워크 피어링* | *VPN*  |
|-----|-----|
| 플러그인 이름: private-network-peering  <br> [문서 보기](/docs/cli/plugins/pnp/index.html) | 플러그인 이름: VPN <br> [문서 보기](/docs/cli/plugins/bx_vpn/index.html) |
{: caption="표 3. 플러그인" caption-side="top"}

또한 {{site.data.keyword.Bluemix_notm}} cli 아키텍처를 준수하는 기타 저장소에서 플러그인을 추가할 수 있습니다.
1. 다른 저장소에서 {{site.data.keyword.Bluemix_notm}} CLI 플러그인을 설치하려면 플러그인 레지스트리 엔드포인트를 설정하십시오.
```
bluemix plugin repo-add bluemix-other-repo [repo_url]
```
여기서 `repo_url`은 플러그인 저장소의 https url입니다.

2. 다음 명령을 실행하여 플러그인을 설치하십시오.
```
bluemix plugin install plugin_name -r bluemix-other-repo
```


### Cloud Foundry 명령행 인터페이스 확장: bx cf
{: #cli_cf_ext notoc}

{{site.data.keyword.Bluemix_notm}} 명령행 도구를 설치하면 Cloud Foundry 명령행 인터페이스도 Bluemix CLI 디렉토리에 설치됩니다. `bluemix cf`를 사용하여 Cloud Foundry CLI 명령을 실행하십시오.

* {{site.data.keyword.Bluemix_notm}} 레지스트리에서 cf CLI 플러그인을 설치하려면 플러그인 레지스트리 엔드포인트를 설정하십시오. 

```
bluemix cf add-plugin-repo bluemix-cf-repo https://plugins.ng.bluemix.net
```
{: codeblock}

* 그런 다음, 다음 명령을 실행하여 플러그인을 설치하십시오.

```
bluemix cf install-plugin plugin_name -r bluemix-cf-repo
```
{: codeblock}

| *Active Deploy* | *관리 콘솔* |
|-----------------|-----------------|
| 플러그인 이름: active-deploy<br>  [문서 보기](/docs/services/ActiveDeploy/cli.html#cli) |  플러그인 이름: bluemix-admin<br> [문서 보기](/docs/cli/plugins/bluemix_admin/index.html) |
{: caption="표 4. 플러그인" caption-side="top"}

| *{{site.data.keyword.IBM}} Containers for {{site.data.keyword.Bluemix_notm}}* | *VPN* |
|-----------------|-----------------|
| 플러그인 이름: ibm-containers<br> [문서 보기 ![외부 링크 아이콘](../icons/launch-glyph.svg)](https://www.{DomainName}/docs/containers/container_cli_cfic.html#container_cli_cfic){: new_window} | 플러그인 이름: VPN <br> [문서 보기](/docs/cli/plugins/vpn/index.html) |
{: caption="표 5. 플러그인" caption-side="top"}

## ![](./images/Integrated_Dev_Tools.svg) 통합 개발 도구
{: #ide notoc}

즐겨찾기 {{site.data.keyword.Bluemix_notm}} 서비스를 통합하기 위해 플러그인을 다운로드하고 설치합니다.

| *{{site.data.keyword.jazzhub_short}}* | *Liberty for Java* | *MobileFirst* | *{{site.data.keyword.rules_short}}* | *API Connect* | *Eclipse Tools for Bluemix* |
|-------------|----------|----------|----------|----------|----------|
| [Egit Eclipse 플러그인 ![외부 링크 아이콘](../icons/launch-glyph.svg)](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_egit){: new_window} <br> [RTC Eclipse 플러그인 ![외부 링크 아이콘](../icons/launch-glyph.svg)](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_rtc){: new_window} | [Liberty Eclipse 플러그인 ![외부 링크 아이콘](../icons/launch-glyph.svg)](https://developer.ibm.com/wasdev/downloads/liberty-profile-using-eclipse/){: new_window} | [Eclipse 플러그인 ![외부 링크 아이콘](../icons/launch-glyph.svg)](https://marketplace.eclipse.org/content/ibm-mobilefirst-platform-studio){: new_window} | [Rules Designer Eclipse 플러그인](../services/rules/index.html#rulov002) | [개발자 툴킷 ![외부 링크 아이콘](../icons/launch-glyph.svg)](https://nextstage.torolab.ibm.com/apimanagement/getting-started/ ){: new_window} | [Bluemix Eclipse 플러그인](/docs/manageapps/eclipsetools/eclipsetools.html) |
{: caption="표 6. 플러그인" caption-side="top"}
