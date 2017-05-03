---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# 開始コマンド
{: #startup_commmand}

Bluemix Node.js アプリケーションの開始コマンドを指定するための推奨方法は、**Procfile** ファイルまたは **package.json** ファイルを使用することです。
{: shortdesc}

下記の形式で、**Procfile** に開始コマンドを指定します。app.js は、アプリケーション用の開始 js スクリプトです。
```
web: node app.js
```
{: codeblock}

**Procfile** をアプリケーションのルート・ディレクトリーに保存します。

**Procfile** がない場合、IBM Bluemix Node.js ビルドパックは **package.json** ファイルの scripts.start 項目を検査します。下の例でも、app.js はアプリケーション用の開始 js スクリプトです。

```
{
    ...   
    "scripts": {
      "start": "node app.js"
    }
}
```
{: codeblock}

開始スクリプト項目が **package.json** にある場合は、**Procfile** が自動的に生成されます。自動生成された **Procfile** の内容は次のようになります。

```
    web: npm start
```
{: codeblock}

**Procfile** および **package.json** ファイルについて詳しくは、[Tips for Node.js Applications ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.cloudfoundry.org/buildpacks/node/node-tips.html) を参照してください。
