{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

*마지막 업데이트 날짜: 2016년 1월 12일*

# Python 런타임
{: #python_runtime}

{{site.data.keyword.Bluemix}}의 Python 런타임은 python_buildpack 기반입니다.
python_buildpack은 Python 앱을 위한 전체 런타임 환경을 제공합니다.
{: shortdesc}

앱의 루트 디렉토리에 requirements.txt 파일 또는 setup.py 파일이 포함되어 있는 경우 python_buildpack이 사용됩니다. 

## 스타터 애플리케이션
{: #starter_application}

{{site.data.keyword.Bluemix}}는 Python 스타터 애플리케이션을 제공합니다. Python 스타터 애플리케이션은 사용자가 앱에 사용할 수 있는 템플리트를 제공하는 단순 Python 앱입니다. 스타터 앱을 실험해 보고 필요한 변경사항을 작성하고 이를 {{site.data.keyword.Bluemix}} 환경에 푸시할 수 있습니다. 스타터 애플리케이션 사용에 대한 지원이 필요한 경우 [스타터 애플리케이션 사용](../../cfapps/starter_app_usage.html)을 참조하십시오. 

## 런타임 버전
{: #runtime_versions}

애플리케이션의 루트에 있는 runtime.txt 파일의 python-versionnumber를 설정하여 앱에서 사용할 Python 버전을 지정할 수 있습니다. 예를 들면, 다음과 같습니다. 

```
python-3.4.3
```
{: codeblock}


### 사용 가능한 버전: 
{: #available_versions}

다음은 현재 {{site.data.keyword.Bluemix}}에 설치되어 있는 [Python
빌드팩](https://github.com/cloudfoundry/python-buildpack/releases/tag/v1.5.1)에서 사용 가능한 Python 버전입니다. 

* 2.7.9
* 2.7.10
* 3.3.5
* 3.3.6
* 3.4.2
* 3.4.3
* 3.5.0

애플리케이션에서 목록에 없는 Python 버전을 필요로 하는 경우 앱을 배치하기 위해
외부 [Python 빌드팩](https://github.com/cloudfoundry/python-buildpack)을 사용할 수 있습니다.


## 관련 링크
{: #related_links}
* [Python용 Cloud Foundry 빌드팩](https://github.com/cloudfoundry/python-buildpack)
