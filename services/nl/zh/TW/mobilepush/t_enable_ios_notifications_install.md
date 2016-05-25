# 起始設定 Push SDK for iOS 應用程式
{: #enable-push-ios-notifications-install}

若為現有的 Xcode 專案，您可以使用 CocoaPods 相依關係管理工具來設定 Bluemix Mobile Services Client SDK。替代方案是手動安裝 SDK。

**附註**：若要檢視 Swift Push Readme 檔，請移至 https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master

##安裝 CocoaPods

1. 在 Mac 終端機中，使用下列指令來安裝 CocoaPods。
```
$ sudo gem install cocoapods
```
2. 在終端機中輸入下列指令，以起始設定 CocoaPods。發出此指令時，請確定是在 Xcode 專案所在的目錄中執行它。`pod init` 指令會建立檔案標題。
```
$ pod init
```
3. 在產生的 Podfile 中，新增您需要的 SDK 相依關係。請複製下列 Podfile。

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
3. 從「終端機」中，移至您的專案資料夾，並使用下列指令來安裝相依關係：```
$ pod update
```
該指令會安裝相依關係並建立新的 Xcode 工作區。**附註**：請確定您一律開啟新的 Xcode 工作區，而不是原始 Xcode 專案檔：

	```
	$ open App.xcworkspace
	```
工作區會包含原始專案以及包含相依關係的 Pods 專案。如果您想要修改 Bluemix Mobile Services 來源資料夾，則可以在 Pods 專案的 `Pods/yourImportedSourceFolder` 下找到它，例如：`Pods/IMFGoogleAuthentication`。

##使用匯入的架構和來源資料夾

在您的程式碼中參照 SDK。


### Objective-C

撰寫相關標頭的 #import 指引，例如：

```
//Objective-C

#import <IMFCore/IMFCore.h>
#import <IMFPush/IMFPush.h>
```

**附註**：使用 CocoaPods 指令 `pod install` 或 `pod update` 更新 Pods 專案時，可能會置換 Bluemix Mobile Services 來源資料夾。如果您要保留原始檔案的自訂版本，請確保先進行備份，然後再發出下列其中一個指令。

###Swift

**先決條件**

- iOS 8.0 或以上版本
- Xcode 7


撰寫相關標頭的 #import 指引，例如：

```
//swift
import BMSCore
import BMSPush
```


##建置設定

移至 **Xcode > 建置設定 > 建置選項，然後將啟用位元碼**設為**否**。

**注意**：自 iOS 9 開始，對「應用程式傳輸安全 (ATS)」特性進行的變更可能會影響您處理鑑別處理程序的方式。下列部落格文章說明了這些變更的相關資訊：[ATS and Bitcode in iOS 9](https://developer.ibm.com/mobilefirstplatform/2015/09/09/ats-and-bitcode-in-ios9/) 及 [Connect your iOS 9 app to Bluemix today](https://developer.ibm.com/bluemix/2015/09/16/connect-your-ios-9-app-to-bluemix/)
