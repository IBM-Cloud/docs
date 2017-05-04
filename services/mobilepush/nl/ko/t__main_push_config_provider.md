
---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 알림 제공자의 신임 정보 구성
{: #create-push-credentials}
마지막 업데이트 날짜: 2017년 4월 12일
{: .last-updated}

{{site.data.keyword.mobilepushshort}} 서비스를 설정하려면 모바일 디바이스에 대해 푸시 알림 제공자 - FCM(Firebase Cloud Messaging) 또는 APNs(Apple Push Notification service)의 필수 신임 정보를 가져오십시오.  

**IBM Bluemix Services** 대시보드를 사용하거나 [REST API ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://mobile.{DomainName}/imfpush/){: new_window}을 사용하여 {{site.data.keyword.mobilepushshort}}를 설정할 수 있습니다. 


## FCM의 신임 정보 구성
{: #create-push-enable-gcm}

FCM(Firebase Cloud Messaging)은 Android 디바이스 및 Google Chrome에 푸시 알림을 전달하는 데 사용되는 게이트웨이입니다. FCM은 GCM(Google Cloud Messaging)의 새 버전입니다. 대시보드에서 {{site.data.keyword.mobilepushshort}} 서비스를 설정하려면 FCM 신임 정보를 가져와야 합니다. 새 앱에 FCM 구성을 사용하십시오. 기존 앱은 계속해서 GCM 구성으로 작동합니다. 

### 발신인 ID 및 API 키 가져오기
{: #android-senderid-apikey}

API 키는 안전하게 저장되어 {{site.data.keyword.mobilepushshort}} 서비스에서 FCM 서버에 연결하는 데 사용되며 발신인 ID(프로젝트 번호)는 클라이언트 측의 Google Chrome 및 Mozilla Firefox용 Android SDK와 JS SDK에서 사용됩니다.  

FCM을 설정하려면 API 키와 발신인 ID를 생성하고 다음 단계를 완료하십시오. 

1. [Firebase 콘솔 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.firebase.google.com/?pli=1){: new_window}을 방문하십시오. 
2. **새 프로젝트 작성**을 선택하십시오.  
3. 프로젝트 작성 창에서 프로젝트 이름을 입력하고 국가/지역을 선택한 후 **프로젝트 작성**을 클릭하십시오. 
3. 탐색 분할창에서 설정 아이콘을 클릭한 후 **프로젝트 설정**을 선택하십시오. 
4. 클라우드 메시징 탭을 선택하여 서버 API 키와 발신인 ID를 생성하십시오. 

### Android 및 Chrome 앱 및 확장 프로그램의 Push Notification 서비스 설정
{: #setup-push-android}

**참고:** FCM/GCM API 키와 발신인 ID(프로젝트 번호)가 필요합니다. 

1. Bluemix 대시보드를 연 후 작성한 {{site.data.keyword.mobilepushfull}} 서비스 인스턴스를 클릭하여 대시보드를 여십시오. 푸시 대시보드가 표시됩니다. 바인딩되지 않은 Android용 {{site.data.keyword.mobilepushshort}} 서비스를 설정하려면 바인딩되지 않은 {{site.data.keyword.mobilepushshort}} 서비스 아이콘을 선택하여 {{site.data.keyword.mobilepushshort}} 서비스 대시보드를 여십시오. 

![푸시 대시보드](images/push_unbound.jpg)

2. **푸시 설정** 단추를 클릭하여 Android 애플리케이션과 Google Chrome 앱 및 확장 프로그램의 FCM/GCM 신임 정보를 구성하십시오. 
3. **구성** 페이지에서, Android의 경우 **모바일** 탭으로 이동하여 발신인 ID(GCM 프로젝트 번호)와 API 키를 구성하십시오. Google Chrome 앱 및 확장 프로그램의 경우 **웹** 탭으로 이동하여 발신인 ID(FCM/GCM 프로젝트 번호)와 API 키를 적절히 구성하십시오. 
4. **저장**을 클릭하십시오.
5. 다음 단계. [Android의 알림 사용](c_enable_push.html) 또는 [Google Chrome 앱 및 확장 프로그램의 알림 사용](c_web_extensions.html). 


## APNs의 신임 정보 구성
{: #create-push-credentials-apns}

애플리케이션 개발자는 APNs(Apple Push Notification Service)를 이용하여 Bluemix의 {{site.data.keyword.mobilepushshort}} 서비스 인스턴스(제공자)에서 iOS 디바이스와 애플리케이션으로 원격 알림을 전송할 수 있습니다. 디바이스의 대상 애플리케이션으로 메시지가 전송됩니다.  

APNs 신임 정보를 획득하여 구성합니다. {{site.data.keyword.mobilepushshort}} 서비스에서 APNs 인증서를 안전하게 관리하며 제공자로 APNs 서버에 연결하는 데 이 인증서를 사용합니다. 

<!-- 1. Obtain an [Apple Developers ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://developer.apple.com/){: new_window} account.-->

<!--2. [Register an App ID](#create-push-credentials-apns-register)
3. [Create a development and distribution APNs SSL certificate](#create-push-credentials-apns-ssl)
4. [Create a development provisioning profile](#create-push-credentials-dev-profile)
5. [Create a store distribution provisioning profile](#create-push-credentials-apns-distribute_profile)
6. [Creating .p12 push certificate file for Bluemix push](#create-p12-push-certificate-file-for-Bluemix-push)
7. [Set up APNs on the Push Dashboard](#create-push-credentials-apns-dashboard)
-->


### App ID 등록
{: #create-push-credentials-apns-register}


App ID(번들 ID)는 특정 애플리케이션을 식별하는 고유 ID입니다. 각 애플리케이션에 App ID가 필요합니다. {{site.data.keyword.mobilepushshort}} 서비스와 같은 서비스는 App ID에 따라 구성됩니다. 

1. [Apple Developer ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.apple.com/){: new_window} 계정이 있는지 확인하십시오. 
2. [Apple Developer ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.apple.com){: new_window} 포털로 이동하여 **멤버 센터**를 클릭하고 **인증서, ID 및 프로파일**을 선택하십시오. 
3. [Apple Developer Library ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html#//apple_ref/doc/uid/TP40012582-CH30-SW991){: new_window}의 **Registering App IDs** 섹션으로 이동하고 지시사항에 따라 App ID를 등록하십시오. 

App ID를 등록할 때 다음 옵션을 선택하십시오. 

* Push Notifications
![앱 서비스](images/appID_appservices_enablepush.jpg)
* 명시적 ID 접미부
![명시적 ID](images/appID_bundleID.jpg)
4. 개발 및 배포 APNs SSL 인증서를 작성하십시오. 

### 개발 및 배포 APNs SSL 인증서 작성
{: #create-push-credentials-apns-ssl}

APNs 인증서를 획득하려면 먼저 인증서 서명 요청(CSR)을 작성하여 이를 Apple 인증 기관(CA)에 제출해야 합니다. CSR에는 사용자의 회사, Apple 푸시 알림을 신청할 때 사용하는 공용 키와 개인 키를 식별하는 정보가 포함됩니다. 그런 다음 iOS 개발자 포털에서 SSL 인증서를 생성하십시오. 인증서와 이의 공개 및 개인 키는 Keychain Access에 저장됩니다. 

<!-- ###Before you begin -->
<!-- {: before-you-begin-certificate} -->

<!--[Register an App ID](#create-push-credentials-apns-register)-->

다음 두 모드에서 APNs를 사용할 수 있습니다.  

* 개발 및 테스트를 위한 샌드박스 모드에서
* 앱 저장소(또는 다른 엔터프라이즈 배포 메커니즘)를 통해 애플리케이션을 배포할 때 프로덕션 모드에서

개발 및 배포 환경을 위한 별도의 인증서를 획득해야 합니다. 인증서는 원격 알림의 수신인인 앱의 App ID와 연관되어 있습니다. 프로덕션의 경우 최대 2개의 인증서를 작성할 수 있습니다. Bluemix는 인증서를 사용하여 APNs와의 SSL 연결을 설정합니다. 

<!-- Create a development and distribution SSL certificate. -->

1. [Apple Developer ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.apple.com){: new_window} 웹 사이트로 이동하여 **멤버 센터**를 클릭하고 **인증서, ID 및 프로파일**을 선택하십시오. 
2. **ID** 영역에서 **App ID**를 클릭하십시오. 
3. App ID 목록에서 <!--newly created--> App ID를 선택한 다음 **설정**을 선택하십시오. 
4. **Push Notifications** 영역에서 개발 SSL 인증서를 작성한 다음 프로덕션 SSL 인증서를 작성하십시오.

	![Push Notification SSL 인증서](images/certificate_createssl.jpg)

5. **인증서 서명 요청(CSR) 작성 정보 화면**이 표시되면 Mac에서 **Keychain Access** 애플리케이션을 시작하여 인증서 서명 요청(CSR)을 작성하십시오.
6. 메뉴에서 **Keychain Access > 인증서 지원 > 인증 기관에 인증서 요청…**을 선택하십시오. 
7. **인증서 정보**에서 앱 개발자 계정과 연관된 이메일 주소와 공통 이름을 입력하십시오. 개발(샌드박스)용 인증서인지 배포(프로덕션)용 인증서인지 식별할 수 있도록 의미있는 이름을 지정하십시오(예: *sandbox-apns-certificate* 또는 *production-apns-certificate*).
8. **디스크에 저장**을 선택하여 `.certSigningRequest` 파일을 데스크탑에 다운로드한 다음 **계속**을 클릭하십시오. 
9. **다른 이름으로 저장** 메뉴 옵션에서 `.certSigningRequest` 파일의 이름을 지정한 후 **저장**을 클릭하십시오.
10. **완료**를 클릭하십시오. 이제 CSR이 작성되었습니다. 
11. **인증서 서명 요청(CSR) 작성 정보** 창으로 돌아가서 **계속**을 클릭하십시오.  
12. **생성** 화면에서 **파일 선택... **을 클릭하고 데스크탑에 저장한 CSR 파일을 선택하십시오. 그런 다음 **생성**을 클릭하십시오.
![인증서 생성](images/generate_certificate.jpg)
13. 인증서가 준비되면 **완료**를 클릭하십시오. 
14. **Push Notifications** 화면에서 **다운로드**를 클릭하여 인증서를 다운로드하고 **완료**를 클릭하십시오.
 ![인증서 다운로드](images/certificate_download.jpg)
15. Mac의 경우 **Keychain Access > 내 인증서**로 이동하여 새로 설치된 인증서를 찾아보십시오. 인증서를 두 번 클릭하여 Keychain Access에 인증서를 설치하십시오. 
16. 인증서와 개인 키를 선택한 다음 **내보내기**를 선택하여 인증서를 개인 정보 변환 형식(`.p12` 형식)으로 변환하십시오.
 ![인증서 및 키 내보내기](images/keychain_export_key.jpg)
17. **다른 이름으로 저장** 필드에서 인증서에 의미있는 이름을 지정하십시오. 예를 들어, `sandbox_apns.p12_certifcate` 또는 `production_apns.p12`를 지정한 후 **저장**을 클릭하십시오.
	![인증서 및 키 내보내기](images/certificate_p12v2.jpg)
18. **비밀번호 입력** 필드에 내보낸 항목을 보호하기 위한 비밀번호를 입력한 다음 **확인**을 클릭하십시오. 이 비밀번호를 사용하여 푸시 대시보드에서 APNs 설정을 구성할 수 있습니다.{: #step18}
	![인증서 및 키 내보내기](images/export_p12.jpg)
19. **Key Access.app**이 **키 체인** 화면에서 키를 내보내도록 프롬프트를 표시합니다. 시스템이 해당 항목을 내보낼 수 있도록 Mac의 관리 비밀번호를 입력한 다음 **항상 허용** 옵션을 선택하십시오. 데스크탑에 `.p12` 인증서가 생성됩니다. 


### 개발 프로비저닝 프로파일 작성
{: #create-push-credentials-dev-profile}

프로비저닝 프로파일은 App ID와 함께 작동하여 사용자 앱을 설치하고 실행할 수 있는 디바이스 및 사용자 앱에서 액세스할 수 있는 서비스를 판별합니다. 각 App ID에 대해 개발 및 배포용으로 두 개의 프로비저닝 프로파일을 작성하십시오. Xcode는 개발 프로비저닝 프로파일을 사용하여 애플리케이션을 빌드할 수 있는 개발자와 애플리케이션을 테스트할 수 있는 디바이스를 판별합니다.

App ID를 등록하고 이를 {{site.data.keyword.mobilepushshort}} 서비스에 사용할 수 있도록 설정하였으며 개발 및 프로덕션 APNs SSL 인증서를 사용하도록 구성했는지 확인하십시오.

개발 프로비저닝 프로파일을 다음과 같이 작성하십시오.

1. [Apple Developer ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.apple.com){: new_window} 포털로 이동하여 **멤버 센터**를 클릭하고 **인증서, ID 및 프로파일**을 선택하십시오. 
2. [Mac Developer Library ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html#//apple_ref/doc/uid/TP40012582-CH30-SW62site){: new_window}으로 이동하고, **Creating Development Provisioning Profiles** 섹션으로 화면 이동하여 지시사항에 따라 개발 프로파일을 작성하십시오.
**참고**:개발 프로비저닝 프로파일을 구성할 때 다음 옵션을 선택하십시오. 
	* **iOS 앱 개발**
	* **iOS 및 watchOS 앱용**


### 저장소 배포 프로비저닝 프로파일 작성
{: #create-push-credentials-apns-distribute_profile}

저장소 프로비저닝 프로파일을 사용하여 배포용 앱을 앱 저장소에 제출하십시오. 

1. [Apple Developer ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.apple.com){: new_window} 포털로 이동하여 **멤버 센터**를 클릭하고 **인증서, ID 및 프로파일**을 선택하십시오. 
2. 다운로드한 프로비저닝 프로파일을 두 번 클릭하여 이를 Xcode에 설치하십시오. 

### Push Notification 대시보드에서 APNs 설정
{: #create-push-credentials-apns-dashboard}

{{site.data.keyword.mobilepushshort}} 서비스를 사용하여 알림을 전송하려면 APNs(Apple Push Notification Service)에 필요한 SSL 인증서를 업로드하십시오. REST API를 사용하여 APNs 인증서를 업로드할 수도 있습니다. 

<!-- Get your development and production APNs SSL certificate and the password associated with each type of certificate. For information, see Creating and configuring push credentials for APNs.-->

APNs에 필요한 인증서는 `.p12` 인증서입니다. 이러한 인증서에는 애플리케이션 빌드와 공개에 필요한 개인 키와 SSL 인증서가 있습니다. Apple Developer 웹 사이트의 Member Center에서 인증서를 생성해야 합니다(유효한 Apple Developer 계정 필요). 개발 환경(샌드박스)과 프로덕션(배포) 환경에 대해 별도의 인증서가 필요합니다.

**참고**: `.cer` 파일이 키 체인 액세스에 있으면 이를 컴퓨터로 내보내서 `.p12` 인증서를 작성하십시오.

APNs 사용에 대한 자세한 정보는 [iOS Developer Library: Local and Push Notification Programming Guide ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ProvisioningDevelopment.html#//apple_ref/doc/uid/TP40008194-CH104-SW4){: new_window}을 참조하십시오. 

Push Notification 서비스 대시보드에서 APNs를 설정하려면 다음을 수행하십시오. 

1. Push Notification 서비스 대시보드에서 **구성**을 선택하십시오.
2. **모바일** 옵션을 선택하여 **APNs 알림 신임 정보** 양식의 정보를 업데이트하십시오. 
3. **샌드박스**(개발) 또는 **프로덕션**(배포)을 선택한 후 이전 [단계](#step18)에서 작성한 `p.12` 인증서를 업로드하십시오.
  ![푸시 알림 설정 대시보드](images/wizard.jpg)
3. **비밀번호** 필드에서 `.p12` 인증서 파일과 연관된 비밀번호를 입력하고 **저장**을 클릭하십시오.

올바른 비밀번호를 사용하여 인증서를 업로드한 후 알림 전송을 시작할 수 있습니다. 

## 웹 브라우저의 신임 정보 구성
{: #configure-credential-for-browsers}

IBM {{site.data.keyword.mobilepushshort}} 서비스는 이제 기능을 확장하여 사용자의 브라우저에 알림을 전송합니다. 

{{site.data.keyword.mobilepushshort}} 서비스에서 허용해야 할 요청을 식별하려면 웹 사이트 URL 또는 웹 사이트의 도메인 이름이 필요합니다. {{site.data.keyword.mobilepushshort}} 서비스 인스턴스는 한 번에 하나의 도메인 이름만 지원합니다. 그러므로 Chrome, Firefox 및 Safari에 동일한 값이 설정되는지 확인하십시오. 

Chrome 및 Safari 브라우저에서는 웹 푸시를 위해 추가 구성이 필요합니다. FCM 엔드포인트를 사용하여 Chrome에서 메시지를 제공하므로 FCM API 키가 필요합니다.  


### Chrome 및 Firefox 웹 푸시 구성 
{: #config-chrome-firefox}

1. 푸시 대시보드 패널에서 **구성**을 선택하십시오.
2. 웹 탭을 선택하십시오.
	![WebPush 구성](images/webpush_configure.jpg)
3. 푸시 알림을 수신하도록 등록할 웹 사이트의 URL과 FCM/GCM API 키를 구성하십시오. 
4. **저장**을 클릭하십시오.
5. 다음 단계. [Google Chrome 및 Mozilla Firefox 브라우저에 알림 사용](c_chrome_firefox_enable.html).


### Safari 웹 푸시 구성 
{: #configure-safari}

Safari에서 {{site.data.keyword.mobilepushshort}} 서비스에 지원되는 버전은 10.0입니다. Apple Developer 계정을 통해 인증서를 생성해야 알림을 받도록 브라우저를 구성할 수 있습니다.

#### 인증서 생성
{: #certificate-generation}

Apple 개발자 계정이 있는지 확인하십시오. 알림을 수신하도록 Safari 브라우저를 구성하려면 웹 사이트 푸시 ID를 등록하고 인증서를 생성해야 합니다. 다음 단계를 수행하면 시작에 도움이 됩니다. 

1. Apple 개발자 구성원 센터에서 **인증서, ID 및 프로파일**을 클릭하십시오.  
2. **ID**를 클릭한 후 **웹 사이트 푸시 ID**를 클릭하십시오. 
3. 더하기 아이콘을 선택하여 새 항목을 작성하도록 선택하십시오.
  ![푸시 대시보드](images/safari_1.jpg)

4. 웹 사이트 푸시 ID 등록 패널에서 적절한 웹 사이트 푸시 ID 설명 및 식별자 ID를 제공하십시오. `web`으로 시작하는 역 도메인 이름 형식을 사용하도록 권장합니다. 예: `web.com.example.dailyweatherreports`.
5. 웹 사이트 푸시 ID를 등록하십시오. 사용자의 웹 사이트 푸시 ID가 생성됩니다.  
6. **편집**을 선택하여 웹 사이트 푸시 ID에 사용할 인증서를 생성하십시오. 
7. 인증서 정보의 인증서 지원 창에서 이메일 ID와 공통 이름을 제공하십시오. 인증 기관 이메일 주소는 공백으로 두십시오. 
8. **디스크에 저장**을 클릭하고 **계속**을 선택하십시오. 
9. 인증서를 적절한 폴더에 저장하도록 선택하십시오. 
10. 마법사에서 인증서를 생성하도록 프롬프트하면 디스크에 작성된 `.certSigningRequest`를 선택하십시오. `.cer` 형식으로 작성된 웹 사이트 푸시 인증서를 다운로드해야 합니다. 
11. KeyChain Access 도구에서 인증서를 여십시오. 마우스 오른쪽 단추를 클릭하고 p12 인증서로 내보내십시오. p12 인증서 생성 중에 입력한 비밀번호를 기록하십시오. 


#### 알림 구성
{: #configuration-notification}
 
인증서를 생성한 후에 서비스를 구성하여 알림을 Safari로 보낼 수 있습니다.  

다음 단계를 완료하십시오. 

1. Push Notifications 서비스 대시보드에서 **구성을 클릭**하십시오. 
2. 웹 탭을 선택하십시오. 
3. Safari 푸시 섹션에서 필수 정보로 양식을 업데이트하십시오.  
	- **웹 사이트 이름**: 알림 센터에서 입력한 이름입니다. 
	- **웹 사이트 푸시 ID**: 웹 사이트 푸시 ID에 대한 역 도메인 문자열로 업데이트하십시오. 예: web.com.example.www.
	- **웹 사이트 URL**: 푸시 알림에 등록될 웹 사이트의 URL을 입력하십시오. 예: https://www.example.com.
	- **허용 도메인**: 선택적 매개변수입니다. 사용자에게 권한을 요청하는 웹 사이트 목록입니다. URL은 쉼표로 구분된 값이어야 합니다. 이 값을 입력하지 않으면 웹 사이트 URL 값을 사용합니다.  
	- **URL 형식 문자열**: 알림을 클릭할 때 분석할 URL입니다. 예: ["https://www.example.com"]. 이 URL은 http 또는 https 체계를 사용해야 합니다. 
	- **Safari 웹 푸시 인증서**: .p12 인증서를 업로드하고 비밀번호를 입력하십시오. 
4. **저장**을 클릭하십시오.	

![푸시 대시보드](images/push_configure_safari.jpg)	

이제 Safari 브라우저로 푸시 알림을 전송하는 구성이 완료되었습니다. 
