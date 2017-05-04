---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-06"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 使用可能なバージョン
{: #available_versions}

{{site.data.keyword.Bluemix}} は、[現在使用可能な Node.js ランタイム](http://nodejs.org/dist/)のすべてを提供します。これらのうち、IBM では機能拡張およびバグ修正を含むバージョンを提供しています。詳しくは、[『Node.js ビルドパックに対する最新の更新』](/docs/runtimes/nodejs/updates.html)を参照してください。
{: shortdesc}

IBM Node.js ビルドパックは、IBM ランタイム・バージョンをキャッシュに入れます。そのため、IBM SDK for Node.js ランタイムをアプリケーションで使用している場合は、アプリケーションを Bluemix にプッシュすると、アプリケーションのパフォーマンスが向上します。

実行したい Node.js ランタイムのバージョンを指定するには、**package.json** ファイルの **engines** セクションで **node** パラメーターを使用します。

Node.js にバンドルされたバージョン以外の npm のバージョンを指定する必要がある場合は、**package.json** ファイルの **engines** セクションで **npm** パラメーターを使用します。  

以下の例を参照してください。

```
{
  "name": "myapp",
  "description": "this is my app",
  "version": "0.1",
  "engines": {"node": "4.2.4",
     "npm": "3.10.10"
  }
}
```
{: codeblock}

ノード・バージョンは常に **package.json** ファイルで指定される必要があります。指定されていない場合は、最新のノード・バージョンが使用されます。
