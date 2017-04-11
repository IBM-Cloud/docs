---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# BMSClient の初期化
{: #sdk_BMSClient}

`BMSCore` は、他の {{site.data.keyword.Bluemix}} モバイル・サービス・クライアント SDK が、それぞれに対応する {{site.data.keyword.Bluemix_notm}} サービスと通信するために使用する HTTP インフラストラクチャーを提供します。


## Android アプリケーションの初期化
{: #init-BMSClient-android}

`BMSCore` パッケージをダウンロードして Android Studio プロジェクトにインポートするか、または  Gradle を使用します。

1. プロジェクト・ファイルの先頭に以下の `import` ステートメントを追加して、クライアント SDK をインポートします。

  ```
  import com.ibm.mobilefirstplatform.clientsdk.android.core.api.*;
  ```
  {: codeblock}

2. Android アプリケーション内のメイン・アクティビティーの `onCreate` メソッド、またはプロジェクトの最適な動作位置に初期化コードを追加して、Android アプリケーションで `BMSClient` SDK を初期化します。

  ```Java
	BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_US_SOUTH); // Make sure that you point to your region
	```
  {: codeblock}

  **bluemixRegion** パラメーターを指定して `BMSClient` を初期化する必要があります。初期化指定子では、**bluemixRegion** 値は、どの {{site.data.keyword.Bluemix_notm}} デプロイメントを使用するか (例えば、`BMSClient.REGION_US_SOUTH`、`BMSClient.REGION_UK`、または `BMSClient.REGION_SYDNEY`) を指定します。


## iOS アプリケーションの初期化
{: #init-BMSClient-ios}

[CocoaPods](https://cocoapods.org){: new_window} または [Carthage](https://github.com/Carthage/Carthage){: new_window} を使用して、`BMSCore` パッケージを取得できます。

1. CocoaPods を使用して `BMSCore` をインストールするには、以下の行を Podfile に追加します。プロジェクトにまだ Podfile がない場合は、`pod init` コマンドを使用してください。

  ```Swift
  use_frameworks!

  target 'MyApp' do
    pod 'BMSCore'
  end
  ```
  {: codeblock}

  次に、`pod install` コマンドを実行し、生成された `.xcworkspace` ファイルを開きます。新しいリリースの `BMSCore` に更新するには、`pod update BMSCore` を使用します。

  CocoaPods の使用方法について詳しくは、[「CocoaPods Guides」 ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://guides.cocoapods.org/using/index.html){: new_window} を参照してください。

2. Carthage を使用して `BMSCore` をインストールするには、次の[手順 ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/Carthage/Carthage#getting-started){: new_window} を参照してください。

  1. 次の行を Cartfile に追加します。

      ```
      github "ibm-bluemix-mobile-services/bms-clientsdk-swift-core"
      ```
      {: codeblock}

  2. `carthage update` コマンドを実行します。

  3. ビルドが終了したら、Carthage の手順の[ステップ 3 ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/Carthage/Carthage#getting-started) に従って `BMSCore.framework` をプロジェクトに追加します。

      Swift 2.3 でビルドされているアプリケーションの場合は、`carthage update --toolchain com.apple.dt.toolchain.Swift_2_3` コマンドを使用します。その他の場合は、`carthage update` コマンドを使用します。

3. モジュールをインポートします。

  ```Swift
  import BMSCore
  ```
  {: codeblock}

4. 以下のコードを使用して、`BMSClient` クラスを初期化します。

  アプリケーション代行の `application(_:didFinishLaunchingWithOptions:)` メソッド、またはプロジェクトの最適な動作位置に、初期化コードを挿入します。

  ```Swift
    BMSClient.sharedInstance.initialize(bluemixRegion: BMSClient.Region.usSouth) // Make sure that you point to your region
    ```
  {: codeblock}

  **bluemixRegion** パラメーターを指定して `BMSClient` を初期化する必要があります。初期化指定子では、**bluemixRegion** 値は、どの {{site.data.keyword.Bluemix_notm}} デプロイメントを使用するか (例えば、`BMSClient.Region.usSouth`、 `BMSClient.Region.unitedKingdom`、または `BMSClient.Region.sydney`) を指定します。


## Cordova アプリケーションの初期化
{: #init-BMSClient-cordova}

1. Cordova アプリケーションのルート・ディレクトリーから以下のコマンドを実行して、Cordova プラグインを追加します。

  ```
  cordova plugin add bms-core
  ```
  {: codeblock}

2. メイン JavaScript ファイル、またはプロジェクトの最適な動作位置に初期化コードを追加して、Cordova アプリケーションで `BMSClient` クラスを初期化します。

  ```
  BMSClient.initialize(BMSClient.REGION_US_SOUTH);
  ```
  {: codeblock}
	
  **bluemixRegion** パラメーターを指定して `BMSClient` を初期化する必要があります。初期化指定子では、**bluemixRegion** 値は、どの {{site.data.keyword.Bluemix_notm}} デプロイメントを使用するか (例えば、`BMSClient.REGION_US_SOUTH`、`BMSClient.REGION_UK`、または `BMSClient.REGION_SYDNEY`) を指定します。


# 関連リンク
{: #rellinks notoc}

## 関連リンク
{: #general notoc}

* [BMSCore Android SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core){: new_window}
* [BMSCore iOS SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core){: new_window}
* [BMSCore Cordova Plugin](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core){: new_window}
