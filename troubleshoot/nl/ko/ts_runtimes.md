---

copyright:
  years: 2015, 2017
  
lastupdated: "2017-01-10"

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 


# 런타임 문제점 해결
{: #runtimes}

{{site.data.keyword.Bluemix}} 런타임 사용 시 문제점이 발생할 수 있습니다. 대부분 몇 가지 간단한 단계를 수행하여 이러한 문제점에서 복구할 수 있습니다.
{:shortdesc}


## 앱을 푸시할 때 더 이상 사용되지 않는 빌드팩이 사용됨
{: #ts_loading_bp}

앱을 푸시할 때 최신 빌드팩 컴포넌트를 사용하지 못할 수 있습니다. 더 이상 사용되지 않는 컴포넌트가 로드되지 않도록 기본 제공되는 메커니즘이 있는 빌드팩을 사용하거나, 앱을 푸시하거나 다시 스테이징하기 전에 앱의 캐시 디렉토리에서 컨텐츠를 삭제할 수 있습니다. 

빌드팩을 업데이트한 후 앱을 푸시하거나 다시 스테이징할 때 최신 빌드팩 컴포넌트가 자동으로 로드되지 않습니다. 결과적으로 앱은 캐시에서 더 이상 사용되지 않는 빌드팩 컴포넌트를 사용합니다. 마지막으로 앱을 푸시한 후 빌드팩에 적용된 업데이트가 구현되지 않습니다.
{: tsSymptoms}

일부 빌드팩은 사용자가 항상 최신 버전을 사용할 수 있게 인터넷에서 업데이트된 모든 컴포넌트를 자동으로 다운로드하도록 구성되지 않았습니다.
{: tsCauses} 

기본 제공 메커니즘이 더 이상 사용되지 않는 컴포넌트를 로드하지 않도록 하는 빌드팩을 사용할 수 있습니다(예: 다음 빌드팩).
{: tsResolve}

  * [Cloud Foundry Java buildpack ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/cloudfoundry/java-buildpack){: new_window}. 최신 버전의 빌드팩을 사용하도록 이 빌드팩에는 기본 메커니즘이 포함되어 있습니다. 이 메커니즘의 작동 방식에 대한 자세한 정보는 [extending-caches.md ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/cloudfoundry/java-buildpack/blob/master/docs/extending-caches.md){: new_window}를 참조하십시오. 
  * [Cloud Foundry Node.js buildpack ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/cloudfoundry/nodejs-buildpack){: new_window}. 이 빌드팩은 환경 변수를 사용하여 비슷한 기능을 제공합니다. Node.js 빌드팩이 항상 인터넷에서 노드 모듈을 다운로드하게 하려면 cf 명령행 인터페이스에서 다음 명령을 입력하십시오. 	
  ```
  set NODE_MODULES_CACHE=false
  ```

사용 중인 빌드팩이 자동으로 최신 컴포넌트를 로드하는 메커니즘을 제공하지 않는 경우 수동으로 캐시 디렉토리에서 컨텐츠를 삭제하고 앱을 다시 푸시할 수 있습니다. 다음 단계를 수행하십시오.

 1. 널 빌드팩의 분기를 체크아웃합니다. 예: https://github.com/ryandotsmith/null-buildpack 분기를 체크아웃하는 방법에 대한 정보는 [Git Basics - Getting a Git Repository ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.git-scm.com/book/en/v2/Git-Basics-Getting-a-Git-Repository){: new_window}를 참조하십시오.  
 2. `null-buildpack/bin/compile` 파일에 다음 링크를 추가하고 변경사항을 커미트합니다. 변경사항을 커미트하는 방법에 대한 정보는 [Git Basics - Recording Changes to the Repository ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository){: new_window}를 참조하십시오.
  ```
  rm -rfv $2/*
  ```
 3. 다음 명령을 사용하여 캐시를 삭제하기 위해 수정한 널 빌드팩으로 앱을 푸시합니다. 이 단계를 완료하고 나면 앱의 캐시 디렉토리에 있는 모든 컨텐츠가 삭제됩니다.
  ```
  cf push appname -p app_path -b <modified_null_buildpack>
  ```
 4. 다음 명령을 사용하여 사용할 최신 빌드팩으로 앱을 푸시합니다. 
  ```
  cf push appname -p app_path -b <latest_buildpack>
  ```
 
## PHP 빌드팩의 NOTICE 메시지
{: #ts_phplog}

로그에 NOTICE가 포함된 메시지가 표시될 수 있습니다. 로깅 레벨을 변경하여 이러한 메시지의 로깅을 중지할 수 있습니다.	

PHP 빌드팩을 사용하여 {{site.data.keyword.Bluemix_notm}}에 앱을 푸시하는 경우 다음과 같이 `NOTICE`가 포함된 메시지를 볼 수 있습니다.
{: tsSymptoms}

```
• 2015-01-26T15:00:59.70+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: [pool www] 'user' directive is ignored when FPM is not running as root
• 2015-01-26T15:01:00.63+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: [pool www] 'user' directive is ignored when FPM is not running as root
• 2015-01-26T15:01:00.63+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: fpm is running, pid 93
• 2015-01-26T15:01:00.63+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: ready to handle connections
```
PHP 빌드팩에서 error_log 매개변수는 로깅 레벨을 정의합니다. 기본적으로 `error_log` 매개변수의 값은 **stderr notice**입니다. 다음 예는 Cloud Foundry가 제공하는 PHP 빌드팩의 `nginx-defaults.conf` 파일에 있는 기본 로깅 레벨 구성을 표시합니다. 자세한 정보는 [cloudfoundry/php-buildpack ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/cloudfoundry/php-buildpack/blob/ff71ea41d00c1226d339e83cf2c7d6dda6c590ef/defaults/config/nginx/1.5.x/nginx-defaults.conf){: new_window}을 참조하십시오.
{: tsCauses} 

```
daemon off;
error_log stderr notice;
pid @{HOME}/nginx/logs/nginx.pid;
```
	
`NOTICE` 메시지는 정보용이며 문제점을 표시하지 않습니다. 빌드팩의 nginx-defaults.conf 파일에서 `stderr notice`로부터 `stderr error`로 로깅 레벨을 변경하여 이러한 메시지의 로깅을 중지할 수 있습니다. 예를 들어, 다음과 같습니다. 	
{: tsResolve}

```
daemon off;
error_log stderr error;
pid @{HOME}/nginx/logs/nginx.pid;
```
기본 로깅 구성 변경 방법에 대한 자세한 정보는 [error_log ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](http://nginx.org/en/docs/ngx_core_module.html#error_log){: new_window}를 참조하십시오.
	

## 써드파티 Python 라이브러리를 {{site.data.keyword.Bluemix_notm}}로 가져올 수 없음
{: #ts_importpylib}

써드파티 Python 라이브러리를 {{site.data.keyword.Bluemix_notm}}로 가져오지 못할 수 있습니다. 문제점을 해결하려면 Python 앱의 루트 디렉토리에 구성 파일을 추가하십시오.

써드파티 Python 라이브러리(예: `web.py` 라이브러리)를 가져오려고 하면 `cf push` 명령이 실패합니다.
{: tsSymptoms}

Python 앱에 대한 구성 정보가 누락되었습니다.
{: tsCauses}

Python 앱의 루트 디렉토리에 `requirements.txt` 파일 및 `Procfile` 파일을 추가하십시오. 다음 정보는 `web.py` 라이브러리를 가져온다고 가정합니다.
{: tsResolve}

 1. Python 앱의 루트 디렉토리에 `requirements.txt` 파일을 추가하십시오.
 
 `requirements.txt` 파일은 Python 앱에 필요한 라이브러리 패키지 및 패키지 버전을 지정합니다. 다음 예에서는 `requirements.txt` 파일의 컨텐츠를 보여줍니다. 여기서 `web.py==0.37`은 다운로드할 `web.py` 라이브러리의 버전이 0.37임을 나타내고, `wsgiref==0.1.2`는 web.py 라이브러리에 필요한 웹 서버 게이트웨이 인터페이스가 0.1.2임을 나타냅니다.
	 ```
	 web.py==0.37
     wsgiref==0.1.2
	 ```
	 `requirements.txt` 파일을 구성하는 방법에 대한 자세한 정보는 [Requirements files](https://pip.readthedocs.org/en/1.1/requirements.html)를 참조하십시오.

 2. Python 앱의 루트 디렉토리에 `Procfile` 파일을 추가하십시오.
 `Procfile` 파일에는 Python 앱에 대한 시작 명령이 포함되어야 합니다. 다음 명령에서 *yourappname*은 Python 앱의 이름이며 *PORT*는 Python 앱이 앱 사용자의 요청을 수신하기 위해 사용해야 하는 포트 번호입니다. *$PORT*는 선택사항입니다. 시작 명령에 PORT를 지정하지 않으면 앱 내에 있는 `VCAP_APP_PORT` 환경 변수 아래의 포트 번호가 사용됩니다. 
	```
	web: python <yourappname>.py $PORT
	```

이제 써드파티 Python 라이브러리를 {{site.data.keyword.Bluemix_notm}}로 가져올 수 있습니다.	


## 인스턴스 세부사항 페이지의 조치 단추가 비활성화됨
{: #ts_actionsbutton}

인스턴스 세부사항 페이지의 조치 단추가 비활성화되어 있습니다.
{: tsSymptoms} 

이 문제점은 다음과 같은 이유로 발생합니다.
{: tsCauses}

 * 앱이 Java&trade; 웹 앱이 아닙니다. RMU(Runtime Management Utilities)는 Liberty 빌드팩을 사용하여 배치된 웹 앱만 지원합니다.
 * 앱이 임베디드 Liberty 빌드팩을 사용하여 배치되지 않았습니다.
 * 앱이 이전 버전의 Liberty 빌드팩을 사용하여 배치되었습니다.

이전 버전의 Liberty 빌드팩으로 인해 문제점이 발생한 경우 앱을 {{site.data.keyword.Bluemix_notm}}에 다시 배치하십시오. 그렇지 않은 경우 다음과 같은 클라이언트 애플리케이션 로그 파일을 지원 팀에 제공하십시오.
{: tsResolve} 

  * logs/messages.log
  * logs/stdout.log
  * logs/stderr.log
 
  
## 추적 또는 덤프 창을 여는 데 신임 정보가 필요함
{: #ts_username}

추적 또는 덤프 창을 여는 데 사용자 이름과 비밀번호가 필요합니다.
{: tsSymptoms}

이 문제점은 로그인 세션 제한시간 초과로 인해 발생합니다.
{: tsCauses}

사용자 이름과 비밀번호를 다시 입력하십시오.
{: tsResolve}


## 추적 또는 덤프 오퍼레이션이 실행 중일 때 오류 발생
{: #ts_target}

추적 또는 덤프 오퍼레이션이 실행 중일 때 오류 메시지가 표시됩니다. 앱의 대상 인스턴스가 실행 중 상태가 아니라는 메시지가 표시됩니다.	
{: tsSymptoms}

```
Instance 0: Trace specification is set successfully
Instance 2: Trace specification is set successfully
Instance 1: Target instance 1 for app abcd is not in the running state.
Instance 3: Trace specification is set successfully
Instance 4: Trace specification is set successfully
```

이 문제점은 다음과 같은 이유로 발생합니다.
{: tsCauses} 

  * 추적 또는 덤프 관리 기능은 실행 중인 앱 인스턴스에만 사용할 수 있습니다. 중지됨, 시작 중 또는 충돌됨 상태의 앱 인스턴스에는 추적 또는 덤프 오퍼레이션을 사용할 수 없습니다.
  * 추적 또는 덤프 대화 상자가 열린 경우 앱 인스턴스의 상태가 변경됩니다. 

창을 닫은 다음 다시 여십시오.
{: tsResolve} 


## 인스턴스에 다른 traceSpecification 구성이 있음
{: #ts_different_config}

하나의 앱의 여러 인스턴스에서 traceSpecification 구성이 서로 다를 수 있습니다.
{: tsSymptoms}

이 동작은 다음과 같은 이유로 발생합니다.
{: tsCauses}

  * 이전에는 하나 이상의 인스턴스에 대한 구성을 변경했습니다. 하나의 인스턴스에 대한 traceSpecification 구성을 변경한 경우 동일한 앱의 다른 인스턴스에는 변경사항이 적용되지 않습니다. 예를 들어, 앱이 log4j를 사용하고 이 앱에 두 개의 인스턴스가 있습니다. 인스턴스 0의 로그 레벨을 정보에서 디버그로 변경할 수 있지만 인스턴스 1의 로그 레벨은 정보로 남아 있습니다.
  
  * 앱이 스케일 확장되고 새 인스턴스를 갖습니다. RMU는 기존 인스턴스의 traceSpecification 구성을 스케일 확장된 새 인스턴스에 적용하지 않습니다. 새 인스턴스는 기본 구성을 사용합니다. 예를 들어, 앱이 log4j를 사용하고 1개의 인스턴스가 있습니다. 이 인스턴스의 로그 레벨을 정보에서 디버그로 변경할 수 있습니다. 이렇게 변경한 후 앱을 두 개의 인스턴스로 스케일 확장하는 경우 새 인스턴스의 로그 레벨은 디버그가 아닌 정보입니다.

조치는 필요하지 않습니다. 이는 예상된 동작입니다.
{: tsResolve} 


## 디스크 할당량이 초과됨
{: #ts_diskquota}

앱 로그에 디스크 할당량이 초과되었다고 표시될 수 있습니다.

앱 로그에 `디스크 할당량 초과` 오류 메시지가 표시됩니다.
{: tsSymptoms}

이 문제점은 다음과 같은 이유로 발생합니다.
{: tsCauses} 

  * 앱 인스턴스가 실행 중인 상태에서 덤프 파일이 생성되며, 파일이 디스크 할당량을 모두 사용합니다. 기본적으로 한 앱 인스턴스의 디스크 할당량은 1GB입니다. **대시보드>애플리케이션>앱 런타임**을 클릭하면 디스크 사용량을 확인할 수 있습니다. 다음 예는 앱의 두 인스턴스에 대해 디스크 사용량 등의 런타임 정보를 표시합니다.
    ```
    Instance	State	CPU	Memory Usage	Disk Usage

	0		Running	1.0%	344.8MB/512MB	236.8MB/1GB
	2		Running	2.3%	361.2MB/512MB	235.7MB/1GB
    ```
  * 디스크 할당량은 현재 조직 할당량으로 제한됩니다.

다음 방법 중 하나를 사용하십시오.
{: tsResolve} 

  * 덤프 파일을 다운로드한 후 삭제하십시오.
  * 배치 Manifest에 다음 항목을 포함시켜 디스크 할당량 늘려 앱을 다시 배치하십시오.
    ```
	disk_quota: 2048
	```
	
