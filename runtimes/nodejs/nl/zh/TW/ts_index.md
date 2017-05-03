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

# SDK for Nodejs 疑難排解
{: #ts}


以下是有關在 {{site.data.keyword.Bluemix}} 上使用 SDK for Nodejs 的常見疑難排解問題的答案。
{:shortdesc}

## 應用程式無法啟動，錯誤為「裝置上沒有可用的空間」
{: #no_space_left_on_device}


Nodejs 應用程式無法啟動，錯誤為「裝置上沒有可用的空間」。例如，日誌中的錯誤可能類似下列內容：
{: tsSymptoms}

```
   2017-01-16T14:25:14.61-0500 [CELL/0]     ERR tar: ./app/node_modules/pm2/node_modules/cron/node_modules/moment-timezone/LICENSE: Cannot write: No space left on device

```
{: #codeblock}

下載相依關係時，使用第 3 版之前的 NPM 版本的 Nodejs 應用程式會耗用更多空間。
{: tsCauses}

修改應用程式的 package.json 檔案，以使用 NPM 第 3 版或以上版本。
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
