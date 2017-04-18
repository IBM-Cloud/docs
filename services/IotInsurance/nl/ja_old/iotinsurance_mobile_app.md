---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-08"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


<!-- {{site.data.keyword.iotinsurance_full}}  {{site.data.keyword.iotinsurance_short}}  -->


# サンプル・モバイル・アプリのインストールと接続
{: #iot4i_gettingstarted}

{{site.data.keyword.iotinsurance_full}} サンプル・モバイル・アプリは、{{site.data.keyword.iotinsurance_short}} のモバイル・クライアントの参照実装です。このアプリを使用して、システムに新規デバイスを登録し、デバイスのアラートを受信することができます。
{:shortdesc}

**注**: {{site.data.keyword.iotinsurance_short}} は、{{site.data.keyword.amafull}} と {{site.data.keyword.mobilepushfull}} のいずれもデプロイしなくなりました。旧バージョンの {{site.data.keyword.iotinsurance_short}} は、{{site.data.keyword.amashort}} サービスを使用してモバイル・アプリからの応答を処理していました。このプロセスは、既存のすべての {{site.data.keyword.iotinsurance_short}} インスタンスで引き続き機能します。しかし、新規の {{site.data.keyword.iotinsurance_short}} インスタンスでモバイル・アプリを使用するには、カスタムの認証プロセスを作成する必要があります。またオプションで、[{{site.data.keyword.mobilepushshort}} のインスタンスを作成し](../mobilepush/index.html)、それを構成し、{{site.data.keyword.iotinsurance_short}} API にバインドすることができます。

**前提条件:** 始めに、以下の前提条件が満たされていることを確認します。
  - Apple Xcode 8 以降の統合開発環境。
  - iOS 9.0 以降の iPhone モバイル・デバイス。
  - CocoaPods がコンピューターにインストールされている。[CocoaPods Web サイト ![外部リンク・アイコン](../../icons/launch-glyph.svg)](https://guides.cocoapods.org/using/getting-started.html){: new_window} を参照してください。
  - サンプル・モバイル・アプリをサービスのインスタンスに接続するために必要な[パラメーター](#iot4i_mobileParam)。

## サンプル・モバイル・アプリのビルド
{: #building_mobile}
サンプル・モバイル・アプリを試すには、以下のタスクを実行します。

1. Xcode 7.3 以降がインストールされているコンピューターに[サンプル・モバイル・アプリのソース・コード・リポジトリー ![外部リンク・アイコン](../../icons/launch-glyph.svg)](https://github.com/ibm-watson-iot/ioti-mobile){: new_window} を複製します。
2. CocoaPods の pod install コマンドをプロジェクトで実行して、必要なパッケージをインストールし、IoT4I.xcworkspace ファイルを生成します。このタスクを実行するには、CocoaPods をインストールしておく必要があります。
3. IoT4I.xcworkspace ファイルをダブルクリックして、Xcode でプロジェクトを開きます。
4. iPhone をコンピューターに接続し、それをビルドの宛先として選択します。
5. ファイルのリストの IoT4I ファイルを選択し、「ID (Identity)」ダイアログ・ボックスを表示します。
6. Xcode の「ID (Identity)」ダイアログ・ボックスで、以下の変更を行ないます。
  - **「バンドル ID (Bundle Identifier)」**を固有 ID (例: **myIoT4Ibundle**) に変更します。
  - **「チーム (Team)」**を個人のチーム名に設定し、**「問題の修正 (Fix Issue)」**をクリックします。
7. アプリを {{site.data.keyword.iotinsurance_short}} のインスタンスに接続するには、**constants.swift** ファイルの以下のパラメーターを設定します。  
    - [applicationRoute](#iot4i_mobileParam) = {{site.data.keyword.iotinsurance_short}} API アプリケーションの URL。この値は、{{site.data.keyword.iotinsurance_short}} サービス・コンソールの「サービス資格情報」タブで確認できます。
    - [applicationId](#iot4i_mobileParam) = {{site.data.keyword.amashort}} のインスタンスの GUID。この値は、{{site.data.keyword.amashort}} を開き、**「モバイル・オプション」**をクリックすると確認できます。この値は、アプリ GUID / テナント ID と呼ばれます。
8. コンピューターで矢印をクリックして、現在のスキームをビルドして実行します。サンプル・モバイル・アプリが電話機にインストールされます。詳しくは、[Xcode からデバイスでアプリを実行するための Apple 開発者への指示 ![外部リンク・アイコン](../../icons/launch-glyph.svg)](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/LaunchingYourApponDevices/LaunchingYourApponDevices.html){: new_window} を参照してください。

  **注:** ビルドしようとしたときに*「アプリ開発用証明書がデバイスで信頼できることがまだ確認されていないため IoT4I を起動できませんでした (Could not launch IoT4I because you have not yet verified that your Developer App certificate is trusted on your device)」*というエラーが表示される場合、次の手順で自分自身を「信頼できる開発者 (Trusted Developer)」として選択します。  
    1. 電話機で、**「設定 (Settings)」>「一般 (General)」>「デバイス管理 (Device Management)」>「yourDeveloperID」**に移動します。
    2. 開発者 ID アカウント名をタップし、開発者 ID の信頼を設定します。
    3. プロンプトが表示されたら、開発者 ID が信頼できることを確認します。

## モバイル・アプリのプッシュ通知の有効化
{: #iot4i_pushNotification}

モバイル・デバイスのプッシュ通知を有効化するには、以下のタスクを実行します。プッシュ通知サービスを使用するには、有効な Apple 開発者アカウント・メンバーシップが必要です。

1. [Apple 開発者アカウント ![外部リンク・アイコン](../../icons/launch-glyph.svg)](https://developer.apple.com/account){: new_window} にログインします。

2. 証明書ファイルを作成します。
  1. **「証明書、ID、およびプロファイル (Certificates, Identifiers & Profiles)」**を選択します。
  2. 「ID: アプリ ID (Identifiers: App IDs)」を選択します。
  3. 追加ボタン (+) をクリックして、新規アプリ ID を作成します。
  4. アプリの説明を**「説明 (Description)」**に入力します。
  5. **「明示的アプリ ID (Explicit App ID)」**を選択し、バンドル ID (例えば com.YourOrganizationName.iot4i.mobileApp) を入力します。
  6. **「プッシュ通知 (Push Notifications)」**で (V) を選択し、**「続行 (Continue)」>「登録 (Register)」>「完了 (Done)」**をクリックします。

3. プッシュ通知証明書を作成します。
  1. **「証明書: すべて (Certificates: All)」**を選択します。
  2. 追加ボタン (+) をクリックして、新規 APN 証明書を作成します。
  3. 「iOS 証明書の追加 (Add iOS Certificate)」ページで、**「Apple プッシュ通知サービスの SSL (サンドボックス) (Apple Push Notification service SSL (Sandbox))」**を選択し、**「続行 (Continue)」**をクリックします。
  4. 前のステップで作成したアプリ ID を選択し、**「続行 (Continue)」**をクリックします。
  5. ページにある指示を使用して CSR ファイルを作成し、**「続行 (Continue)」**をクリックします。
  6. 作成した CSR ファイルを選択し、**「続行 (Continue)」**をクリックします。
  7. 証明書ファイルをダウンロードして実行します。

4. プロファイルを作成します。
  1. **「プロビジョニング・プロファイル: 開発 (Provisioning profile: Development)」**を選択します。
  2. 追加ボタン (+) をクリックして、新規開発プロファイルを作成します。
  3. **「iOS アプリ開発 (iOS App Development)」**を選択し、**「続行 (Continue)」**をクリックします。
  4. 前に作成したアプリ ID を選択します。
  5. **「開発者証明書: すべて (Developer Certificates: All)」**を選択し、**「続行 (Continue)」**をクリックします。
  5. **「すべての開発デバイス (テスト・デバイス) (All development devices (testing devices))」**を選択し、**「続行 (Continue)」**をクリックします。
  6. プロファイル名を指定し、**「続行 (Continue)」**をクリックします。
  7. 生成されたプロファイルをダウンロードして実行します。

5. Public Key Cryptography Standards (PKCS) 12 ファイルを作成し、{{site.data.keyword.mobilepushshort}} サービスに追加します。
  1. キーチェーン・アクセスを開き、**「私の証明書 (My Certificates)」**を選択します。
  2. **「Apple Development IOS Push Service: (bundleID)」**を右クリックし、ファイルのパスワードをエクスポート、保存、そして入力します。
  3. {{site.data.keyword.Bluemix_notm}} コンソールで、{{site.data.keyword.mobilepushshort}} サービスを開きます。
  4. **「構成 (Configure)」**をクリックします。
  5. 「Apple プッシュ通知証明書 (Apple Push Notifications Certificate)」セクションで、PKCS 12 ファイルをアップロードし、パスワードを入力します。
  6. Xcode で、バンドル ID を前に作成したものに変更します。
  7. アプリを実行し、プッシュ通知サービスの許可を付与します。
