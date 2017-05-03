---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-30"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# ASP.NET 核心 buildpack 的最新更新
{: #latest_updates}


aspnet buildpack 中最新更新的列表。

## 2017 年 3 月 29 日：更新了 ASP.NET 核心 buildpack V1.0.13-20170330-1023

* 添加对 .NET 核心运行时 1.0.4 的支持
* 添加对 .NET 核心运行时 1.1.1 的支持
* 添加对 .NET 核心 SDK 1.0.1 的支持
* 将 Node 版本更新为 6.10.0
* 除去对 .NET 核心 SDK 1.0.0-preview2-003131 的支持
* 除去对 .NET 核心 SDK 1.0.0-preview3-004056 的支持

## 2017 年 1 月 31 日：更新了 ASP.NET 核心 buildpack V1.0.10-20170124-1145

* 添加对 .NET 核心 1.0.3 的支持
* 添加对 .NET 核心 MSBuild 工具的支持
* 添加对 F# 项目的支持
* 除去对 .NET 核心 SDK 1.0.0-preview2-003121 的支持

## 2016 年 12 月 9 日：更新了 ASP.NET 核心 buildpack V1.0.6-20161205-0912

* 添加对 .NET 核心 1.1.0 的支持
* 除去对 .NET 核心 1.0.0 RC2 的支持
* 添加用于清除 NuGet 数据包高速缓存的选项

## 2016 年 10 月 10 日：更新了 ASP.NET 核心 buildpack V1.0.1-20161005-1225

* 添加 .NET Core 1.0.1 的支持
* 修订了高速缓存 NuGet 软件包时导致部署失败的间歇问题

## 2016 年 8 月 31 日：更新了 ASP.NET 核心 buildpack V1.0-20160826-1345

* 添加了如下支持：使用 NPM 和 Bower 运行前期和后期编译脚本，以安装前端 javascript 和 css 库。
* 将 buildpack 从 Beta 状态移为 GA 状态

## 2016 年 7 月 11 日：更新了 ASP.NET 核心 buildpack V0.9-20160706-1603

此版本 buildpack 包含以下更改：

* 此版本 buildpack 支持 .NET CLI 1.0 Preview 2 构建版和 .NET 核心 1.0 RTM
* 该 buildpack 继续支持 .NET CLI 1.0 Preview 1 和 .NET 核心 1.0 RC2
* 现在，要安装的缺省 .NET CLI 版本为 1.0.0-preview2-003121

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
{: #rellinks notoc}
## 常规
{: #general notoc}
* [Dotnet 核心运行时](index.html)
