---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-17"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# ユーザーのアクセス権限の管理
{: #managing-user-access}

「メンバー」ダッシュボードから、{{site.data.keyword.iot_full}} 組織に対するアクセス権限を制御、管理できます。ユーザーを追加する方法には、追加、招待<!--, registering-->、インポートがあります。また、役割の割り当てによって、さまざまなレベルのアクセス権限をユーザーに付与できます。
{:shortdesc}

## ユーザーの追加
{: #adding-new-users}

ダッシュボードの**「メンバー」**タブで、<!--Add, Invite, or Register-->「追加」または「招待」機能を使用してメンバーを個々に追加できます。また、「インポート」機能を使用して、同時に複数のメンバーを<!--add, invite, or register-->追加したり招待したりすることも可能です。

デフォルトでは、メンバー・アカウントに有効期限はありません。ユーザーを {{site.data.keyword.iot_short_notm}} 組織に追加するときに、オプションでユーザー・アカウントの有効期限日付を設定できます。

### {{site.data.keyword.iot_short_notm}} 組織へのメンバーの追加

組織にメンバーを追加するには、メンバーの IBMid が必要です。メンバーを追加するときに、そのメンバーからの確認は不要です。

1 人のメンバーを {{site.data.keyword.iot_short_notm}} 組織に追加するには、次の手順を実行します。
1. {{site.data.keyword.iot_short_notm}} ダッシュボードで**「メンバー」**に移動します。
2. **「メンバーの追加」**をクリックし、**「追加」**タブを選択します。
3. メンバーの IBMid を入力します。
4. メンバーの役割を選択します。
5. オプション: メンバーの有効期限日付を設定します。
6. **「追加」**をクリックします。

複数のメンバーを同時に追加するには、各メンバーの IBMid、役割、(オプションの) 有効期限日付が含まれた `.csv` ファイルをアップロードする必要があります。詳しくは、[CSV ファイルの作成](#constructing-your-csv)を参照してください。
1. {{site.data.keyword.iot_short_notm}} ダッシュボードで**「メンバー」**に移動します。
2. **「メンバーの追加」**をクリックし、**「インポート」**タブを選択します。
3. ファイルを参照するか、`.csv` ファイルを**「CSV のアップロード (Upload CSV)」**ウィンドウにドラッグします。
4. CSV ファイルで指定されている役割が認識されない場合に使用する、デフォルトの役割を選択します。
5. CSV ファイル内の列番号を、対応する IBMid、役割、有効期限日付 (オプション) のエントリーにマップします。
6. `.csv` ファイルで使用されている列区切り文字と一致する区切り文字 (コンマまたはセミコロン) を選択します。
7. **「インポート」**をクリックして IBMids をインポートし、メンバーを作成します。


### {{site.data.keyword.iot_short_notm}} 組織へのメンバーの招待

{{site.data.keyword.iot_short_notm}} 組織のメンバーになるようにユーザーを招待すると、そのユーザーは、招待リンクが含まれた電子メールを受信します。招待リンクの有効期限は、送信してから 48 時間後です。48 時間以内に招待リンクを使用しなかった場合、ユーザーは、もう一度招待を受けて、新しい招待リンクを受信しなければなりません。

**重要:** 招待機能を使用するには、メール・サービスを構成しておく必要があります。詳しくは、[外部サービスの統合](reference/extensions/index.html#email)トピックの『E メール』セクションを参照してください。

{{site.data.keyword.iot_short_notm}} 組織に 1 人のメンバーを招待するには、次の手順を実行します。
1. {{site.data.keyword.iot_short_notm}} ダッシュボードで**「メンバー」**に移動します。
2. **「招待」**タブを選択します。
2. **「メンバーの招待」**をクリックし、**「招待」**タブを選択します。
3. メンバーの E メール・アドレスを入力します。
4. このメンバーの役割を選択します。
5. オプション: メンバーの有効期限日付を設定します。
6. **「メンバーの招待 (Invite Member)」**をクリックします。

複数のメンバーを同時に招待するには、各メンバーの E メール・アドレス、役割、(オプションの) 有効期限日付が含まれた `.csv` ファイルをアップロードする必要があります。詳しくは、[CSV ファイルの作成](#constructing-your-csv)を参照してください。
1. {{site.data.keyword.iot_short_notm}} ダッシュボードで**「メンバー」**に移動します。
2. **「招待」**タブを選択します。
2. **「メンバーの招待」**をクリックし、**「インポート」**タブを選択します。
3. ファイルを参照するか、`.csv` ファイルを**「CSV のアップロード (Upload CSV)」**ウィンドウにドラッグします。
4. CSV ファイルで指定されている役割が認識されない場合に使用する、デフォルトの役割を選択します。
5. CSV ファイル内の列番号を、対応する E メール・アドレス、役割、有効期限日付 (オプション) のエントリーにマップします。
6. `.csv` ファイルで使用されている列区切り文字と一致する区切り文字 (コンマまたはセミコロン) を選択します。
7. **「インポート」**をクリックして、招待を送信します。

<!-- ### Registering a member with your {{site.data.keyword.iot_short_notm}} organization

If your organization is using {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.ssoshort}}, you can add individual members to your organization by registering them, which does not require an IBMid.

To register a member with your {{site.data.keyword.iot_short_notm}} organization:
1. In the {{site.data.keyword.iot_short_notm}} dashboard, go to **Members**.
2. Select the **Invitations** tab.
2. Click **Invite Members** and select **Invite**.
3. Enter the email address of the member.
4. Select a role for this member.
5. Enter the subject, realm name, and issuer.
   **Important:** Ensure that the `Subject`, `Realm Name`, and `Issuer` fields comply with the OpenID Connect recommendations and standards. For more information, see the [OpenID Connect ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://openid.net/connect/){: new_window} website.
6. Optional: Set an expiry date for the member.
7. Click **Register Member**.

To register multiple members simultaneously, you must upload a CSV (`.csv`) file that contains the email address, role, subject, realm name, issuer, and the optional expiry date of each member.
1. In the {{site.data.keyword.iot_short_notm}} dashboard, go to **Access**.
2. Click **Add Member** and select **Import**.
3. Click **Bulk Register**.
4. Select a default role and ensure that the column numbers on your CSV file match the column numbers in the CSV settings.
5. Ensure the column separator in your CSV file matches the column separator in the CSV settings.
6. Click **Browse your files** or drag the CSV file into the **Upload CSV** window. -->

### CSV ファイルの作成
{: #constructing-your-csv}

複数のメンバーを組織にインポートするために CSV ファイルを作成するときには、使用する方式に応じて必要な情報を含めてください。列の区切りには、コンマまたはセミコロンを使用します。  
**重要:** CSV ファイルをアップロードするときに、**「CSV 設定 (CSV settings)」**で、列の区切り文字として正しいものを選択してください。

コンマ区切りのサンプル CSV ファイル:  
```
user1@sample.com,PD_DEVELOPER_USER,1489505652152
user2@sample.com,PD_OPERATOR_USER,1489505652152
user3@sample.com,PD_ADMIN_USER,1489505652152
```

ここでは次の列エントリーが使用されています。  
- 1 列目: ユーザーの E メール・アドレス。  
メンバーを追加する場合は、有効な IBMid に対応する E メール・アドレスを使用していることを確認してください。メンバーを招待する場合は、任意の有効な E メール・アドレスを使用できます。
- 2 列目: ユーザーに割り当てられる役割。  
以下のいずれかの役割を入力します。
 - PD_ADMIN_USER
 - PD_OPERATOR_USER
 - PD_DEVELOPER_USER
 - PD_ANALYST_USER
 - PD_READER_USER  
ユーザー役割について詳しくは、[ユーザー、アプリケーション、ゲートウェイの役割](roles_index.html#user_roles)を参照してください。
- 3 列目: ユーザーの有効期限日付に対応する UNIX タイム・スタンプ (ミリ秒単位、UTC 1970 年 1 月 1 日 00:00 以降)。

## ユーザーの編集
{: #editing-users}

ユーザーを編集して、役割の変更、アクセス権限の有効期限の追加、削除、変更、または組織へのアクセス権限の追加、削除を行うことができます。

1. {{site.data.keyword.iot_short_notm}} ダッシュボードから、左側のナビゲーション・バーの**「メンバー」**をクリックしてください。
2. 編集するユーザーの横にある**「編集」**アイコンをクリックします。
3. ユーザーに対して必要な変更を行います。
4. **「保存」**をクリックします。

## ユーザー・アクセスのブロック
{: #blocking-users}

組織のメンバーシップは保持したままで、ユーザーによる {{site.data.keyword.iot_short_notm}} 組織へのアクセスをブロックすることができます。

1. {{site.data.keyword.iot_short_notm}} ダッシュボードから、左側のナビゲーション・バーの**「メンバー」**をクリックしてください。
2. {{site.data.keyword.iot_short_notm}} 組織へのアクセスをブロックするユーザーの横にあるトグルをクリックします。


## ユーザーの削除
{: #removing-users}

ユーザーを {{site.data.keyword.iot_short_notm}} 組織から完全に削除することができます。ユーザーを削除すると、元に戻すことはできません。アクセス権限を復元するためには、ユーザーを[プラットフォームに追加する](#adding-new-users)必要があります。

1. {{site.data.keyword.iot_short_notm}} ダッシュボードから、左側のナビゲーション・バーの**「メンバー」**をクリックしてください。
2. 削除するユーザーの横にある**「削除」**アイコンをクリックします。
3. 確認のダイアログで**「削除」**をクリックします。
