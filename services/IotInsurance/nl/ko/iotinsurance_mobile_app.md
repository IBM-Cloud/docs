---

copyright:
  years: 2016

---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


<!-- {{site.data.keyword.iotinsurance_full}}  {{site.data.keyword.iotinsurance_short}}  -->


# 샘플 모바일 앱 설치 및 연결
{: #iotins_gettingstarted}
마지막 업데이트 날짜: 2016년 9월 15일
{: .last-updated}

{{site.data.keyword.iotinsurance_full}} 샘플 모바일 앱은 {{site.data.keyword.iotinsurance_short}}의 모바일 클라이언트에서 사용할 참조 구현입니다. 앱을 사용하여 시스템에 새 디바이스를 등록하고 해당 디바이스와 대한 경보를 받을 수 있습니다.
{:shortdesc}

**전제조건** 시작하기 전에 다음 전제조건에 부합하는지 확인하십시오. 
  - Apple Xcode 7.3 이상 통합 개발 환경.
  - iOS 9.0 이상 iPhone 모바일 디바이스.
  - 컴퓨터에 설치된 CocoaPods. [CocoaPods 웹 사이트](https://guides.cocoapods.org/using/getting-started.html)를 참조하십시오. 
  - 샘플 모바일 앱을 서비스의 인스턴스에 연결하는 데 필요한 [parameters](#iot4i_mobileParam).

## 샘플 모바일 앱 빌드
{: #building_mobile}
샘플 모바일 앱을 사용해보려면 다음 태스크를 수행하십시오. 

1. [샘플 모바일 앱의 소스 코드 저장소](https://github.com/ibm-watson-iot/ioti-mobile)를 Xcode 7.3 이상이 설치되어 있는 컴퓨터에 복제하십시오. 
2. 필수 패키지를 설치하고 프로젝트에서 CocoaPods pod install 명령을 실행하여 IoT4I.xcworkspace 파일을 생성하십시오. 이 태스크를 완료하려면 CocoaPod가 반드시 설치되어야 합니다. 
3. IoT4I.xcworkspace 파일을 두 번 클릭하여 Xcode에서 프로젝트를 여십시오. 
4. iPhone을 컴퓨터에 연결하고 빌드 대상으로 선택하십시오. 
5. 파일 목록에서 IoT4I 파일을 선택하여 ID 대화 상자를 표시하십시오. 
6. Xcode의 ID 대화 상자에서 다음과 같이 변경하십시오. 
  - **번들 ID**를 고유 ID로 변경하십시오. 예: **myIoT4Ibundle**.
  - **팀**을 개인 팀 이름으로 설정한 후 **문제 수정**을 클릭하십시오. 
7. 앱을 {{site.data.keyword.iotinsurance_short}}의 인스턴스에 연결하려면 **constants.swift** 파일에서 다음 매개변수를 설정하십시오.   
    - [applicationRoute](#iot4i_mobileParam) = {{site.data.keyword.iotinsurance_short}} 인스턴스의 URL
    - [applicationId](#iot4i_mobileParam) = {{site.data.keyword.amashort}} 인스턴스의 URL
8. 컴퓨터에서 화살표를 클릭하여 현재 스킴을 빌드하고 실행하십시오. 샘플 모바일 앱이 휴대폰에 설치됩니다. 자세한 정보는 [Xcode에서 디바이스의 앱을 실행하는 방법에 대한 Apple 개발자 지시사항](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/LaunchingYourApponDevices/LaunchingYourApponDevices.html)의 내용을 참조하십시오. 

  **참고:** 빌드 시 *사용자 디바이스에서 개발자 앱 인증서를 신뢰할 수 있는지 여부를 아직 확인하지 않았으므로 IoT4I를 시작할 수 없음*이라는 오류가 표시되는 경우 다음과 같이 자신을 신뢰할 수 있는 개발자로 선택하십시오.   
    1. 휴대폰에서 **설정 > 일반 > 디바이스 관리 > 개발자 ID**로 이동하십시오. 
    2. 개발자 ID 계정 이름을 탭하여 개발자 ID의 신뢰를 설정하십시오. 
    3. 프롬프트가 표시되면 개발자 ID를 신뢰할 수 있음을 확인하십시오. 

## 모바일 앱의 푸시 알림 사용
{: #iot4i_pushNotification}

모바일 디바이스의 푸시 알림을 사용하려면 다음 태스크를 수행하십시오. 푸시 알림 서비스를 사용하려면 올바른 Apple 개발자 계정 멤버십이 있어야 합니다. 

1. 다음에서 Apple 개발자 계정으로 로그인하십시오. https://developer.apple.com/account

2. 인증 파일을 작성하십시오. 
  1. **인증서, ID & 프로파일**을 선택하십시오. 
  2. ID(앱 ID)를 선택하십시오. 
  3. 추가 단추(+)를 클릭하여 새 앱 ID를 작성하십시오. 
  4. **설명**에 앱에 대한 설명을 입력하십시오. 
  5. **명시적 앱 ID**를 선택하고 번들 ID(예: com.YourOrganizationName.iot4i.mobileApp)를 입력하십시오. 
  6. **푸시 알림**에서 (V)를 선택한 후 **계속 > 등록 > 완료**를 클릭하십시오. 

3. 푸시 알림 인증서를 작성하십시오. 
  1. **인증서: 모두**를 선택하십시오. 
  2. 추가 단추(+)를 클릭하여 새 APN 인증서를 작성하십시오. 
  3. iOS 인증서 추가 페이지에서 **Apple 푸시 알림 서비스 SSL(샌드박스)**을 선택하고 **계속**을 클릭하십시오. 
  4. 이전 단계에서 작성한 앱 ID를 선택하고 **계속**을 클릭하십시오. 
  5. 페이지에 있는 지시사항을 수행하여 CSR 파일을 작성하고 **계속**을 클릭하십시오. 
  6. 작성한 CSR 파일을 선택하고 **계속**을 클릭하십시오. 
  7. 인증 파일을 다운로드하여 실행하십시오. 

4. 프로파일을 작성하십시오. 
  1. **프로파일 프로비저닝: 개발**을 선택하십시오. 
  2. 추가 단추(+)를 클릭하여 새 개발 프로파일을 작성하십시오. 
  3. **iOS 앱 개발**을 선택하고 **계속**을 클릭하십시오. 
  4. 앞서 작성한 앱 ID를 선택하십시오. 
  5. **개발자 인증서: 모두**를 선택하고 **계속**을 클릭하십시오. 
  5. **모든 개발 디바이스(테스트 디바이스)**를 선택하고 **계속**을 클릭하십시오. 
  6. 프로파일 이름을 지정하고 **계속**을 클릭하십시오. 
  7. 생성된 프로파일을 다운로드하여 실행하십시오. 

5. 공개 키 암호 표준(PKCS) 12 파일을 작성하여 {{site.data.keyword.mobilepushshort}} 서비스에 추가하십시오. 
  1. 키 체인 액세스를 열고 **내 인증서**를 선택하십시오. 
  2. **Apple 개발 IOS 푸시 서비스: (번들 ID)**를 마우스 오른쪽 단추로 클릭한 후 파일의 비밀번호 내보내기, 저장, 입력을 수행하십시오. 
  3. {{site.data.keyword.Bluemix_notm}} 콘솔에서 {{site.data.keyword.mobilepushshort}} 서비스를 여십시오. 
  4. **푸시 설정**을 클릭하십시오. 
  5. Apple 푸시 알림 인증서 섹션에 PKCS 12 파일을 업로드한 후 비밀번호를 입력하십시오. 
  6. Xcode에서 번들 ID를 앞서 작성한 ID로 변경하십시오. 
  7. 앱을 실행하고 푸시 알림 서비스를 사용할 수 있는 권한을 부여하십시오. 

# 관련 링크
{: #rellinks}

## API 참조
{: #api}
* [{{site.data.keyword.iotinsurance_short}} API 예](https://iot4i-docs-api.mybluemix.net/dist/){:new_window}

## 관련 링크
{: #general}
* [{{site.data.keyword.iot_full}} 문서](https://console.ng.bluemix.net/docs/services/IoT/index.html)
* [개발자 지원 포럼](https://developer.ibm.com/answers/search.html?f=&type=question&redirect=search%2Fsearch&sort=relevance&q=%2B[iot]%20%2B[bluemix])
* [스택 오버플로우 지원 포럼](http://stackoverflow.com/questions/tagged/ibm-bluemix)
