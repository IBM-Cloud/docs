{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

*마지막 업데이트 날짜: 2016년 1월 12일*

# Go 런타임
{: #go_runtime}

{{site.data.keyword.Bluemix}}의 Go 런타임은 go_buildpack 기반입니다.
go_buildpack은 Go 앱을 위한 전체 런타임 환경을 제공합니다.
{: shortdesc}

애플리케이션에 *.go 파일이 있는 경우 go_buildpack이 사용됩니다. 

## 스타터 애플리케이션
{: #starter_application}

{{site.data.keyword.Bluemix}}는 Go 스타터 애플리케이션을 제공합니다. Go 스타터 애플리케이션은 사용자가 앱에 사용할 수 있는 템플리트를 제공하는 단순 Go 앱입니다. 스타터 앱을 실험해 보고 필요한 변경사항을 작성하고 이를 Bulemix 환경에 푸시할 수 있습니다. 스타터 애플리케이션 사용에 대한 지원이 필요한 경우 [스타터 애플리케이션 사용](../../cfapps/starter_app_usage.html)을 참조하십시오. 

## 런타임 버전
{: #runtime_versions}

애플리케이션의 루트에 있는 Godeps/Godeps.json 파일에서 GoVersion 특성을 설정하여 앱이 사용할 Go 버전을 지정할 수 있습니다. 예를 들면, 다음과 같습니다. 

```
{
	"ImportPath": "gohelloworld",
	"GoVersion": "go1.3.3",
	"Deps": []
}
```
{: codeblock}
자세한 정보는
[godep](https://github.com/tools/godep)를 참조하십시오.

### 사용 가능한 버전: 
{: #available_versions}

다음은 현재 {{site.data.keyword.Bluemix}}에 설치되어 있는 [Go
빌드팩](https://github.com/cloudfoundry/go-buildpack/releases/tag/v1.6.2)에서 사용 가능한 Go 버전입니다. 

* 1.2.1
* 1.2.2
* 1.3.2
* 1.3.3
* 1.4.2
* 1.4.3
* 1.5
* 1.5.1

앱에서 목록에 없는 Go 버전을 필요로 하는 경우 애플리케이션을 배치하기 위해 외부 [Go 빌드팩](https://github.com/cloudfoundry/go-buildpack.git)을 사용할 수 있습니다. 

## 관련 링크
{: #related_links}
* [GoLang](http://golang.org/)
* [Go용 Cloud Foundry 빌드팩](https://github.com/cloudfoundry/go-buildpack)
