---



copyright:

  years: 2016, 2017
lastupdated: "2017-03-17"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# IBM ID への切り替え
SoftLayer での認証は、IBM ID を使用して {{site.data.keyword.Bluemix_notm}} のすべてに対して単一のログインを提供するようになりました。既存の SoftLayer アカウントは IBM ID 認証への切り替えが有効になっています。マイグレーション・ウィザードを使用して、この切り替えの処理を行います。
{:shortdesc}

IBM ID への切り替えを開始しても、処理が完了する前であればいつでも切り替えを取り消すことができます。ただし、ログインするたびに、IBM ID への切り替えを促すプロンプトが表示されます。{{site.data.keyword.Bluemix_notm}} アカウントにリンクする予定の各 SoftLayer アカウントは、固有の E メール・アドレスを持つ固有の IBM ID によって所有される必要があります。

既存の SoftLayer アカウントを IBM ID に切り替えるには、以下の手順を実行します。
1. SoftLayer アカウントにログインし、IBM ID への切り替えを促すプロンプトが表示されたら、**「OK」**をクリックします。

   マスター・ユーザーであるのに {{site.data.keyword.slportal}} に IBM ID への切り替えを促すプロンプトが表示されない場合、[IBM サポートに連絡](/docs/support/index.html#contacting-support)して、支援を依頼してください。
  
   既にログインしており、プロンプトに対して**「後で」**をクリックしたものの、IBM ID 認証への切り替えを現行セッションで行うことにした場合は、「ユーザー・プロファイルの編集」ページに移動し、**「IBM ID への切り替え」**をクリックします。

2. ウィザードのプロンプトに従って IBM ID を作成します。 

   どの IBM ID でも現在使用されていない E メール・アドレスを入力します。この E メール・アドレスは、新規 IBM ID のユーザー名として使用され、IBM ID の作成後に登録コードが送信される宛先となります。IBM ID に関連付けられている E メール・アドレスは後で更新できますが、ユーザー名は変更できません。

3. 登録コードを受信したら、E メールのリンクをクリックするか、URL をブラウザーにコピーして、登録コードを入力します。

   コードは 7 日間有効で、1 回のみ使用できます。
  
4. 登録コードを送信した後、IBM ID を使用して {{site.data.keyword.slportal}} にログインします。

   「アカウントのログイン」プロンプトで、**「IBM ID アカウントでのログイン」**セクションに移動し、**「IBM ID でログイン」**をクリックします。以前に SoftLayer ID で使用していた**「ユーザー名」**と**「パスワード」**のフィールドは使用しないでください。

新規のお客様の場合、注文を清算すると、既存の IBM ID を入力するか、新規 IBM ID を作成するように求められます。 
  * 既存の IBM ID を使用するには、ユーザー名を入力するか、または IBM ID の E メール・アドレスが固有の場合 (つまり、複数の IBM ID 間で共有されていない場合) は E メール・アドレスを入力します。
  
  * 新規 IBM ID を作成するには、どの IBM ID でも現在使われていない E メール・アドレスを入力します。この E メール・アドレスは、IBM ID のユーザー名であり、IBM ID の作成後に登録コードが送信される宛先となります。IBM ID に関連付けられている E メール・アドレスは後で更新できますが、ユーザー名を変更することはできません。 
  
IBM ID でのログインに関する問題を解決するには、『[Bluemix へのアクセスに関するトラブルシューティング](/docs/troubleshoot/ts_accessing.html#accessing)』を参照してください。

## IBM ID の認証用のユーザー・アカウントの有効化
{: #link_accounts_resellers}

場合によっては、アカウントでの IBM ID 認証の使用を販売店または流通業者が前もって有効にしておかないと、ユーザーが IBM ID に切り替えることができないことがあります。 

  * IBM ID 認証は、Bluemix アカウントにリンクする既存のユーザー・アカウントごとに有効にする必要があります。その後、各ユーザーは、前のセクションで説明されているように、マイグレーション・ウィザードを使用して IBM ID に切り替えるプロセスを完了する必要があります。既存の SoftLayer アカウントが IBM ID 認証を使用できるようにするには、[IBM サポート](/docs/support/index.html#contacting-support)に連絡してください。 
  
  * 新規ユーザー・アカウントが確実に IBM ID を使用して作成されるようにするには、即時マスター・ユーザー・アカウントに `CREATE_NEW_ACCOUNT_WITH_IBMid_AUTHENTICATION` 属性が設定される必要があります。[IBM サポート](/docs/support/index.html#contacting-support)またはベンダーに連絡して、アカウントに属性を設定するように依頼してください。  

## IBM ID ユーザー・アカウントのリンク
{: #link_user_accounts}

ユーザー・アカウントを IBM ID 認証に切り替えた後、販売店および流通業者は SoftLayer アカウントと {{site.data.keyword.Bluemix_notm}} アカウントをリンクして、結合されたインフラストラクチャーおよびプラットフォームのリソースを利用できます。

**注**:
  * リンクされるアカウントのマスター・ユーザーは、IBM ID を持っていなければなりません。
  * {{site.data.keyword.Bluemix_notm}} アカウントにリンクする各ユーザー・アカウントは、固有の E メール・アドレスを持つ固有の IBM ID によって所有される必要があります。単一の IBM ID が複数の SoftLayer アカウントを所有することは可能ですが、マスター・ユーザーを、アカウントごとに固有の IBM ID となるように変更する必要があります。SoftLayer アカウントのマスター・ユーザーを変更するには、[IBM SoftLayer サポート![「外部リンク」アイコン](../icons/launch-glyph.svg)](https://knowledgelayer.softlayer.com/topic/support){: new_window}に連絡してください。
  * リンクされたアカウントに新規ユーザーを追加する場合、ユーザーを SoftLayer アカウントと {{site.data.keyword.Bluemix_notm}} アカウントの両方に追加して、統合されたコンソールのすべての機能にアクセスできるようにする必要があります。 
  
各アカウントを {{site.data.keyword.Bluemix_notm}} アカウントにリンクするには、以下のステップを実行します。
1. 既存の {{site.data.keyword.Bluemix_notm}} アカウントにリンクするか、新規に作成するには、マスター・ユーザーとして SoftLayer アカウントにログインし、{{site.data.keyword.Bluemix_notm}} リンクをクリックします。

   SoftLayer アカウントのマスター・ユーザーである IBM ID は、リンクする先の {{site.data.keyword.Bluemix_notm}} アカウントの所有者でなければなりません。 
   
2. SoftLayer アカウントのユーザーを {{site.data.keyword.Bluemix_notm}} アカウントに追加する操作も含めて、ウィザードのプロンプトに従います。
3. アカウントをリンクした後、各アカウントのエンド・ユーザーに通知して、前のセクションに説明されている手順に従って IBM ID にマイグレーションするように指示します。

**推奨**: エンド・ユーザー・アカウントのみを IBM ID にマイグレーションしてください。ブランド・アカウント (エンド・ユーザー・アカウントの親アカウントであり、リソースを含んでいない) はマイグレーションしないでください。ブランド・アカウント・ユーザーは、IBM ID にマイグレーションすると、Brand Agent Portal (BAP) にログインできなくなります。  
  
