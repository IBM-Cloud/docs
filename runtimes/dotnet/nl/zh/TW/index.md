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

{{site.data.keyword.Bluemix}} 上的 ASP.NET Core 運行環境是採用 ASP.NET Core 建置套件的技術。ASP.NET Core 是模組化開放程式碼架構，用於建置 .NET Web 應用程式。
.Net Core 是 ASP.NET Core 應用程式可以設為目標的小型跨平台運行環境。
它們會合併，以啟用現代化雲端型 Web 應用程式。
{: shortdesc}

## 偵測
{: #detection}
如果應用程式中的任何位置有一個以上的資料夾同時包含 project.json 檔案以及至少一個 .cs 檔案，或是從 *dotnet publish* 指令的輸出目錄推送應用程式，就會使用 Bluemix ASP.NET Core 建置套件。

## 入門範本應用程式
{: #starter_application}

{{site.data.keyword.Bluemix}} 提供 ASP.NET Core 入門範本應用程式。ASP.NET Core 入門範本應用程式是簡單的應用程式，提供可以讓您使用的範本。您可以用入門範本應用程式進行實驗，並進行及推送對 Bluemix 環境的變更。如需關於使用入門範本應用程式的協助，請參閱[使用入門範本應用程式](/docs/cfapps/starter_app_usage.html)。

## 運行環境版本
{: #runtime_versions}

### 支援的版本
{: #supported_versions}
此建置套件支援下列版本，未來的建置套件版本將移除標示為已淘汰的版本。請參閱 [Microsoft 的 LTS 及 Current 版本的支援聲明](https://www.microsoft.com/net/core/support)。

#### project.json 工具（已淘汰）

| .NET SDK 版本        | 預設值 |
|-------------------------|---------|
| 1.0.0-preview2-003156   |   否    |
| 1.0.0-preview2-1-003177 |   否    |

#### MSBuild SDK 工具

| .NET SDK 版本        | 預設值 |
|-------------------------|---------|
| 1.0.0-preview4-004233   |   否    |
| 1.0.1                   |   是   |

#### .NET Core 運行環境版本

| .NET Core 運行環境版本 | 版本類型 | 預設值 |
|---------------------------|--------------|---------|
| 1.0.0                     | LTS          |   否    |
| 1.0.1                     | LTS          |   否    |
| 1.0.3                     | LTS          |   否    |
| 1.0.4                     | LTS          |   是   |
| 1.1.0                     | Current      |   否    |
| 1.1.1                     | Current      |   否    |

### 指定 .NET SDK 版本

控制應用程式根目錄中具有選用 global.json 的 .NET SDK 版本。例如：
```
   {
      "projects": [ "src" ],
      "sdk": {
        "version": "1.0.1"
      }
   }
```
{: codeblock}

如果未指定，則會使用最新「長期支援 (LTS)」運行環境的 MSBuild 工具。若要使用 project.json 工具，您可以指定上面所列的其中一個 project.json 版本，但也應該記住未來會移除這些版本。

## 自訂 NuGet 套件來源
{: #customizing_nuget_package_sources}

控制從應用程式根目錄的 NuGet.Config 檔案中下載應用程式相依關係的位置。例如：
```
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
   <packageSources>
      <add key="NuGet.org" value="https://api.nuget.org/v3/index.json"/>
   </packageSources>
   </configuration>
```
{: codeblock}

## 在本端開發應用程式
{: #developing_locally}

如需在本端執行 ASP.NET Core 應用程式的相關資訊，請參閱[開始使用 ASP.NET](http://docs.asp.net/en/latest/getting-started/index.html)。
為了最密切符合應用程式在 Bluemix 中的執行方式，請遵循適用於 .NET Core 的 Linux 指示，但不需要在 Linux 上開發應用程式。

Yeoman 工具可以用來產生新的專案範本（如[使用 Yeoman 建置專案](http://docs.asp.net/en/latest/client-side/yeoman.html)中所述）。

如需使用 Visual Studio 進行本端開發的相關資訊，請參閱[使用 Visual Studio 開發](/docs/starters/deploy_vs.html){: new_window}。

## 推送已發佈的應用程式
{: #pushing_published_app}

如果您要應用程式包含其所有必要的二進位檔，讓建置套件不需要下載任何外部二進位檔，則可以推送已發佈的*自行包含* 應用程式。如需自行包含應用程式的相關資訊，請參閱 [.NET Core 應用程式類型](https://docs.microsoft.com/en-us/dotnet/articles/core/app-types){: new_window}。

若要發佈應用程式，請發出指令，例如：
```
dotnet publish -r ubuntu.14.04-x64 
```
{: codeblock}

針對自行包含的應用程式，接著可以從下列位置推送應用程式：
```
  bin/<Debug|Release>/<framework>/<runtime>/publish
```
{: codeblock}
目錄。

針對可攜式應用程式，可以從下列位置推送應用程式：
```
  bin/<Debug|Release>/<framework>/publish
```
{:codeblock}
目錄。

也請注意，如果您是在應用程式中使用 manifest.yml 檔案，則可以在 manifest.yml 中指定發佈輸出資料夾的路徑。因此，推送應用程式時，就不需要位在該資料夾中。

## 部署包含多個專案的應用程式
{: #developing_apps_with_multiple_projects}

若要部署包含多個專案的應用程式，則需要指定您要建置套件將哪個專案執行為主要專案。作法是在解決方案的根資料夾中建立可設定主要專案路徑的 .deployment 檔案。主要專案的路徑可以指定為專案資料夾或專案檔（.xproj 或 .csproj）。

例如，如果解決方案在 *src* 資料夾中包含 *MyApp.DAL*、*MyApp.Services* 及 *MyApp.Web* 這三個專案，而且 *MyApp.Web* 是主要專案，則 .deployment 檔案的格式將如下所示：
```
  [config]
  project = src/MyApp.Web/MyApp.Web.csproj
```
{: codeblock}

在此範例中，建置套件將自動編譯 *MyApp.DAL* 及 *MyApp.Services* 專案（如果它們列為 *MyApp.Web* 之 project.json 檔案中的相依關係），但建置套件使用 dotnet run -p src/MyApp.Web 時只會嘗試執行主要專案 (*MyApp.Web*)。

## 應用程式配置
{: #application_configuration}

### 配置要在適當埠接聽的應用程式
{: #configuring_listen_proper_port}

建置套件將使用 *dotnet run* 指令來執行您的應用程式，以及傳遞下列指令行引數：
```
--server.urls http://0.0.0.0:${PORT}
```
{: codeblock}

您的應用程式需要將此引數傳遞給 kestrel，以確保 kestrel 正在接聽正確的埠。

若要實作此引數的傳遞作業，cli-samples 儲存庫中所提供的範例及 Visual Studio 所提供的範本需要稍加修改，才能部署至 Bluemix。

需要如下面範例中的註解所述，修改 Main 方法：

<pre>
  public static void Main(string[] args)
  {
    var config = new ConfigurationBuilder() //ADD THESE 3 LINES AT THE TOP OF THE MAIN METHOD
        .AddCommandLine(args)
        .Build();

    var host = new WebHostBuilder()
        .UseKestrel()
        .UseConfiguration(config) //ADD THIS LINE BEFORE 'UseStartup'
        .UseStartup&lt;Startup&gt;()        .Build();
    host.Run();
}
</pre>
{: codeblock}

針對 project.json 工具，將這一行新增至 project.json 檔案：
```
  "Microsoft.Extensions.Configuration.CommandLine": "1.0.1",
```
{: codeblock}

針對 MSBuild 工具，將這一行新增至 .csproj 檔案：
```
  <PackageReference Include="Microsoft.Extensions.Configuration.CommandLine" Version="1.0.1" />
```
{:codeblock}

將 *using* 陳述式新增至包含 Main 方法的檔案：
```
using Microsoft.Extensions.Configuration;
```
{: codeblock}

### 確定應用程式的建置輸出資料夾中具有所有必要檔案
{: #configure_output_files}

#### 使用 project.json 工具

將下列內容新增至 project.json 的 `buildOptions` 區段：
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

在 Startup.cs `Startup` 方法中，移除下列一行：
```
  .SetBasePath(env.ContentRootPath)
```
{: codeblock}

在 Program.cs `Main` 方法中，移除下列一行：
```
  .UseContentRoot(Directory.GetCurrentDirectory())
```
{: codeblock}

這些變更應該容許 .NET CLI 尋找應用程式的 `Views`，因為當 `dotnet run` 指令執行時，它們將立即複製至建置輸出。如果您的應用程式具有運行環境需要的任何其他檔案（例如 json 配置檔），則也應該將那些檔案新增至專案之 project.json 檔案中 `copyToOutput` 的 `include` 區段。

#### 使用 MSBuild 工具

將 `<Content>` 元素新增至 .csproj 檔案的 `<ItemGroup>` 元素：
```
  <ItemGroup>
    <Content Include="wwwroot/**/*;Areas/**/Views/*;Views/*;appsettings.json">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
      <CopyToPublishDirectory>Always</CopyToPublishDirectory>
    </Content>
  </ItemGroup>
```
{: codeblock}

在 Startup.cs `Startup` 方法中，移除下列一行：
```
  .SetBasePath(env.ContentRootPath)
```
{: codeblock}

在 Program.cs `Main` 方法中，移除下列一行：
```
  .UseContentRoot(Directory.GetCurrentDirectory())
```
{: codeblock}

這些變更應該容許 .NET CLI 尋找應用程式的 `Views`，因為當 `dotnet publish` 指令執行時，它們將立即複製到建置輸出。如果您的應用程式具有運行環境需要的任何其他檔案（例如 json 配置檔），則也應該將那些檔案新增至專案之 .csproj 檔案中 `Content` 元素的 `Include` 內容，並以分號區隔。

## 在 Release 配置中編譯應用程式（僅限 MSBuild）
{: #compiling_in_release_configuration}

現在，在編譯打包期間，使用 `dotnet publish` 指令來發佈 MSBuild 型專案。建置套件預設會在 `Debug` 配置中發佈應用程式。
若要在 `Release` 配置中發佈應用程式，請將 `PUBLISH_RELEASE_CONFIG` 環境變數設為 `true`。

您可以搭配使用 CloudFoundry CLI 與下列指令來執行這項作業：

```shell
  cf set-env <app_name> PUBLISH_RELEASE_CONFIG true
```

或者，您也可以在應用程式的 manifest.yml 檔案中設定此變數：

```yml
---
applications:
- name: sample-aspnetcore-app
  memory: 512M
  env:
    PUBLISH_RELEASE_CONFIG: true
```

## 停用 NuGet 套件快取
{: #disabling_the_nuget_package_cache}

在某些情況下，可能需要清除應用程式的 NuGet 套件快取。這麼做將會清除任何現有的已快取 NuGet 套件，並防止建置套件快取任何新的套件。

這項作業的作法是使用 CloudFoundry CLI，將 `CACHE_NUGET_PACKAGES` 環境變數設為 `false`：

```shell
  cf set-env <app_name> CACHE_NUGET_PACKAGES false
```

或者，您也可以在應用程式的 manifest.yml 檔案中將 `CACHE_NUGET_PACKAGES` 環境變數設為 `false`：

```yml
---
applications:
- name: sample-aspnetcore-app
  memory: 512M
  env:
    CACHE_NUGET_PACKAGES: false
```

## 使用自訂原生程式庫
{: #using_custom_native_libraries}

某些程式庫可能需要使用 NuGet 套件及一些原生程式庫檔案（.so 檔案）。若要搭配使用這些程式庫與建置套件，您應該將它們放在應用程式根資料夾中名為 "ld_library_path" 的資料夾。
在編譯打包期間，此建置套件會將此路徑自動新增至 `LD_LIBRARY_PATH` 環境變數。或者，您也可以在應用程式的 `manifest.yml` 檔案中指定 `LD_LIBRARY_PATH` 環境變數，或是使用 `cf set-env` 指令，以使用與 "ld_library_path" 不同的資料夾名稱。在此情況下，建置套件會將此自訂路徑附加至建置套件所產生的 `LD_LIBRARY_PATH`。

## 疑難排解常見問題 (FAQ)
{: #troubleshooting_faq}

**問**：我的應用程式無法部署，訊息為：`API/0App instance exited ... payload: {... "reason"=>"CRASHED", "exit_status"=>-1, ...}`。這表示什麼？

**答**：如果您在推送應用程式時收到類似訊息，最可能是因為應用程式超出記憶體或磁碟限額限制。增加應用程式的配額，即可解決此問題。

**問**：我的應用程式無法部署，訊息為：`Failed to compress droplet: signal: broken pipe` 或 `No space left on device`。如何修正這個問題？

**答**：從包含大量 NuGet 套件相依關係的原始碼中所推送的專案，有時可能會在啟用 NuGet 套件快取時造成此錯誤。將 `CACHE_NUGET_PACKAGES` 環境變數設為 `false`，即可停用快取。

# 相關鏈結
{: #rellinks notoc}
## 一般
{: #general notoc}
* [NuGet](https://docs.nuget.org/Consume/Overview){: new_window}
* [ASP.NET Core 概觀](http://docs.asp.net/en/latest/conceptual-overview/aspnet.html){: new_window}
