---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# REST API の使用
{: #push-api-rest}
最終更新日: 2017 年 1 月 16 日
{: .last-updated}

{{site.data.keyword.mobilepushshort}}には REST (Representational State Transfer) API (アプリケーション・プログラム・インターフェース) を使用できます。また、SDK と[プッシュ API ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://mobile.{DomainName}/imfpush/ "外部リンク・アイコン"){: new_window} を使用して、クライアント・アプリケーションをさらに開発することもできます。

バックエンド・サーバー・アプリケーションとクライアントは、Push REST API を使用して、{{site.data.keyword.mobilepushshort}}機能にアクセスできます。

- デバイス登録
- 登録
- メッセージ
- サブスクリプション
- タグ (Tags)
- Web フック

REST API のベース URL を取得するには、以下の手順を実行します。

1. MobileFirst Services Starter を選択することで、Bluemix® カタログの Boilerplates セクションでバックエンド・アプリケーションを作成します。これにより、{{site.data.keyword.mobilepushshort}}サービスがアプリケーションにバインドされます。Push のサービス・インスタンスを作成してアンバインドのままにすることもできます。 
1. Bluemix ダッシュボードのメインページで、**「アプリケーション」**エリアに移動し、アプリを選択します。
3. **「モバイル・オプション」**をクリックします。アプリの詳細ページの最初に、経路およびアプリ GUID の値が表示されます。「資格情報の表示」画面に、AppSecret に関する情報が表示されます。「モバイル・オプション」のアプリケーション秘密鍵や、いくつかの API のクライアント秘密鍵も取得できます。

また、以下のようにコマンド・ラインを使用してサービス資格情報を取得することも可能です。

```
    cf create-service-key {push_instance_name} {key_name}
    cf service-key {push_instance_name} {key_name}
```
	{: codeblock}

## Accept-Language ヘッダー
{: #push-api-rest-accept}

「Accept-Language」ヘッダーは、[Push REST API ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://mobile.{DomainName}/imfpush/ "外部リンク・アイコン"){: new_window}によって出力されるエラー・メッセージに使用する言語を指定します。エラー・メッセージでサポートされる言語は、中国語 (簡体字)、中国語 (繁体字)、英語 (米国)、ドイツ語、フランス語、イタリア語、日本語、韓国語、ポルトガル語、およびスペイン語です。

## appSecret 
{: #push-api-rest-secret}

アプリケーションが {{site.data.keyword.mobilepushshort}} にバインドされると、サービスは appSecret (固有キー) を生成し、それを応答ヘッダーで渡します。IBM {{site.data.keyword.mobilepushshort}} for Bluemix Rest API を使用している場合は、REST API リファレンスを使用して、保護する必要のある API に関する情報を取得してください。詳しくは、[Push REST API ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://mobile.{DomainName}/imfpush/ "外部リンク・アイコン"){: new_window}を参照してください。

要求ヘッダーには appSecret が含まれている必要があります。含まれていない場合、サーバーは 401 無許可エラー・コードを返します。{{site.data.keyword.mobilepushshort}} がアプリケーションに追加されると、特定の AppID が作成されます。応答の一部として、タグの作成やメッセージの送信に使用される appSecret というヘッダーを取得します。操作は、カタログまたはボイラープレートのサービスを介して行われます。

appSecret 値を取得するには、以下のようにします。

1. プッシュ・サービスにバインドされている *app-name* をクリックします。
2. **「資格情報の表示」**リンクをクリックして appSecret (AppID) を表示します。

**「資格情報の表示」**画面に、AppSecret に関する情報が表示されます。
```
	{
    "imfpush_Dev": [
    {
     "name": "testapp1",
     "label": "imfpush_Dev",
     "plan": "Basic",
     "credentials": {
       "url": "http://imfpush.ng.bluemix.net/imfpush/v1/apps/b615b280-b37e-4042-8815-38a758f234e2",
       "admin_url": "//mobile.ng.bluemix.net/imfpushdashboard/?appGuid=b615b280-b37e-4042-8815-38a758f234e2",
       "appSecret": "8dac71a5-2219-42b3-a9f3-dbb828ba1f04",
       }
     }
    ]
    }
```
	{: codeblock} 


##Push REST API のフィルター
{: #push-api-rest-filters}

フィルターは、{{site.data.keyword.mobilepushshort}}の GET API から返されるデータを制限する検索条件を定義します。フィルタリングする GET 操作の結果に対してフィルターを適用します。フィルターは、結果に含まれる項目の数を制限します。例えば、フィルターを使用して、名前が「test」で始まるタグを検索できます。 

フィルターは、以下の構文で生成できます。

**name**: フィルターが適用されるフィールドの名前。

**operator**: 使用するフィルターの一致条件を記述する == (完全一致) または =@ (サブストリングを含む)。

**expression**: 結果に含める値。

コンマおよび円記号 () は、式で表示する場合、円記号 () でエスケープする必要があります。

複数のフィルターを使用する場合、AND ロジックと OR ロジックを使用してそれらを結合することができます。

- AND ロジックの場合、照会で複数のフィルターを使用します。
- OR ロジックの場合、フィルター式内でコンマ (,) を使用します。
- AND と OR の両方のロジックの場合、単一の照会で AND ロジックと OR ロジックの両方を含めることができます。各フィルターが個別に評価されてから、AND 式で結合されます。

デバイス GET API では、以下の組み合わせがサポートされます。
- name は platform フィールドです。
- platform 以外の場合、operator は == または =@ にすることができます。
- platform の場合、operator は == でなければなりません。operator として =@ が使用された場合、値はサブストリングになることがあります。
- == が使用された場合、値は完全一致ストリングでなければなりません。

サブスクリプション GET API では、以下の組み合わせがサポートされます。

- name は、tagName または deviceId のいずれかのフィールドにすることができます。
- platform 以外の場合、operator は == または =@ にすることができます。
- platform の場合、operator は == でなければなりません。
- operator として =@ が使用された場合、値はサブストリングになることがあります。operator として == が使用された場合、値は完全一致ストリングでなければなりません。
- タグ GET API では、以下の組み合わせがサポートされます。
- name は、name または description のいずれかのフィールドにすることができます。
- operator として =@ が使用された場合、値はサブストリングになることがあります。
- == が使用された場合、値は完全一致ストリングでなければなりません。


##{{site.data.keyword.mobilepushshort}}の応答コード
{: #push-api-response-codes}

状況: 405 Method Not Allowed - 適切なメソッドを使用する必要があります。
