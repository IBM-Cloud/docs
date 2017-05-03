---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-06"
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

## 検出
{: #detection}
アプリケーションのどこかに project.json ファイルと少なくとも 1 つの .cs ファイルの両方を含むフォルダーが 1 つ以上存在する場合、あるいはアプリケーションが *dotnet publish* コマンドの出力ディレクトリーからプッシュされた場合、Bluemix ASP.NET Core ビルドパックが使用されます。

## スターター・アプリケーション
{: #starter_application}

{{site.data.keyword.Bluemix}} には、ASP.NET Core スターター・アプリケーションが用意されています。ASP.NET Core スターター・アプリケーションは、使用可能なテンプレートを提供する、シンプルなアプリケーションです。スターター・アプリケーションを試し、Bluemix 環境に対して変更を行い、プッシュすることができます。スターター・アプリケーションの使用に関するヘルプについては、[『スターター・アプリケーションの使用』](/docs/cfapps/starter_app_usage.html)を参照してください。

## ランタイム・バージョン
{: #runtime_versions}

### サポート対象のバージョン
{: #supported_versions}
このビルドパックでは、以下のバージョンがサポートされます。非推奨としてマークされているバージョンは、将来のビルドパックのリリースで削除されます。[Microsoft による LTS および現行リリースに関するサポート記述](https://www.microsoft.com/net/core/support)を参照してください。

#### project.json ツール (非推奨)

| .NET SDK バージョン        | デフォルト |
|-------------------------|---------|
| 1.0.0-preview2-003156   |   いいえ    |
| 1.0.0-preview2-1-003177 |   いいえ    |

#### MSBuild SDK ツール

| .NET SDK バージョン        | デフォルト |
|-------------------------|---------|
| 1.0.0-preview4-004233   |   いいえ    |
| 1.0.1                   |   はい   |

#### .NET Core ランタイムのバージョン

| .NET Core ランタイムのバージョン | リリース・タイプ | デフォルト |
|---------------------------|--------------|---------|
| 1.0.0                     | LTS          |   いいえ    |
| 1.0.1                     | LTS          |   いいえ    |
| 1.0.3                     | LTS          |   いいえ    |
| 1.0.4                     | LTS          |   はい   |
| 1.1.0                     | 現行      |   いいえ    |
| 1.1.1                     | 現行      |   いいえ    |

### .NET SDK バージョンの指定

アプリケーションのルート・ディレクトリーにあるオプションの global.json を使用して、.NET SDK バージョンを制御します。例えば、次のように指定します。
```
   {
      "projects": [ "src" ],
      "sdk": {
        "version": "1.0.1"
      }
   }
```
{: codeblock}

指定されていない場合、最新の長期サポート (LTS) ランタイムの MSBuild ツールが使用されます。project.json ツールを使用するために、上にリストされている project.json バージョンのいずれかを指定できますが、それらのバージョンは将来削除される予定であることにも留意してください。

## NuGet パッケージ・ソースのカスタマイズ
{: #customizing_nuget_package_sources}

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

自己完結型アプリケーションの場合、次に、以下のディレクトリーからアプリケーションをプッシュできます。
```
  bin/<Debug|Release>/<framework>/<runtime>/publish
```
{: codeblock}

ポータブル・アプリケーションの場合、以下のディレクトリーからアプリケーションをプッシュできます。
```
  bin/<Debug|Release>/<framework>/publish
```
{:codeblock}

また、アプリケーションで manifest.yml ファイルを使用している場合は、manifest.yml でパブリッシュ出力フォルダーへのパスを指定できます。これにより、アプリケーションをプッシュする際に、そのフォルダーに入る必要がなくなります。

## 複数のプロジェクトを含むアプリケーションのデプロイ
{: #developing_apps_with_multiple_projects}

複数のプロジェクトを含むアプリケーションをデプロイする場合、どのプロジェクトをビルドパックでメイン・プロジェクトとして実行するかを指定する必要があります。これを行うには、ソリューションのルート・フォルダー内に、メイン・プロジェクトへのパスを設定する .deployment ファイルを作成します。メイン・プロジェクトへのパスは、プロジェクト・フォルダーまたはプロジェクト・ファイル (.xproj または .csproj) として指定できます。

例えば、あるソリューションの *src* フォルダー内に 3 つのプロジェクト *MyApp.DAL*、*MyApp.Services*、および *MyApp.Web* が含まれており、*MyApp.Web* がメイン・プロジェクトである場合、.deployment ファイルのフォーマットは、次のようになります。
```
  [config]
  project = src/MyApp.Web/MyApp.Web.csproj
```
{: codeblock}

この例では、*MyApp.DAL* プロジェクトと *MyApp.Services* プロジェクトが *MyApp.Web* の project.json ファイルに依存関係としてリストされている場合、ビルドパックはこれらのプロジェクトを自動的にコンパイルします。しかし、dotnet run -p src/MyApp.Web コマンドを使用した場合は、ビルドパックはメイン・プロジェクトである *MyApp.Web* の実行のみを試みます。

## アプリケーション構成
{: #application_configuration}

### 正しいポートで listen するようにアプリケーションを構成
{: #configuring_listen_proper_port}

ビルドパックは、*dotnet run* コマンドを使用してアプリケーションを実行し、後続のコマンド・ライン引数を渡します。
```
  --server.urls http://0.0.0.0:${PORT}
```
{: codeblock}

kestrel が正しいポートで listen するようにするために、アプリケーションはこの引数を kestrel に渡す必要があります。

この引数の引き渡しを実装するには、Bluemix にデプロイする前に、cli-samples リポジトリーで提供されているサンプルおよび Visual Studio によって提供されるテンプレートを多少変更する必要が生じます。

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

project.json ツールの場合、以下の行を project.json ファイルに追加します。
```
  "Microsoft.Extensions.Configuration.CommandLine": "1.0.1",
```
{: codeblock}

MSBuild ツールの場合、以下の行を .csproj ファイルに追加します。
```
  <PackageReference Include="Microsoft.Extensions.Configuration.CommandLine" Version="1.0.1" />
```
{:codeblock}

main メソッドを含むファイルに、*using* ステートメントを追加します。
```
  using Microsoft.Extensions.Configuration;
```
{: codeblock}

### アプリケーションでビルド出力フォルダー内に必要なすべてのファイルが含まれていることの確認
{: #configure_output_files}

#### project.json ツールの使用

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

これらの変更により、.NET CLI がアプリケーションの `Views` を見つけることができます。これは、`dotnet run` コマンドの実行時にビルド出力にコピーされるようになるためです。JSON 構成ファイルなど、実行時に必要な他のファイルがアプリケーションにある場合、これらのファイルもプロジェクトの project.json ファイルの `copyToOutput` の `include` セクションに追加する必要があります。

#### MSBuild ツールの使用

以下のように、`<Content>` エレメントを .csproj ファイルの `<ItemGroup>` エレメントに追加します。
```
  <ItemGroup>
    <Content Include="wwwroot/**/*;Areas/**/Views/*;Views/*;appsettings.json">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
      <CopyToPublishDirectory>Always</CopyToPublishDirectory>
    </Content>
  </ItemGroup>
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

これらの変更により、.NET CLI がアプリケーションの `Views` を見つけることができます。これは、`dotnet publish` コマンドの実行時にビルド出力にコピーされるようになるためです。JSON 構成ファイルなど、実行時に必要な他のファイルがアプリケーションにある場合、これらのファイルも、セミコロン区切りでプロジェクトの .csproj ファイルの `Content` エレメントの `Include` プロパティーに追加する必要があります。

## Release 構成でのアプリケーションのコンパイル (MSBuild の場合のみ)
{: #compiling_in_release_configuration}

MSBuild ベースのプロジェクトは、ステージング時に `dotnet publish` コマンドを使用してパブリッシュされるようになっています。デフォルトでは、ビルドパックは、`Debug` 構成でアプリケーションをパブリッシュします。
`Release` 構成でアプリケーションをパブリッシュするには、`PUBLISH_RELEASE_CONFIG` 環境変数を `true` に設定します。

これを行うには、CloudFoundry CLI で以下のコマンドを使用します。

```shell
  cf set-env <app_name> PUBLISH_RELEASE_CONFIG true
```

あるいは、アプリケーションの manifest.yml ファイルに以下のように変数を設定することもできます。

```yml
---
applications:
- name: sample-aspnetcore-app
  memory: 512M
  env:
    PUBLISH_RELEASE_CONFIG: true
```

## NuGet パッケージのキャッシュの無効化
{: #disabling_the_nuget_package_cache}

場合によっては、アプリケーションの NuGet パッケージのキャッシュをクリアする必要が生じることがあります。そうすることにより、キャッシュに入れられている既存の NuGet パッケージがクリアされ、ビルドパックで新規パッケージがキャッシュに入れられなくなります。

これを行うには、CloudFoundry CLI を使用して以下のように `CACHE_NUGET_PACKAGES` 環境変数を `false` に設定します。

```shell
  cf set-env <app_name> CACHE_NUGET_PACKAGES false
```

あるいは、アプリケーションの manifest.yml ファイルで、以下のように `CACHE_NUGET_PACKAGES` 環境変数を `false` に設定することもできます。

```yml
---
applications:
- name: sample-aspnetcore-app
  memory: 512M
  env:
    CACHE_NUGET_PACKAGES: false
```

## カスタム・ネイティブ・ライブラリーの使用
{: #using_custom_native_libraries}

一部のライブラリーでは、NuGet パッケージとネイティブ・ライブラリー・ファイル (.so ファイル) の両方を使用する必要がある場合があります。ビルドパックでこれらのライブラリーを使用するには、アプリケーションのルート・フォルダー内の「ld_library_path」という名前のフォルダーに当該ライブラリーを配置する必要があります。
ビルドパックでは、ステージング時に、このパスが `LD_LIBRARY_PATH` 環境変数に自動的に追加されます。あるいは、アプリケーションの `manifest.yml` ファイルで、または `cf set-env` コマンドを使用して、「ld_library_path」以外のフォルダー名を使用するように `LD_LIBRARY_PATH` 環境変数を指定できます。その場合、ビルドパックでは、ビルドパックによって生成される `LD_LIBRARY_PATH` にそのカスタム・パスが追加されます。

## トラブルシューティングに関するよくある質問
{: #troubleshooting_faq}

**Q**: アプリケーションがデプロイに失敗し、メッセージ `API/0App instance exited ... payload: {... "reason"=>"CRASHED", "exit_status"=>-1, ...}` が出されます。これは何を意味するのでしょうか。

**A**: アプリケーションのプッシュ時にも同様のメッセージを受け取っている場合、最も考えられる原因は、ご使用のアプリケーションがメモリーまたはディスクの割り当て量制限を超えていることです。これは、アプリケーションに対する割り当て量を増やすことで解決できます。

**Q**: アプリケーションがデプロイに失敗し、「`Failed to compress droplet: signal: broken pipe`」または「`No space left on device`」というメッセージが出されます。これを修正する方法を教えてください。

**A**: 多数の NuGet パッケージ依存関係が含まれているソース・コードからプッシュされるプロジェクトでは、NuGet パッケージのキャッシュが有効になっている場合に、このエラーが発生することがあります。`CACHE_NUGET_PACKAGES` 環境変数を `false` に設定して、キャッシュを無効にしてください。

# 関連リンク
{: #rellinks notoc}
## 一般
{: #general notoc}
* [NuGet](https://docs.nuget.org/Consume/Overview){: new_window}
* [ASP.NET Core Overview](http://docs.asp.net/en/latest/conceptual-overview/aspnet.html){: new_window}
