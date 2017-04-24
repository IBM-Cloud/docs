
# 使用 OpenWhisk 行動 SDK

OpenWhisk 提供適用於 iOS 及 watchOS 裝置的行動 SDK，讓行動應用程式輕鬆地發動遠端觸發程式以及呼叫遠端動作。目前沒有適用於 Android 的版本；Android 開發人員可以直接使用 OpenWhisk REST API。

行動 SDK 是以 Swift 3.0 撰寫，並且支援 iOS 10 及更新版次。您可以使用 Xcode 8.0 來建置行動 SDK。SDK 的舊式 Swift 2.2/Xcode 第 7 版最多可到 0.1.7，但是現在已淘汰。

## 將 SDK 新增至應用程式

您可以使用 CocoaPods 或 Carthage 或者從來源目錄中安裝行動 SDK。

### 使用 CocoaPods 進行安裝

適用於行動的 OpenWhisk SDK 可用於透過 CocoaPods 進行的公用配送。假設已安裝 CocoaPods，請將下列幾行放入入門範本應用程式專案目錄內名為 'Podfile' 的檔案中。

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

從指令行鍵入 `pod install`。此指令會安裝適用於具有 watchOS 延伸的 iOS 應用程式的 SDK。使用 CocoaPods 為您的應用程式所建立的工作區檔案，在 Xcode 中開啟專案。 

安裝之後，請開啟專案工作區。您可能會在建置時收到下列警告：
`Use Legacy Swift Language Version” (SWIFT_VERSION) is required to be configured correctly for targets which use Swift. Use the [Edit > Convert > To Current Swift Syntax…] menu to choose a Swift version or use the Build Settings editor to configure the build setting directly.`
如果 Cocoapods 未在 Pods 專案中更新 Swift 版本，則會導致此情況。若要修正，請選取 Pods 專案及 OpenWhisk 目標。移至「建置設定」，並將`使用舊式 Swift 語言版本`設定變更為 `no`。或者，您也可以在 Podfile 尾端新增下列後置安裝指示：

```
post_install do |installer|
  installer.pods_project.targets.each do |target|
    target.build_configurations.each do |config|
      config.build_settings['SWIFT_VERSION'] = '3.0'
    end
  end
end
```

### 使用 Carthage 進行安裝

在應用程式的專案目錄中建立檔案，並將它命名為 'Cartfile'。請在檔案中放入下一行：
```
github "openwhisk/openwhisk-client-swift.git" ~> 0.2.2 # Or latest version
```

從指令行鍵入 `carthage update --platform ios`。Carthage 會下載並建置 SDK，並在應用程式的專案目錄中建立稱為 Carthage 的目錄，然後將 OpenWhisk.framework 檔案放入 Carthage/build/iOS 中。

然後，您必須將 OpenWhisk.framework 新增至 Xcode 專案中的內嵌架構

### 從原始碼進行安裝

原始碼位於 https://github.com/openwhisk/openwhisk-client-swift.git。使用 Xcode，以透過使用 `OpenWhisk.xcodeproj` 來開啟專案。
專案包含兩個方法："OpenWhisk"（目標設為 iOS）及 "OpenWhiskWatch"（目標設為 watchOS 2）。
建置所需目標的專案，以及將產生的架構新增至應用程式（通常是在 ~/Library/Developer/Xcode/DerivedData/your app name 中）。

## 安裝入門範本應用程式範例

您可以使用 OpenWhisk CLI 來下載內嵌 OpenWhisk SDK 架構的範例程式碼。  

若要安裝入門範本應用程式範例，請輸入下列指令：

```
$ wsk sdk install iOS
```

此指令會下載包含入門範本應用程式的壓縮檔。專案目錄中會有 podfile。 

若要安裝 SDK，請輸入下列指令：

```
$ pod install
```

## 開始使用 SDK

若要快速啟動並執行，請使用 OpenWhisk API 認證來建立 WhiskCredentials 物件，以及透過該物件來建立 OpenWhisk 實例。

例如，使用下列範例程式碼來建立認證物件：

