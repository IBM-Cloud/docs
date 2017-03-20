---

copyright:
  years: 2015, 2017
  
lastupdated: "2017-01-11"

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 



# {{site.data.keyword.Bluemix_notm}} へのアクセスに関するトラブルシューティング 
{: #accessing}


{{site.data.keyword.Bluemix}} へのアクセスに関する一般的な問題には、{{site.data.keyword.Bluemix_notm}} へのログインができないユーザー、保留状態で使用できないアカウントなどが含まれます。しかし多くの場合、いくつかの簡単なステップを実行することで、これらの問題から復旧することが可能です。
{:shortdesc}

## {{site.data.keyword.Bluemix_notm}} にログインできない
{: #ts_unabletologin}

ログインするには、有効な {{site.data.keyword.Bluemix_notm}} アカウントが必要です。


{{site.data.keyword.Bluemix_notm}} にログインしようとすると、以下のいずれかのエラー・メッセージが表示されます。
{: tsSymptoms} 

 * カスタマー・ポータルから
  
   `このページは、認証が正常に行われたために表示されています。ただし、この IBM ID は IBM クラウド・アカウントに関連付けられていません。(You have reached this page because your authentication was successful, however, this IBMid is not associated with any IBM Cloud accounts.) これがエラーと思われる場合は、アカウント所有者またはマスター・ユーザーにお問い合わせください。(If you believe this to be in error, contact your Account Owner or Master User.)`

 * {{site.data.keyword.Bluemix_notm}} コンソールから
  
  `このページは、認証が正常に行われたために表示されています。ただし、この IBM ID は {{site.data.keyword.Bluemix_notm}} アカウントに関連付けられていません。(You have reached this page because your authentication was successful, however, this IBMid is not associated with any {{site.data.keyword.Bluemix_notm}} accounts.)`


このエラー・メッセージを受け取る最も可能性が高い理由の 1 つは、{{site.data.keyword.Bluemix_notm}} アカウントがまだ作成されていないこと、または IBM ID 認証に切り替える必要があることです。
{: tsCauses} 
 

登録プロセスに従って {{site.data.keyword.Bluemix_notm}} アカウントを作成するか、マスター・ユーザーまたはアカウント管理者に連絡して、IBM ID への切り替えを依頼してください。
{: tsResolve}

アカウントのセットアップに応じて、以下の一部のログイン・オプションが適用されることがあります。 
 * SoftLayer ID を持つ SoftLayer ユーザーは、[カスタマー・ポータル ![「外部リンク」アイコン](../icons/launch-glyph.svg)](https://control.softlayer.com){: new_window} を介してログインする必要があります。
 * IBM ID を持つ SoftLayer ユーザーは、リンクされている Bluemix アカウントの有無を問わず、[カスタマー・ポータル ![「外部リンク」アイコン](../icons/launch-glyph.svg)](https://control.softlayer.com){: new_window} を介してログインして SoftLayer カスタマー・ポータルを開くか、[Bluemix コンソール ![「外部リンク」アイコン](../icons/launch-glyph.svg)](https://console.{DomainName}){: new_window} を介して「インフラストラクチャー」ダッシュボードを開くことができます。 
 * リンクされた SoftLayer アカウントを持たない Bluemix ユーザーは、Bluemix コンソールを介してログインする必要があります。
 * リンクされた SoftLayer アカウントを持つ Bluemix ユーザーは、[Bluemix コンソール ![「外部リンク」アイコン](../icons/launch-glyph.svg)](https://console.{DomainName}){: new_window} または[カスタマー・ポータル ![「外部リンク」アイコン](../icons/launch-glyph.svg)](https://control.softlayer.com){: new_window} を介してログインできます。
 

## パスワードが無効
{: #ts_logintobm}

{{site.data.keyword.Bluemix_notm}} コンソールにログインするには、有効な IBM ID が必要です。

{{site.data.keyword.Bluemix_notm}} にログインしようとすると、以下のエラー・メッセージが表示されます。
{: tsSymptoms} 

`入力したパスワードは正しくありません。`

{{site.data.keyword.Bluemix_notm}} へのログインに使用した IBM ID およびパスワードが無効です。
{: tsCauses} 
 
有効な IBM ID とパスワードを取得するには、「マイ IBM プロファイル (My IBM profile)」ページに移動し、以下のいずれかのステップを実行します。
{: tsResolve}
  * IBM ID について登録済みであり、自分の ID とパスワードが有効であるかどうかを確認したい場合は、**「ログイン」**をクリックし、「ログイン」ページで IBM ID とパスワードを入力します。パスワードを忘れた場合は、「ログイン」ページにある**「パスワードを忘れた場合 (Forgot your password)」**をクリックして、パスワードをリセットします。IBM ID を忘れた場合、あるいはパスワードに関する問題が続く場合は、Worldwide IBM Registration Help Desk にご相談ください。 
  * IBM ID をお持ちでない場合は、**「登録」**をクリックして IBM ID とパスワードを登録してください。 



## Softlayer ユーザー名を使用してログインできない
{: #ts_softlayer_username}

{{site.data.keyword.Bluemix_notm}} にログインするには、有効な IBM ID とパスワードが必要です。


Softlayer ユーザー名を使用して {{site.data.keyword.Bluemix_notm}} コンソールにログインしようとすると、以下のメッセージを受け取ります。
{: tsSymptoms} 

`この IBM ID または E メールを認識できません。(We didn't recognize this IBM ID or email.)`

ログインして Bluemix コンソールの「インフラストラクチャー」ダッシュボードを使用するには、IBM ID が必要です。
{: tsCauses} 
 
SoftLayer ID を使用している SoftLayer ユーザーは、IBM ID 認証を使用してログインするには、アクセスできる各アカウント内のカスタマー・ポータルで IBM ID 認証に切り替える必要があります。 

マスター・ユーザーまたはアカウント管理者に連絡して、IBM ID への切り替えを依頼してください。
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



## アカウントが保留になっている
{: #ts_accntpding}

アカウントが保留になっている場合は、{{site.data.keyword.Bluemix_notm}} にログインできません。

 
{{site.data.keyword.Bluemix_notm}} トライアル・アカウントに登録した後、{{site.data.keyword.Bluemix_notm}} にログインできない場合があります。代わりに次のメッセージが表示されます。
{: tsSymptoms}

<code>アカウントが保留になっています。E メールの確認を最大 24 時間待って、スパム・フォルダーも確認してください。それでも確認の E メールが届かない場合は、<a href="http://ibm.biz/bluemixsupport.com" target="_blank">Bluemix サポート <img src="../icons/launch-glyph.svg" alt="「外部リンク」アイコン"></a> までお問い合わせください。</code>


{{site.data.keyword.Bluemix_notm}} トライアル・アカウントに登録した後、確認の E メールが届きます。その確認 E メールに記載されたリンクをクリックして、登録プロセスを完了する必要があります。
{: tsCauses} 

確認の E メールは、ユーザーが入力した E メール・アドレス宛に送信されます。受信ボックスとジャンク・メール・フォルダーを確認してください。確認の E メールが届かない場合は、[{{site.data.keyword.Bluemix_notm}} サポート ![「外部リンク」アイコン](../icons/launch-glyph.svg)](http://ibm.biz/bluemixsupport.com){: new_window} にお問い合わせください。  
{: tsResolve}



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

  1. {{site.data.keyword.Bluemix_notm}} ダッシュボードにアクセスします。メニュー・バーで**「サポート」**メニュー項目をクリックし、**「組織の管理」**をクリックします。
  2. 所属する組織にアクセスすると、組織の管理者の情報が**「ユーザー」**タブに表示されます。  
  
自分がコラボレーターでありメンバーではないためにユーザーを招待できない場合、古い {{site.data.keyword.Bluemix_notm}} アカウントを削除してから、招待を受けて組織のメンバーとしてアカウントに参加する必要があります。古いアカウントを削除してメンバーとしてアカウントに参加するには、以下のステップを実行してください。 

  1. [{{site.data.keyword.Bluemix_notm}} サポート ![「外部リンク」アイコン](../icons/launch-glyph.svg)](http://ibm.biz/bluemixsupport){: new_window} に連絡して、サポート・チケットをオープンし、アカウントの削除を要請します。古いアカウントに関連付けられているデータで、保存して新規アカウントに移行したいものがあれば、その情報を E メールに記載してください。 
  2. 自分のアカウントが削除された後、組織の管理者の役割を持つユーザーに、自分を組織の管理者として組織に招待してもらいます。その後、招待から {{site.data.keyword.Bluemix_notm}} に登録します。 




## ユーザーのバッチ登録がサポートされない
{: #ts_batchregistration}

{{site.data.keyword.Bluemix_notm}} 用にユーザーを登録する時は、各ユーザーを個別に登録しなければなりません。
 

{{site.data.keyword.Bluemix_notm}} には、複数のユーザーを同時に登録する機能は用意されていません。
{: tsSymptoms}
 

{{site.data.keyword.Bluemix_notm}} では、ユーザーのバッチ登録はサポートしていません。{{site.data.keyword.Bluemix_notm}} 用にユーザーを登録するには、各ユーザーを個別に登録しなければなりません。
{: tsCauses}
 

 {{site.data.keyword.Bluemix_notm}} 用に複数のユーザーを登録するには、ユーザーごとに以下の手順を実行しなければなりません。
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

 
必要に応じて次のアクションを 1 つ以上実行することができます。
{: tsResolve}

  * ブラウザーを最新表示または再始動します。
  * {{site.data.keyword.Bluemix_notm}} をいったんログアウトしてから、再度ログインします。
  * ブラウザーのプライベート表示モードを使用します。 
  * ブラウザーの Cookie およびキャッシュをクリアします。
  * 異なるブラウザーを使用します。{{site.data.keyword.Bluemix_notm}} でサポートされているブラウザーのバージョンについて詳しくは、[{{site.data.keyword.Bluemix_notm}} の前提条件 ![「外部リンク」アイコン](../icons/launch-glyph.svg)](https://developer.ibm.com/bluemix/support/#prereqs){: new_window} を参照してください。
  * cf コマンド・ライン・インターフェースがインストール済みであれば、`cf apps` コマンドを入力してアプリケーションが実行中であるかどうか確認します。
  
  
  
  
  

