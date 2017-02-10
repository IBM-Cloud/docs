---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Android 用のアンバインド・{{site.data.keyword.mobilepushshort}}サービスの作成
{: #create_android_unbound}
最終更新日: 2017 年 1 月 11 日
{: .last-updated}

{{site.data.keyword.mobilepushshort}}サービス・インスタンスを作成します。バックエンド・アプリケーションにバインドせずに、{{site.data.keyword.mobilepushshort}}サービス・インスタンスを使用することができます。

1. {{site.data.keyword.mobilepushshort}}サービス・インスタンスを Bluemix アプリケーションにバインドします。バインドすると、サービスに関連するすべての詳細が、JSON 形式で VCAP_SERVICES 環境変数に保管されていることを確認できます。 

![プッシュ通知サービスのバインド](images/unbound_1.jpg)
 2. **「バインド」**をクリックして、バインドする{{site.data.keyword.mobilepushshort}}サービス・インスタンスを選択します。アプリケーションが{{site.data.keyword.mobilepushshort}}サービスにバインドされると、サービスに関する情報が JSON 形式でアプリの VCAP_SERVICES 環境変数に保管されます。例えば、次のようにします。 
```
 	{
    "imfpush_Dev": [
      {
         "name": "myname_sampleUnbound",
         "label": "imfpush_Dev",
         "plan": "Basic",
         "credentials": null
      }
    ]
    }
```
	{: codeblock}
