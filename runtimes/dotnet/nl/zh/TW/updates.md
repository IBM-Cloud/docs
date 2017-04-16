---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-06"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# ASP.NET Core 建置套件的最新更新項目
{: #latest_updates}


aspnet 建置套件中的最新更新項目清單。

## 2016 年 10 月 10 日：已更新 ASP.NET Core 建置套件 v1.0.1-20161005-1225

* 新增 .NET Core 1.0.1 支援
* 修正在快取 NuGet 套件時導致部署失敗的間歇性問題

## 2016 年 8 月 31 日：已更新 ASP.NET Core 建置套件 v1.0-20160826-1345

* 新增支援，讓您可以使用 NPM 及 Bower 來執行前置及後置編譯 Script，以安裝前端 JavaScript 及 CSS 程式庫。
* 將建置套件從測試版狀態移至 GA 狀態

## 2016 年 7 月 11 日：已更新 ASP.NET Core 建置套件 v0.9-20160706-1603

建置套件的這個版本包括下列變更：

* 這個版本的建置套件支援 .NET CLI 1.0 Preview 2 建置和 .NET Core 1.0 RTM
* 此建置套件會繼續支援 .NET CLI 1.0 Preview 1 和 .NET Core 1.0 RC2
* 現在要安裝的預設 .NET CLI 版本為 1.0.0-preview2-003121

## 2016 年 6 月 10 日：已更新 ASP.NET Core 建置套件 v0.8.1-20160526-0957

建置套件的這個版本包括下列變更：

* 運行環境的名稱從 ASP.NET 5 變更成 ASP.NET Core。
* 建置套件版本號碼包括在偵測 Script 輸出中。
* 建置套件的這個版本不再支援使用 CoreCLR RC1 及以下版本的 DNX 型應用程式。
* 建置套件的這個版本支援 .NET CLI 和 .NET Core RC2。
* 建置套件從發佈輸出中偵測到具有 project.json 檔案或 *.runtimeconfig.json 檔案的專案。

## 2015 年 10 月 22 日：已更新 ASP.NET 5 建置套件 v0.7-20151022-1257

* 建置套件的這個版本移除了 Mono，改為支援 Beta 8 CoreCLR。

## 2015 年 9 月 18 日：已更新 ASP.NET 5 建置套件 v0.6-20150916-1220

* 建置套件的這個版本支援 Beta 7 DNX 變更，而且可以執行與具有下列自訂啟動指令的舊測試版相依的應用程式：

```
dnx src/dotnetstarter kestrel --server.urls http://${VCAP_APP_HOST}:${PORT}
```
{: codeblock}

* 這個建置套件已經不再使用 Nowin Web 伺服器，改為使用 [Kestrel]{https://github.com/aspnet/KestrelHttpServer} Web 伺服器。

# 相關鏈結
{: #rellinks}
## 一般
{: #general}
* [Dotnet 核心運行環境](index.html)
