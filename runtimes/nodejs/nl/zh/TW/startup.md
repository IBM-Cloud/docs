---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Startup 指令
{: #startup_commmand}

為您的 Bluemix Node.js 應用程式指定 start 指令的建議方式，是使用 **Procfile** 或 **package.json** 檔案。
{: shortdesc}

請使用下列格式在 **Procfile** 中指定 startup 指令。這裡的 app.js 是應用程式的 startup JS Script。

```
web: node app.js
```
{: codeblock}

將 **Procfile** 儲存在應用程式的根目錄中。

如果 **Procfile** 不存在，IBM Bluemix Node.js 建置套件會檢查 **package.json** 檔案中是否有 scripts.start 項目。同樣地，在以下範例中，app.js 是應用程式的 startup JS Script。

```
{
    ...   
    "scripts": {
      "start": "node app.js"
    }
}
```
{: codeblock}

如果 **package.json** 中有 start Script 項目存在，則會自動產生 **Procfile**。自動產生的 **Procfile** 內容如下：

```
    web: npm start
```
{: codeblock}

如需 **Procfile** 和 **package.json** 檔案的相關資訊，請參閱 [Node.js 應用程式的提示 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://docs.cloudfoundry.org/buildpacks/node/node-tips.html)。
