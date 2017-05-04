---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-06"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Node.js アプリケーションをローカルに実行するためのヒント
{: #hints}

この情報は、Node.js アプリケーションをローカルと Bluemix 上の両方で容易に実行するために使用します。
{: shortdesc}

次の例は、**js** ファイルのソースの一部を示しています。

```
var port = (process.env.PORT || 3000);
```
{: codeblock}

このコードでは、アプリケーションが Bluemix 上で実行される場合、PORT 環境変数には、アプリケーションが着信接続を listen する Bluemix 内部のポート値が入ります。アプリケーションがローカルに実行される場合、PORT は定義されないため、ポート番号として **3000** が使用されます。このような方法でコードを書くと、アプリケーションをテスト目的でローカルに実行でき、またさらに変更を行うことなく Bluemix 上で実行できます。
