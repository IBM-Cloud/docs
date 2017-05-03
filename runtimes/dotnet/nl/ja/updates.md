---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-30"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# ASP.NET Core ビルドパックに対する最新の更新
{: #latest_updates}


aspnet ビルドパックの最新更新のリスト。

## 2017 年 3 月 29 日: ASP.NET Core ビルドパック v1.0.13-20170330-1023 の更新

* .NET Core ランタイム 1.0.4 のサポートを追加
* .NET Core ランタイム 1.1.1 のサポートを追加
* .NET Core SDK 1.0.1 のサポートを追加
* Node バージョンを 6.10.0 に更新
* .NET Core SDK 1.0.0-preview2-003131 のサポートを削除
* .NET Core SDK 1.0.0-preview3-004056 のサポートを削除

## 2017 年 1 月 31 日: ASP.NET Core ビルドパック v1.0.10-20170124-1145 の更新

* .NET Core 1.0.3 のサポートを追加
* .NET Core MSBuild ツールのサポートを追加
* F# プロジェクトのサポートを追加
* .NET Core SDK 1.0.0-preview2-003121 のサポートを削除

## 2016 年 12 月 9 日: ASP.NET Core ビルドパック v1.0.6-20161205-0912 の更新

* .NET Core 1.1.0 のサポートを追加
* .NET Core 1.0.0 RC2 のサポートを削除
* NuGet パッケージのキャッシュをクリアするオプションを追加

## 2016 年 10 月 10 日: ASP.NET Core ビルドパック v1.0.1-20161005-1225 の更新

* .NET Core 1.0.1 のサポートの追加
* NuGet パッケージのキャッシュ時にデプロイメントが失敗する原因になった偶発的な問題の修正

## 2016 年 8 月 31 日: 更新された ASP.NET Core ビルドパック v1.0-20160826-1345

* NPM および Bower を使用してプリコンパイル・スクリプトとポストコンパイル・スクリプトを実行するためのサポートを追加して、フロントエンド JavaScript ライブラリーと css ライブラリーをインストールします。
* ビルドパックをベータ状況から GA 状況に移行します。

## 2016 年 7 月 11 日: 更新された ASP.NET Core ビルドパック v0.9-20160706-1603

このバージョンのビルドパックには、以下の変更が含まれています。

* このバージョンのビルドパックは、.NET CLI 1.0 Preview 2 ビルドおよび .NET Core 1.0 RTM をサポートします
* このビルドパックでは .NET CLI 1.0 Preview 1 および .NET Core 1.0 RC2 のサポートを継続します
* インストールされるデフォルトの .NET CLI バージョンは現在、1.0.0-preview2-003121 です

## 2016 年 6 月 10 日: ASP.NET Core ビルドパック v0.8.1-20160526-0957 の更新

このバージョンのビルドパックには、以下の変更が含まれています。

* ランタイムの名前が ASP.NET 5 から ASP.NET Core に変更されています。
* ビルドパックのバージョン番号が検出スクリプトの出力に含まれています。
* このバージョンのビルドパックでは、CoreCLR RC1 以下を使用している DNX ベースのアプリケーションのサポートが削除されます。
* このバージョンのビルドパックは、.NET CLI および .NET Core RC2 をサポートします。
* ビルドパックは、project.json ファイルまたはパブリッシュの出力からの *.runtimeconfig.json ファイルを使用して、プロジェクトを検出します。

## 2015 年 10 月 22 日: ASP.NET 5 ビルドパック v0.7-20151022-1257 の更新

* このバージョンのビルドパックは、Mono を削除し、代わりに Beta 8 CoreCLR をサポートします。

## 2015 年 9 月 18 日: ASP.NET 5 ビルドパック v0.6-20150916-1220 の更新

* このバージョンのビルドパックは Beta 7 DNX の変更に対応しており、以下のカスタム開始コマンドを使用して、以前のベータ版に依存するアプリケーションを実行できます。

```
   dnx src/dotnetstarter kestrel --server.urls http://${VCAP_APP_HOST}:${PORT}
```
{: codeblock}

* Nowin Web サーバーの使用はこのビルドパックから削除され、代わりに [Kestrel]{https://github.com/aspnet/KestrelHttpServer} Web サーバーが使用されます。

# 関連リンク
{: #rellinks notoc}
## 一般
{: #general notoc}
* [Dotnet Core ランタイム](index.html)
