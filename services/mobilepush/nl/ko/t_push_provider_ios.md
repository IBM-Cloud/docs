---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# APNs의 신임 정보 구성
{: #create-push-credentials-apns}
마지막 업데이트 날짜: 2017년 1월 16일
{: .last-updated}

애플리케이션 개발자는 APNs(Apple Push Notification Service)를 이용하여 Bluemix의 {{site.data.keyword.mobilepushshort}} 서비스 인스턴스(제공자)에서 iOS 디바이스와 애플리케이션으로 원격 알림을 전송할 수 있습니다. 디바이스의 대상 애플리케이션으로 메시지가 전송됩니다.  

APNs 신임 정보를 획득하여 구성합니다. {{site.data.keyword.mobilepushshort}} 서비스에서 APNs 인증서를 안전하게 관리하며 제공자로 APNs 서버에 연결하는 데 이 인증서를 사용합니다. 

<!-- 1. Obtain an [Apple Developers ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://developer.apple.com/ "External link icon"){: new_window} account.-->

<!--2. [Register an App ID](#create-push-credentials-apns-register)
3. [Create a development and distribution APNs SSL certificate](#create-push-credentials-apns-ssl)
4. [Create a development provisioning profile](#create-push-credentials-dev-profile)
5. [Create a store distribution provisioning profile](#create-push-credentials-apns-distribute_profile)
6. [Creating .p12 push certificate file for Bluemix push](#create-p12-push-certificate-file-for-Bluemix-push)
7. [Set up APNs on the Push Dashboard](#create-push-credentials-apns-dashboard)
-->


##앱 ID 등록
{: #create-push-credentials-apns-register}


앱 ID(번들 ID)는 특정 애플리케이션을 식별하는 고유 ID입니다. 각 애플리케이션에 앱 ID가 필요합니다. {{site.data.keyword.mobilepushshort}} 서비스와 같은 서비스는 앱 ID에 따라 구성됩니다. 

1. [Apple 개발자 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.apple.com/ "외부 링크 아이콘"){: new_window} 계정이 있는지 확인하십시오.
2. [Apple 개발자 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.apple.com "외부 링크 아이콘"){: new_window} 포털로 이동하여 **멤버 센터**를 클릭한 다음 **인증서, ID 및 프로파일**을 선택하십시오.
3. [Apple 개발자 라이브러리 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html#//apple_ref/doc/uid/TP40012582-CH30-SW991 "외부 링크 아이콘"){: new_window}의 **앱 ID 등록** 섹션으로 이동하여 지시사항에 따라 앱 ID를 등록하십시오.

앱 ID를 등록할 때 다음 옵션을 선택하십시오. 

* 푸시 알림
![앱 서비스](images/appID_appservices_enablepush.jpg)
* 명시적 ID 접미부
![명시적 ID](images/appID_bundleID.jpg)
4. 개발 및 배포 APNs SSL 인증서를 작성하십시오. 

##개발 및 배포 APNs SSL 인증서 작성
{: #create-push-credentials-apns-ssl}

APNs 인증서를 획득하려면 먼저 인증서 서명 요청(CSR)을 작성하여 이를 Apple 인증 기관(CA)에 제출해야 합니다. CSR에는 사용자의 회사, Apple 푸시 알림을 신청할 때 사용하는 공용 키와 개인 키를 식별하는 정보가 포함됩니다. 그런 다음 iOS 개발자 포털에서 SSL 인증서를 생성하십시오. 인증서와 이의 공개 및 개인 키는 Keychain Access에 저장됩니다. 

<!-- ###Before you begin -->
<!-- {: before-you-begin-certificate} -->

<!--[Register an App ID](#create-push-credentials-apns-register)-->

다음 두 모드에서 APNs를 사용할 수 있습니다.  

* 개발 및 테스트를 위한 샌드박스 모드에서
* 앱 저장소(또는 다른 엔터프라이즈 배포 메커니즘)를 통해 애플리케이션을 배포할 때 프로덕션 모드에서

개발 및 배포 환경을 위한 별도의 인증서를 획득해야 합니다. 인증서는 원격 알림의 수신인인 앱의 앱 ID와 연관되어 있습니다. 프로덕션의 경우 최대 2개의 인증서를 작성할 수 있습니다. Bluemix는 인증서를 사용하여 APNs와의 SSL 연결을 설정합니다. 

<!-- Create a development and distribution SSL certificate. -->

1. [Apple 개발자 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.apple.com "외부 링크 아이콘"){: new_window} 웹 사이트로 이동하여 **멤버 센터**를 클릭한 다음 **인증서, ID 및 프로파일**을 선택하십시오.
2. **ID** 영역에서 **앱 ID**를 클릭하십시오. 
3. 앱 ID 목록에서 <!--newly created--> 앱 ID를 선택한 다음 **설정**을 선택하십시오. 
4. **푸시 알림** 영역에서 개발 SSL 인증서를 작성한 다음 프로덕션 SSL 인증서를 작성하십시오.

	![푸시 알림 SSL 인증서](images/certificate_createssl.jpg)

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
14. **푸시 알림** 화면에서 **다운로드**를 클릭하여 인증서를 다운로드하고 **완료**를 클릭하십시오.
 ![인증서 다운로드](images/certificate_download.jpg)
15. Mac의 경우 **Keychain Access > 내 인증서**로 이동하여 새로 설치된 인증서를 찾아보십시오. 인증서를 두 번 클릭하여 Keychain Access에 인증서를 설치하십시오. 
16. 인증서와 개인 키를 선택한 다음 **내보내기**를 선택하여 인증서를 개인 정보 변환 형식(`.p12` 형식)으로 변환하십시오.
 ![인증서 및 키 내보내기](images/keychain_export_key.jpg)
17. **다른 이름으로 저장** 필드에서 인증서에 의미있는 이름을 지정하십시오. 예를 들어, `sandbox_apns.p12_certifcate` 또는 `production_apns.p12`를 지정한 후 **저장**을 클릭하십시오.
	![인증서 및 키 내보내기](images/certificate_p12v2.jpg)
18. **비밀번호 입력** 필드에 내보낸 항목을 보호하기 위한 비밀번호를 입력한 다음 **확인**을 클릭하십시오. 이 비밀번호를 사용하여 푸시 대시보드에서 APNs 설정을 구성할 수 있습니다.{: #step18}
	![인증서 및 키 내보내기](images/export_p12.jpg)
19. **Key Access.app**이 **키 체인** 화면에서 키를 내보내도록 프롬프트를 표시합니다. 시스템이 해당 항목을 내보낼 수 있도록 Mac의 관리 비밀번호를 입력한 다음 **항상 허용** 옵션을 선택하십시오. 데스크탑에 `.p12` 인증서가 생성됩니다. 


##개발 프로비저닝 프로파일 작성
{: #create-push-credentials-dev-profile}

프로비저닝 프로파일은 APP ID와 함께 작동하여 사용자 앱을 설치하고 실행할 수 있는 디바이스 및 사용자 앱에서 액세스할 수 있는 서비스를 판별합니다. 각 앱 ID에 대해 개발 및 배포용으로 두 개의 프로비저닝 프로파일을 작성하십시오. Xcode는 개발 프로비저닝 프로파일을 사용하여 애플리케이션을 빌드할 수 있는 개발자와 애플리케이션을 테스트할 수 있는 디바이스를 판별합니다.

앱 ID를 등록하고 이를 {{site.data.keyword.mobilepushshort}} 서비스에 사용할 수 있도록 설정하였으며 개발 및 프로덕션 APNs SSL 인증서를 사용하도록 구성했는지 확인하십시오.

개발 프로비저닝 프로파일을 다음과 같이 작성하십시오.

1. [Apple 개발자 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.apple.com "외부 링크 아이콘"){: new_window} 포털로 이동하여 **멤버 센터**를 클릭한 다음 **인증서, ID 및 프로파일**을 선택하십시오.
2. [Mac 개발자 라이브러리 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html#//apple_ref/doc/uid/TP40012582-CH30-SW62site "외부 링크 아이콘"){: new_window}으로 이동하여 **개발 프로비저닝 프로파일 작성** 섹션으로 화면이동한 다음 지시사항에 따라 개발 프로파일을 작성하십시오.
**참고**:개발 프로비저닝 프로파일을 구성할 때 다음 옵션을 선택하십시오. 
	* **iOS 앱 개발**
	* **iOS 및 watchOS 앱용**



##저장소 배포 프로비저닝 프로파일 작성
{: #create-push-credentials-apns-distribute_profile}

저장소 프로비저닝 프로파일을 사용하여 배포용 앱을 앱 저장소에 제출하십시오. 

1. [Apple 개발자 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.apple.com "외부 링크 아이콘"){: new_window} 포털로 이동하여 **멤버 센터**를 클릭한 다음 **인증서, ID 및 프로파일**을 선택하십시오.
2. 다운로드한 프로비저닝 프로파일을 두 번 클릭하여 이를 Xcode에 설치하십시오. 

##{{site.data.keyword.mobilepushshort}} 대시보드에서 APNs 설정
{: #create-push-credentials-apns-dashboard}

{{site.data.keyword.mobilepushshort}} 서비스를 사용하여 알림을 전송하려면 APNs(Apple Push Notification Service)에 필요한 SSL 인증서를 업로드하십시오. REST API를 사용하여 APNs 인증서를 업로드할 수도 있습니다. 

<!-- Get your development and production APNs SSL certificate and the password associated with each type of certificate. For information, see Creating and configuring push credentials for APNs.-->

APNs에 필요한 인증서는 `.p12` 인증서입니다. 이러한 인증서에는 애플리케이션 빌드와 공개에 필요한 개인 키와 SSL 인증서가 있습니다. Apple Developer 웹 사이트의 Member Center에서 인증서를 생성해야 합니다(유효한 Apple Developer 계정 필요). 개발 환경(샌드박스)과 프로덕션(배포) 환경에 대해 별도의 인증서가 필요합니다.

**참고**: `.cer` 파일이 키 체인 액세스에 있으면 이를 컴퓨터로 내보내서 `.p12` 인증서를 작성하십시오.

APNs 사용에 대한 자세한 정보는 [iOS 개발자 라이브러리: 로컬 및 푸시 알림 프로그래밍 안내서 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ProvisioningDevelopment.html#//apple_ref/doc/uid/TP40008194-CH104-SW4 "외부 링크 아이콘"){: new_window}을 참조하십시오.

푸시 알림 서비스 대시보드에서 APNs를 설정하려면 다음을 수행하십시오. 

1. 푸시 알림 서비스 대시보드에서 **구성**을 선택하십시오.
2. **모바일** 옵션을 선택하여 **APNs 알림 신임 정보** 양식의 정보를 업데이트하십시오. 
3. **샌드박스**(개발) 또는 **프로덕션**(배포)을 선택한 후 이전 [단계](#step18)에서 작성한 `p.12` 인증서를 업로드하십시오.
  ![푸시 알림 설정 대시보드](images/wizard.jpg)
3. **비밀번호** 필드에서 `.p12` 인증서 파일과 연관된 비밀번호를 입력하고 **저장**을 클릭하십시오.

올바른 비밀번호를 사용하여 인증서를 업로드한 후 알림 전송을 시작할 수 있습니다. 
