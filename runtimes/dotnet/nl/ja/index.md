---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-14"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# ASP.NET Core 
{: #dotnet_core}

{{site.data.keyword.Bluemix}} の ASP.NET Core ランタイムには ASP.NET Core ビルドパックが採用されています。ASP.NET Core は、.NET Web アプリケーションをビルドするためのオープン・ソースのモジュラー・フレームワークです。
.Net Core は、ASP.NET Core アプリケーションのターゲットにできる小規模なクロスプラットフォーム・ランタイムです。
この組み合わせによって、最新のクラウド・ベース Web アプリケーションが使用可能になります。
{: shortdesc}

# サポート対象のバージョン
{: #supported_versions}
このビルドパックでは、以下のバージョンがサポートされます。非推奨としてマークされているバージョンは、将来のビルドパックのリリースで削除されます。

1. .NET Core 1.0.0-rc2-final (ベータ) (非推奨)
2. .NET Core 1.0.0
3. .NET Core 1.0.1

## 検出
{: #detection}
アプリケーションのどこかに project.json ファイルと少なくとも 1 つの .cs ファイルの両方を含むフォルダーが 1 つ以上存在する場合、あるいはアプリケーションが *dotnet publish* コマンドの出力ディレクトリーからプッシュされた場合、Bluemix ASP.NET Core ビルドパックが使用されます。

## スターター・アプリケーション
{: #starter_application}

{{site.data.keyword.Bluemix}} には、ASP.NET Core スターター・アプリケーションが用意されています。ASP.NET Core スターター・アプリケーションは、使用可能なテンプレートを提供する、シンプルなアプリケーションです。スターター・アプリケーションを試し、Bluemix 環境に対して変更を行い、プッシュすることができます。スターター・アプリケーションの使用に関するヘルプについては、[『スターター・アプリケーションの使用』](/docs/cfapps/starter_app_usage.html)を参照してください。

## ランタイム・バージョン
{: #runtime_versions}

### .NET CLI バージョンの指定

アプリケーションのルート・ディレクトリーにあるオプションの global.json を使用して、.NET CLI バージョンを制御します。例えば、次のように指定します。
```
   {
      "projects": [ "src" ],
      "sdk": {
        "version": "1.0.0-preview2-003121"
      }
   }
```
{: codeblock}

サポート対象の CLI バージョンのリストについては、[ASP.NET Core ビルドパックに対する最新の更新](/docs/runtimes/dotnet/updates.html)を参照してください。指定されていない場合、最新の安定したリリース候補が使用されます。

### NuGet パッケージ・ソースのカスタマイズ

アプリケーションのルート・ディレクトリーにある NuGet.Config ファイルで、アプリケーションの依存関係のダウンロード元を制御します。例えば、次のように指定します。
```
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
   <packageSources>
      <add key="NuGet.org" value="https://api.nuget.org/v3/index.json"/>
   </packageSources>
   </configuration>
```
{: codeblock}

## ローカルでのアプリケーションの開発
{: #developing_locally}

ローカルでの ASP.NET Core アプリケーションの実行について詳しくは、[『Getting	Started with ASP.NET』](http://docs.asp.net/en/latest/getting-started/index.html)を参照してください。Bluemix でのアプリケーションの実行方法に最も厳密に適合させるには、.NET Core に関する Linux の手順に従ってください。ただし、Linux 上でアプリケーションを開発する必要はありません。

[『Building Projects with Yeoman』](http://docs.asp.net/en/latest/client-side/yeoman.html)に説明されているように、Yeoman ツールを使用して新規プロジェクトのテンプレートを生成できます。

Visual Studio を使用したローカルでの開発については、[『Visual Studio を使用した開発』](/docs/starters/deploy_vs.html){: new_window}を参照してください。

## パブリッシュされたアプリケーションのプッシュ
{: #pushing_published_app}

ビルドパックが外部のバイナリーをダウンロードしないように、アプリケーションに必要なバイナリーをすべて組み込む場合、パブリッシュされた*自己完結型*アプリケーションをプッシュすることができます。自己完結型アプリケーションについて詳しくは、[『.NET Core App Types』](https://docs.microsoft.com/en-us/dotnet/articles/core/app-types){: new_window}を参照してください。

アプリケーションをパブリッシュするには、次のようなコマンドを発行します。
```
  dotnet publish -r ubuntu.14.04-x64
```
{: codeblock}
  
次に、以下のディレクトリーからアプリケーションをプッシュできます。
```
  bin/<Debug|Release>/<framework>/<runtime>/publish
```
{: codeblock}

また、アプリケーションで manifest.yml ファイルを使用している場合は、manifest.yml でパブリッシュ出力フォルダーへのパスを指定できます。これにより、アプリケーションをプッシュする際に、そのフォルダーに入る必要がなくなります。

## 複数のプロジェクトを含むアプリケーションのデプロイ
{: #developing_apps_with_multiple_projects}

複数のプロジェクトを含むアプリケーションをデプロイする場合、どのプロジェクトをビルドパックでメイン・プロジェクトとして実行するかを指定する必要があります。これを行うには、ソリューションのルート・フォルダー内に、メイン・プロジェクトへのパスを設定する .deployment ファイルを作成します。メイン・プロジェクトへのパスは、プロジェクト・フォルダーまたはプロジェクト・ファイル (.xproj または .csproj) として指定できます。

例えば、あるソリューションの *src* フォルダー内に 3 つのプロジェクト *MyApp.DAL*、*MyApp.Services*、および *MyApp.Web* が含まれており、*MyApp.Web* がメイン・プロジェクトである場合、.deployment ファイルのフォーマットは、次のようになります。
```
  [config]
  project = src/MyApp.Web
```
{: codeblock}

この例では、*MyApp.DAL* プロジェクトと *MyApp.Services* プロジェクトが *MyApp.Web* の project.json ファイルに依存関係としてリストされている場合、ビルドパックはこれらのプロジェクトを自動的にコンパイルします。しかし、dotnet run -p src/MyApp.Web コマンドを使用した場合は、ビルドパックはメイン・プロジェクトである *MyApp.Web* の実行のみを試みます。*MyApp.Web* へのパスは、このプロジェクトが xproj プロジェクトであると想定して、以下のように指定することもできます。 
```
  project = src/MyApp.Web/MyApp.Web.xproj
```
{: codeblock}

## 正しいポートで listen するようにアプリケーションを構成
{: #configuring_listen_proper_port}

ビルドパックは、*dotnet run* コマンドを使用してアプリケーションを実行し、後続のコマンド・ライン引数を渡します。
```
  --server.urls http://0.0.0.0:${PORT}
```
{: codeblock}

kestrel が正しいポートで listen するようにするために、アプリケーションはこの引数を kestrel に渡す必要があります。

この引数の引き渡しを実装するには、Bluemix にデプロイする前に、cli-samples リポジトリーで提供されているサンプルおよび Visual Studio によって提供されるテンプレートを多少変更する必要があります。

以下の例のコメントに示されているように、Main メソッドに対する変更が必要です。

<pre>
  public static void Main(string[] args)
  {
    var config = new ConfigurationBuilder() //Main メソッドの先頭にこの 3 行を追加します
        .AddCommandLine(args)
        .Build();

    var host = new WebHostBuilder()
        .UseKestrel()
        .UseConfiguration(config) //「UseStartup」の前にこの行を追加します
        .UseStartup&lt;Startup&gt;()        .Build();
    host.Run();
}
</pre>
{: codeblock}

以下の依存関係を project.json に追加します。 
```
  "Microsoft.Extensions.Configuration.CommandLine": "1.0.0",
```
{: codeblock}

以下のプロパティーを project.json の `buildOptions` セクションに追加します。
```
  "copyToOutput": {
    "include": [
      "wwwroot",
      "Areas/**/Views",
      "Views",
      "appsettings.json"
    ]
  }
```
{: codeblock}

main メソッドを含むファイルに、*using* ステートメントを追加します。 
```
  using Microsoft.Extensions.Configuration;
```
{: codeblock}

Startup.cs の `Startup` メソッドで、次の行を削除します。
```
  .SetBasePath(env.ContentRootPath)
```
{: codeblock}

Program.cs の `Main` メソッドで、次の行を削除します。
```
  .UseContentRoot(Directory.GetCurrentDirectory())
```
{: codeblock}

これらの変更により、.NET CLI がアプリケーションの `Views` を見つけることができます。これは、`dotnet run` コマンドの実行時にビルド出力にコピーされるようになるためです。JSON 構成ファイルなど、実行時に必要な他のファイルがアプリケーションにある場合、これらのファイルも project.json ファイルの `copyToOutput` の `include` セクションに追加する必要があります。

## トラブルシューティングに関するよくある質問
{: #troubleshooting_faq}

**Q**: アプリケーションがデプロイに失敗し、メッセージ `API/0App instance exited ... payload: {... "reason"=>"CRASHED", "exit_status"=>-1, ...}` が出されます。これは何を意味するのでしょうか。

**A**: アプリケーションのプッシュ時にも同様のメッセージを受け取っている場合、最も考えられる原因は、ご使用のアプリケーションがメモリーまたはディスクの割り当て量制限を超えていることです。これは、アプリケーションに対する割り当て量を増やすことで解決できます。

# 関連リンク
{: #rellinks}
## 一般
{: #general}
* [ASP.NET Core ビルドパックに対する最新の更新](updates.html)
* [NuGet](https://docs.nuget.org/Consume/Overview){: new_window}
* [ASP.NET Core Overview](http://docs.asp.net/en/latest/conceptual-overview/aspnet.html){: new_window}
