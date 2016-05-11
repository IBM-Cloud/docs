---

 

copyright:

  years: 2015, 2016

 

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# CLI 및 개발 도구
{: #cli}

*마지막 업데이트 날짜: 2016년 3월 30일*

{{site.data.keyword.Bluemix_short}}를 통해 통합 명령행 인터페이스 및 CLI 플러그인과 같은 강력한 도구를 이용할 수 있습니다. 각각의 CLI를 다운로드하여 {{site.data.keyword.Bluemix_notm}} 환경에 사용 가능합니다.
{:shortdesc}

## ![명령행 인터페이스](./images/CLI.svg) 명령행 인터페이스
{: #downloads}

{{site.data.keyword.Bluemix_notm}} 환경을 지원하는 명령행 인터페이스를 다운로드하여 설치하십시오. Cloud Foundry cf 명령행 도구는 다른 모든 {{site.data.keyword.Bluemix_notm}} CLI 도구를 사용하기 위한 전제조건입니다. {{site.data.keyword.Bluemix_notm}} 명령행 도구는 Cloud Foundry 애플리케이션 이외에 {{site.data.keyword.Bluemix_notm}} 환경을 관리하는 확장된 경험을 제공합니다.

두 CLI 도구는 모두 기본적으로 433 포트를 사용합니다. CLI 도구 및 {{site.data.keyword.Bluemix_notm}} 환경 간에 HTTP 프록시가 있는 경우에는 실제 HTTP 프록시 url 및 포트(있는 경우)로 `http-proxy` 환경 변수를 구성해야 합니다. 추가 세부사항은 [HTTP 프록시 서버에서 CLI 사용](http://docs.cloudfoundry.org/cf-cli/http-proxy.html){: new_window}을 참조하십시오.


| *{{site.data.keyword.Bluemix_notm}}: bx* | *Cloud Foundry: cf* |
|---------------------|---------------|
| [CLI 다운로드](http://clis.ng.bluemix.net/)  <br> [문서 보기](./reference/bluemix_cli/index.html)|  [CLI 다운로드](https://github.com/cloudfoundry/cli/releases){: new_window}  <br> [문서 보기](./reference/cfcommands/index.html) |


## ![명령행 인터페이스 플러그인](./images/CLI_Plugin.svg) 명령행 인터페이스 플러그인

더 많은 명령으로 {{site.data.keyword.Bluemix_notm}} 명령행 인터페이스를 간편하게 확장합니다. {{site.data.keyword.Bluemix_notm}} 명령행 인터페이스 플러그인에 액세스하려면 [ CLI 플러그인 저장소](http://plugins.ng.bluemix.net/)를 참조하십시오.

### {{site.data.keyword.Bluemix_notm}} 명령행 인터페이스 확장: bx

1. {{site.data.keyword.Bluemix_notm}} 레지스트리에서 {{site.data.keyword.Bluemix_notm}} CLI 플러그인을 설치하려면 플러그인 레지스트리 엔드포인트를 설정하십시오.
```
bluemix plugin repo-add bluemix-bx-staging http://plugins.ng.bluemix.net
```
2. 다음 명령을 실행하여 플러그인을 설치하십시오.
```
bluemix plugin install plugin_name -r bluemix-bx-staging
```

| *{{site.data.keyword.activedeployshort}} CLI* | *{{site.data.keyword.autoscaling}} CLI* | *Network Security Groups* |
|-----|-----|-----|
| 플러그인 이름: active-deploy<br> [문서 보기](../services/ActiveDeploy/cli.html#cli) | 플러그인 이름: auto-scaling <br> [문서 보기](./plugins/auto-scaling/index.html) |  플러그인 이름: nsg<br> [문서 보기](./plugins/networksecuritygroups/index.html)  |


### Cloud Foundry 명령행 인터페이스 확장: cf

1. {{site.data.keyword.Bluemix_notm}} 레지스트리에서 cf CLI 플러그인을 설치하려면 플러그인 레지스트리 엔드포인트를 설정하십시오.
```
cf add-plugin-repo bluemix-cf-staging http://plugins.ng.bluemix.net
```
2. 다음 명령을 실행하여 플러그인을 설치하십시오.
```
cf install-plugin plugin_name -r bluemix-cf-staging
```

| *Active Deploy* | *관리 콘솔* | *개발 모드* |
|-----------------|-----------------|-----------------|
| 플러그인 이름: active-deploy<br>  [문서 보기](../services/ActiveDeploy/cli.html#cli) |  플러그인 이름: bluemix-admin<br> [문서 보기](../cli/plugins/bluemix_admin/index.html) | 플러그인 이름: dev_mode <br> [문서 보기](./plugins/dev_mode/index.html) |

| *{{site.data.keyword.IBM}} Containers for {{site.data.keyword.Bluemix_notm}}* | *VPN* |
|-----------------|-----------------|
| 플러그인 이름: ibm-containers<br> [문서 보기](https://www.{DomainName}/docs/containers/container_cli_cfic.html#container_cli_cfic) | 플러그인 이름: VPN <br> [문서 보기](./plugins/vpn/index.html) |

<!-- View docs link for bluemix-admin plug-in cannot go live until December time frame. Check in with Michelle -->


## ![통합 개발 도구](./images/Integrated_Dev_Tools.svg) 통합 개발 도구

즐겨찾기 {{site.data.keyword.Bluemix_notm}} 서비스를 통합하기 위해 플러그인을 다운로드하고 설치합니다.

| *{{site.data.keyword.jazzhub_short}}* | *Liberty for Java* | *MobileFirst* | *{{site.data.keyword.rules_short}}* |
|-------------|----------|----------|----------|
| [Egit Eclipse 플러그인](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_egit){: new_window} <br> [RTC Eclipse 플러그인](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_rtc){: new_window} | [Liberty Eclipse 플러그인](https://developer.ibm.com/wasdev/downloads/liberty-profile-using-eclipse/){: new_window} | [Eclipse 플러그인](https://marketplace.eclipse.org/content/ibm-mobilefirst-platform-studio){: new_window} | [Rules Designer Eclipse 플러그인](../services/rules/index.html#rulov002) |
