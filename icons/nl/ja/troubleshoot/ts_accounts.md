---

copyright:
  years: 2015, 2017
  
lastupdated: "2017-01-10"

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 


# アカウントの管理に関するトラブルシューティング
{: #managingaccounts}

アカウントの管理に関する一般的な問題としては、異なるアプリが同じドメイン名を共有していることや、管理者が一部の組織を表示できないことなどが考えられます。多くの場合、いくつかの簡単なステップを実行することで、これらの問題から復旧することが可能です。
{:shortdesc}


## アカウントが非アクティブである
{: #ts_accnt_inactive}

アカウントが非アクティブの場合は、{{site.data.keyword.Bluemix_notm}} 内でアプリを作成することはできません。この問題を修正するには、サポート・チームに連絡する必要があります。

{{site.data.keyword.Bluemix_notm}} でアプリを作成しようとすると、以下のエラー・メッセージが表示されます。
{: tsSymptoms} 

`BXNUI0096E: アプリは作成されませんでした。アカウントは取り消されたか中断されたため、非アクティブです。`

{{site.data.keyword.Bluemix_notm}} アカウントの状況は、アカウントが取り消されるか、または中断されると非アクティブになります。
{: tsCauses}


アカウントを再アクティブ化する場合は、[{{site.data.keyword.Bluemix_notm}} サポート![「外部リンク」アイコン](../icons/launch-glyph.svg "External link icon")](http://ibm.biz/bluemixsupport.com){: new_window}に連絡してください。E メールに、以下の情報を含めてください。
{: tsResolve}

  * {{site.data.keyword.Bluemix_notm}} へのログインに使用している IBM ID。
  * アプリを作成している組織の名前。この情報は、サポート・チームが、組織内の正しい役割またはメンバーシップがユーザーに割り当てられているかどうかを判別するのに役立ちます。


## 現行組織に関連付けられたスペースがない
{: #ts_no_space}

現行組織に関連付けられたスペースがない場合、アプリケーションを作成することはできません。

{{site.data.keyword.Bluemix_notm}} でアプリを作成しようとすると、以下のエラー・メッセージが表示されます。
{: tsSymptoms} 

`BXNUI0097E: アプリを追加するには、その前に、少なくとも 1 つのスペースが組織と地域に関連付けられていなければなりません。ダッシュボードで、「スペースの作成」をクリックします。スペースが作成されたら、やり直してください。`

{{site.data.keyword.Bluemix_notm}} 内のアプリは、組織のスペース内に作成される必要があります。
{: tsCauses} 

スペースを作成するには、次のいずれかの方法を使用します。
{: tsResolve}
 
  * {{site.data.keyword.Bluemix_notm}} ダッシュボードで、スペースを作成する組織を選択し、次に**「スペースの作成」**をクリックします。
  * cf コマンド・ライン・インターフェースに `cf create-space <space_name>
-o <organization_name>` と入力します。

  
## 複数のアプリが同じドメイン・ネームを共有している
{: #ts_domain_diff}

{{site.data.keyword.Bluemix_notm}} で、複数のアプリが同じ URL を共有していることがあります。

この問題は、同じスペース内の異なるアプリに対して同一の URL 経路を指定した場合に発生する可能性があります。
{: tsCauses}

例えば、myApp1 アプリを {{site.data.keyword.Bluemix_notm}} にプッシュし、そのドメインを「mynewapp.stage1.mybluemix.net」に設定します。次に、別の myApp2 アプリを同じスペースにプッシュし、その URL 経路の 1 つを「mynewapp.stage1.mybluemix.net」に設定します。この経路は、この時点で両方のアプリにマップされています。

これは {{site.data.keyword.Bluemix_notm}} のサポートされている動作で、このプラクティスを用いてアプリのアップグレードにおけるゼロ・ダウン時間を実現することができます。詳しくは、[Using Blue-Green Deployment to Reduce Downtime and Risk ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.cloudfoundry.org/devguide/deploy-apps/blue-green.html){: new_window}を参照してください。
{: tsResolve}
  

## 管理者が {{site.data.keyword.Bluemix_notm}} ユーザー・インターフェースを使用してすべての組織を表示できない
{: #ts_ui_org}

管理者として {{site.data.keyword.Bluemix_notm}} ユーザー・インターフェースを使用したときに、管理のためにすべての組織を表示することはできません。自分が所属する組織のみを表示して管理することができます。

管理者として、{{site.data.keyword.Bluemix_notm}} ユーザー・インターフェースを使用してすべての組織を表示することはできません。
{: tsSymptoms}

これは、{{site.data.keyword.Bluemix_notm}} ユーザー・インターフェースの制限です。
{: tsCauses}

すべての組織を管理するには、cf コマンド・ライン・インターフェースから `cf orgs`、`cf create-org`、`cf delete-org` などのコマンドを使用できます。cf コマンドの全リストを表示するには、`cf help` と入力してください。
{: tsResolve}
	
## クレジット・カードを追加できない
{: #ts_addcc}

トライアル・アカウントを従量課金 (PAYG) アカウントに変換するためにクレジット・カード情報を送信することができません。

「クレジット・カードの追加」の**「送信」**ボタンが使用不可になっています。
{: tsSymptoms}

この問題は、「クレジット・カードの追加」ページに情報が正しく入力されていない場合に発生します。
{: tsCauses}


以下のステップを実行します。
{: tsResolve}

  1. 「クレジット・カードの追加」ページで、連絡先情報、連絡先住所、および請求先住所の各セクションに含まれているすべての必須フィールドに記入します。
  2. **「IBM の使用条件を読み、これに同意します (I have read and agree to IBM's Terms and Conditions)」**を選択して**「送信 (Submit)」**をクリックします。**「お支払い方法の選択 (Select a payment method)」**セクションが表示されます。
  3. クレジット・カード番号、カードの有効期限日付、およびカードに記載されたセキュリティー・コードを入力します。次に**「送信 (Submit)」**をクリックします。
