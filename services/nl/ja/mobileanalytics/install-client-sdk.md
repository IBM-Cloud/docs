---

copyright:
  years: 2015, 2016

---

# {{site.data.keyword.mobileanalytics_short}} のインストール
クライアント SDK
{: #mobileanalytics_sdk}
*最終更新日時: 2016 年 4 月 21 日*
{: .last-updated}

{{site.data.keyword.mobileanalytics_short}} クライアント SDK は、現在 Android、iOS および WatchOS で使用できます。

{: #shortdesc}

## Android クライアント SDK のインストール
{: #install-sdk-android}

{{site.data.keyword.mobileanalytics_short}} クライアント SDK は、Gradle (Android プロジェクト用の依存関係マネージャー) で配布されています。Gradle は自動的に成果物をリポジトリーからダウンロードし、それらを Android アプリケーションで使用できるようにします。

1. [Android Studio](http://developer.android.com/sdk/index.html) プロジェクトを作成するか、既存のプロジェクトを開きます。

2. ご使用のアプリケーション・モジュールにある `build.gradle` ファイルを開きます。

  **ヒント**: ご使用の Android プロジェクトには、プロジェクト用とアプリケーション・モジュール用の 2 つの `build.gradle` ファイルがある場合があります。必ず**アプリケーション・モジュール**・ファイルの方を使用してください。

3. `build.gradle` ファイルの `Dependencies` セクションを探し、以下のように {{site.data.keyword.mobileanalytics_short}} クライアント SDK のコンパイル依存関係を追加します。

  ```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
      name:'analytics',
      version: '1.+',
      ext: 'aar',
      transitive: true
  ```
  {: codeblock}

  リポジトリー・ステートメントは、以下のコード例のようにする必要があります。

	```Gradle
      dependencies {
        compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
          name:'analytics',
          version: '1.+',
          ext: 'aar',
          transitive: true
    	// other dependencies  
      }
  ```
  {: screen}

4. **「ツール」&gt;「Android」&gt;「プロジェクトを Gradle ファイルと同期 (Sync Project with Gradle Files)」**の順にクリックしてプロジェクトを Gradle と同期します。

5. Android プロジェクトの `AndroidManifest.xml` ファイルを開き、インターネット・アクセス許可を `<manifest>` 要素の下に追加します:

	```XML
	 <uses-permission android:name="android.permission.INTERNET" />
   ```
   {: codeblock}


## Swift SDK のインストール
{: #installing-sdk-ios}

{{site.data.keyword.mobileanalytics_full}} SDK によって、モバイル・アプリケーションを装備できるようになります。Swift SDK は iOS および watchOS で使用できます。

### 始める前に
{: #before-you-begin-ios}

Xcode が正しくセットアップされていることを確認します。iOS 開発環境のセットアップ方法について詳しくは、[Apple Developer Web サイト](https://developer.apple.com/support/xcode/)を参照してください。

{{site.data.keyword.mobileanalytics_short}} SDK は、Cocoa プロジェクトの依存関係マネージャーである [Cocoapods](https://cocoapods.org/) および [Carthage](https://github.com/Carthage/Carthage#getting-started) で配布されています。CocoaPods および Carthage は、自動的に成果物をリポジトリーからダウンロードし、それらをアプリケーションで使用できるようにします。

#### Cocoapods
{: #cocoapods}
1. CocoaPods がインストールされていない場合は、次のコマンドを実行します:

    ```
    sudo gem install cocoapods
    ```
    {: codeblock}

2. まだ CocoaPods 用のワークスペースを初期設定していない場合は、プロジェクトのルート・ディレクトリーで `pod init` コマンドを実行します。CocoaPods によって `Podfile` ファイルが作成されます。このファイルに Xcode プロジェクトの依存関係を定義します。

3. `BMSAnalytics` ポッドを Podfile の target に、次の例のように追加します:

	### iOS

  ```
  use_frameworks!

  target 'MyApp' do
     platform :ios, '8.0'
     pod 'BMSAnalytics'
  end
  ```

4. `Podfile` ファイルを保存し、コマンド・ラインから `pod install` を実行します。

5. CocoaPods が生成した `.xcworkspace` ファイルを使用して Xcode プロジェクトのワークスペースを開きます。

#### Carthage
{: #carthage}

[Carthage](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos) を使用してプロジェクトにフレームワークを追加します。

1. `BMSAnalytics` フレームワークを Cartfile に追加します:
  ```
  github "ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics"
  ```
2. `carthage update` コマンドを実行します。ビルドが完了したら、`BMSAnalytics.framework`、`BMSCore.framework`、および `BMSAnalyticsAPI.framework` を Xcode プロジェクトにドラッグします。
3. [Carthage](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos) サイトにある説明に従って、統合を実行します。

# 関連リンク

## SDK
* [Android SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-analytics){: new_window}  
* [iOS SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics){: new_window}

## API リファレンス
{: #api}
* [REST API](https://mobile-analytics-dashboard.eu-gb.bluemix.net/analytics-service/){:new_window}
