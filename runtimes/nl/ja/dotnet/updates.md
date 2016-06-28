---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# ASP.NET Core ビルドパックに対する最新の更新
{: #latest_updates}

*最終更新日時: 2016 年 6 月 10 日*


aspnet ビルドパックの最新更新のリスト。

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
{: #rellinks}
## 一般
{: #general}
* [Dotnet Core ランタイム](index.html)
