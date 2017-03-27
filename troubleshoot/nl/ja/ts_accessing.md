---

copyright:
  years: 2015, 2017
  
lastupdated: "2017-03-02"

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 



# {{site.data.keyword.Bluemix_notm}} へのアクセスに関するトラブルシューティング 
{: #accessing}


{{site.data.keyword.Bluemix}} へのアクセスに関する一般的な問題には、{{site.data.keyword.Bluemix_notm}} にログインできない、アカウントが保留状態にあるなどがあります。多くの場合、いくつかの簡単なステップを実行することで、これらの問題から復旧することが可能です。
{:shortdesc}

## {{site.data.keyword.Bluemix_notm}} にログインできない: パスワードの誤り
{: #ts_logintobm}

{{site.data.keyword.Bluemix_notm}} コンソールにログインするには、IBM ID に関連付けられている有効なパスワードが必要です。

[カスタマー・ポータル](https://control.softlayer.com)を介してログインするには、IBM ID または SoftLayer ID に関連付けられている有効なパスワードが必要です。

{{site.data.keyword.Bluemix_notm}} にログインしようとすると、以下のエラー・メッセージが表示されます。
{: tsSymptoms} 

`入力したパスワードは正しくありません。`

{{site.data.keyword.Bluemix_notm}} へのログインに使用した IBM ID およびパスワードが無効です。
{: tsCauses} 
 
以下のいずれかの解決策を使用してください。
{: tsResolve}
 * 正しいパスワードを入力します。自分の IBM ID とパスワードが有効であるかどうかを確認するには、「My IBM 」の「プロファイル」ページに移動して、**「ログイン」**をクリックし、「ログイン」ページで IBM ID とパスワードを入力します。 
 * パスワードを忘れた場合は、**「パスワードを忘れた場合 (Forgot your password)」**をクリックして、パスワードをリセットします。この後、[Bluemix コンソール](https://console.{DomainName})または[カスタマー・ポータル](https://control.softlayer.com)に戻り、再度ログインします。
 * IBM ID を忘れた場合、あるいはパスワードに関する問題が続く場合は、Worldwide IBM Registration Help Desk にご相談ください。 
 * 有効な IBM ID とパスワードを取得するには、「My IBM」の「プロファイル」ページに移動して、**「登録」**をクリックします。
  
**注:** 「Sign in to IBM」ページで、ログイン・プロセスが何らかの理由 (例えば、パスワードのリセット) で中断された場合、[Bluemix コンソール](https://console.{DomainName})または[カスタマー・ポータル](https://control.softlayer.com)に戻り、ログイン・プロセスを最初からやり直してください。
 

## {{site.data.keyword.Bluemix_notm}} にログインできない: 無効なログイン資格情報
{: #ts_login_invalid_credentials}

IBM ID を使用してログインすると、以下のメッセージが表示されます。
{: tsSymptoms}

`無効なログイン資格情報が入力されました。IBM ID をアカウントに関連付けている場合は、ここからログインしてください` 

* IBM ID に切り替えましたが、以前の SoftLayer のユーザー名とパスワードを使用して[カスタマー・ポータル](https://control.softlayer.com)を介してログインしようとしました。
{: tsCauses}

* [カスタマー・ポータル](https://control.softlayer.com)を介してログインしようとしましたが、「ユーザー名」と「パスワード」のフィールドに IBM ID とパスワードを入力しました。 

メッセージ内の**「ここからログイン」**をクリックするか、「IBM ID アカウントでのログイン」セクションに移動して**「IBM ID でログイン」**をクリックします。
{: tsResolve}

以前の Softlayer ID で使用していた**「ユーザー名」**と**「パスワード」**のフィールドは使用しないでください。


## {{site.data.keyword.Bluemix_notm}} にログインできない: 認識されない IBM ID または E メール
{: #ts_softlayer_username}

{{site.data.keyword.Bluemix_notm}} コンソールにログインすると、以下のメッセージが表示されます。
{: tsSymptoms} 

`この IBM ID または E メールを認識できません。(We didn't recognize this IBM ID or email.)`

{{site.data.keyword.Bluemix_notm}} コンソールにログインしようとしましたが、有効な IBM ID を使用しませんでした。例えば、IBM ID に完全修飾 E メール・アドレスを入力しなかったか、SoftLayer のユーザー名とパスワードを使用しようとしました。
{: tsCauses}
 
{{site.data.keyword.Bluemix_notm}} にログインするには、有効な IBM ID とパスワードが必要です。

 * IBM ID には必ず完全修飾 E メール・アドレスを入力してください。{: tsResolve}
 * SoftLayer ID を使用している SoftLayer ユーザーの場合、IBM ID 認証を使用してログインするには、アクセス権限を持つ各アカウント内のカスタマー・ポータルで事前に IBM ID 認証に切り替えておく必要があります。詳しくは、[IBM ID への切り替え](/docs/admin/softlayerlink.html#ibmid_switch)を参照してください。


## {{site.data.keyword.Bluemix_notm}} にログインできない: IBM ID がどの IBM Cloud アカウントにも関連付けられていない
{: #ts_login_noswitch}

IBM ID を使用してログインすると、以下のメッセージが表示されます。
{: tsSymptoms}

`このページは、認証が正常に行われたために表示されています。ただし、この IBM ID は IBM クラウド・アカウントに関連付けられていません。(You have reached this page because your authentication was successful, however, this IBMid is not associated with any IBM Cloud accounts.) これがエラーと思われる場合は、アカウント所有者またはマスター・ユーザーにお問い合わせください。(If you believe this to be in error, contact your Account Owner or Master User.)`

有効な IBM ID を使用して[カスタマー・ポータル](https://control.softlayer.com)からログインしましたが、SoftLayer で IBM ID 認証への切り替えが行われていません。
{: tsCauses} 
 
必要に応じて、以下の確認を行ってください。
{: tsResolve}
 * マスター・ユーザーまたはアカウント管理者に連絡して、IBM ID 認証への切り替えが有効になっているかどうかを確認します。
 * SoftLayer アカウントで「IBM ID への切り替え」ステップが完了していることを確認します。[IBM ID への切り替え](/docs/admin/softlayerlink.html#ibmid_switch)を参照してください。
 * **「SoftLayer ユーザーと IBM ID の関連付け (Associate your SoftLayer user with an IBMid)」** E メールのアクションに従っていることを確認します。E メールの受信ボックスとスパム・フォルダーを確認してください。この E メールを再度取得するには (例えば、有効期限が切れた場合)、コントロール・ポータルの「ユーザー・プロファイルの編集」ページに移動し、**「E メールの再送」**をクリックします。あるいは、[{{site.data.keyword.Bluemix_notm}} サポート![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](http://ibm.biz/bluemixsupport.com){: new_window}に連絡してください。

**注:** IBM ID を使用して直接 IBM ID を作成した場合、処理する必要がある 2 つの E メールを受け取ります。1 つは IBM ID 登録からのもので、もう 1 つは Softlayer からのものです。両方の E メールのアクションに従っていることを確認してください。

アカウントのセットアップに応じて、以下の一部のログイン・オプションが適用されることがあります。 
 * SoftLayer ID を使用する SoftLayer ユーザーは、[カスタマー・ポータル](https://control.softlayer.com)を介してログインする必要があります。
 * IBM ID を使用する SoftLayer ユーザーは、リンクされている Bluemix アカウントの有無を問わず、[カスタマー・ポータル](https://control.softlayer.com)を介してログインして SoftLayer カスタマー・ポータルを開くか、[Bluemix コンソール](https://console.{DomainName})を介して「インフラストラクチャー」ダッシュボードを開くことができます。 


## {{site.data.keyword.Bluemix_notm}} にログインできない: IBM ID がどの {{site.data.keyword.Bluemix_notm}} アカウントにも関連付けられていない
{: #ts_unabletologin}

{{site.data.keyword.Bluemix_notm}} にログインすると、以下のメッセージが表示されます。
{: tsSymptoms} 
 
`このページは、認証が正常に行われたために表示されています。ただし、この IBM ID は {{site.data.keyword.Bluemix_notm}} アカウントに関連付けられていません。(You have reached this page because your authentication was successful, however, this IBMid is not associated with any {{site.data.keyword.Bluemix_notm}} accounts.)`

有効な IBM ID を使用して [Bluemix コンソール](https://console.{DomainName})からログインしましたが、まだ {{site.data.keyword.Bluemix_notm}} アカウントが作成されていません。
{: tsCauses} 

{{site.data.keyword.Bluemix_notm}} アカウントを作成するには、登録プロセスに従います。
{: tsResolve}

アカウントのセットアップに応じて、以下の一部のログイン・オプションが適用されることがあります。 
 * リンクされた SoftLayer アカウントを持たない Bluemix ユーザーは、Bluemix コンソールを介してログインする必要があります。
 * リンクされた SoftLayer アカウントを持つ Bluemix ユーザーは、[Bluemix コンソール](https://console.{DomainName})または[カスタマー・ポータル](https://control.softlayer.com)を介してログインできます。
 

## {{site.data.keyword.Bluemix_notm}} にログインできない: コンソールが開かない
{: #ts_login_stalls}

IBM ID を使用してログインすると、ログインに成功したというメッセージが表示されますが、[Bluemix コンソール](https://console.{DomainName})または[カスタマー・ポータル](https://control.softlayer.com)に戻りません。
{: tsSymptoms}

以下のいずれかの解決策を使用してください。
{: tsResolve}
 * ブラウザーを閉じ、キャッシュと Cookie を消去してから、ログインを再試行します。
 * IBM ID 認証サービスから直接ログインしたのではなく、[Bluemix コンソール](https://console.{DomainName})または[カスタマー・ポータル](https://control.softlayer.com)からログインしていることを確認します。
 
 
## {{site.data.keyword.Bluemix_notm}} にログインできない: IBM ID のログインが完了しない
{: #ts_login_ibmid}

{{site.data.keyword.Bluemix_notm}} にログインしたときに、IBM ID を使用した認証が完了しません。
{: tsSymptoms}

IBM ID 認証サービスに問題がある可能性があります。
{: tsCauses}

[IBM BlueID ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://new.wind.ibmcloud.com/webapp/#/status/a1a0c5d743d94a6a9597087541564d8e){: new_window}でサービスの状況を確認し、再試行してください。
{: tsResolve}


## {{site.data.keyword.Bluemix_notm}} にログインできない: アカウントが保留になっている
{: #ts_accntpding}

アカウントが保留になっている場合は、{{site.data.keyword.Bluemix_notm}} にログインできません。
 
{{site.data.keyword.Bluemix_notm}} トライアル・アカウントに登録した後、{{site.data.keyword.Bluemix_notm}} にログインできない場合があります。次のメッセージが表示されます。
{: tsSymptoms}

<code>アカウントが保留になっています。E メールの確認を最大 24 時間待って、スパム・フォルダーも確認してください。それでも E メールの確認が届かない場合は、<a href="http://ibm.biz/bluemixsupport.com" target="_blank">Bluemix サポート</a>までお問い合わせください。</code>


{{site.data.keyword.Bluemix_notm}} トライアル・アカウントに登録した後、確認の E メールが届きます。その確認 E メールに記載されたリンクをクリックして、登録プロセスを完了する必要があります。
{: tsCauses} 

確認の E メールは、ユーザーが入力した E メール・アドレス宛に送信されます。受信ボックスとスパム・フォルダーを確認してください。確認の E メールが届かない場合は、[{{site.data.keyword.Bluemix_notm}} サポート![「外部リンク」アイコン](../icons/launch-glyph.svg "「外部リンク」アイコン")](http://ibm.biz/bluemixsupport.com){: new_window}にお問い合わせください。  
{: tsResolve}


## 保存されていない変更があります
{: #ts_unsaved_changes}

アプリの詳細ページでナビゲートしている時に、アクションを実行できなくなり、続行する前に変更を保存するよう求めるプロンプトが出される場合があります。 

アプリの詳細ページでアプリまたはサービスを確認しようとすると、次のエラー・メッセージを受信し続けます。
{: tsSymptoms} 

`保存されていない変更がページ app_name にあります。変更を保存するか取り消してください。`

マウスをスクロールして、「ランタイム」ペインの**「インスタンス」**フィールドまたは**「メモリー割り当て量」**フィールドの上に移動すると、それらの値が変わります。この動作は設計によるものですが、エラー・メッセージにより、そのペインの外にナビゲートする前にメモリー設定またはインスタンス設定を保存するよう求めるプロンプトが表示されます。
{: tsCauses}

メッセージ・ウィンドウを閉じ、「ランタイム」ペイン内の**「リセット」**ボタンをクリックします。
{: tsResolve} 
  
    
## {{site.data.keyword.Bluemix_notm}} 領域間の自動フェイルオーバーを使用できない
{: #ts_failover}

{{site.data.keyword.Bluemix_notm}} 領域間の自動フェイルオーバーは使用できません。ただし、回避策として、複数の IP アドレス間のフェイルオーバーをサポートする DNS プロバイダーを使用できます。

ある {{site.data.keyword.Bluemix_notm}} 領域が使用不可になると、その領域で実行されているアプリは、たとえそれと同じアプリが別の {{site.data.keyword.Bluemix_notm}} 領域で実行されていても、使用不可になります。
{: tsSymptoms}
 
{{site.data.keyword.Bluemix_notm}} では、ある領域から別の領域への自動フェイルオーバーはまだ提供されていません。
{: tsCauses}
 
複数の ID アドレス間のインテリジェント・フェイルオーバーをサポートする DNS プロバイダーを使用し、{{site.data.keyword.Bluemix_notm}} 領域間の自動フェイルオーバーを使用可能にするように、DNS 設定を手動で構成することができます。この機能を備えた DNS プロバイダーとしては、NSONE、Akamai、Dyn があります。
{: tsResolve}

DNS 設定を構成する場合、アプリが実行されている {{site.data.keyword.Bluemix_notm}} 領域のパブリック IP アドレスを指定する必要があります。{{site.data.keyword.Bluemix_notm}} 領域のパブリック IP アドレスを取得するには、`nslookup` コマンドを使用します。例えば、次のコマンドをコマンド・ライン・ウィンドウに入力できます。
```
nslookup stage1.mybluemix.net
```

## ユーザーを組織に追加できない
{: #ts_adduser}

同じ組織の下で作業するユーザーを複数招待することができます。ユーザーを自分の組織に招待できるのは、自分がアカウント所有者の場合か、またはその組織の管理者とメンバーを兼ねている場合のみです。
 
**「組織の管理」**セクションに**「新規ユーザーの招待」**リンクが表示されません。
{: tsSymptoms}

以下の {{site.data.keyword.Bluemix_notm}} ユーザーのみが、組織にユーザーを招待できます。
{: tsCauses}
  * 組織のアカウント所有者
  * 組織のコラボレーターではなく、組織のメンバーでもある組織管理者
  
{{site.data.keyword.Bluemix_notm}} で、ユーザーは組織のメンバーまたはコラボレーターになることができます。

<dl><dt>コラボレーター</dt>
<dd>既に {{site.data.keyword.Bluemix_notm}}アカウントを持っており、別のユーザーから組織に招待された場合は、組織のコラボレーターです。</dd>
<dt>メンバー</dt>
<dd>{{site.data.keyword.Bluemix_notm}} アカウントを持っていないが、別のユーザーから組織に招待され、その招待から  {{site.data.keyword.Bluemix_notm}} への申し込みを行った場合は、組織のメンバーです。</dd>
</dl>

組織のコラボレーターである場合は、組織管理者に任命されていても、組織にユーザーを招待することはできません。

**注:** すべての組織管理者 (組織のコラボレーターである管理者を含む) は、ユーザーを追加したり、既に組織内にいるユーザーを変更および削除したりすることができます。

組織にユーザーを招待することができず、招待するために別の役割を必要とする場合は、組織管理者に連絡して、役割の変更を依頼してください。組織の管理者を特定するには、以下のステップを実行します。
{: tsResolve}

  1. {{site.data.keyword.Bluemix_notm}} ダッシュボードにアクセスします。メニュー・バーで**「アカウント」**メニュー項目をクリックし、**「組織の管理」**をクリックします。
  2. 所属する組織にアクセスすると、組織の管理者の情報が**「ユーザー」**タブに表示されます。  
  
自分がコラボレーターでありメンバーではないためにユーザーを招待できない場合、古い {{site.data.keyword.Bluemix_notm}} アカウントを削除してから、招待を受けて組織のメンバーとしてアカウントに参加する必要があります。古いアカウントを削除してメンバーとしてアカウントに参加するには、以下のステップを実行してください。 

  1. [{{site.data.keyword.Bluemix_notm}} サポート![「外部リンク」アイコン](../icons/launch-glyph.svg "「外部リンク」アイコン")](http://ibm.biz/bluemixsupport){: new_window}に連絡してサポート・チケットをオープンし、アカウントの削除を依頼します。古いアカウントに関連付けられているデータで、保存して新規アカウントに移行したいものがあれば、その情報を E メールに記載してください。 
  2. 自分のアカウントが削除された後、組織の管理者の役割を持つユーザーに、自分を組織の管理者として組織に招待してもらいます。その後、招待から {{site.data.keyword.Bluemix_notm}} に登録します。 

## ユーザーのバッチ登録がサポートされない
{: #ts_batchregistration}

{{site.data.keyword.Bluemix_notm}} 用にユーザーを登録する時は、各ユーザーを個別に登録しなければなりません。

{{site.data.keyword.Bluemix_notm}} には、複数のユーザーを同時に登録する機能は用意されていません。
{: tsSymptoms}
 
{{site.data.keyword.Bluemix_notm}} では、ユーザーのバッチ登録はサポートしていません。{{site.data.keyword.Bluemix_notm}} 用にユーザーを登録するには、各ユーザーを個別に登録しなければなりません。
{: tsCauses}
 
{{site.data.keyword.Bluemix_notm}} 用に複数のユーザーを登録するには、ユーザーごとに以下の手順を実行します。
{: tsResolve}

  1. {{site.data.keyword.Bluemix_notm}} コンソールにある**「登録 (SIGN UP)」**をクリックします。
  2. ウィザードに従って手順を実行します。
    

## {{site.data.keyword.Bluemix_notm}} ページをロードできない
{: #ts_err}

{{site.data.keyword.Bluemix_notm}} コンソールを使用する際、{{site.data.keyword.Bluemix_notm}} ページをロードできない場合があります。代わりに、エラー・メッセージ BXNUI0001E または BXNUI0016E が表示されることがあります。
 
{{site.data.keyword.Bluemix_notm}} コンソールを使用する際、次のいずれかのエラー・メッセージが表示される可能性があります。
{: tsSymptoms}

`BXNUI0001E: セッションが存在しているかどうかを Bluemix が検出しなかったため、ページはロードされませんでした。`

`BXNUI0016E: Bluemix ページがロードされなかったため、アプリおよびサービスは取得されませんでした。`

必要に応じて、以下の 1 つ以上のアクションを実行してください。
{: tsResolve}

  * ブラウザーを最新表示または再始動します。
  * {{site.data.keyword.Bluemix_notm}} をいったんログアウトしてから、再度ログインします。
  * ブラウザーのプライベート表示モードを使用します。 
  * ブラウザーの Cookie およびキャッシュをクリアします。
  * 異なるブラウザーを使用します。{{site.data.keyword.Bluemix_notm}} によりサポートされているブラウザーのバージョンについて詳しくは、[Bluemix の前提条件](/docs/overview/whatisbluemix.html#prereqs)を参照してください。
  * cf コマンド・ライン・インターフェースがインストール済みであれば、`cf apps` コマンドを入力してアプリが実行中であるかどうか確認します。
