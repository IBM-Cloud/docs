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

# SDK for Nodejs 故障诊断
{: #ts}


以下是对在 {{site.data.keyword.Bluemix}} 上使用 SDK for Nodejs 的常见故障诊断问题的回答。
{:shortdesc}

## 应用程序未能启动，错误为“No space left on device”
{: #no_space_left_on_device}


Nodejs 应用程序未能启动，错误为“No space left on device”。例如，日志中的错误可能看起来如下所示：
{: tsSymptoms}

```
   2017-01-16T14:25:14.61-0500 [CELL/0]     ERR tar: ./app/node_modules/pm2/node_modules/cron/node_modules/moment-timezone/LICENSE: Cannot write: No space left on device

```
{: #codeblock}

使用的 NPM 版本早于 V3 的 Nodejs 应用程序会消耗更多空间来下载依赖项。
{: tsCauses}

修改应用程序的 package.json 文件，以使用 NPM V3 或更高版本。
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
