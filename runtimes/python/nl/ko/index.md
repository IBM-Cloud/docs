---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-14"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Python
{: #python_runtime}

{{site.data.keyword.Bluemix}}의 Python 런타임은 python_buildpack을 통해 제공됩니다.
python_buildpack은 Python 2 및 Python 3 앱 둘 다를 위한 전체 런타임 환경을 제공합니다.
{: shortdesc}

python_buildpack은 앱의 루트 디렉토리에 requirements.txt 파일 또는 setup.py 파일이 포함된 경우 사용됩니다. 

## 스타터 애플리케이션
{: #starter_application}

{{site.data.keyword.Bluemix}}는 Python 스타터 애플리케이션을 제공합니다. Python 스타터 애플리케이션은 앱에 사용할 수 있는 템플리트를 제공하는 단순한 Python 앱입니다. 스타터 앱을 사용하여 시험해 볼 수 있으며 {{site.data.keyword.Bluemix}} 환경을 변경하고 변경사항을 푸시할 수
있습니다. 스타터 애플리케이션 사용에 대한 도움말은 [스타터 애플리케이션 사용](/docs/cfapps/starter_app_usage.html)을 참조하십시오. 

## 런타임 버전
{: #runtime_versions}

애플리케이션 루트에 있는 runtime.txt 파일에서 python-versionnumber를 설정하여 앱에서 사용할 Python 버전을 지정할 수 있습니다. 예: 

```
python-3.5.0
```
{: codeblock}

버전이 지정되지 않은 경우 기본적으로 버전 2.7.11이 선택됩니다.

### 사용 가능한 버전: 
{: #available_versions}

다음 Python 버전은 현재
{{site.data.keyword.Bluemix}}에 설치된 [Python 빌드팩](https://github.com/cloudfoundry/python-buildpack/releases/tag/v1.5.5)에서 사용
가능합니다. 

* 2.7.10
* 2.7.11
* 3.3.5
* 3.3.6
* 3.4.3
* 3.4.4
* 3.5.0
* 3.5.1

나열되지 않은 Python 버전이 애플리케이션에 필요한 경우
외부
[Python 빌드팩](https://github.com/cloudfoundry/python-buildpack)을 사용하여 애플리케이션을 배치할 수
있습니다. 

# 관련 링크
## 일반
* [Python에 대한 Cloud Foundry 빌드팩](https://github.com/cloudfoundry/python-buildpack)
