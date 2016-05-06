---

 

copyright:

  years: 2015, 2016

 

---
{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}


# 개발 모드 CLI
{: #devmodecli}

*마지막 업데이트 날짜: 2016년 2월 25일*

개발 모드(dev_mode)는 클라우드에서 앱을 실행하는 동안 앱에 대한 작업을 수행하는 데 사용할 수 있는 Bluemix 기능입니다. 개발 모드에는 dev_mode 명령행 인터페이스가 포함되어 있습니다. dev_mode CLI는 cf CLI 플러그인으로 빌드되며 Liberty 앱과 IBM Node.js 앱을 모두 지원합니다.

dev_mode CLI에서는 다음과 같은 기능을 제공합니다.
- 앱을 개발 모드와 정상 모드로 전환합니다.
- 새 푸시 없이 애플리케이션 파일을 점진적으로 업데이트합니다.
- 기존 컨테이너에서 앱을 시작하거나, 중지하거나, 다시 시작합니다.

## 시작하기
**전제조건:** 시작하기 전에 Cloud Foundry CLI를 설치하십시오. 세부사항은 [Cloud Foundry 명령행 인터페이스를 사용하여 코딩 시작](https://github.com/cloudfoundry/cli)을 참조하십시오. 


dev_mode 명령행 도구를 설치하려면 다음 방법 중 하나를 사용하십시오.
- 로컬로 설치합니다.
  1. [IBM Bluemix CLI 플러그인 저장소](http://plugins.ng.bluemix.net)에서 플랫폼에 맞는 dev_mode 플러그인을 다운로드하십시오.
  2. cf install-plugin 명령을 사용하여 dev_mode 플러그인을 설치하십시오.
  
        ```
        cf install-plugin dev_mode-linux_amd64
        ```

- Bluemix CLI 저장소에서 설치합니다.
  1. 다음 명령을 사용하여 Cloud Foundry CLI 저장소에 bluemix-repo 저장소를 추가하십시오.
  
        ```
        cf add-plugin-repo bluemix-repo http://plugins.ng.bluemix.net
        ```

  2. cf repo-plugins를 입력하십시오. dev_mode 플러그인이 bluemix-repo 저장소에 나타납니다. 
		
		```
        cf repo-plugins
        ```
  
  3. 다음 명령을 사용하여 Cloud Foundry CLI 플러그인에 dev_mode 플러그인을 설치하십시오.
  
        ```
        cf install-plugin dev_mode -r bluemix-repo
        ```

## 사용량
**모든 dev_mode CLI 명령을 표시하려면 다음 명령을 사용하십시오.**

```
cf plugins
```

### dev_mode 명령

### 모드

```
cf mode <appName> <dev|normal>
```

앱 모드를 변경합니다.

### status

```
cf status <appName>
```

앱 모드와 런타임 상태를 표시합니다.

### update-file

```
cf update-file <remotePath> <localPath> [command_options]
```

클라우드의 애플리케이션 파일을 업데이트합니다.

명령 옵션:

**펼치기**

업로드된 파일을 zip 파일에서 압축을 풀어야 하는지 여부를 표시합니다.

**다시 시작**

파일이 업데이트된 후 앱 런타임을 다시 시작합니다.
  
### delete-file

```
cf delete-file <remotePath> [command_options]
```

클라우드의 애플리케이션 파일을 삭제합니다.

명령 옵션:

**다시 시작**

파일이 삭제된 후 앱 런타임을 다시 시작합니다.

### start-inplace

```
cf start-inplace <appName>
```

기존 컨테이너에서 앱을 시작합니다.

### stop-inplace

```
cf stop-inplace <appName>
```

기존 컨테이너에서 앱을 중지합니다.

### restart-inplace

```
cf restart-inplace <appName>
```

기존 컨테이너에서 앱을 다시 시작합니다.



### help

```
cf help <commandName>
```
명령에 대한 도움말을 표시합니다.
