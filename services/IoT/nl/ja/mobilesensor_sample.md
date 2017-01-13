---

copyright:
  years: 2016

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}

# モバイル・デバイス・センサーのサンプル

モバイル・デバイス・センサーのサンプルは、JavaScript を使用して電話を {{site.data.keyword.iot_full}} に接続し、センサー・データを {{site.data.keyword.iot_short}} 組織にパブリッシュします。
{:shortdesc}

{{site.data.keyword.iot_short}} Python クライアント・ライブラリーを使用して、コマンドにサブスクライブし、電話によってパブリッシュされたセンサー・データを視覚化します。データ可視化は、Web Server Gateway Interface (WSGI) フレームワークで作成される Web サイトで提供されます。

このアプリケーションは、特定のデバイスからのセンサー・データへのユーザー・アクセスを制御する方法を示します。**「再生してみましょう (Let's Play)」**がクリックされると、アプリケーションはユーザー・レコードを {{site.data.keyword.cloudantfull}} データベースに作成し、{{site.data.keyword.iot_short}} デバイス管理 API を呼び出してデバイスを登録します。

## 前提条件

このサンプルをデプロイする前に:

- {{site.data.keyword.bluemix_notm}} アカウントを作成してログインします。{{site.data.keyword.bluemix_notm}} について詳しくは、[無料トライアルの開始](https://apps.admin.ibmcloud.com/manage/trial/bluemix.html)を参照してください。
- Cloud Foundry コマンド・ライン・インターフェースをダウンロードしてインストールします。Cloud Foundry コマンド・ライン・インターフェースを使用すると、サービス・インスタンスを変更して {{site.data.keyword.bluemix_notm}} にデプロイすることができます。詳しくは、[cf コマンド・ライン・インターフェースを使用したコーディングの開始](https://www.ng.bluemix.net/docs/#starters/install_cli.html)を参照してください。

## このサンプルのデプロイ

このサンプルの独自コピーを {{site.data.keyword.bluemix_notm}} にデプロイするには、以下のステップを使用してください。

1. {{site.data.keyword.bluemix_notm}} で新規 Python アプリケーションを作成します。
  a. {{site.data.keyword.bluemix_notm}} ダッシュボードで、**「アプリの作成」**をクリックし、**「Web」**をクリックします。
  b.**「Python」**を選択し、**「続行」**をクリックします。
  c. アプリケーション名を選択し、**「完了」**をクリックします。
  これで、Python アプリケーションがステージングされます。
2. {{site.data.keyword.cloudant_short_notm}} NoSQL DB サービスのインスタンスを作成します。
  a. {{site.data.keyword.bluemix_notm}} ダッシュボードで、**「サービスまたは API の使用」**をクリックします。
  b. メニューの**「データおよび分析」**を選択し、**「Cloudant NoSQL DB」**をクリックします。
  c.**「作成」**をクリックします。
3. {{site.data.keyword.cloudant_short_notm}} NoSQL DB のインスタンスと {{site.data.keyword.iot_short}} のインスタンスを Python アプリケーションにバインドします。
  a. **「サービスまたは API のバインド」**をクリックします。
  b. {{site.data.keyword.cloudant_short_notm}} NoSQL DB サービスと {{site.data.keyword.iot_short}} インスタンスを選択し、**「追加」**をクリックします。
4. [{{site.data.keyword.iot_short}} Python Github リポジトリー](https://github.com/ibm-messaging/iot-python.git)を複製します。リポジトリーをコマンド・ライン・インターフェースから複製するには、リポジトリー複製の宛先となるディレクトリーにナビゲートし、以下のコマンドを実行します。
```
$ git clone https://github.com/ibm-messaging/iot-python.git
```
5. コマンド・ライン・インターフェースで、以下のコマンドを使用して、ディレクトリーをモバイル・デバイス・センサーのサンプルに変更します。
```
$ cd iot-python/samples/bluemixZoneDemo
```
6. 以下のコマンドを使用してアプリケーションを {{site.data.keyword.bluemix_notm}} にプッシュし、`app_name` を Python アプリケーションの名前に置き換えます。
```
$ cf push app_name -m 32M -b https://github.com/cloudfoundry/cf-buildpack-python.git -c "python server.py"
```
7. `http://app_name.mybluemix.net/` を電話の Web ブラウザーで開きます。方法について説明するページが表示されるはずです。

MQTT メッセージングを使用して電話から加速度センサー・データを
<keyword conref="cloudoeconrefs.dita#cloudoeconrefs/iot_short"/> に送信する方法について説明するページが表示されます。
<keyword conref="cloudoeconrefs.dita#cloudoeconrefs/bluemix_short"/> アプリはこのデータを使用して、移動内容をミラーリングします。
デバイス ID を入力し、<uicontrol>「接続」</uicontrol>をクリックし、
電話の移動を引き続き試行します。
