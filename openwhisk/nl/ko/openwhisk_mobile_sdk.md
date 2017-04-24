
# OpenWhisk 모바일 SDK 사용

OpenWhisk에서는 쉽게 원격 트리거를 실행하고 원격 조치를 호출할 수 있도록 모바일 앱을 사용하는 iOS 및 watchOS 디바이스에 대한 모바일 SDK를 제공합니다. 현재 Android용 버전은 사용할 수 없습니다. Android 개발자는 직접 OpenWhisk REST API를 사용할 수 있습니다. 

모바일 SDK는 Swift 3.0로 작성되고 iOS 10 이상의 릴리스를 지원합니다. Xcode 8.0을 사용하여 모바일 SDK를 빌드할 수 있습니다. SDK의 Legacy Swift 2.2/Xcode 7 버전은 현재 더 이상 사용되지 않지만 0.1.7까지 사용 가능합니다. 

## 앱에 SDK 추가

CocoaPods, Carthage를 사용하거나 소스 디렉토리에서 모바일 SDK를 설치할 수 있습니다.

### CocoaPods를 사용하여 설치

모바일용 OpenWhisk SDK는 CocoaPods를 통해 공용 배포에 대해 사용 가능합니다. CocoaPods가 설치되었다고 가정하고, 스타터 앱 프로젝트 디렉토리 내의 'Podfile'이라고 하는 파일에 다음 행을 두십시오. 

```
install! 'cocoapods', :deterministic_uuids => false
use_frameworks!

target 'MyApp' do
     pod 'OpenWhisk', :git => 'https://github.com/openwhisk/openwhisk-client-swift.git', :tag => '0.2.2'
end

target 'MyApp WatchKit Extension' do
     pod 'OpenWhisk', :git => 'https://github.com/openwhisk/openwhisk-client-swift.git', :tag => '0.2.2'
end
```

명령행에서 `pod install`을 입력하십시오. 이 명령은 watchOS 확장이 있는 iOS 앱용 SDK를 설치합니다. CocoaPods에서 앱용으로 작성하는 작업공간 파일을 사용하여 Xcode에서 프로젝트를 여십시오.  

설치 후 프로젝트 작업공간을 여십시오. 빌드할 때 다음 경고가 표시될 수 있습니다.
`Use Legacy Swift Language Version” (SWIFT_VERSION) is required to be configured correctly for targets which use Swift. Use the [Edit > Convert > To Current Swift Syntax…] menu to choose a Swift version or use the Build Settings editor to configure the build setting directly.`
이 경고는 Cocoapods가 Pods 프로젝트에서 Swift 버전을 업데이트하지 않은 경우 발생합니다. 해결하려면 Pods 프로젝트 및 OpenWhisk 대상을 선택하십시오. 빌드 설정으로 이동하여 `Use Legacy Swift Language Version`을 `no`로 설정을 변경하십시오. 또는 Podfile의 끝에 다음 설치 후 지시사항을 추가할 수 있습니다.

```
post_install do |installer|
  installer.pods_project.targets.each do |target|
    target.build_configurations.each do |config|
      config.build_settings['SWIFT_VERSION'] = '3.0'
    end
  end
end
```

### Carthage를 사용하여 설치

앱의 프로젝트 디렉토리에서 파일을 작성하고 이름을 'Cartfile'로 지정하십시오. 파일에 다음 행을 넣으십시오. 
```
github "openwhisk/openwhisk-client-swift.git" ~> 0.2.2 # Or latest version
```

명령행에서 `carthage update --platform ios`를 입력하십시오. Carthage가 SDK를 다운로드하여 빌드하고 사용자 앱의 프로젝트 디렉토리에 Carthage라는 디렉토리를 작성하고 OpenWhisk.framework 파일을 Carthage/build/iOS 내에 배치합니다. 

그런 다음 OpenWhisk.framework를 Xcode 프로젝트의 임베디드 프레임워크에 추가해야 합니다. 

### 소스 코드에서 설치

소스 코드는 https://github.com/openwhisk/openwhisk-client-swift.git에서 사용 가능합니다.
Xcode를 통해 `OpenWhisk.xcodeproj`를 사용하여 프로젝트를 여십시오.
프로젝트는 "OpenWhisk"(iOS 대상)와 "OpenWhiskWatch"(watchOS 2 대상)라는 두 개의 스킴을 포함합니다.
필요한 대상의 프로젝트를 빌드하고 결과 프레임워크를 앱(일반적으로 ~/Library/Developer/Xcode/DerivedData/사용자 앱 이름에 있음)에 추가하십시오. 

## 스타터 앱 설치 예

