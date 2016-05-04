---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Go
{: #go_runtime}
*마지막 업데이트 날짜: 2016년 3월 16일*

{{site.data.keyword.Bluemix}}의 Go 런타임은 go_buildpack을 통해 제공됩니다.
go_buildpack은 Go 앱을 위한 완전한 런타임 환경을 제공합니다.
{: shortdesc}

go_buildpack은 애플리케이션에 *.go 파일이 포함된 경우에 사용됩니다.

## 스타터 애플리케이션
{: #starter_application}

{{site.data.keyword.Bluemix}}는 Go 스타터 애플리케이션을 제공합니다. Go 스타터 애플리케이션은 앱에 사용할 수 있는 템플리트를 제공하는 단순한 Go 앱입니다. 스타터 앱을 사용하여 시험해 볼 수 있으며 Bluemix 환경을 변경하고 변경사항을 푸시할 수 있습니다. 스타터 애플리케이션 사용에 대한 도움말은 [스타터 애플리케이션 사용](../../cfapps/starter_app_usage.html)을 참조하십시오. 

## 런타임 버전
{: #runtime_versions}

애플리케이션 루트에 있는 Godeps/Godeps.json 파일에서 GoVersion 특성을 설정하여 앱에서 사용할 Go 버전을 지정할 수 있습니다. 예:

```
{
	"ImportPath": "gohelloworld",
	"GoVersion": "go1.3.3",
	"Deps": []
}
```
{: codeblock}
자세한 정보는 [godep](https://github.com/tools/godep){: new_window}를 참조하십시오.

### 사용 가능한 버전: 
{: #available_versions}

다음 Go 버전은 현재 {{site.data.keyword.Bluemix}}에 설치된 [Go 빌드팩](https://github.com/cloudfoundry/go-buildpack/releases/tag/v1.6.2){: new_window}에서 사용 가능합니다.


* 1.2.1
* 1.2.2
* 1.3.2
* 1.3.3
* 1.4.2
* 1.4.3
* 1.5
* 1.5.1

나열되지 않은 Go 버전이 애플리케이션에 필요한 경우
외부 [Go 빌드팩](https://github.com/cloudfoundry/go-buildpack.git){: new_window}을 사용하여 애플리케이션을 배치할 수 있습니다.


# 관련 링크
## 일반
* [GoLang](http://golang.org/){: new_window}
* [Go에 대한 Cloud Foundry 빌드팩](https://github.com/cloudfoundry/go-buildpack){: new_window}
