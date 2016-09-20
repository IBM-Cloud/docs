# iOS アプリ用の Push SDK の初期化
{: #enable-push-ios-notifications-install}

既存の Xcode プロジェクトでは、CocoaPods 依存関係管理ツールを使用して Bluemix Mobile Services クライアント SDK をセットアップできます。あるいは、手動で SDK をインストールすることもできます。

**注**: Swift の Push の readme ファイルを確認するには、 https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master にアクセスしてください。

##CocoaPods のインストール

1. Mac ターミナルで以下のコマンドを使用して CocoaPods をインストールします。```
$ sudo gem install cocoapods
```
2. ターミナルで以下のコマンドを入力して CocoaPods を初期化します。このコマンドを発行する際には、必ず、Xcode プロジェクトがあるディレクトリーで実行してください。`pod init` コマンドはファイルのタイトルを作成します。
```
$ pod init
```
3. 生成された Podfile に、必要な SDK 依存関係を追加します。以下の Podfile をコピーします。

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
3. ターミナルで、プロジェクト・フォルダーに移動し、以下のコマンドを使用して依存関係をインストールします。
```
$ pod update
```
このコマンドにより、依存関係がインストールされ、新しい Xcode ワークスペースが作成されます。**注**: 元の Xcode プロジェクト・ファイルではなく、次のように必ず新しい Xcode ワークスペースを開いてください。

	```
	$ open App.xcworkspace
	```
このワークスペースには、元のプロジェクトと、依存関係が含まれている Pods プロジェクトが含まれています。Bluemix Mobile Services ソース・フォルダーを変更したい場合は、Pods プロジェクト内の `Pods/yourImportedSourceFolder` の下にあります (例えば、`Pods/IMFGoogleAuthentication`)。

##インポートされたフレームワークおよびソース・フォルダーの使用

コードで SDK を参照します。


### Objective-C

関連するヘッダーの #import ディレクティブを記述します。例えば、以下のようにします。

```
//Objective-C

#import <IMFCore/IMFCore.h>
#import <IMFPush/IMFPush.h>
```

**注**: CocoaPods コマンド `pod install` または `pod update` を使用して Pods プロジェクトを更新すると、Bluemix Mobile Services のソース・フォルダーがオーバーライドされる可能性があります。元ファイルのカスタマイズしたバージョンを保持する場合は、これらのコマンドのいずれかを発行する前には、それらをバックアップしてください。

###Swift

**前提条件**

- iOS 8.0 以降
- Xcode 7


関連するヘッダーの #import ディレクティブを記述します。例えば、以下のようにします。

```
//swift
import BMSCore
import BMSPush
```


##ビルド設定

**「Xcode」>「ビルド設定」>「ビルド・オプション」に移動し、「Bitcode を使用可能に設定 (Set Enable Bitcode)」**を**「いいえ」**に設定します。

**重要**: iOS 9 現在では、App Transport Security (ATS) 機能に対する変更が、認証プロセスの処理方法に影響する可能性があります。以下のブログ投稿に、変更に関する詳細情報が記載されています。 [ATS and Bitcode in iOS 9](https://developer.ibm.com/mobilefirstplatform/2015/09/09/ats-and-bitcode-in-ios9/) および [Connect your iOS 9 app to Bluemix today](https://developer.ibm.com/bluemix/2015/09/16/connect-your-ios-9-app-to-bluemix/)
