---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Trajectory Pattern Analysis の管理
{: #tp_iotdriverinsights_admin}

最終更新: 2016 年 7 月 22 日
{: .last-updated}

Trajectory Pattern Analysis サービスを管理するには、{{site.data.keyword.Bluemix_notm}} ダッシュボードの管理コンソールを使用します。
管理コンソールから、Trajectory Pattern Analysis のさまざまなパラメーターを構成し、サービス中に格納されているデータを管理することができます。
また、テナント情報を表示したり、テナントのパスワードをリセットしたりすることもできます。


{:shortdesc}

## 管理コンソールの開始
{: #start-admin-console}

{{site.data.keyword.iotdriverinsights_full}} の Trajectory Pattern Analysis サービスの管理コンソールにアクセスするには、次のようにします。


1. {{site.data.keyword.Bluemix_notm}} ダッシュボードで、{{site.data.keyword.iotdriverinsights_short}} サービス・タイルをクリックします。

2. サービス・インスタンスの**「管理」**ビューを選択します。
ユーザー名とパスワードの資格情報をメモします。
後でそれらが必要になります。
管理コンソールにアクセスするには、IBM ID が必要です。
それは、{{site.data.keyword.Bluemix_notm}} の資格情報と同じとは限りません。

3. **「起動」**をクリックし、プロンプトに対して IBM ID 資格情報を入力します。

4. **「ログイン」**をクリックします。
**管理コンソール**のウィンドウが表示されます。



## テナント情報の管理
{: #viewtenantinfo}

テナント情報を表示するには、**「テナント情報 (Tenant Information)」**をクリックします。


### テナント・パスワードのリセット
{: #resettenantpassword}

テナントのパスワードを再設定するには、


1. **「テナント情報 (Tenant Information)」**ウィンドウから**「リセット」**をクリックします。

2. 確認ダイアログ・ボックスで**「OK」**をクリックします。
新規パスワードが生成され、**「テナント情報 (Tenant Information)」**ビューに表示されます。
**重要:** {{site.data.keyword.iotdriverinsights_short}} API にアクセスするアプリケーションのすべてで、パスワードを更新するようにしてください。


## サービス・パラメーターの構成
{: #configureparameters}

サービス・パラメーターは、トリップ・データの分析方法を制御します。
Trajectory Pattern Analysis サービス・パラメーターに変更を加えるには、次のようにします。


1. **「パラメーター」**ビューを開きます。

2. **「経路パターンのパラメーター (Parameters of Trajectory Pattern)」**タブをクリックし、実際の要件に合わせて[経路パターン分析パラメーター](#tp_parameters)を更新します。

3. **「保存」**をクリックします。

4. **「OK」**をクリックします。


サブミットされる次のジョブには、更新後のパラメーター値が適用されます。


### サポートのしきい値パラメーター

**「経路パターンのパラメーター (Parameters of Trajectory Pattern)」**タブで構成可能なサポートしきい値パラメーターについて、次の表で説明します。


|パラメーター名|説明|デフォルト値|
|:--------|:--------|:-------|
|1 つの O/D の最小トリップ・サポート回数|1 つの O/D (起点/終点) パターンに必要な最小限のトリップ・サポートの絶対回数|4 (常に正)|
|1 つのルートの最小トリップ・サポート回数|1 つのルート・パターンに必要な最小限のトリップ・サポートの絶対回数|2 (常に正)|

## 結果データの管理
{: #managedata}

Trajectory Pattern Analysis サービスの分析によって生成される結果データはシステムに格納され、削除するまでそこに保管されます。


結果データを削除するには、次のようにします。


1. **「データ管理」**>**「経路パターンの結果 (Result of Trajectory Pattern)」**をクリックします。
結果データが表示されます。

2. レコードを選択し、**「削除」**をクリックします。

