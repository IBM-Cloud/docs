---

copyright:
  years: 2016
lastupdated: "2016-10-13"

---
{:new_window: target="_blank"}

# チュートリアル - Store Catalog UI スターター
{: #tutorial_store_catalog}

最終更新日: 2016 年 10 月 13 日
{: .last-updated}

{{site.data.keyword.Bluemix}} Store Catalog UI スターターは、カスタマイズ可能な基本的販売アプリ構造を提供し、各 {{site.data.keyword.Bluemix_notm}} モバイル・サービスの統合ポイントを提供します。


## 必要条件
{: #tutorial_requirements}

* [Bluemix](http://bluemix.net) アカウント


## 開始
{: #tutorial_gs}

Store Catalog コード・スターターを使用して素早く稼働中にするには、以下のステップに従ってください。

1. {{site.data.keyword.Bluemix_notm}} 「モバイル」ダッシュボードでプロジェクトを作成します。

   1. 「モバイル」ダッシュボードの**「開始」**ページで**「プロジェクトの作成」**をクリックします。

      代替方法として、**「プロジェクト」**ページで**「プロジェクトの作成」**をクリックすることもできます。

   2. **「UI スターター (UI Starters)」**を選択します (まだ選択されていない場合)。

   3. **「Store Catalog」**を選択し、**「プロジェクトの作成」**をクリックします。

   4. プロジェクト名を入力し、**「作成」**をクリックします。

2. オプション: Push Notifications (プッシュ通知) を追加します。

   1. **「プロジェクト概要 (Project Overview)」**ページで、**「Push Notifications」**に対して**「追加」**をクリックします。

      代替方法として、**「Push Notifications」**ページで**「作成」**をクリックすることもできます。

   2. サービス名を入力し、**「作成」**をクリックします。

   3. iOS の場合、[Apple プッシュ通知サービスの構成](../services/mobilepush/t_push_provider_ios.html){: new_window}を行います。

   4. Android の場合、[Google クラウド・メッセージングの構成](../services/mobilepush/t_push_provider_android.html){: new_window}を行います。

3. オプション: その他のサービスを追加します。

   1. **「プロジェクト概要 (Project Overview)」**ページで、追加するサービスに対して**「追加」**をクリックします。

   2. サービス名を入力し、**「作成」**をクリックします。

   3. サービスの指示に従ってサービスをセットアップします。

4. アプリを設計します。

   1. アプリの設計をカスタマイズするため、ナビゲーション・メニューで**「UI ビルダー (UI Builder)」**を選択します。

   2. ナビゲーションで**「設計」**タブを選択します。

      アプリの設計のためのワークスペースと、アプリの外観をシミュレートしたビューがあります。

   3. オプションで、**「画面の作成 (Create Screen)」**を選択することによって新規画面を追加します。アプリ内で簡単に参照できるように新規画面に名前を付けます。ツリーで何が選択されているのかに関わらず、新規画面は主画面と同じレベルで作成されます。以下の画面タイプから選択できます。
      * メニュー
      * リスト
      * マップ
      * カスタム
      * グラフ (Chart)	   

   4. インターフェースの*「レイアウト」*セクションにある**「メニュー」**テキスト・ボックスを選択し、**「表示するデータ (Data to display)」**フィールドの内容を置き換えることによって、アプリのメニュー・タイトルを変更することができます。シミュレートされたデバイスのセクションで更新内容を確認します。

      必要に応じて、設計項目を更新するため、各項目を選択して情報を更新します。これらの項目はツリー形式で表示されます。メニュー項目の順序または場所は、項目を新しい場所までドラッグすることによって変更できます。その項目の子もすべて親と一緒に移動されます。**「表示するデータ (Data to display)」**フィールドに表示されるツリー項目内のテキスト情報は、データ・ソース・スプレッドシートの内容を参照します。*これらの項目は**「データ」**ビュー内で識別されるデータ・ソースの内容で上書きされるため、**「設計」**ビューでこれらの項目を変更しないでください。*

		ツリー内で*「フォーム」*として識別される項目は独立していて、インラインで変更可能です。そういった項目は、データ・ソースからの情報を参照しません。

   5. ナビゲーションで**「データ」**を選択して、アプリによって使用されているデータを表示します。テンプレートにはデフォルトの情報が含まれていますが、**「新規作成 (Create New)」**を選択することによってデータのソースを変更することができます。複数のデータ・ソースを参照できるため、使用するそれぞれに名前を付けてください。以下のデータ・ソース・オプションから選択できます。
      * クラウド
      * ローカル
      * Cloudant
      * Google Sheet
      * Excel Online
      * Google ドライブ

      ボタンを使用し、表の内容を選択することによって、表の内容をインポート、エクスポート、または変更することもできます (表がローカルである場合)。

	  注意: デフォルト・データの構造と一致しないデータをインポートする場合、*「スキーマの置換」*スライダーをオンにしてください。これの例は、スターターで提供されるデータよりも列の数が少ない .csv ファイルです。

   6. ナビゲーションで**「ユーザー・アクセス (User Access)」**を選択して、プロジェクトのアクセス要件を変更します。ユーザー・アクセスをスイッチでオンとオフに切り替えることができます。ユーザー・アクセスがオンになっている場合、非アクティブ・ユーザーのタイムアウトと、アプリにアクセスできるユーザーの資格情報を設定できます。

   7. ナビゲーション・メニューで**「設定」**を選択して、プロジェクトの全体的情報およびカラーを変更します。この画面は、プロジェクトに追加したサービスで必要な場合に Google API キーを入力する場所です。この画面は、Apple Store または Google Play Store に登録される固有のバンドル ID を追加する場所でもあります。

      IBM MobileFirst Foundation SDK をプロジェクトに追加したい場合、スイッチをオンに切り替えてください。

   8. IBM MobileFirst Platform Foundation をプロジェクトに追加するために*「設定」*画面でスイッチを切り替えた場合、ナビゲーションに**「ファウンデーション (Foundation)」**の選択が表示されます。**「ファウンデーション (Foundation)」**を選択し、IBM MobileFirst Platform Foundation 固有の必要な情報を入力してください。

   9. ナビゲーション・メニューで**「公開」**を選択して、モバイル・アプリを作成するために必要な最後の情報を入力します。バンドル ID (iOS の場合) およびアプリケーション ID (Android の場合) を入力できます。

       iOS アプリを作成している場合、バンドル ID、配布証明書 (*.p12* ファイル)、およびプロビジョニング・プロファイル (*.mobileprovision* ファイル) を Apple プロビジョニング・ポータルから取得する必要があります。これら 3 つは、同時に同じコンピューター (Apple ストアにアプリを送るときに使用する予定のもの) で作成される必要があります。配布証明書およびプロビジョニング・プロファイルは、バンドル ID に基づいている必要があります。 	

5. プロジェクトをダウンロードします。

   1. **「コード」**をクリックし、優先するプラットフォームまたはプログラミング言語を選択します。

   2. Android の場合、コードが生成された後、以下のオプションから選択することができます。

      **コードのダウンロード**

      **APK のダウンロード**

      **QR コードとともにダウンロード**

   3. iOS の場合、コードが生成された後、以下のオプションから選択することができます。

      **コードのダウンロード**

6. デバイスまたはシミュレーターでアプリを実行します。


## 次のタスク
{: #tutorial_next}

[試してみてください](http://new-console.{DomainName}/mobile/create-project?starter=fb5e31a9-1186-4d46-939e-2f620f35b83b){: new_window}


# 関連リンク
{: #rellinks}

<!-- links to internal services don't work
## {{site.data.keyword.Bluemix_notm}} Mobile services
{: #general}
* [Mobile Analytics (Beta)](../services/mobileanalytics/index.html){: new_window}
* [Mobile Client Access](../services/mobileaccess/index.html){: new_window}
* [Mobile Foundation](../services/mobilefoundation/index.html){: new_window}
* [Mobile Quality Assurance)](../services/MobileQualityAssurance/index.html){: new_window}
* [Push Notifications](../services/mobilepush/index.html){: new_window}
-->

## ブログ投稿
{: #general}
* [ブログ投稿: Introducing the Bluemix Mobile dashboard](https://developer.ibm.com/bluemix/2016/07/08/new-bluemix-mobile-dashboard/){: new_window}
* [ブログ投稿: Introducing the next generation of the Bluemix Mobile dashboard](https://ibm.com/blogs/bluemix/2016/10/introducing-the-next-generation-of-the-bluemix-mobile-dashboard/){: new_window}
* [ブログ投稿: Introducing Bluemix Mobile Code Starters](https://www.ibm.com/blogs/bluemix/2016/10/rapid-dev-with-mobile-code-starters/){: new_window}
* [ブログ投稿: Bluemix Mobile, Part 1: Creating a Store Catalog application](https://developer.ibm.com/bluemix/2016/07/13/bluemix-mobile-creating-store-catalog-app-part1/){: new_window}
* [ブログ投稿: Bluemix Mobile, Part 2: Integrating custom Bluemix backend into the Store Catalog app](https://developer.ibm.com/bluemix/2016/07/14/bluemix-mobile-integrating-custom-backend-part2/){: new_window}

## チュートリアルおよびサンプル
{: #samples}
* [Mobile Backend for Bluemix](https://github.com/ibm-bluemix-mobile-services/mobiledashboard-storecatalog-backend){: new_window}
