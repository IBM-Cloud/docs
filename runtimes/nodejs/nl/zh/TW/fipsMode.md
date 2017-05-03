---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# FIPS 模式
{: #fips_mode}

Nodejs 建置套件 v3.2-20160315-1257 版以及更新版本支援 [FIPS ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://en.wikipedia.org/wiki/Federal_Information_Processing_Standards)。  
{: shortdesc}

若要使用已啟用 FIPS 功能的 node 引擎，請將環境變數 FIPS_MODE 設為 true。
例如：

```
    $ cf set-env myapp FIPS_MODE true
```
{: codeblock}

請務必瞭解，當 FIPS_MODE 為 true 時，部分 node 模組可能會無法運作。例如，**使用 [MD5 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://en.wikipedia.org/wiki/MD5) 的節點模組將會失敗**，例如 [Express ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://expressjs.com/)。對於 Express，在 Expess 應用程式中將 [etag ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://expressjs.com/en/api.html) 設為 false 可能有助於暫時解決此問題。例如，您可以在程式碼中執行下列動作：

```
    app.set('etag', false);
```
{: codeblock}
如需相關資訊，請參閱這則 [Stack Overflow 貼文 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://stackoverflow.com/questions/15191511/disable-etag-header-in-express-node-js)。

**附註**：*未* 同時支援[應用程式管理](/docs/manageapps/app_mng.html)及 FIPS_MODE。如果設定 BLUEMIX_APP_MGMT_ENABLE 環境變數，而且 FIPS_MODE 環境變數設為 true，將無法編譯打包應用程式。

有各種方法可檢查 FIPS_MODE 的狀態：
<ul>
<li> 您可以檢查應用程式的日誌，以尋找類似於下列內容的訊息：    

  <pre>
  正在從快取中安裝已啟用 FIPS 功能的 IBM SDK for Node.js (4.4.3)
  </pre>
  {: codeblock}

這則訊息指出已啟用 FIPS 功能的 node.js 引擎正在執行中，但 FIPS 不一定要正在執行
</li>

<li> 您可以檢查 **process.versions.openssl** 的值。例如：

  <pre>
  console.log('ssl version is [' +process.versions.openssl +']');
  </pre>
  {: codeblock}

如果 SSL 版本包含 "fips"，則使用中的 SSL 版本支援 FIPS。  
</li>

<li> 若為 node.js 第 6 版及更高版本，您可以在與下面類似的程式碼中檢查 crypto.fips 所傳回的值：

  <pre>
  console.log('crypto.fips== [' +crypto.fips +']');
  </pre>
  {: codeblock}

如果傳回的值是 1，則表示正在使用 FIPS。請注意，若為第 6 版之前的 node.js 版本，crypto.fips 將傳回*未定義*。
</li>
</ul>

## Nodejs 第 4 版
{: #nodejs_v4_fips}

下表說明 node.js 第 4 版在使用 FIPS 時的行為：

|                 | 結果          |
| :-------------- | :------------ |
|FIPS_MODE=true   |成功 (1)    |
|FIPS_MODE !=true |成功 (2)    |

* 成功 (1)
  * FIPS 正在使用中。
  * 日誌將包括*正在安裝已啟用 FIPS 功能的 IBM SDK for Node.js* 訊息。
  * process.versions.openssl 所傳回的值將包含 "fips"。
* 成功 (2)
  * FIPS 目前*不* 在使用中。
  * 日誌*不* 包括*正在安裝已啟用 FIPS 功能的 IBM SDK for Node.js* 訊息。
  * process.versions.openssl 所傳回的值*不* 會包含 "fips"。

## Nodejs 第 6 版
{: #nodejs_v6_fips}

若要以 FIPS 模式與 Node.js 第 6 版搭配執行，則除了設定 **FIPS_MODE=true** 之外，您還必須在 start 指令中包括 **--enable-fips**，如下列範例中所示：
```
{
    ...   
    "scripts": {
      "start": "node --enable-fips app.js"
    }
}
```
{: codeblock}

下表說明 node.js 第 6 版在使用 FIPS 時的行為。

|                 |--enable-fips  |NO --enable-fips |
| :-------------- | :------------ | :-------------- |
|FIPS_MODE=true   |成功 (1)    |成功 (2)      |
|FIPS_MODE !=true |失敗 (3)    |成功 (4)      |

* 成功 (1)
  * FIPS 正在使用中。
  * 日誌將包括*正在安裝已啟用 FIPS 功能的 IBM SDK for Node.js* 訊息。
  * process.versions.openssl 所傳回的值將包含 "fips"。
  * crypto.fips 將傳回 1，指出 FIPS 正在使用中。
* 成功 (2)
  * FIPS 目前*不* 在使用中。
  * 日誌將包括*正在安裝已啟用 FIPS 功能的 IBM SDK for Node.js* 訊息。
  * process.versions.openssl 所傳回的值將包含 "fips"。
  * crypto.fips 將傳回 0，指出 FIPS 目前*不* 在使用中。
* 失敗 (3)
  * FIPS 目前*不* 在使用中。
  * 日誌*不* 包括*正在安裝已啟用 FIPS 功能的 IBM SDK for Node.js* 訊息。
  * 編譯打包將會失敗，訊息為「ERR node：選項錯誤：--enable-fips」。
* 成功 (4)
  * FIPS 目前*不* 在使用中。
  * 日誌*不* 包括*正在安裝已啟用 FIPS 功能的 IBM SDK for Node.js* 訊息。
  * process.versions.openssl 所傳回的值*不* 會包含 "fips"。
  * crypto.fips 將傳回 0，指出 FIPS 目前*不* 在使用中。
