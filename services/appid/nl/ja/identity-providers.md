---

copyright:
  years: 2017
lastupdated: "2017-03-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# ID プロバイダーの構成
{: #setting-up-idp}

Facebook、Google、またはその両方を構成して、アプリケーションを認証し、保護されたバックエンド・リソースへのアクセスを許可することができます。
{:shortdesc}


## Facebook
{: #facebook}

Facebook を ID プロバイダーとして使用するように {{site.data.keyword.appid_short}} サービスを構成します。

<!--- ### Sequence diagram
{: #facebook-sequence-diagram}--->

### Facebook からアプリ ID とアプリ・シークレットを取得する
{: #getting-facebook-appid}

モバイル・アプリや Web アプリで Facebook を ID プロバイダーとして使用するには、Facebook アプリケーションで Web サイトのプラットフォームを追加して構成する必要があります。

1. Facebook for Developers サイトで自分のアカウントにログインします。新しい Facebook アプリの作成方法について詳しくは、<a href="https://developers.facebook.com/docs/apps/register" target="_blank">アプリケーションの作成<img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a>を参照してください。
2. Facebook のアプリ ID とアプリ・シークレットをメモします。サービスのダッシュボードで Web プロジェクトの認証を構成するときに、これらの値が必要になります。
3. Web プラットフォームを追加して、サイト URL を入力します。
4. 製品リストから、**「Facebook ログイン」**を選択します。
5. 「有効な OAuth リダイレクト URL」フィールドに、許可サーバーのコールバック・エンドポイント URL を入力します。以下のステップで {{site.data.keyword.appid_short_notm}} サービスを構成した後で、この値を追加できます。
6. **「変更の保存」**をクリックします。

### Facebook 認証用の {{site.data.keyword.appid_short_notm}} の構成
{: #configuring-facebook-appid}

Facebook のアプリ ID とアプリ・シークレットを取得し、Web クライアントを処理できるように Facebook for Developers アプリを構成すると、サービスのダッシュボードで Facebook 認証を編集できます。

1. サービスのダッシュボードの**「管理」**タブで、**「Facebook」**を選択して**「編集」**をクリックします。
2. Facebook for Developers Web サイトから取得した Facebook のアプリ ID とアプリ・シークレットを入力します。
3. **「Facebook for Developers のリダイレクト URI (Redirect URI for Facebook for Developers)」**フィールドにある URI をコピーします。この URI を Facebook Developers ポータルの**「Facebook ログイン」**セクションの**「有効な OAuth リダイレクト URI」**フィールドに貼り付けます。
4. **「保存」**をクリックします。
5. オプション: Web アプリの認証を構成する場合は、リダイレクト URI を「Web アプリケーションのリダイレクト URI (your Web Application Redirect URIs)」に入力します。この値は、開発者が決定する値であり、許可プロセスの完了後にリダイレクト URI にアクセスするために使用されます。


## Google
{: #google}

Google を ID プロバイダーとして使用するように {{site.data.keyword.appid_short_notm}} サービスを構成します。

<!--- ### Sequence diagram
{: #google-sequence-diagram}--->

### Google からクライアント ID とシークレットを取得する
{: #google-client-id}

Google を ID プロバイダーとして使用するには、Google のクライアント ID とシークレットを取得して Google Developer Console でプロジェクトを作成します。

1. Google Developer Console で Google アプリケーションを開きます。
2. Google+ API を追加します。
3. OAuth を使用して資格情報を作成します。**「アプリケーションの種類」**フィールドで、**「ウェブ アプリケーション」**を選択します。**「承認済みのリダイレクト URI」**フィールドにこのアプリ ID のリダイレクト URI を入力します。App ID のリダイレクト許可 URI は、サービスのダッシュボードの Google 構成画面から取得できます。
4. 変更内容を保存します。Google のクライアント ID とシークレットをメモします。




### Google 認証用の {{site.data.keyword.appid_short_notm}} の構成
{: #google-client-appid}

Google のクライアントとシークレットを取得し、Web クライアントを処理できるように Google Developers コンソールを構成すると、サービスのダッシュボードで Google 認証を編集できます。

1. サービスのダッシュボードの**「管理」**タブで、**「Google」**を選択して**「編集」**をクリックします。
3. Google Developers コンソールから取得した Google のクライアント ID とシークレットを入力します。
4. **「Google for Developers のリダイレクト URI (Redirect URI for Google for Developers)」**フィールドにある URI をコピーします。この URI を、Google Developers Portal の**「Web アプリケーションのクライアント ID」**の**「制限事項」**の下にある**「承認済みのリダイレクト URI」** フィールドに貼り付けます。
5. **「保存」**をクリックします。
6. オプション: Web アプリの認証を構成する場合は、リダイレクト URI を「Web アプリケーションのリダイレクト URI (Web Application Redirect URIs)」フィールドに入力します。この値は、開発者が決定する値であり、許可プロセスの完了後にリダイレクト URI にアクセスするために使用されます。



<!---[## Bring your own OAuth2/OIDC identity provider
{: #oauth2}

### About
{: #oauth2-about}
### Sequence diagram
{: #oauth2-sequence-diagram}
### Configuring AppID for BYOIDP OAuth2 authentication
{: #oauth2-appid} SHAWNA: Is this Interconnect?]--->
