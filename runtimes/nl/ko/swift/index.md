{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .pre}


# Swift 런타임
{: #swift_runtime}
*마지막 업데이트 날짜: 2016년 6월 10일*
{: .last-updated}

{{site.data.keyword.Bluemix}}의 Swift 런타임은 Bluemix용 Swift 빌드팩(예: swift_buildpack)을 통해 제공됩니다.
swift_buildpack은 Swift 애플리케이션을 위한 완전한 런타임 환경을 제공합니다.
{: shortdesc}

swift_buildpack은 앱의 루트 디렉토리에 Package.swift 파일이 포함된 경우 사용됩니다. 

## 스타터 애플리케이션
{: #starter_application}

{{site.data.keyword.Bluemix}}는 Swift 스타터 애플리케이션을 제공합니다. Swift 스타터 애플리케이션은 Swift 프로그래밍 언어를 사용하여 개발할 수 있는 서버 애플리케이션 유형에 대해 학습하는 데 사용할 수 있는 단순한 Swift 앱니다. 이 샘플 앱은 클라이언트에 HTML 컨텐트를 리턴하는 기본 HTT 서버를 작성합니다. 

**참고:** 이 스타터 애플리케이션은 프로덕션-준비 애플리케이션이 아닙니다. 대신 이는 교육용으로 사용됩니다. 스타터 앱을 사용하여 시험해 볼 수 있으며 {{site.data.keyword.Bluemix}} 환경을 변경하고 변경사항을 푸시할 수 있습니다. 스타터 애플리케이션 사용에 대한 도움말은 [스타터 애플리케이션 사용](../../cfapps/starter_app_usage.html)을 참조하십시오. 

## 런타임 버전
{: #runtime_versions}

Bluemix에 설치된 swift_buildpack은 Swift 2진의 `DEVELOPMENT-SNAPSHOT-2016-05-03-a` 버전을 지원합니다.애플리케이션에 대해 Bluemix에서 다른 버전의 Swift를 사용하려는 경우 사용자 저장소의 루트에 있는 `.swift-version` 파일을 사용하여 버전을 지정할 수 있습니다. 

```
cat .swift-version
swift-DEVELOPMENT-SNAPSHOT-2016-04-25-a
```
{: pre}

`.swift-version` 파일을 포함하는 것 외에 다음과 같이 `-b https://github.com/IBM-Swift/swift-buildpack` 매개변수를 `cf push` 명령에 추가해야 합니다. 

```
cf push -b https://github.com/IBM-Swift/swift-buildpack
```

Swift 지원 버전의 전체 목록은 빌드팩의 [manifest.yml](https://github.com/IBM-Swift/swift-buildpack/blob/bluemix-buildpack/manifest.yml) 파일을 참조하십시오. 

{{site.data.keyword.Bluemix}}에 설치된 Swift 빌드팩의 현재 버전에 대해 알아보려면 빌드팩의 [릴리스 정보](https://github.com/IBM-Swift/swift-buildpack/releases/tag/1.1.1)를 참조하십시오.

Swift 언어는 자주 변경되므로 사용자 애플리케이션이 함께 작동하는 것으로 알려진 Swift 버전에 "고정"되도록 `.swift-version` 파일을 포함해야 합니다. `DEVELOPMENT-SNAPSHOT-2016-05-03-a` 이외의 Swift 버전을 사용 중이라면 앱을 푸시할 때 `-b https://github.com/IBM-Swift/swift-buildpack` 매개변수를 지정해야 합니다(아래 참조).

# 관련 링크
{: #rellinks}
## 일반
{: #general}
* [Bluemix용 Swift 빌드팩](https://github.com/IBM-Swift/swift-buildpack)
* [Swift 언어 문서](https://swift.org/)
