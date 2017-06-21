---



copyright:

  years: 2015, 2017
lastupdated: "2017-03-08"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.Bluemix_notm}} CLI 시작하기
{: #getting-started}

{{site.data.keyword.Bluemix_notm}} CLI는 명령행 인터페이스를 사용하여 애플리케이션, 컨테이너, 인프라 및 기타 서비스와 상호작용하기 위한 통합된 방법을 제공합니다. 

**제한사항**: {{site.data.keyword.Bluemix_notm}} CLI는 Cygwin에서 지원되지 않으므로 Cygwin 명령행 창에서는 {{site.data.keyword.Bluemix_notm}} CLI를 사용하지 마십시오. 

**참고**: 네트워크에 CLI를 실행하는 호스트와 {{site.data.keyword.Bluemix_notm}} 간에 HTTP 프록시 서버가 포함되어 있는 경우 HTTP_PROXY 환경 변수에 프록시 서버의 호스트 이름 또는 IP 주소를 지정해야 합니다. 

**참고:** {{site.data.keyword.Bluemix_notm}} CLI 도구는 설치에 Cloud Foundry 명령행 인터페이스를 번들화했습니다. 하지만 고유 cf cli 설치가 있는 경우 {{site.data.keyword.Bluemix_notm}} CLI 명령 `bx xxx`와 Cloud Foundry CLI 명령 `cf xxx`를 혼합해서 사용할 수 없습니다. 대신 cf cli를 사용하여 Cloud Foundry 리소스를 관리하려면 `bluemix cf`를 사용하십시오. 백엔드에서 {{site.data.keyword.Bluemix_notm}} CLI와의 공유 컨텍스트의 번들화된 Cloud Foundry CLI 명령을 실행합니다. 또한 `bluemix cf api/login/logout/target`이 허용되지 않으므로 대신 `bluemix api/login/logout/target`을 사용하십시오.

## {{site.data.keyword.Bluemix_notm}} CLI 설치
{: #install_bluemix_cli}


Mac OS 및 Windows의 경우, [{{site.data.keyword.Bluemix_notm}} CLI 패키지](/docs/cli/index.html#downloads)를 다운로드하고 설치 프로그램을 실행하십시오. 

Linux의 경우, 다음 단계를 수행하십시오. 

  1. 패키지를 다운로드하여 압축을 푸십시오. 예를 들어, 다음과 같습니다. 

  ```
  ~$ tar -xvf Bluemix_CLI.tar.gz
  Bluemix_CLI/
  Bluemix_CLI/update_global_config
  Bluemix_CLI/install_bluemix_cli
  Bluemix_CLI/bx/
  Bluemix_CLI/bx/bash_autocomplete
  Bluemix_CLI/bx/zsh_autocomplete
  Bluemix_CLI/bin/
  Bluemix_CLI/bin/bluemix
  ~$
  ```

  2. `Bluemix_CLI` 디렉토리로 이동하여 루트 권한으로 `./install_bluemix_cli` 명령을 실행하십시오. 루트 사용자로 명령을 실행하거나 `sudo` 명령을 사용하여 루트 권한을 확보하십시오. 예를 들어, 다음과 같습니다. 

  ```
  ~# cd Bluemix_CLI
  ~/Bluemix_CLI# sudo ./install_bluemix_cli
  Superuser privileges are required to run this script.
  The Cloud Foundry CLI version 6.15 is already installed.
  Copying files...
  The Bluemix CLI installed successfully. To get started, open a new Linux terminal and enter "bluemix help", or enter "bx help" as short name.
  ~/Bluemix_CLI#
  ```

이제 {{site.data.keyword.Bluemix_notm}} CLI 사용을 시작하거나 추가 플러그인을 설치할 수 있습니다.

## 플러그인 설치
{: #install_plug-in}

{{site.data.keyword.Bluemix_notm}} CLI는 플러그인 확장 프레임워크를 지원하여 기본 제공 명령 외에 다른 명령을 통합합니다.


저장소에서, 로컬로 또는 원격 서버에서 플러그인을 설치할 수 있습니다. {{site.data.keyword.Bluemix_notm}}에는 {{site.data.keyword.Bluemix_notm}} CLI 플러그인 및 Cloud Foundry CLI 플러그인을 호스팅하는 저장소가 있습니다. 

   * [{{site.data.keyword.Bluemix_notm}} CLI 플러그인 저장소](http://clis.ng.bluemix.net/ui/repository.html#bluemix-plugins){: new_window} ![외부 링크 아이콘](../../../icons/launch-glyph.svg)는 {{site.data.keyword.Bluemix_notm}} CLI의 플러그인을 호스팅합니다.

저장소에서 설치하려면 다음 단계를 수행하십시오. 

  1. 저장소에서 플러그인을 찾으십시오. {{site.data.keyword.Bluemix_notm}} CLI를 설치하고 나면, 기본적으로 공식 저장소 `Bluemix`가 추가됩니다. `bluemix plugin repo-plugins` 명령을 사용하여 `Bluemix` 저장소에 플러그인을 나열할 수 있습니다. 예를 들어, 다음과 같습니다. 

  ```
  ~$ bluemix plugin repo-plugins -r Bluemix
  Getting plug-ins from repository 'Bluemix'...

  Repository: Bluemix
  Name           Description                                    Versions
  auto-scaling   Bluemix CLI plugin for Auto-Scaling service    0.2.1, 0.2.2
  nsg            Bluemix Network Security Group plugin          0.1.1

  ~$
  ```

  2. `bluemix plugin install` 명령을 사용하여 `Bluemix` 저장소에서 플러그인을 설치하십시오. 예를 들어, 다음과 같습니다. 

  ```
  ~$ bluemix plugin install auto-scaling -r Bluemix
  Looking up 'auto-scaling' from repository 'Bluemix'...
  9857792 bytes downloaded
  Installing plugin '/var/folder/v7/l3hnkz0x0b9b5mf1fyxh7yw00000gn/T/BluemixFileDownload062468676/auto-scaling-darwin-adm64-0.2.2'...
  OK
  Plugin 'auto-scaling 0.2.2' was successfully installed.
  ~$
  ```


로컬 환경에서 플러그인을 설치하려면 다음 단계를 수행하십시오. 

  1. 플러그인을 다운로드하십시오. 예를 들어, 다음과 같습니다. 

  ```
  ~$ wget http://public.dhe.ibm.com/cloud/bluemix/cli/bluemix-plugins/auto-scaling-darwin-amd64.0.2.2--2016-02-18 14:02:12-- http://public.dhe.ibm.com/cloud/bluemix/cli/bluemix-plugins/auto-scaling-darwin-amd64.0.2.2
  Resolving public.dhe.ibm.com... 9.17.248.112
  Connection to public.dhe.ibm.com|9.17.248.112|:80... connected.
  HTTP request sent, awaiting response... 200 OK
  Length: 9857792 (9.4M) [text/plain]
  Saving to: 'auto-scaling-darwin-amd64-0.2.2'

  auto-scaling-darwin-0.2.2 100%[===================>] 9.40M 518KB/s in 22s

  2016-02-18 14:02:34 (443 KB/s) - `auto-scaling-darwin-amd64-0.2.2' saved [9857792/9857792]
  ```

  2. UNIX 계열 시스템의 경우 `chmod` 명령을 사용하여 다운로드된 파일을 실행 파일로 만들어야 합니다. 예를 들어, 다음과 같습니다. 

  ```
  ~$ sudo chmod 755 auto-scaling-darwin-amd64-0.2.2
  Password:
  ~$
  ```

  3. `bluemix plugin install` 명령을 사용하여 플러그인을 설치하십시오. 예를 들어, 다음과 같습니다. 

  ```
  ~$ bluemix plugin install ./auto-scaling-darwin-amd64-0.2.2
  Installing pluign './auto-scaling-darwin-amd64-0.2.2'...
  OK
  Plugin 'auto-scaling 0.2.2' was successfully installed.
  ~$
  ```

원격 서버에서 설치하려면 다음 단계를 수행하십시오. 

  1. `bluemix plugin install` 명령을 사용하여 원격 URL에서 직접 플러그인을 설치하십시오. 예를 들어, 다음과 같습니다. 

  ```
  ~$ bluemix plugin install http://public.dhe.ibm.com/cloud/bluemix/cli/bluemix-plugins/auto-scaling-darwin-amd64-0.2.2
  Attempting to download the binary file...
  9857792 bytes downloaded
  Installing plugin '/var/folder/v7/l3hnkz0x0b9b5mf1fyxh7yw00000gn/T/BluemixFileDownload274645142/auto-scaling-darwin-adm64-0.2.2'...
  OK
  Plugin 'auto-scaling 0.2.2' was successfully installed.
  ~$
  ```


{{site.data.keyword.Bluemix_notm}} 명령행을 사용할 준비가 되었습니다. `bluemix help`를 실행하여 명령 및 설명 목록을 확인하십시오. 
