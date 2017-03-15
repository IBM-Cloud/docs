---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# iOS 앱을 사용하여 MQA 인스트루먼트(더 이상 사용되지 않음)
{: #instrumentios}

{{site.data.keyword.mqafull}}를 iOS 앱과 함께 사용하려면, SDK를 다운로드하고 Xcode 개발 환경에서 몇 가지 변경사항을 작성하여 이를 인스트루먼트해야 합니다.
{: shortdesc}

{{site.data.keyword.mqa}}를 사용하여 앱을 인스트루먼트할 수 있으려면 {{site.data.keyword.Bluemix}} 계정이 있어야 하며 인스트루먼트하는 앱의 플랫폼에 대한 배치 환경의 버전이 올바르게 설치되어 있어야 합니다. 

Objective-C 또는 Swift 앱과 작동하도록 {{site.data.keyword.mqa}}를 인스트루먼트하려면, 다음 태스크를 완료하십시오. 

1. 필수 권한 및 다운로드한 SDK를 iOS 프로젝트에 추가하십시오. 

	1. Xcode에서 프로젝트를 작성하거나 여십시오. 

	2. Xcode 프로젝트의 *일반* 탭에 있는 *링크된 프레임워크 및 라이브러리* 섹션을 선택하여 다음 종속 항목 라이브러리를 추가하십시오. 

		* AssetsLibrary.framework
		* AudioToolbox.framework
		* AVFoundation.framework
		* CoreData.framework
		* CoreLocation.framework
		* CoreMedia.framework
		* CoreMotion.framework
		* CoreTelephony.framework
		* CoreText.framework
		* CoreVideo.framework
		* MediaPlayer.framework
		* QuartzCore.framework
		* Security.framework
		* SystemConfiguration.framework

	3. iOS `Q4M.framework`용 {{site.data.keyword.mqa}} SDK 폴더를 네비게이터 트리의 **프레임워크** 그룹으로 끌어 놓으십시오. 옵션 선택 창에서 *필요한 경우 항목 복사*, **그룹 작성**을 선택하고 대상으로 프로젝트 이름에 대한 상자를 선택하십시오. 

	4. *빌드 설정* 탭의 연결 섹션에서 디버그 및 릴리스에 대한 *기타 링커 플래그*를 **-ObjC**로 설정하십시오. 중요: 기타 링커 플래그가 목록에 포함되도록 *모두* 탭이 선택되어 있는지 확인하십시오. 

	5. *Objective-C 전용의 경우:* 다음 import 문을 `AppDelegate.m` 및 `ViewController.m` 파일에 추가하십시오. 

		```
		#import <Q4M/MQALogger.h>
		```
		{: codeblock}

	6. *Swift 전용의 경우:* 다음 단계를 완료하여 iOS용 {{site.data.keyword.mqa}} SDK에 대한 Objective-C 브릿지 헤더를 추가하십시오. 

		1. 프로젝트 루트 노드를 마우스 오른쪽 단추로 클릭하고 **새 파일**을 선택하십시오. 

		2. iOS 아래의 템플리트 선택 창에서 소스 섹션에 있는 헤더 파일 템플리트를 클릭하십시오. 

		3. 파일의 이름을 `MyProject-Bridging-Header.h`로 지정하십시오. 여기서 *MyProject*는 Swift 프로젝트의 이름입니다. 대상으로 프로젝트의 이름을 선택하십시오. 예를 들어, 파일의 이름을 `MyProject-Bridging-Header.h`로 지정하십시오. 

		4. **작성**을 클릭하여 프로젝트의 루트에 파일을 저장하십시오. 

		5. 새로운 브릿지 헤더 파일에 브릿지 헤더 파일에 대한 다음 import 문을 추가하십시오. 

			```
			#import <Q4M/MQALogger.h>
			```
			{: codeblock}

		6. Xcode 프로젝트 네비게이터에서 프로젝트를 선택한 상태로 **빌드 설정**을 클릭하고 `Objective-C Bridging Header`를 검색하십시오. 

		7. **Swift 컴파일러 - 일반** 아래에서 **Objective-C 브릿지 헤더**의 값을 브릿지 헤더의 경로로 설정하십시오. 경로는 프로젝트 루트에 대한 상대 경로입니다. 예를 들어, MQASampleApp 프로젝트가 `/user/example/MQASampleApp`에 있는 경우 경로는 `/user/example/MQASampleApp/MQASampleApp-Bridging-Header.h`입니다. 파일을 프로젝트의 루트에 저장한 경우에는 `${SRCROOT}/${PROJECT}-Bridging-Header.h`를 입력하여 경로를 설정하는 데 환경 변수를 사용할 수 있습니다. 

		8. 경로가 올바른지 확인하려면 앱을 저장하고 빌드하십시오. 

	7. `info.plist` 파일에서 프로젝트 정보의 다음 설정을 확인하십시오. 

		* 번들 버전 - {{site.data.keyword.mqa}}는 이 필드의 값을 사용하여 새 빌드 알림을 테스터에게 전송할 시기를 판별합니다. 새 빌드를 {{site.data.keyword.mqa}}에 업로드하는 경우 이 숫자를 늘려야 합니다. 번들 버전 필드의 문자열은 숫자와 마침표(.) 문자로 제한됩니다. 이 제한사항은 Xcode 요구사항이므로 대부분의 애플리케이션은 이 규칙을 따르며 변경이 필요하지 않습니다. 
		* 번들 버전 문자열 - 이 필드는 버전 번호의 문자열 표시를 포함합니다. 문자열에는 번들 버전 필드와 동일한 제한사항은 없습니다. 

2. 로그인할 때마다 시작하도록 새 세션을 구성하십시오. 

    1. `AppDelegate` 파일에서 `didFinishLaunchingWithOptions` 메소드를 찾으십시오. 

        * Objective-C: `AppDelegate.m` 파일
        * Swift: `AppDelegate.swift` 파일

	2. {{site.data.keyword.mqa}} 세션을 시작하십시오. 

		* Objective-C

			1. `applicationDelegate` 메소드 내의 메소드(예: `didFinishLaunchingWithOptions` 메소드)에서 새 세션을 시작하십시오. 프로젝트 네비게이터에 있는 프로젝트와 동일한 이름의 폴더를 열어 위임자를 찾을 수 있습니다. `projectDelegate.m` 파일을 찾으십시오. 

			2. `didFinishLaunchingWithOptions` 메소드 내부의 `return YES;`가 있는 행 앞에 다음 코드를 추가하십시오. 

				```
				// Starts a quality assurance session using a
				    placeholder key and QA mode
				[MQALogger startNewSessionWithApplicationKey:@"Your_Application_Key"];
				```
				{: codeblock}

			3. *Your_Application_Key* 변수를 {{site.data.keyword.mqa}}의 애플리케이션 키로 대체하십시오.
               팁: 앱 설정 아래의 {{site.data.keyword.mqa}} 웹 분할창에서 앱 키를 찾을 수 있습니다. 

		* Swift

			1. `AppDelegate.swift` 파일에서 `didFinishLaunchingWithOptions` 메소드를 찾으십시오. 

			2. 메소드 내부의 `return true`가 있는 행 앞에 다음 코드를 추가하십시오. 여기서 *Your_Application_Key*는 앱에 대한 올바른 키입니다. 

				```
				// Set the application key
				MQALogger.startNewSession(withApplicationKey: "Your_Application_Key")
				```
				{: codeblock}

	3. 사전 준비 모드 또는 프로덕션 모드를 사용할지 정의하십시오. 사전 준비 및 프로덕션 모드 간의 차이점에 대한 정보는 IBM Knowledge Center의 [사전 준비 및 프로덕션 모드 간의 차이점 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/cPreprodvsProd.html){: new_window}을 참조하십시오. 

		* Objective-C

			1. `didFinishLaunchingWithOptions` 메소드를 찾으십시오. 

			2. didFinishLaunchingWithOptions 메소드 내부의 `return YES;`가 있는 행 앞에 다음 코드 행 중 하나를 추가하십시오. 

			사전 준비 모드를 사용하려면, 이 코드 행을 추가하십시오. 

				```
				[[MQALogger settings] setMode:MQAModeQA];
				```
				{: codeblock}

			프로덕션 모드를 사용하려면, 이 코드 행을 추가하십시오. 

				```
				[[MQALogger settings] setMode:MQAModeMarket];
				```
				{: codeblock}

				**Objective-C complete example**
				<pre><code>
					- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
						{
					   // Override point for customization after application launch.
					   if ([[UIDevice currentDevice] userInterfaceIdiom] == UIUserInterfaceIdiomPad) {
					      UISplitViewController *splitViewController = (UISplitViewController*)self.window.rootViewController;
					      UINavigationController *navigationController = [splitViewController.viewControllers lastObject];
					      splitViewController.delegate = (id)navigationController.topViewController;
						}
					     #ifdef Debug
					   [[MQALogger settings] setMode:MQAModeQA];
					   #else
					   [[MQALogger settings] setMode:MQAModeMarket];
					   #endif
					      // Starts a quality assurance session using a placeholder key
					      [MQALogger startNewSessionWithApplicationKey:@"Your-Application-Key"];
					      // Enables the quality assurance application crash reporting
					      NSSetUncaughtExceptionHandler(&MQAUncaughtExceptionHandler);
					      return YES; }
				</code></pre>
				{: codeblock}

        * Swift

			1. AppDelegate.swift 파일에서 `didFinishLaunchingWithOptions` 메소드를 검색하십시오. 

			2. `didFinishLaunchingWithOptions` 메소드의 `return true`가 있는 행 앞에 다음 행을 추가하십시오. 

				```
				//Set the SDK mode Market vs QA for Production
				   and Pre-Production
				#if Debug
				  MQALogger.settings().mode = MQAMode.QA
				#elseif Release
				  MQALogger.settings().mode = MQAMode.Market
				#endif
				```
				{: codeblock}

			코드의 예는 다음과 같습니다. 

				```
				func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

				//Set the SDK mode Market vs QA for Production
				   and Pre-Production
				#if Debug
					MQALogger.settings().mode = MQAMode.QA
				#elseif Release
					MQALogger.settings().mode = MQAMode.Market
				#endif

				// Set the application key
				MQALogger.startNewSession(withApplicationKey: "Your_Application_Key")

				// Override point for customization after
				   application launch.
				return true
				```
				{: codeblock}

				**Swift complete example**
				<pre><code>				
				func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions:[NSObject: AnyObject]?) -> Bool {
					// Override point for customization after application launch.
					//Set the Shake Device option to true or false. If this is not explicitly set, the Shake Device is enabled by default.
					MQALogger.settings().reportOnShakeEnabled = true
					//Set the SDK mode Market vs QA for Production and Pre-Production
					#if Debug
					MQALogger.settings().mode = MQAMode.QA
					#elseif Release
					MQALogger.settings().mode = MQAMode.Market
					#endif

				//Start the MQA session with the specified app key
					   MQALogger.startNewSession(withApplicationKey: "Your_Application_Key")
				// Enables MQA crash reporting to catch uncaught exceptions
					   NSSetUncaughtExceptionHandler(exceptionHandlerPointer);

					   return true
					}
				</code></pre>
				{: codeblock}

3. 앱을 실행하여 앱이 시작될 때 {{site.data.keyword.mqa}}가 시작되는지 확인하십시오. 

4. [{{site.data.keyword.mqa}} 시작하기](index.html) 페이지의 단계를 계속하십시오. 

# 관련 링크
{: #rellinks notoc}

## 관련 링크
{: #general notoc}
* [{{site.data.keyword.mqa}} 시작하기](index.html){:new_window}
