---

copyright:
  years: 2017
lastupdated: "2017-02-06"

---

{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# SDK for Nodejs のトラブルシューティング
{: #ts}


ここでは、{{site.data.keyword.Bluemix}} 上での SDK for Nodejs の使用に関する一般的なトラブルシューティングの質問に対する回答を示します。
{:shortdesc}

## 「No space left on device」エラーでアプリケーションが開始に失敗する
{: #no_space_left_on_device}


「No space left on device」エラーで Nodejs アプリケーションが開始に失敗します。例えば、ログ内のエラーは、次のようになっています。{: tsSymptoms}

```
   2017-01-16T14:25:14.61-0500 [CELL/0]     ERR tar: ./app/node_modules/pm2/node_modules/cron/node_modules/moment-timezone/LICENSE: Cannot write: No space left on device

```
{: #codeblock}

バージョン 3 より前の NPM バージョンを使用している Nodejs アプリケーションは、依存関係のダウンロードのために、より大きいスペースを消費します。
{: tsCauses}

NPM バージョン 3 以上を使用するように、アプリケーションの package.json ファイルを変更してください。
{: tsResolve}

```
{
  "name": "myapp",
  "description": "this is my app",
  "version": "0.1",
  "engines": {
     "node": "4.2.4",
     "npm": "3.10.10"
  }
}
```
{: codeblock}