```
let credentialsConfiguration = WhiskCredentials(accessKey: "myKey", accessToken: "myToken")
let whisk = Whisk(credentials: credentialsConfiguration!)
```

在前一個範例中，您傳入從 OpenWhisk 取得的 `myKey` 及 `myToken`。您可以使用下列 CLI 指令來擷取金鑰及記號：

```
$ wsk property get --auth
```
```
whisk auth        kkkkkkkk-kkkk-kkkk-kkkk-kkkkkkkkkkkk:tttttttttttttttttttttttttttttttttttttttttttttttttttttttttttttttt
```

冒號之前的字串是您的金鑰，冒號之後的字串則是您的記號。

## 呼叫 OpenWhisk 動作


若要呼叫遠端動作，您可以使用動作名稱來呼叫 `invokeAction`。您可以指定動作所屬的名稱空間，或讓它保留空白，以接受預設名稱空間。請視需要使用字典將參數傳遞給動作。

例如：

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

在前一個範例中，您可以使用預設名稱空間來呼叫 `helloConsole` 動作。

## 發動 OpenWhisk 觸發程式

若要發動遠端觸發程式，您可以呼叫 `fireTrigger` 方法。使用字典，視需要傳入參數。

```swift
// In this example we are firing a trigger when our location has changed by a certain amount
var locationParams = Dictionary<String, String>()
locationParams["payload"] = "{\"lat\":41.27093, \"lon\":-73.77763}"
do {try whisk.fireTrigger(name: "locationChanged", package: "mypackage", namespace: "mynamespace", parameters: locationParams, callback: {(reply, error) -> Void in
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

在前一個範例中，您是發動稱為 `locationChanged` 的觸發程式。

## 使用可傳回結果的動作

如果動作傳回結果，請在 invokeAction 呼叫中將 hasResult 設定為 true。回覆字典中會傳回動作的結果，例如：

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

SDK 預設只會傳回啟動 ID 以及所呼叫動作所產生的任何結果。若要取得整個回應物件的 meta 資料（包括 HTTP 回應狀態碼），請使用下列設定：

```swift
whisk.verboseReplies = true
```

## 配置 SDK

您可以使用 baseURL 參數配置 SDK，以使用不同的 OpenWhisk 安裝。例如：

```swift
whisk.baseURL = "http://localhost:8080"
```

在此範例中，您使用在 localhost:8080 執行的安裝。如果您未指定 baseUrl，行動 SDK 會使用在 https://openwhisk.ng.bluemix.net 執行的實例。

如果您需要特殊網路處理，則可以傳入自訂 NSURLSession。例如，您可能自己有使用自簽憑證的 OpenWhisk 安裝：

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

### 完整名稱支援

所有動作及觸發程式的完整名稱都是由名稱空間、套件及動作或觸發程式名稱所構成。呼叫動作或發動觸發程式時，SDK 可以接受這些元素作為參數。SDK 也提供接受類似 `/mynamespace/mypackage/nameOfActionOrTrigger` 之完整名稱的函數。完整名稱字串支援所有 OpenWhisk 使用者都有的名稱空間及套件的未命名預設值，因此適用下列剖析規則：

- qName = "foo" 導致名稱空間 = 預設值、套件 = 預設值、動作/觸發程式 = "foo"
- qName = "mypackage/foo" 導致名稱空間 = 預設值、套件 = mypackage、動作/觸發程式 = "foo"
- qName = "/mynamespace/foo" 導致名稱空間 = mynamespace、套件 = 預設值、動作/觸發程式 = "foo"
- qName = "/mynamespace/mypackage/foo 導致名稱空間 = mynamespace、套件 = mypackage、動作/觸發程式 = "foo"

所有其他組合都會發出 WhiskError.QualifiedName 錯誤。因此，當您使用完整名稱時，必須使用 "`do/try/catch`" 建構括住呼叫。

### SDK 按鈕

為方便起見，SDK 包含 `WhiskButton`，以擴充 `UIButton` 容許它呼叫動作。若要使用 `WhiskButton`，請遵循此範例：

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
do {// use qualified name API which requires do/try/catch
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
