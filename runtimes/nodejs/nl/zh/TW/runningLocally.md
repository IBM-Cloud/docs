---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-06"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# 在本端執行 Node.js 應用程式的提示
{: #hints}

使用此資訊，以協助在本端和 Bluemix 上執行 Node.js 應用程式。
{: shortdesc}

下列範例顯示 **js** 檔案的部分原始碼：

```
var port = (process.env.PORT || 3000);
```
{: codeblock}

使用此程式碼，當應用程式在 Bluemix 上執行時，PORT 環境變數包含的埠值是 Bluemix 的內部值，應用程式藉此來接聽送入的連線。當應用程式在本端執行時，不會定義 PORT，因此會使用 **3000** 作為埠號。透過此撰寫方式，您可以在本端（若是進行測試）以及在 Bluemix 上執行應用程式，而不必做進一步的變更。
