---



copyright:

  years: 2015，2017

lastupdated: "2017-01-12"



---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# (더 이상 사용되지 않음) 개발 모드 CLI
{: #devmodecli}

**이 CLI는 더 이상 사용되지 않음:** 개발 모드(dev_mode) CLI를 사용하는 대신, IBM Eclipse Tools for Bluemix 또는 DevOps 웹 IDE를 사용하십시오. 2016년 6월 30일까지는 dev_mode CLI 사용을 계속할 수 있습니다. 

Bluemix 개발 모드 명령행 인터페이스(dev_mode CLI)에서는 앱이 클라우드에서 실행 중인 동안 앱을 업데이트할 수 있습니다. dev_mode CLI는 cf CLI 플러그인으로 빌드되며 Liberty 앱과 IBM Node.js 앱을 모두 지원합니다.
{: shortdesc}


dev_mode CLI로 다음 태스크를 수행할 수 있습니다.
- 앱을 개발 모드와 정상 모드로 전환합니다.
- 새 푸시 없이 애플리케이션 파일을 점진적으로 업데이트합니다.
- 기존 컨테이너에서 앱을 시작하거나, 중지하거나, 다시 시작합니다.

## dev_mode 플러그인 설치
**전제조건:** 시작하기 전에 Cloud Foundry CLI를 설치하십시오. 세부사항은 [Cloud Foundry 명령행 인터페이스를 사용하여 코딩 시작](https://github.com/cloudfoundry/cli)을 참조하십시오.


dev_mode 명령행 도구를 설치하려면 다음 방법 중 하나를 사용하십시오.
- 로컬로 설치합니다.
  1. [IBM Bluemix CLI 플러그인 저장소](http://plugins.ng.bluemix.net)에서 플랫폼에 맞는 dev_mode 플러그인을 다운로드하십시오.
  2. dev_mode 플러그인이 저장된 폴더로 이동하고, cf install-plugin 명령을 사용하여 dev_mode 플러그인을 설치하십시오. 예를 들어, 다음과 같습니다. 

        ```
        cf install-plugin dev_mode-linux64
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

## dev_mode 명령 보기

모든 dev_mode CLI 명령을 표시하려면 다음 명령을 사용하십시오.

```
cf plugins
```

## dev_mode CLI 명령 색인
{: #dev_mode_cmds_index}

자주 사용되는 dev_mode CLI 명령을 참조하려면 다음 표의 색인을 사용하십시오.

<table summary="dev_mode 명령 색인">
 <caption>표 1. dev_mode 명령</caption>
 <thead>
 <th colspan="4">dev_mode 명령</th>
 </thead>
 <tbody>
 <tr>
 <td>[help](#help)</td>
 <td>[mode](#mode)</td>
 <td>[status](#status)</td>
 <td>[update-file](#update_file)</td>
 </tr>
 <tr>
 <td>[delete-file](#delete_file)</td>
 <td>[start-inplace](#start_inplace)</td>
 <td>[stop-inplace](#stop_inplace)</td>
 <td>[restart-inplace](#restart_inplace)</td>
 </tr>
  </tbody>
 </table>


## help
{: #help}

명령에 대한 도움말을 표시합니다.

```
cf help <commandName>
```


## mode
{: #mode}

앱 모드를 변경합니다.

```
cf mode <appName> <dev|normal>
```
<strong>명령 옵션</strong>:

   <dl>
   <dt>dev</dt>
   <dd>개발 모드.</dd>
   <dt>normal</dt>
   <dd>프로덕션 모드.</dd>
   </dl>


## status
{: #status}

앱 모드와 런타임 상태를 표시합니다. 
```
cf status <appName>
```



## update-file
{: #update_file}

클라우드의 애플리케이션 파일을 업데이트합니다.

```
cf update-file <remotePath> <localPath> [command_options]
```


<strong>명령 옵션</strong>:

   <dl>
   <dt>expand</dt>
   <dd>업로드된 파일을 zip 파일에서 압축을 풀어야 하는지 여부를 표시합니다.</dd>
   <dt>restart</dt>
   <dd>파일이 업데이트된 후 앱 런타임을 다시 시작합니다.</dd>
   </dl>



## delete-file
{: #delete_file}

클라우드의 애플리케이션 파일을 삭제합니다.

```
cf delete-file <remotePath> [command_options]
```


<strong>명령 옵션</strong>:
 <dl>
   <dt>restart</dt>
   <dd>파일이 업데이트된 후 앱 런타임을 다시 시작합니다.</dd>
  </dl>


## start-inplace
{: #start_inplace}
기존 컨테이너에서 앱을 시작합니다.

```
cf start-inplace <appName>
```



## stop-inplace
{: #stop_inplace}
기존 컨테이너에서 앱을 중지합니다.

```
cf stop-inplace <appName>
```



## restart-inplace
{: #restart_inplace}

기존 컨테이너에서 앱을 다시 시작합니다.

```
cf restart-inplace <appName>
```



# 관련 링크
{: #rellinks}

## 관련 링크
{: #general}
* [개발 모드 CLI ![외부 링크 아이콘](../../../icons/launch-glyph.svg)](http://clis.ng.bluemix.net/ui/repository.html#cf-plugins){:new_window}
* [DevOps 웹 IDE ![외부 링크 아이콘](../../../icons/launch-glyph.svg)](https://hub.jazz.net/docs/deploy/){:new_window}
