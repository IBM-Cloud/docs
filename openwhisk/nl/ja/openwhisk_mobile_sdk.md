---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.openwhisk_short}} モバイル SDK の使用
{: #openwhisk_mobile_sdk}
*最終更新日: 2016 年 3 月 28 日*

{{site.data.keyword.openwhisk}} は、モバイル・アプリが簡単にリモート・トリガーを発生させてリモート・アクションを起動できるようにする、iOS デバイスおよび watchOS 2 デバイス用のモバイル SDK を提供します。
Android 用のバージョンは、現時点では使用できません。Android 開発者は、直接、{{site.data.keyword.openwhisk}} REST API を使用することができます。
{: shortdesc}

モバイル SDK は、Swift 2.2 で作成されており、iOS 9 以降のリリースをサポートしています。

## アプリへの SDK の追加
{: #openwhisk_add_sdk}
モバイル SDK は、CocoaPods または Carthage を使用するか、あるいはソース・ディレクトリーから、インストールすることができます。

### CocoaPods を使用したインストール 

モバイル用 {{site.data.keyword.openwhisk_short}} SDK は、
CocoaPods を通して公開配布で入手できます。Cocoapods がインストールされていることを前提として、スターター・アプリのプロジェクト・ディレクトリー内部の「Podfile」というファイルに以下の行を追加します。 

```
source 'https://github.com/openwhisk/openwhisk-podspecs.git'

use_frameworks!

target 'MyApp' do
     platform :ios, '9.0'
     pod 'OpenWhisk'
end

target 'MyApp WatchKit Extension' do
     platform :watchos, '2.0'
     pod 'OpenWhisk-Watch'
end
```
{: codeblock}

コマンド・ラインから「pod install」と入力します。これにより、watchOS 2 拡張機能が付いた iOS アプリ用の SDK がインストールされます。プロジェクトを Xcode で開くために Cocoapods によってアプリ用に作成されたワークスペース・ファイルを使用します。

### Carthage を使用したインストール

アプリのプロジェクト・ディレクトリーに「Cartfile」というファイルを作成します。Cartfile に次の行を追加します。
```
github "openwhisk//openwhisk-client-swift.git" ~> 0.1.0 # Or latest version
```
{: codeblock}

コマンド・ラインから「carthage update --platform ios」と入力します。Carthage は、SDK をダウンロードおよびビルドして、アプリのプロジェクト・ディレクトリーに「Carthage」というディレクトリーを作成し、
Carthage/build/iOS 内部に OpenWhisk.framework ファイルを置きます。Xcode プロジェクトの組み込みフレームワークに OpenWhisk.framework を追加します。

### ソース・コードからのインストール

ソース・コードは、https://github.com/openwhisk//openwhisk-client-swift.git で入手可能です。
Xcode の OpenWhisk.xcodeproj ファイルを使用して、プロジェクトを開きます。プロジェクトには、それぞれ iOS と watchOS2 用の「OpenWhisk」と「OpenWhiskWatch」という 2 つのスキーマが含まれます。
必要なターゲットのプロジェクトをビルドし、結果のフレームワークをご使用のアプリに追加します (通常は ~/Library/Developer/Xcode/DerivedData/ご使用のアプリ名)。

## スターター・アプリ・サンプルのインストール
{: #openwhisk_install_sdkstart}

{{site.data.keyword.openwhisk_short}} CLI　を使用して、{{site.data.keyword.openwhisk_short}} SDK フレームワーク
を組み込むサンプル・コードをダウンロードします。  

スターター・アプリ・サンプルをインストールするには、次のコマンドを入力します。
```
wsk sdk install iOS
```
これにより、スターター・アプリを含む zip ファイルがダウンロードされます。プロジェクト・ディレクトリーの内部は Podfile です。端末から「pod install」を実行して、SDK をインストールします。
{: pre}

## SDK 入門
{: #openwhisk_sdk_getstart}

迅速に立ち上げて稼動させるためには、
{{site.data.keyword.openwhisk_short}} API 資格情報を使用して WhiskCredentials オブジェクトを作成し、そこから {{site.data.keyword.openwhisk_short}} インスタンスを作成します。


例えば Swift 2.1 では、次のサンプル・コードを使用して資格情報オブジェクトを作成します。

```
let credentialsConfiguration = WhiskCredentials(accessKey: "myKey", accessToken: "myToken")

let whisk = Whisk(credentials: credentialsConfiguration!)
```
{: codeblock}

前述の例で、{{site.data.keyword.openwhisk_short}} から取得した `myKey` と `myToken` を受け渡します。次の CLI コマンドでキーとトークンを検索します。

```
wsk property get --auth
```
{: pre}
```
whisk auth        kkkkkkkk-kkkk-kkkk-kkkk-kkkkkkkkkkkk:tttttttttttttttttttttttttttttttttttttttttttttttttttttttttttttttt
```
{: screen}

コロンの前後の文字列は、それぞれご使用のキーとトークンです。

## {{site.data.keyword.openwhisk_short}} アクションの起動
{: #openwhisk_sdk_invoke}


リモート・アクションを起動するために、アクション名を使用して `invokeAction` を呼び出すことができます。アクションが属する名前空間を指定するか、ブランクのままにしてデフォルトの名前空間を受け入れます。必要に応じて、ディクショナリーを使用して、パラメーターをアクションに渡します。

例えば次のようにします。

```
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
{: codeblock}

前述の例では、デフォルトの名前空間を使用して `helloConsole` アクションを起動します。

## {{site.data.keyword.openwhisk_short}} トリガーの発生
{: #openwhisk_sdk_fire}

リモート・トリガーを発生させるために、
`fireTrigger` メソッドを呼び出すことができます。ディクショナリーを使用して、必要に応じてパラメーターを受け渡します。

```
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
{: codeblock}

前述の例では、`locationChanged` というトリガーを発生させています。

## 結果を返すアクションの使用
{: #openwhisk_sdk_actionresult}

アクションが結果を返す場合、invokeAction 呼び出しで hasResult を true に設定します。アクションの結果は、次のように応答ディクショナリーに返され
ます。

```
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
{: codeblock}

デフォルトでは、SDK は、アクティベーション ID と起動されたアクションによって生成された結果のみを返します。HTTP 応答状況コードを含む完全な応答オブジェクトのメタデータを取得するには、次のような設定を使用します。

```
whisk.verboseReplies = true
```
{: codeblock}

## SDK の構成
{: #openwhisk_sdk_configure}

baseURL パラメーターを使用して、SDK を構成し、
{{site.data.keyword.openwhisk_short}} の異なるインストール済み環境で作業することができます。
以下に例を示します。

```
whisk.baseURL = "http://localhost:8080"
```
{: codeblock}

この例では、localhost:8080 で実行されているインストール済み環境を使用します。
baseUrl を指定しない場合は、モバイル SDK は https://openwhisk.ng.bluemix.net で実行されるインスタンスを使用します。

特殊なネットワーク・ハンドリングが必要な場合、
カスタム NSURLSession を受け渡すことができます。例えば、自己署名証明書を使用する独自の {{site.data.keyword.openwhisk_short}} インストール済み環境がある場合などです。

```
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
{: codeblock}

### 修飾名のサポート

すべてのアクションとトリガーには、名前空間、パッケージ、およびアクション名またはトリガー名から構成される完全修飾名があります。SDK は、アクションを起動する時またはトリガーを発生させる時に、これらをパラメーターとして受け入れることができます。SDK は、
`/mynamespace/mypackage/nameOfActionOrTrigger` のような完全修飾名を受け入れる関数も提供します。修飾名のストリングは、すべての {{site.data.keyword.openwhisk_short}} ユーザーが所有する名前空間とパッケージに対して名前なしのデフォルト値をサポートするため、以下の構文解析規則が適用されます。

- qName = "foo" の場合は、名前空間 = デフォルト、パッケージ = デフォルト、アクション/トリガー = "foo" となります。
- qName = "mypackage/foo" の場合は、名前空間 = デフォルト、パッケージ = mypackage、アクション/トリガー = "foo" となります。
- qName = "/mynamespace/foo" の場合は、名前空間 = mynamespace、パッケージ = デフォルト、アクション/トリガー = "foo" となります。
- qName = "/mynamespace/mypackage/foo" の場合は、名前空間 = mynamespace、パッケージ = mypackage、アクション/トリガー = "foo" となります。

他のすべての組み合わせでは WhiskError.QualifiedName エラーが発行されます。
そのため、修飾名を使用する際は、
「`do/try/catch`」構成で呼び出しをラップする必要があります。

### SDK ボタン

利便性を図るため、SDK には `WhiskButton` が含まれています。これにより `UIButton` が拡張され、アクションを起動することが可能になります。`WhiskButton` を使用するには、次の例に従います。

```
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
{: codeblock}
