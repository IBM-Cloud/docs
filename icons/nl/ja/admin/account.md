---



copyright:

  years: 2015, 2017
lastupdated: "2017-01-09"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# {{site.data.keyword.Bluemix_notm}} アカウントの管理
{: #mngacct}

**「アカウント」**リンクに移動して、アカウントの通知の設定、アカウントの使用量の表示、または請求の表示を行います。
{:shortdesc}

## {{site.data.keyword.Bluemix_notm}} への登録
{: #signup}

{{site.data.keyword.Bluemix_notm}} アカウントの登録には、既存の IBM ID を使用するか、新規 IBM ID を作成するか、フェデレーテッド ID を使用することができます。フェデレーテッド ID は、IBM に登録済みの会社ドメイン内の ID で、これにより、ドメインとユーザーの資格情報を使用して IBM Web アプリケーションにアクセスできます。  

お客様の会社が IBM への登録作業を完了している場合にのみ、フェデレーテッド ID で {{site.data.keyword.Bluemix_notm}} にアカウント登録できます。会社のドメインを IBM に登録すると、会社の既存のユーザー資格情報で IBM の製品やサービスにログインできるようになります。認証は、お客様の会社の ID プロバイダーによって処理されます。フェデレーテッド ID で {{site.data.keyword.Bluemix_notm}} にログインすると、お客様の会社のログイン・ページを通じたログインを求められます。会社または組織のドメインを IBM に登録するための申請、またはこのプロセスの詳細については、[IBMid Enterprise Federation Adoption Guide ![「外部リンク」アイコン](../icons/launch-glyph.svg)](https://ibm.box.com/v/IBMid-Federation-Guide){: new_window} を参照してください。フェデレーテッド ID の登録を申請する際には、IBM のサポート役 (オファリング担当者やお客様担当者など) が必要です。

| 登録方法 | 詳細 |    
|-----------------|---------|
|既存の IBM ID | IBM ID を既にお持ちの場合は、IBM の他の製品やサービスに使用する既存の資格情報で {{site.data.keyword.Bluemix_notm}} に登録します。登録の際には、電話番号の入力が必要です。 |
|新しい IBM ID | IBM ID をまだお持ちではない場合は、その作成を選択できます。IBM ID により、1 つのログイン・ユーザー名を、お客様が使用する IBM のすべての製品やサービス ({{site.data.keyword.Bluemix_notm}} を含む) に使用することが可能になります。氏名や電話番号などの個人情報と、新しい資格情報のパスワードの入力が必要です。IBM の他の製品やサービスを使用する際に、この IBM ID でログインできます。  |
|フェデレーテッド ID | お客様の会社が、そのドメインのユーザー資格情報を IBM に登録するための申請を完了している場合は、会社のログインに既に使用している資格情報で {{site.data.keyword.Bluemix_notm}} へのアカウント登録を行えます。登録の際には、電話番号の入力が必要です。 |
{:caption="Table 1. Sign up methods" caption-side="top"}

## 通知の設定
{: #notifications}

**「アカウント」**&gt;**「通知」**をクリックして、一般アカウントおよび消費量通知をセットアップします。消費量通知は、サブスクリプションおよび従量課金 (PAYG) {{site.data.keyword.Bluemix_notm}} アカウントの所有者のみ利用可能です。

プラットフォームの {{site.data.keyword.Bluemix_notm}} インシデントおよび計画保守に関する E メール通知の設定、およびアカウントがユーザー指定の消費量しきい値に近づいたときに警告を出す消費量通知の設定を行うことができます。以下のタスクを実行して、ご使用のアカウントに各種タイプの通知を設定します。

### プラットフォームの通知の設定

**「アカウント」**&gt;**「通知」**&gt;**「プラットフォーム」**をクリックして、{{site.data.keyword.Bluemix_notm}} のインシデントおよび計画保守に関する E メール通知を設定します。各オプションを選択またはクリアすることにより、E メール通知を有効または無効にできます。

<!-- staging only

**Note**: You are always alerted by email about emergencies and pricing changes.

On the **Platform** tab you can also customize notifications for your orgs, spaces, or applications. Complete the following steps to add a customized notification:

<ol>
<li>Select **Add a Notification**.</li>
<li>Use the search field to find the org, application, service, or resource that you want to set a notification for, or expand the item in the pre-populated list.</li>
<li>Select *Email* to set the notification type.</li>
</ol>

staging only end -->

### 消費量通知の設定
{: #spendingnotifications}

サブスクリプションまたは従量課金 (PAYG) {{site.data.keyword.Bluemix_notm}} アカウント所有者の場合、E メールによる消費量の通知をセットアップできます。合計アカウント消費量、合計ランタイム消費量、合計コンテナー消費量、および合計サービス消費量と個別サービスの消費量 (サード・パーティーのサービスを除く) について、通知を設定します。指定した使用しきい値の 80%、90%、および 100% に達すると、通知を受け取ります。いつでもニーズの変更に応じて、それぞれの消費量の通知を編集できます。

以下のステップを実行して、消費量制限の E メール通知をセットアップします。

<ol>
<li>**「アカウント」**&gt;**「通知」**&gt;**「消費量」**をクリックします。</li>
<li>以下に示す通知のタイプごとに通知をトリガーするための消費量のしきい値を設定する数値を入力します。<br />
<ul>
<li>合計アカウント</li>
<li>合計ランタイム</li>
<li>合計サービス</li>
<li>合計コンテナー</li>
<li>特定サービスの消費量</li>
</ul>
</li>
<li>終了したら、**「保存」**をクリックします。</li>
</ol>

**注**: トライアル・アカウントの場合、サブスクリプション・アカウントまたは従量課金 (PAYG) アカウントにアップグレードして、消費量の制限を設定できます。従量課金 (PAYG) アカウントおよびサブスクリプション・アカウントについて詳しくは、『[支払い形態](/docs/pricing/index.html#pay-accounts)』を参照してください。

## 使用量の表示
{: #acctusage}

アカウント所有者または組織の請求管理者は、「使用状況ダッシュボード」ページを使用して、組織で月ごとに使用されているランタイム、コンテナー、サービス、およびサポートのリアルタイムの課金額を表示することができます。すべての地域のランタイム GB 時間とサービス使用量を表示できます。あるいは、特定の地域を表示するように選択することもできます。

「使用状況ダッシュボード」ページを開くには、**「アカウント」**&gt;「*your_account_name*」&gt;**「使用状況ダッシュボード」**をクリックします。請求管理者は、自分が担当する組織のみの詳細を表示することができます。

アカウント所有者は、各請求サイクルの最後の時点ですべての組織に渡り発生した総使用量に対して課金されます。
アカウント所有者は、地域および組織で使用量サマリーをフィルタリングできます。また、特定の月をクリックして、その月の使用量を表示することもできます。アカウントのすべての組織の使用量を表示するには、**「組織」**リストから**「すべての組織」**を選択します。

## 請求先情報の更新
{: #account_billing}

アカウント所有者は、{{site.data.keyword.Bluemix_notm}} アカウントに関連付けられている、保存されているクレジット・カード情報を編集、追加、または削除できます。**「アカウント」**&gt;「*your_account_name*」&gt;**「請求処理」**をクリックします。

{{site.data.keyword.Bluemix_notm}} アカウントにリンクされている SoftLayer アカウントがある場合は、請求方法の詳細について、『[アカウントがリンクされている場合の {{site.data.keyword.Bluemix_notm}} 使用量に対する請求処理](/docs/admin/softlayerlink.html#bill_usage)』を参照してください。