OpenWhisk CLI를 사용하여 OpenWhisk SDK 프레임워크를 임베드하는 예제 코드를 다운로드할 수 있습니다.  

스타터 앱 예제를 설치하려면 다음 명령을 입력하십시오. 
```
$ wsk sdk install iOS
```

이 명령은 스타터 앱이 포함된 압축 파일을 다운로드합니다. 프로젝트 디렉토리에 podfile이 있습니다. 

SDK를 설치하려면 다음 명령을 입력하십시오.
```
$ pod install
```

## SDK 시작하기

신속하게 시작하고 실행하려면 OpenWhisk API 신임 정보를 사용하여 WhiskCredentials 오브젝트를 작성하고 오브젝트에서 OpenWhisk 인스턴스를 작성하십시오. 

예를 들어, 다음 예제 코드를 사용하여 신임 정보 오브젝트를 작성하십시오.

```
let credentialsConfiguration = WhiskCredentials(accessKey: "myKey", accessToken: "myToken")
let whisk = Whisk(credentials: credentialsConfiguration!)
```

앞의 예제에서 OpenWhisk에서 가져온 `myKey`와 `myToken`을 전달합니다. 다음 CLI 명령을 사용하여 키 및 토큰을 검색할 수 있습니다.

```
$ wsk property get --auth
```
```
whisk auth        kkkkkkkk-kkkk-kkkk-kkkk-kkkkkkkkkkkk:tttttttttttttttttttttttttttttttttttttttttttttttttttttttttttttttt
```

콜론 앞의 문자열이 키이고 콜론 뒤의 문자열은 토큰입니다. 

## OpenWhisk 조치 호출


원격 조치를 호출하려면 조치 이름을 사용하여 `invokeAction`을 호출하십시오. 조치가 속한 네임스페이스를 지정하거나 기본 네임스페이스를 승인하도록 공백으로 둘 수 있습니다. 필요한 경우, 사전을 사용하여 조치에 매개변수를 전달하십시오.

예를 들어, 다음과 같습니다. 

```swift
// In this example, we are invoking an action to print a message to the OpenWhisk Console
var params = Dictionary<String, String>()
params["payload"] = "Hi from mobile"
do {
    try whisk.invokeAction(name: "helloConsole", package: "mypackage", namespace: "mynamespace", parameters: params, hasResult: false, callback: {(reply, error) -> Void in
        if let error = error {
            //do something
            print("Error invoking action \(error.localizedDescription)")
        } else {
            print("Action invoked!")
        }

    })
} catch {
    print("Error \(error)")
}
```

앞의 예에서 기본 네임스페이스를 사용하여 `helloConsole` 조치를 호출합니다.

## OpenWhisk 트리거 실행

원격 트리거를 실행하기 위해 `fireTrigger` 메소드를 호출할 수 있습니다. 사전을 사용하여 필요한 매개변수를 전달하십시오.

```swift
// In this example we are firing a trigger when our location has changed by a certain amount
var locationParams = Dictionary<String, String>()
locationParams["payload"] = "{\"lat\":41.27093, \"lon\":-73.77763}"
do {
    try whisk.fireTrigger(name: "locationChanged", package: "mypackage", namespace: "mynamespace", parameters: locationParams, callback: {(reply, error) -> Void in
        if let error = error {
            print("Error firing trigger \(error.localizedDescription)")
        } else {
            print("Trigger fired!")
        }
    })
} catch {
    print("Error \(error)")
}
```

앞의 예에서 `locationChanged`라는 트리거를 실행합니다. 

## 결과를 리턴하는 조치 사용

조치가 결과를 리턴하는 경우, invokeAction 호출에서 hasResult를 true로 설정하십시오. 조치의 결과는 응답 사전에서 리턴됩니다. 예를 들어, 다음과 같습니다.

```swift
do {
    try whisk.invokeAction(name: "actionWithResult", package: "mypackage", namespace: "mynamespace", parameters: params, hasResult: true, callback: {(reply, error) -> Void in
        if let error = error {
            //do something
            print("Error invoking action \(error.localizedDescription)")
        } else {
            var result = reply["result"]
            print("Got result \(result)")
        }


    })
} catch {
    print("Error \(error)")
}
```

기본적으로 SDK는 호출된 조치에서 생성되는 결과와 활성화 ID만 리턴합니다. HTTP 응답 상태 코드를 포함하여 전체 응답 오브젝트의 메타데이터를 가져오려면 다음 설정을 사용하십시오.

```swift
whisk.verboseReplies = true
```

## SDK 구성

baseURL 매개변수를 사용하면 OpenWhisk의 다른 설치와 함께 작업하도록 SDK를 구성할 수 있습니다. 예를 들어, 다음과 같습니다.

