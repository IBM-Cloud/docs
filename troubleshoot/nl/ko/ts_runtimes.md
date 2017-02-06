---

copyright:
  years: 2015, 2017
  
lastupdated: "2017-01-11"

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 





# 런타임 문제점 해결
{: #runtimes}



IBM® Bluemix™ 런타임을 사용할 때 문제점이 발생할 수 있습니다. 그러나 대부분의 경우 몇 가지 간단한 단계를 수행하여 이러한 문제점에서 복구할 수 있습니다.
{:shortdesc}


## 앱을 푸시할 때 더 이상 사용되지 않는 빌드팩이 사용됨
{: #ts_loading_bp}


앱을 푸시할 때 최신 빌드팩 컴포넌트를 사용하지 못할 수 있습니다. 더 이상 사용되지 않는 컴포넌트가 로드되지 않도록 기본 제공되는 메커니즘이 있는 빌드팩을 사용하거나, 앱을 푸시하거나 다시 스테이징하기 전에 앱의 캐시 디렉토리에서 컨텐츠를 삭제할 수 있습니다. 

 

빌드팩을 업데이트한 후 앱을 푸시하거나 다시 스테이징할 때 최신 빌드팩 컴포넌트가 자동으로 로드되지 않습니다. 결과적으로 앱은 캐시에서 더 이상 사용되지 않는 빌드팩 컴포넌트를 사용합니다. 앱을 마지막으로 푸시한 후 빌드팩에 적용한 업데이트는 구현되지 않습니다. 
{: tsSymptoms}



사용자가 항상 최신 버전을 사용하도록 일부 빌드팩은 인터넷에서 업데이트된 모든 컴포넌트를 자동으로 다운로드하도록 구성되지 않았습니다.
{: tsCauses} 

 

더 이상 사용되지 않는 컴포넌트를 로드하지 않도록 기본 제공 메커니즘이 있는 빌드팩을 사용할 수 있습니다. 두 가지 예로 다음 빌드팩이 있습니다. 
{: tsResolve}

  * [Cloud Foundry Java 빌드팩 ![외부 링크 아이콘](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/java-buildpack){: new_window}. 최신 버전의 빌드팩을 사용하도록 이 빌드팩에는 기본 메커니즘이 포함되어 있습니다. 이 메커니즘의 작동 방식에 대한 자세한 정보는 [extending-caches.md ![외부 링크 아이콘](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/java-buildpack/blob/master/docs/extending-caches.md){: new_window}를 참조하십시오.  
  * [Cloud Foundry Node.js 빌드팩 ![외부 링크 아이콘](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/nodejs-buildpack){: new_window}. 이 빌드팩은 환경 변수를 사용하여 비슷한 기능을 수행합니다. Node.js 빌드팩이 항상 인터넷에서 노드 모듈을 다운로드하게 하려면 cf 명령행 인터페이스에서 다음 명령을 입력하십시오. 	
  ```
  set NODE_MODULES_CACHE=false
  ```
사용 중인 빌드팩에서 자동으로 최신 컴포넌트를 로드하는 메커니즘을 제공하지 않는 경우 수동으로 캐시 디렉토리에서 컨텐츠를 삭제하고 다음 단계를 수행하여 앱을 푸시할 수 있습니다.
  1. 널 빌드팩의 분기를 체크아웃합니다. 예: https://github.com/ryandotsmith/null-buildpack 분기를 체크아웃하는 방법에 대한 정보는 [Git Basics - Getting a Git Repository ![외부 링크 아이콘](../icons/launch-glyph.svg)](http://www.git-scm.com/book/en/v2/Git-Basics-Getting-a-Git-Repository){: new_window}를 참조하십시오.   
  2. `null-buildpack/bin/compile` 파일에 다음 링크를 추가하고 변경사항을 커미트합니다. 변경사항을 커미트하는 방법에 대한 정보는 [Git Basics - Recording Changes to the Repository ![외부 링크 아이콘](../icons/launch-glyph.svg)](http://www.git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository){: new_window}를 참조하십시오. 
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
	
 

PHP 빌드팩을 사용하여 애플리케이션을 Bluemix로 푸시할 때 `NOTICE`가 포함된 메시지가 표시될 수 있습니다.
{: tsSymptoms}

```
• 2015-01-26T15:00:59.70+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: [pool www] 'user' directive is ignored when FPM is not running as root
• 2015-01-26T15:01:00.63+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: [pool www] 'user' directive is ignored when FPM is not running as root
• 2015-01-26T15:01:00.63+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: fpm is running, pid 93
• 2015-01-26T15:01:00.63+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: ready to handle connections
```



PHP 빌드팩에서 error_log 매개변수는 로깅 레벨을 정의하는 데 사용됩니다. 기본적으로 `error_log` 매개변수의 값은 **stderr notice**입니다. 다음 예에서는 Cloud Foundry에서 제공하는 PHP 빌드팩의 `nginx-defaults.conf` 파일에 있는 기본 로깅 레벨 구성을 보여줍니다. 자세한 정보는 [cloudfoundry/php-buildpack ![외부 링크 아이콘](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/php-buildpack/blob/ff71ea41d00c1226d339e83cf2c7d6dda6c590ef/defaults/config/nginx/1.5.x/nginx-defaults.conf){: new_window}을 참조하십시오.
{: tsCauses} 

```
daemon off;
error_log stderr notice;
pid @{HOME}/nginx/logs/nginx.pid;
```

 	
	
`NOTICE` 메시지는 정보 메시지일 뿐 반드시 문제점이 발생했음을 의미하는 것은 아닙니다. 빌드팩의 nginx-defaults.conf 파일에서 로깅 레벨을 stderr notice에서 stderr error로 변경하여 메시지 로깅을 중지할 수 있습니다. 예를 들어, 다음과 같습니다. 	
{: tsResolve}

```
daemon off;
error_log stderr error;
pid @{HOME}/nginx/logs/nginx.pid;
```
기본 로깅 구성을 변경하는 방법에 대한 자세한 정보는 [error_log ![외부 링크 아이콘](../icons/launch-glyph.svg)](http://nginx.org/en/docs/ngx_core_module.html#error_log){: new_window}를 참조하십시오.
	

## 써드파티 Python 라이브러리를 {{site.data.keyword.Bluemix_notm}}로 가져올 수 없음
{: #ts_importpylib}

써드파티 Python 라이브러리를 {{site.data.keyword.Bluemix_notm}}로 가져오지 못할 수 있습니다. Python 애플리케이션의 루트 디렉토리에 구성 파일을 추가하여 이 문제를 해결할 수 있습니다.


써드파티 Python 라이브러리(예: `web.py` 라이브러리)를 가져오려고 하면 `cf push` 명령이 실패합니다.
{: tsSymptoms}


 

이 문제점은 Python 애플리케이션에 대한 구성 정보가 누락된 경우에 발생합니다.
{: tsCauses}


 

문제점을 해결하려면 `requirements.txt` 파일과 `Procfile` 파일을 Python 앱의 루트 디렉토리에 추가하십시오. 다음 정보는 web.py 라이브러리를 가져온다고 가정합니다.
{: tsResolve}

  1. `requirements.txt` 파일을 Python 앱의 루트 디렉토리에 추가하십시오.
     `requirements.txt` 파일에는 Python 애플리케이션에 필요한 라이브러리 패키지와 패키지 버전이 지정되어 있습니다. 다음 예에서는 `requirements.txt` 파일의 컨텐츠를 보여줍니다. 여기서 `web.py==0.37`은 다운로드할 `web.py` 라이브러리의 버전이 0.37임을 나타내고, `wsgiref==0.1.2`는 web.py 라이브러리에 필요한 웹 서버 게이트웨이 인터페이스가 0.1.2임을 나타냅니다.
	 ```
	 web.py==0.37
     wsgiref==0.1.2
	 ```
	`requirements.txt` 파일을 구성하는 방법에 대한 자세한 정보는 [Requirements files](https://pip.readthedocs.org/en/1.1/requirements.html)를 참조하십시오.

  2. `Procfile` 파일을 Python 애플리케이션의 루트 디렉토리에 추가하십시오.
	`Procfile` 파일에는 Python 애플리케이션의 시작 명령이 포함되어 있어야 합니다. 다음 명령에서 *yourappname*은 Python 애플리케이션의 이름이고, *PORT*는 Python 애플리케이션이 앱 사용자로부터 요청을 수신할 때 사용해야 하는 포트 번호입니다. *$PORT*는 선택사항입니다. 시작 명령에 PORT를 지정하지 않으면 앱 내에 있는 `VCAP_APP_PORT` 환경 변수 아래의 포트 번호가 대신 사용됩니다. 
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

  * 애플리케이션이 Java™ 웹 애플리케이션이 아닙니다. RMU(Runtime Management Utilities)에서는 Liberty 빌드팩을 사용하여 배치된 웹 애플리케이션만 지원합니다.
  * 애플리케이션이 임베디드 Liberty 빌드팩을 사용하여 배치되지 않았습니다.
  * 애플리케이션이 이전 버전의 Liberty 빌드팩을 사용하여 배치되었습니다.



이전 버전의 Liberty 빌드팩으로 인해 문제점이 발생한 경우 애플리케이션을 {{site.data.keyword.Bluemix_notm}}에 다시 배치하십시오. 그렇지 않은 경우 다음과 같은 클라이언트 애플리케이션 로그 파일을 지원 팀에 제공하십시오.
{: tsResolve} 

  * logs/messages.log
  * logs/stdout.log
  * logs/stderr.log
  

  
  
## 추적 또는 덤프 창을 열 때 신임 정보가 필요함
{: #ts_username}


 

추적 및 덤프 창을 열 때 사용자 이름과 비밀번호가 필요합니다.
{: tsSymptoms}

 

이 문제점은 로그인 세션 제한시간 초과로 인해 발생합니다.
{: tsCauses}

 

솔루션은 사용자 이름과 비밀번호를 다시 입력하는 것입니다.
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

  * 추적 및 덤프 관리 기능은 실행 중인 애플리케이션 인스턴스에만 사용할 수 있습니다. 중지, 시작 중 또는 충돌됨 상태의 애플리케이션 인스턴스에는 추적 및 덤프 오퍼레이션을 사용할 수 없습니다.
  * 추적 또는 덤프 대화 상자가 열린 경우 애플리케이션 인스턴스의 상태가 변경됩니다. 
  


솔루션은 창을 닫았다가 다시 여는 것입니다.
{: tsResolve} 



## 인스턴스별 traceSpecification 구성이 다름
{: #ts_different_config}

 

하나의 애플리케이션의 다른 인스턴스에서 traceSpecification 구성이 다를 수 있습니다.
{: tsSymptoms}

 

이 문제점은 다음과 같은 이유로 발생합니다.
{: tsCauses}

  * 이전에는 하나 이상의 인스턴스에 대한 구성을 변경할 수 있었습니다. 하나의 인스턴스에 대한 traceSpecification 구성을 변경한 경우, 동일한 애플리케이션의 다른 인스턴스에 적용되지 않습니다. 예를 들어, 애플리케이션이 log4j를 사용하고 이 애플리케이션에 대해 2개의 인스턴스가 있습니다. 인스턴스 0의 로그 레벨을 정보에서 디버그로 변경할 수 있지만, 인스턴스 1의 로그 레벨은 정보로 남아 있습니다. 
  * 애플리케이션이 스케일 확장되고 새 인스턴스를 갖습니다. RMU에서 기존 인스턴스의 traceSpecification 구성을 스케일 확장된 새 인스턴스에 적용하지 않습니다. 새 인스턴스는 기본 구성을 사용합니다. 예를 들어, 애플리케이션이 log4j를 사용하고 1개의 인스턴스가 있습니다. 이 인스턴스의 로그 레벨을 정보에서 디버그로 변경할 수 있습니다. 이렇게 변경한 후 애플리케이션을 두 개의 인스턴스로 스케일 확장하는 경우 새 인스턴스의 로그 레벨은 디버그가 아닌 정보입니다.
  


이는 예상된 동작입니다.
{: tsResolve} 





## 디스크 할당량이 초과됨
{: #ts_diskquota}

앱 로그에 디스크 할당량이 초과되었다고 표시될 수 있습니다.

 

앱 로그에 `디스크 할당량 초과` 오류 메시지가 표시됩니다.
{: tsSymptoms}



이 문제점은 다음 이유 중 하나로 발생합니다.
{: tsCauses} 

  * 애플리케이션 인스턴스가 실행 중인 상태에서 덤프 파일이 생성되었으며, 파일이 디스크 할당량을 모두 사용했습니다. 기본적으로 한 애플리케이션 인스턴스의 디스크 할당량은 1GB입니다. **대시보드>애플리케이션>앱 런타임**을 클릭하면 디스크 사용량을 확인할 수 있습니다. 다음 예에서는 애플리케이션의 두 디스크 인스턴스에 대해 디스크 사용량 등의 런타임 정보를 보여줍니다. 
    ```
    Instance	State	CPU	Memory Usage	Disk Usage

	0		Running	1.0%	344.8MB/512MB	236.8MB/1GB
	2		Running	2.3%	361.2MB/512MB	235.7MB/1GB
    ```
  * 디스크 할당량은 현재 조직 할당량으로 제한됩니다.
  
  


이 문제를 해결하려면 다음 방법 중 하나를 사용하십시오.
{: tsResolve} 

  * 덤프 파일을 다운로드한 후 삭제하십시오.
  * 배치 Manifest에 다음 항목을 포함시켜 디스크 할당량 늘려 애플리케이션을 다시 배치하십시오. 
    ```
	disk_quota: 2048
	```
	
	
<!-- begin STAGING ONLY --> 

	
## Log4js 로거 오브젝트가 Node.js 추적 팝업 창에 표시되지 않음
{: #ts_logger}

앱에서 log4js 모듈과 ibmbluemix 모듈이 모두 사용되는 경우 log4js 로거 오브젝트가 Node.js 추적 팝업 창에 표시되지 않습니다.  	

 
앱에서 log4js, winston, ibmbluemix 모듈이 사용되는 경우 log4js 로거 오브젝트가 Node.js 추적 팝업 창에 표시되지 않습니다.
{: tsSymptoms}


ibmbluemix 모듈은 로그 오퍼레이션에 log4js 모듈과 winston 모듈을 사용하는 통합 API를 제공하므로 ibmbluemix 로거 오브젝트만 Node.js 추적 팝업 창에 표시됩니다. 이는 ibmbluemix, log4js, winston 로거 오브젝트에 대한 로그 레벨 설정을 서로 겹쳐쓰지 않기 위해서입니다.
{: tsCauses}


이는 예상된 동작입니다.
{: tsResolve}

<!-- end STAGING ONLY -->




<!-- begin STAGING ONLY -->


## 애플리케이션의 모든 인스턴스에 추적 설정 적용 선택란이 사용 안함으로 설정됨
{: #ts_bunyan}

Bunyan 로거 레벨이 수정되는 경우 **애플리케이션의 모든 인스턴스에 추적 설정 적용** 선택란이 선택 취소되고 Node.js 추적 팝업 창에서 사용 안함으로 설정됩니다. 



Bunyan 로거 오브젝트의 레벨을 변경하면 **애플리케이션의 모든 인스턴스에 추적 설정 적용** 선택란이 선택 취소되고 Node.js 추적 팝업 창에서 사용 안함으롤 설정됩니다.
{: tsSymptoms} 

 

Bunyan 로그 레벨이 수정되는 경우 애플리케이션의 모든 인스턴스에 추적 설정을 적용할 수 없습니다. Bunyan 라이브러리에서 Bunyan 로거 오브젝트의 이름 또는 ID가 고유하지 않아도 되기 때문입니다. 애플리케이션의 로그 메시지에서 레벨을 지정하는 데 사용되는 둘 이상의 Bunyan 로거 오브젝트에서 동일한 이름 또는 ID를 사용할 수 있습니다. 그러므로 애플리케이션에 대한 추적 설정이 사용되는 경우 애플리케이션의 로그 메시지에 지정된 로그 레벨은 정확하지 않습니다.
{: tsCauses}




이는 예상된 동작입니다.
{: tsResolve} 

<!-- end STAGING ONLY -->

