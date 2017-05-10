---

copyright:
  years: 2015, 2017
lastupdated: "2016-10-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# リソース・データのベータ版からのマイグレーション
{: #globalizationpipeline_betaresourcedatamigration}

{{site.data.keyword.GlobalizationPipeline_full}}のベータ版は、GA バージョンのリリースから一定期間が経過した後に提供を終了する予定です。ベータ・インスタンスのユーザー・データは、GA サービスのインスタンスに移されません。GA 後もデータを保持するには、リソース・データをファイルにエクスポートしてから、新しいインスタンスにインポートします。この操作は、サービス・ダッシュボードでは実行できないので注意してください。また、リソース・データをいずれかのリソース・ファイル形式にエクスポートすると、リソース・エントリーに関連する他のメタデータは保持されないことになります。

ベータ版から GA へのデータ・マイグレーションをサポートするために、ある機能が{{site.data.keyword.GlobalizationPipeline_short}}の Java コマンド・ライン・ツールに追加されています。そのツールのソースは、https://github.com/IBM-Bluemix/gp-java-tools にホストされており、そのバイナリー・リリースも github リポジトリーに提供されています。最新の開発スナップショットが投稿されています。[ここからダウンロード](https://w3-connections.ibm.com/communities/service/html/communityview?communityUuid=589d87cf-d0c7-4e06-ab95-4108547f90aa#fullpageWidgetId=Wa22bb771e29b_4aa9_a114_cfe53fda2cc8&file=5cdaf089-ec7c-4881-b5a0-7ab651491237)してください。

このツールは、***リソース・エントリーのアップロード***のためにベータ・リリース後に機能強化された REST API を使用するため、宛先サービス・インスタンスは GA バージョンでなければなりません。 
* ソース: ベータまたは GA
* 宛先: GA のみ

グローバリゼーション・サービス・インスタンスのすべてのバンドル・データを別のインスタンスにコピーするには、以下のコマンドを使用します。

```> java -jar gp-cli.jar copy-all-bundles -s <source-service-url> -i <source-instance-id> -u <source-user-id> -p <source-password> --dest-url <dest-service-url> --dest-instance-id <dest-instance-id> --dest-user-id <dest-user-id> --dest-password <dest-password>```


`source/target-service-url` やその他のパラメーター値は、ソース/宛先サービスの資格情報の中に含まれています。次に例を示します。

 

```
{
  "gp-beta": [
    {
      "name": "Globalization Pipeline-7x",
      "label": "gp-beta",
      "plan": "gp-beta-plan",
      "credentials": {
 

      "url": "https://gp-beta-rest.ng.bluemix.net/translate/rest",
        "userId": "bd0b84362c6934d222c3a0a40fc1443b",
        "password": "OGxp6jDqCLCL1ui8kQSPTt1mZDi4EQwu",
        "instanceId": "bd0b84362c6934d222c3a0a40fc1233e"
      }
    }
  ]
}
```
また、個々のオプション `(-s / -i / -u / -p)` に加えて json 形式の資格情報をサポートするように GP CLI のすべてが更新されています。以下のような内容の json ファイルを作成できます。

creds.json 
 
```
 {

        "url": "https://gp-rest.stage1.ng.bluemix.net/translate/rest",
        "userId": "36cad58b3a65dc9fe0183208305be137",
        "password": "43F9MRMu9Q8BWRXMLctunUsAe8LTdwq1",
        "instanceId": "b157e3fc63e62d76c50d9f689d7fc965"} 
```
そして、`-j <json-file>` を使用して、このファイルを指定できます。`copy/copy-all-bundles` コマンドの中に、

```-s https://gp-rest.stage1.ng.bluemix.net/translate/rest -i b157e3fc63e62d76c50d9f689d7fc965 -u 36cad58b3a65dc9fe0183208305be137 -p 43F9MRMu9Q8BWRXMLctunUsAe8LTdwq1```

と指定する代わりに、次を指定できます。

`-j creds.json `
 
あるいは、以下のコマンドを使用して、バンドルを別の場所にコピーすることができます。 

```> java -jar gp-cli.jar copy -s <source-service-url> -i <source-instance-id> -u <source-user-id> -p <source-password> -b <source-bundle-id> --dest-url <dest-service-url> --dest-instance-id <dest-instance-id> --dest-user-id <dest-user-id> --dest-password <dest-password> -d <dest-bundle-id>```


**注:** copy-all-bundles で使用できるパラメーターに加えて、`-b <source-bundle-id>` と `-d <dest-bundle-id>` の 2 つを追加で使用できます。このコマンドは、同じインスタンス内でバンドルをコピーする場合も使用できます。その場合、宛先サービス資格情報パラメーター `(--dest-*)` は省略可能です。





上記のコマンドでは、既存のバンドル・データとリソース・エントリー・データが抽出され、新しい場所にアップロードされます。このプロセスの間、REST サーバーが管理するフィールドのいくつかが更新されます (updatedBy/updatedAt フィールドなど)。また、これらのコマンドではサービス・バインディングも構成データもコピーされないため、一般には、宛先インスタンスで MT サービスを構成する必要があります。





例えば、ベータ版では、Watson 言語翻訳プログラムによるアラビア語翻訳がサポートされています。GA バージョンでは、アラビア語翻訳の無償提供は終了しました。ベータ版データを新しい GA インスタンスに移植する際、翻訳済みのアラビア語コンテンツは保持されます。ソース言語を変更しても、アラビア語翻訳を有効にするように Watson バインディングをセットアップしない限り、アラビア語翻訳は自動的にはトリガーされません。これは、ソース・インスタンスが GA バージョンの場合にも当てはまります。外部 MT サービス・バインディングは GP インスタンスに固有のものです。別のインスタンスに対するバインディング/構成は自動的には移植されません。




 