```swift
whisk.baseURL = "http://localhost:8080"
```

이 예에서는 localhost:8080에서 실행 중인 설치를 사용합니다. baseUrl을 지정하지 않으면 모바일 SDK가 다음에서 실행되는 인스턴스를 사용합니다. https://openwhisk.ng.bluemix.net 

특수 네트워크 처리가 필요한 경우 사용자 정의 NSURLSession을 패스할 수 있습니다. 예를 들어, 자체 서명된 인증서를 사용하는 OpenWhisk 설치가 있을 수 있습니다.

```swift
// create a network delegate that trusts everything
class NetworkUtilsDelegate: NSObject, NSURLSessionDelegate {
    func URLSession(session: NSURLSession, didReceiveChallenge challenge: NSURLAuthenticationChallenge, completionHandler: (NSURLSessionAuthChallengeDisposition, NSURLCredential?) -> Void) {
        completionHandler(NSURLSessionAuthChallengeDisposition.UseCredential, NSURLCredential(forTrust: challenge.protectionSpace.serverTrust!))
    }
}
// create an NSURLSession that uses the trusting delegate
let session = NSURLSession(configuration: NSURLSessionConfiguration.defaultSessionConfiguration(), delegate: NetworkUtilsDelegate(), delegateQueue:NSOperationQueue.mainQueue())
// set the SDK to use this urlSession instead of the default shared one
whisk.urlSession = session
```

### 규정된 이름 지원

모든 조치 및 트리거는 네임스페이스, 패키지 및 조치 또는 트리거 이름으로 구성된 완전한 이름을 가지고 있습니다. SDK는 조치를 호출하거나 트리거를 실행할 때 이러한 요소를 매개변수로 허용할 수 있습니다. 또한 SDK는 `/mynamespace/mypackage/nameOfActionOrTrigger`와 같은 완전한 이름을 허용하는 기능을 제공합니다. 규정된 이름 문자열은 모든 OpenWhisk 사용자가 가진 네임스페이스 및 패키지에 대한 이름이 지정되지 않은 기본값을 지원하므로 다음 구문 분석 규칙이 적용됩니다.

- qName = "foo"는 결과적으로 네임스페이스 = 기본값, 패키지 = 기본값, 조치/트리거 = "foo"가 됨
- qName = "mypackage/foo"는 결과적으로 네임스페이스 = 기본값, 패키지는 = mypackage, 조치/트리거 = "foo"가 됨
- qName = "/mynamespace/foo"는 결과적으로 네임스페이스 = mynamespace, 패키지 = 기본값, 조치/트리거 = "foo"가 됨
- qName = "/mynamespace/mypackage/foo"는 결과적으로 네임스페이스 = mynamespace, 패키지 = mypackage, 조치/트리거 = "foo"가 됨

모든 기타 조합은 WhiskError.QualifiedName 오류를 발생시킵니다. 따라서 규정된 이름을 사용할 경우 "`do/try/catch`" 구성에서 호출을 랩핑해야 합니다. 

### SDK 단추

편의상 SDK에는 조치를 호출할 수 있도록 해주는 `UIButton`을 확장하는 `WhiskButton`이 포함됩니다. `WhiskButton`을 사용하려면 다음 예를 따르십시오.

```swift
var whiskButton = WhiskButton(frame: CGRectMake(0,0,20,20))

whiskButton.setupWhiskAction("helloConsole", package: "mypackage", namespace: "_", credentials: credentialsConfiguration!, hasResult: false, parameters: nil, urlSession: nil)
let myParams = ["name":"value"]
// Call this when you detect a press event, e.g. in an IBAction, to invoke the action
whiskButton.invokeAction(parameters: myParams, callback: { reply, error in
    if let error = error {
        print("Oh no, error: \(error)")
    } else {
        print("Success: \(reply)")
    }
})
// or alternatively you can set up a "self contained" button that listens for press events on itself and invokes an action
var whiskButtonSelfContained = WhiskButton(frame: CGRectMake(0,0,20,20))
whiskButtonSelfContained.listenForPressEvents = true
do {

   // use qualified name API which requires do/try/catch
   try whiskButtonSelfContained.setupWhiskAction("mypackage/helloConsole", credentials: credentialsConfiguration!, hasResult: false, parameters: nil, urlSession: nil)
   whiskButtonSelfContained.actionButtonCallback = { reply, error in
       if let error = error {
           print("Oh no, error: \(error)")
       } else {
           print("Success: \(reply)")
       }
   }
} catch {
   print("Error setting up button \(error)")
}
```
