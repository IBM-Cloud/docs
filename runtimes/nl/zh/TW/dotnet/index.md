---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# ASP.NET Core 
{: #dotnet_core}
*前次更新：2016 年 5 月 30 日*

{{site.data.keyword.Bluemix}} 上的 ASP.NET Core 運行環境是採用 ASP.NET Core 建置套件的技術。ASP.NET Core 是模組化開放程式碼架構，用於建置 .NET Web 應用程式。
.Net Core 是 ASP.NET Core 應用程式可以設為目標的小型跨平台運行環境。
它們會合併，以啟用現代化雲端型 Web 應用程式。
{: shortdesc}

## 偵測
{: #detection}
如果應用程式中的任何位置有一個以上的 project.json 檔案，或是從 *dotnet publish* 指令的輸出目錄中推送應用程式，則會使用 Bluemix ASP.NET Core 建置套件。

## 入門範本應用程式
{: #starter_application}

{{site.data.keyword.Bluemix}} 提供 ASP.NET Core 入門範本應用程式。ASP.NET Core 入門範本應用程式是簡單的應用程式，提供可以讓您使用的範本。您可以用入門範本應用程式進行實驗，並進行及推送對 Bluemix 環境的變更。如需關於使用入門範本應用程式的協助，請參閱[使用入門範本應用程式](../../cfapps/starter_app_usage.html)。

## 運行環境版本
{: #runtime_versions}

### 指定 .NET CLI 版本

控制應用程式根目錄中具有選用 global.json 的 .NET CLI 版本。例如：
```
   {
      "projects": [ "src" ],
      "sdk": {
        "version": "1.0.0-preview1-002702"
      }
   }
```
{: codeblock}

如果未指定，則會使用最新的穩定「候選版本」。

### 自訂 NuGet 套件來源

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

## 推送已發佈的應用程式

如果您要應用程式包含其所有必要的二進位檔，讓建置套件不需要下載任何外部二進位檔，則可以推送已發佈的*自行包含* 應用程式。如需自行包含應用程式的相關資訊，請參閱 [.Net Core 中的可攜性類型](http://dotnet.github.io/docs/core-concepts/app-types.html){: new_window}。

若要發佈應用程式，請發出指令，例如：
```
  dotnet publish -r ubuntu.14.04-x64 
```
{: codeblock}
  
接著可以從下列位置推送應用程式：
```
  bin/<Debug|Release>/<framework>/<runtime>/publish
```
{: codeblock}
目錄。

也請注意，如果您是在應用程式中使用 manifest.yml 檔案，則可以在 manifest.yml 中指定發佈輸出資料夾的路徑。因此，推送應用程式時，就不需要位在該資料夾中。

## 部署包含多個專案的應用程式

若要部署包含多個專案的應用程式，則需要指定您要建置套件將哪個專案執行為主要專案。作法是在解決方案的根資料夾中建立可設定主要專案路徑的 .deployment 檔案。主要專案的路徑可以指定為專案資料夾或專案檔（.xproj 或 .csproj）。

例如，如果解決方案在 *src* 資料夾中包含 *MyApp.DAL*、*MyApp.Services* 及 *MyApp.Web* 這三個專案，而且 *MyApp.Web* 是主要專案，則 .deployment 檔案的格式將如下所示：
```
  [config]
  project = src/MyApp.Web
```
{: codeblock}

在此範例中，建置套件將自動編譯 *MyApp.DAL* 及 *MyApp.Services* 專案（如果它們列為 *MyApp.Web* 之 project.json 檔案中的相依關係），但建置套件使用 dotnet run -p src/MyApp.Web 時只會嘗試執行主要專案 (*MyApp.Web*)。*MyApp.Web*（假設此專案是 xproj 專案）的路徑也可以指定為： 
```
  project = src/MyApp.Web/MyApp.Web.xproj 
```
{: codeblock}

## 使用 cli-samples 儲存庫中的範例和 Visual Studio 範本

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
        .UseStartup&lt;Startup&gt;()  
        .Build();
    host.Run();
}
</pre>  
{: codeblock}

將下列相依關係新增至 project.json： 
```
  "Microsoft.Extensions.Configuration.CommandLine": "1.0.0-rc2-final",
```
{: codeblock}

將 *using* 陳述式新增至包含 Main 方法的檔案： 
```
  using Microsoft.Extensions.Configuration;
```
{: codeblock}

# 相關鏈結
{: #rellinks}
## 一般
{: #general}
* [ASP.NET Core 建置套件的最新更新項目](updates.html)
* [NuGet](https://docs.nuget.org/Consume/Overview){: new_window}
* [ASP.NET Core 概觀](http://docs.asp.net/en/latest/conceptual-overview/aspnet.html){: new_window}
