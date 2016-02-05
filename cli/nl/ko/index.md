{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# CLI 및 개발 도구
{: #cli}

*마지막 업데이트 날짜: 2016년 1월 19일*

{{site.data.keyword.Bluemix_short}}를 통해 통합 명령행 인터페이스 및 CLI 플러그인과 같은 강력한 도구를 이용할 수 있습니다. 각각의 CLI를 다운로드하여 {{site.data.keyword.Bluemix_notm}} 환경에 사용 가능합니다.
{:shortdesc}

## ![명령행 인터페이스](./images/CLI.png) 명령행 인터페이스
{: #downloads}

{{site.data.keyword.Bluemix_notm}} 환경을 지원하는 명령행 인터페이스를 다운로드하여 설치하십시오. Cloud Foundry cf 명령행 인터페이스는 다른 모든 {{site.data.keyword.Bluemix_notm}} CLI 도구의 전제 조건입니다. 


| *Cloud Foundry: cf* |	*{{site.data.keyword.Bluemix_notm}}: bx* | 
|---------------------|---------------|
| [CLI 다운로드](https://github.com/cloudfoundry/cli/releases){: new_window}  <br> [문서 보기](./reference/cfcommands/index.html) | [CLI 다운로드](http://clis.{DomainName}/){: new_window}  <br> [문서 보기](./reference/bluemix_cli/index.html)| 

| *{{site.data.keyword.Bluemix_notm}} Live Sync:
bl* |
|---------------|---------------|
| [Mac 설치 프로그램](ftp://public.dhe.ibm.com/cloud/bluemix/cli/Bluemix_bl.pkg){: new_window} <br> [Windows 설치 프로그램](ftp://public.dhe.ibm.com/cloud/bluemix/cli/Bluemix_bl.exe){: new_window} <br> [문서 보기](./reference/bl/index.html) |


## ![명령행 인터페이스 플러그인](./images/CLI_Plugin.png) 명령행 인터페이스 플러그인

더 많은 명령으로 {{site.data.keyword.Bluemix_notm}} 명령행 인터페이스를 간편하게 확장합니다. {{site.data.keyword.Bluemix_notm}} 명령행 인터페이스 플러그인에 액세스하려면 [{{site.data.keyword.Bluemix_notm}} CLI 플러그인 저장소](http://plugins.{DomainName}/){: new_window}를 참조하십시오.

1. {{site.data.keyword.Bluemix_notm}} 레지스트리에서 cf CLI 플러그인을 설치하려면 플러그인 레지스트리 엔드포인트를 설정하십시오.
```
cf add-plugin-repo bluemix-cf http://plugins.ng.bluemix.net
```
2. 다음 명령을 실행하여 플러그인을
설치하십시오.```
cf install-plugin plugin_name -r bluemix-cf
```

| *Active Deploy* | *관리 콘솔* | *개발 모드* | 
|-----------------|-----------------|-----------------|
| 플러그인 이름: active-deploy<br>  [문서 보기](../services/ActiveDeploy/index.html#cli) |  플러그인 이름: bluemix-admin<br> [문서 보기](../cli/plugins/bluemix_admin/index.html) | 플러그인 이름: development-name <br> [문서 보기](./plugins/dev_mode/index.html) | 

### {{site.data.keyword.Bluemix_notm}} 명령행 인터페이스 확장: bx
1. {{site.data.keyword.Bluemix_notm}} 레지스트리에서 {{site.data.keyword.Bluemix_notm}} CLI 플러그인을 설치하려면 플러그인 레지스트리 엔드포인트를 설정하십시오.
```
bluemix plugin repo-add bluemix-bx http://plugins.ng.bluemix.net
```
2. 다음 명령을 실행하여 플러그인을
설치하십시오.```
bluemix plugin install plugin_name -r bluemix-bx
```

| *{{site.data.keyword.IBM}} Containers for {{site.data.keyword.Bluemix_notm}}* | *{{site.data.keyword.autoscaling}} CLI* | *VPN* |
|-----|----|----|
| 플러그인 이름: ibm-containers<br> [문서 보기](https://www.{DomainName}/docs/containers/container_cli_cfic.html#container_cli_cfic) | 플러그인 이름: auto-scaling <br> [문서 보기](./plugins/auto-scaling/index.html) |플러그인 이름: VPN <br> [문서 보기](./plugins/vpn/index.html) |

## ![통합 개발 도구](./images/Integrated_Dev_Tools.png) 통합 개발 도구


즐겨찾기 {{site.data.keyword.Bluemix_notm}} 서비스를 통합하기 위해 플러그인을 다운로드하고 설치합니다.

| *{{site.data.keyword.jazzhub_short}}* | *Liberty for Java* | *MobileFirst* | *{{site.data.keyword.rules_short}}* |
|-------------|----------|----------|----------|
| [Egit Eclipse 플러그인](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_egit){: new_window} <br> [RTC Eclipse 플러그인](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_rtc){: new_window} | [Liberty Eclipse 플러그인](https://developer.ibm.com/wasdev/downloads/liberty-profile-using-eclipse/){: new_window} | [Eclipse 플러그인](https://marketplace.eclipse.org/content/ibm-mobilefirst-platform-studio){: new_window} | [Rules Designer
Eclipse 플러그인](../services/rules/index.html#rulov002) |
