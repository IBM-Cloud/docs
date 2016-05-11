# iOS 앱을 위한 푸시 SDK 초기화
{: #enable-push-ios-notifications-install}

기존 Xcode 프로젝트의 경우 CocoaPods 종속 항목 관리 도구를 사용하여 Bluemix Mobile Services Client SDK를 설정할 수 있습니다. 또는 SDK를 수동으로 설치할 수 있습니다. 

**참고**: Swift Push readme 파일을 보려면 https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master 로 이동하십시오. 

##CocoaPods 설치

1. Mac 터미널에서 다음 명령을 사용하여 CocoaPods를 설치하십시오.
```
$ sudo gem install cocoapods
```
2. 터미널에서 다음 명령을 입력하여 CocoaPods를 초기화하십시오.
이 명령을 실행할 경우 Xcode 프로젝트가 있는 디렉토리에서 실행해야 합니다. ``pod init`` 명령에서 파일 제목을 작성합니다.```
$ pod init
``
3. 생성된 Podfile에서 필요한 SDK 종속 항목을 추가하십시오. 다음 Podfile을 복사하십시오.

   Objective-C

    ```
    source 'https://github.com/CocoaPods/Specs.git'
	Copy the following list as is and remove the dependencies you do not need
	pod 'IMFCore'
	pod 'IMFPush'
	```

   Swift

	```
	source 'https://github.com/CocoaPods/Specs.git'
	// Copy the following list as is and remove the dependencies you do not need.
	use_frameworks!

	target 'MyApp' do
	    platform :ios, '8.0'
	    pod 'BMSCore'
	    pod 'BMSPush'
	end
	```
3. 터미널에서 프로젝트 폴더로 이동한 후, 다음 명령을 사용하여 종속 항목을 설치하십시오.
```
$ pod update
```
해당 명령은 종속 항목을 설치하고 새 Xcode 작업공간을 작성합니다. **참고**: 원래 Xcode 프로젝트 파일 대신, 반드시 항상 새 Xcode 작업공간을 여십시오. 

	```
	$ open App.xcworkspace
	```
작업공간에는 원래 프로젝트 및 종속 항목이 포함된 Pods 프로젝트가 있습니다. Bluemix Mobile Services 소스 폴더를 수정하려는 경우, `Pods/yourImportedSourceFolder`아래의 Pods 프로젝트에서 폴더를 찾을 수 있습니다(예: `Pods/IMFGoogleAuthentication`).

##가져온 프레임워크 및 소스 폴더 사용

코드에서 SDK를 참조하십시오. 


### Objective-C

관련 헤더에 대해 #import 지시문을 작성합니다. 예: 

```
//Objective-C

#import <IMFCore/IMFCore.h>
#import <IMFPush/IMFPush.h>
```

**참고**: CocoaPods 명령 `pod install` 또는 `pod update`를 사용하여 Pods 프로젝트를 업데이트하면 Bluemix Mobile Services 소스 폴더를 대체할 수 있습니다. 원래 파일의 사용자 정의한 버전을 유지하려면, 이러한 명령을 실행하기 전에
해당 버전을 백업해야 합니다. 

###Swift

**사전 전제조건**

- iOS 8.0 이상
- Xcode 7


관련 헤더에 대해 #import 지시문을 작성합니다. 예: 

```
//swift
import BMSCore
import BMSPush
```


##빌드 설정

**Xcode > 빌드 설정 > 빌드 옵션 및 Bitcode 사용 설정**으로 이동하여 **No**로 설정하십시오.

**주의**: iOS 9의 경우, ATS(App Transport Security) 기능을 변경하면 인증 프로세스의 처리 방식에 영향이 미칠 수 있습니다. 다음 블로그 포스팅에서 이러한 변경에 대해 자세히 설명합니다. [iOS 9의 ATS 및 Bitcode](https://developer.ibm.com/mobilefirstplatform/2015/09/09/ats-and-bitcode-in-ios9/) 및 [지금 Bluemix에 iOS 9 앱 연결](https://developer.ibm.com/bluemix/2015/09/16/connect-your-ios-9-app-to-bluemix/)
