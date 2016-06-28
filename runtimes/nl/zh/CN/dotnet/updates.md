---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# ASP.NET 核心 buildpack 的最新更新
{: #latest_updates}

*上次更新时间：2016 年 6 月 10 日*

aspnet buildpack 中最新更新的列表。

## 2016 年 6 月 10 日：更新了 ASP.NET 核心 buildpack V0.8.1-20160526-0957

此版本 buildpack 包含以下更改：

* 运行时的名称从 ASP.NET 5 更改为“ASP.NET 核心”。
* buildpack 版本号包含到检测脚本输出中。
* 此版本 buildpack 不再支持使用 CoreCLR RC1 及更低版本的基于 DNX 的应用程序。
* 此版本 buildpack 支持 .NET CLI 和 .NET 核心 RC2。
* 此 buildpack 会使用 project.json 文件或发布输出中的 *.runtimeconfig.json 文件检测项目。

## 2015 年 10 月 22 日：更新了 ASP.NET 5 buildpack V0.7-20151022-1257

* 此版本 buildpack 除去了 Mono，改为支持 Beta 8 CoreCLR。

## 2015 年 9 月 18 日：更新了 ASP.NET 5 buildpack V0.6-20150916-1220

* 此版本 buildpack 支持 Beta 7 DNX 更改，并且可以通过以下定制启动命令，运行依赖于较低 Beta 发行版的应用程序：

```
   dnx src/dotnetstarter kestrel --server.urls http://${VCAP_APP_HOST}:${PORT}
```
{: codeblock}

* 此 buildpack 中不再使用 Nowin Web 服务器，而改为使用 [Kestrel]{https://github.com/aspnet/KestrelHttpServer} Web 服务器。

# 相关链接
{: #rellinks}
## 常规
{: #general}
* [Dotnet 核心运行时](index.html)
