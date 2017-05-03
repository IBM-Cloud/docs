---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-06"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# ASP.NET 核心
{: #dotnet_core}

{{site.data.keyword.Bluemix}} 上的“ASP.NET 核心”运行时采用“ASP.NET 核心”buildpack 技术。“ASP.NET 核心”是用于构建 .NET Web 应用程序的模块化开放式源代码框架。“.Net 核心”是跨平台的小型运行时，可由“ASP.NET 核心”应用程序实现。将它们相结合可实现基于云的先进 Web 应用程序。
{: shortdesc}

## 检测
{: #detection}
如果应用程序中的任何位置存在一个或多个包含 project.json 文件和至少一个 .cs 文件的文件夹，或者应用程序是从 *dotnet publish* 命令的输出目录进行推送，那么将使用 Bluemix 的“ASP.NET 核心”buildpack。

## 入门模板应用程序
{: #starter_application}

{{site.data.keyword.Bluemix}} 提供了“ASP.NET 核心”入门模板应用程序。“ASP.NET 核心”入门模板应用程序是一个简单的应用程序，它提供了一个可供您使用的模板。您可以体验该入门模板应用程序，对其进行更改并将更改推送到 Bluemix 环境。有关使用入门模板应用程序的帮助，请参阅[使用入门模板应用程序](/docs/cfapps/starter_app_usage.html)。

## 运行时版本
{: #runtime_versions}

### 受支持的版本
{: #supported_versions}
此 buildpack 支持以下版本，那些标记为不推荐的版本将在未来 buildpack 发行版中除去。请参阅 [Microsoft 对 LTS 和当前发行版的支持声明](https://www.microsoft.com/net/core/support)。

#### project.json 工具（不推荐）

| .NET SDK 版本           | 缺省    |
|-------------------------|---------|
| 1.0.0-preview2-003156   |   否    |
| 1.0.0-preview2-1-003177 |   否    |

#### MSBuild SDK 工具

| .NET SDK 版本           | 缺省    |
|-------------------------|---------|
| 1.0.0-preview4-004233   |   否    |
| 1.0.1                   |   是   |

#### .NET 核心运行时版本

| .NET 核心运行时版本       | 发行版类型   | 缺省    |
|---------------------------|--------------|---------|
| 1.0.0                     | LTS          |   否    |
| 1.0.1                     | LTS          |   否    |
| 1.0.3                     | LTS          |   否    |
| 1.0.4                     | LTS          |   是    |
| 1.1.0                     | 当前         |   否    |
| 1.1.1                     | 当前         |   否    |

### 指定 .NET SDK 版本

使用应用程序根目录中的可选 global.json 来控制 .NET SDK 版本。例如：
```
   {
      "projects": [ "src" ],
      "sdk": {
        "version": "1.0.1"
      }
   }
```
{: codeblock}

如果未指定，将使用最新的长期支持 (LTS) 运行时的 MSBuild 工具。要使用 project.json 工具，可以指定上面列出的其中一个 project.json 版本，但同时应该谨记这些版本未来将会除去。

## 定制 NuGet 数据包源
{: #customizing_nuget_package_sources}

在应用程序根目录中的 NuGet.Config 文件中控制应用程序依赖项的下载来源位置。例如：
```
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
   <packageSources>
      <add key="NuGet.org" value="https://api.nuget.org/v3/index.json"/>
   </packageSources>
   </configuration>
```
{: codeblock}

## 在本地开发应用程序
{: #developing_locally}

有关在本地运行“ASP.NET 核心”应用程序的更多信息，请参阅 [ASP.NET 入门](http://docs.asp.net/en/latest/getting-started/index.html)。要尽量匹配应用程序在 Bluemix 中的运行方式，请遵循 Linux 中有关“.NET 核心”的指示信息，但无需在 Linux 上开发应用程序。

使用 Yeoman 工具可生成新的项目模板，如 [Building Projects with Yeoman](http://docs.asp.net/en/latest/client-side/yeoman.html) 中所述。

有关使用 Visual Studio 进行本地开发的信息，请参阅[使用 Visual Studio 进行开发](/docs/starters/deploy_vs.html){: new_window}。

## 推送发布的应用程序
{: #pushing_published_app}

如果想要在应用程序中包含其需要的所有二进制文件，以使 buildpack 无需下载任何外部二进制文件，您可以推送发布的*自包含*应用程序。请参阅 [.NET Core App Types](https://docs.microsoft.com/en-us/dotnet/articles/core/app-types){: new_window}，以获取有关自包含应用程序的更多信息。

要发布应用程序，请发出类似如下命令：
```
dotnet publish -r ubuntu.14.04-x64 
```
{: codeblock}

对于自包含应用程序，然后可以从 
```
  bin/<Debug|Release>/<framework>/<runtime>/publish
```
{: codeblock}
目录推送应用程序。

对于可移植应用程序，可以从 
```
  bin/<Debug|Release>/<framework>/publish
```
{:codeblock}
目录推送应用程序。

另请注意，如果在应用程序中使用 manifest.yml 文件，您可以在 manifest.ymle 中指定发布输出文件夹的路径。之后在推送应用程序时，您无需位于该文件夹中。

## 部署包含多个项目的应用程序
{: #developing_apps_with_multiple_projects}

要部署包含多个项目的应用程序，您需要指定希望 buildpack 将哪个项目作为主要项目运行。在解决方案的根文件夹中创建 .deployment 文件来设置主要项目的路径即可完成此操作。您可以将主要项目的路径指定为项目文件夹或项目文件（.xproj 或 .csproj）。

例如，如果解决方案的 *src* 文件夹中包含 *MyApp.DAL*、*MyApp.Services* 和 *MyApp.Web* 这三个项目，其中 *MyApp.Web* 是主要项目，那么 .deployment 文件的格式应如下所示：
```
  [config]
  project = src/MyApp.Web/MyApp.Web.csproj
```
{: codeblock}

在此示例中，如果在 project.json 文件中将 *MyApp.DAL* 和 *MyApp.Services* 项目列为 *MyApp.Web* 的依赖项，那么 buildpack 会自动编译这两个项目，但 buildpack 只会尝试使用 dotnet run -p src/MyApp.Web 执行主要项目 *MyApp.Web*。

## 应用程序配置
{: #application_configuration}

### 配置应用程序以侦听正确的端口
{: #configuring_listen_proper_port}

buildpack 将使用 *dotnet run* 命令运行您的应用程序，并传递以下内容之后的命令行自变量
```
--server.urls http://0.0.0.0:${PORT}
```
{: codeblock}

应用程序需要将此自变量传递到 kestrel，以确保 kestrel 侦听正确的端口。

要实现此自变量的传递，需要对 cli 样本存储库中提供的样本以及 Visual Studio 提供的模板稍作修改，然后再部署到 Bluemix。

您需要根据以下示例中的注释对 Main 方法进行修改：

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

对于 project.json 工具，请将以下行添加到 project.json 文件：
```
  "Microsoft.Extensions.Configuration.CommandLine": "1.0.1",
```
{: codeblock}

对于 MSBuild 工具，请将以下行添加到 .csproj 文件：
```
  <PackageReference Include="Microsoft.Extensions.Configuration.CommandLine" Version="1.0.1" />
```
{:codeblock}

将 *using* 语句添加到包含 Main 方法的文件中：
```
using Microsoft.Extensions.Configuration;
```
{: codeblock}

### 确保应用程序在构建输出文件夹中具有所需的全部文件
{: #configure_output_files}

#### 使用 project.json 工具

将以下属性添加到 project.json 的 `buildOptions` 部分中：
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

在 Startup.cs `Startup` 方法中，除去以下行：
```
  .SetBasePath(env.ContentRootPath)
```
{: codeblock}

在 Program.cs `Main` 方法中，除去以下行：
```
  .UseContentRoot(Directory.GetCurrentDirectory())
```
{: codeblock}

这些更改应该可以让 .NET CLI 找到应用程序的 `Views`，因为执行 `dotnet run` 命令之后，这些 Views 将复制到构建输出中。如果应用程序具有在运行时需要的其他任何文件（例如 json 配置文件），那么您也应该将这些文件添加到项目的 project.json 文件中 `copyToOutput` 的 `include` 部分。

#### 使用 MSBuild 工具

将 `<Content>` 元素添加到 .csproj 文件的 `<ItemGroup>` 元素：
```
  <ItemGroup>
    <Content Include="wwwroot/**/*;Areas/**/Views/*;Views/*;appsettings.json">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
      <CopyToPublishDirectory>Always</CopyToPublishDirectory>
    </Content>
  </ItemGroup>
```
{: codeblock}

在 Startup.cs `Startup` 方法中，除去以下行：
```
  .SetBasePath(env.ContentRootPath)
```
{: codeblock}

在 Program.cs `Main` 方法中，除去以下行：
```
  .UseContentRoot(Directory.GetCurrentDirectory())
```
{: codeblock}

这些更改应该可以让 .NET CLI 找到应用程序的 `View`，因为现在这些 View 会在执行 `dotnet publish` 命令时复制到构建输出中。如果应用程序具有在运行时需要的其他任何文件（例如 json 配置文件），那么您也应该将这些文件添加到项目的 .csproj 文件中 `Content` 元素的 `Include` 属性，各文件之间用分号分隔。

## 在 Release 配置中编译应用程序（仅限 MSBuild）
{: #compiling_in_release_configuration}

现在，基于 MSBuild 的项目在编译打包期间使用 `dotnet publish` 命令发布。缺省情况下，buildpack 将在 `Debug` 配置中发布应用程序。
要在 `Release` 配置中发布应用程序，请将 `PUBLISH_RELEASE_CONFIG` 环境变量设置为 `true`。

可以通过 Cloud Foundry CLI 使用以下命令来执行此操作：

```shell
  cf set-env <app_name> PUBLISH_RELEASE_CONFIG true
```

或者，可以在应用程序的 manifest.yml 文件中设置此变量：

```yml
---
applications:
- name: sample-aspnetcore-app
  memory: 512M
  env:
    PUBLISH_RELEASE_CONFIG: true
```

## 禁用 NuGet 数据包高速缓存
{: #disabling_the_nuget_package_cache}

在某些情况下，可能有必要清除应用程序的 NuGet 数据包高速缓存。这将清除所有现有高速缓存的 NuGet 数据包，并阻止 buildpack 对任何新的数据包进行高速缓存。

可以通过使用 Cloud Foundry CLI 将 `CACHE_NUGET_PACKAGES` 环境变量设置为 `false` 来执行此操作：

```shell
  cf set-env <app_name> CACHE_NUGET_PACKAGES false
```

或者，可以在应用程序的 manifest.yml 文件中将 `CACHE_NUGET_PACKAGES` 环境变量设置为 `false`：

```yml
---
applications:
- name: sample-aspnetcore-app
  memory: 512M
  env:
    CACHE_NUGET_PACKAGES: false
```

## 使用定制本机库
{: #using_custom_native_libraries}

某些库可能需要使用 NuGet 数据包和一些本机库文件（.so 文件）。为了将这些库与 buildpack 一起使用，应该将这些库放入应用程序根文件夹中名为“ld_library_path”的文件夹中。
buildpack 将在编译打包期间自动将此路径添加到 `LD_LIBRARY_PATH` 环境变量。 或者，您可以在应用程序的 `manifest.yml` 文件中指定 `LD_LIBRARY_PATH` 环境变量，也可以通过 `cf set-env` 命令使用不同于“ld_library_path”的文件夹名称。在这种情况下，buildpack 会将此定制路径附加到 buildpack 生成的 `LD_LIBRARY_PATH`。

## 故障诊断 FAQ
{: #troubleshooting_faq}

**问**：我的应用程序无法部署，消息为：`API/0App instance exited ... payload: {... "reason"=>"CRASHED", "exit_status"=>-1, ...}`。这意味着什么？

**答**：如果在推送应用程序时您收到类似消息，那么很可能是因为应用程序超过内存或磁盘限额限制导致的。通过增加应用程序的配额可以解决此问题。

**问**：我的应用程序无法部署，消息为：`Failed to compress droplet: signal: broken pipe` 或 `No space left on device`。该如何解决这个问题？

**答**：从包含大量 NuGet 数据包依赖项的源代码推送的项目，有时会在启用 NuGet 数据包高速缓存时导致此错误。将 `CACHE_NUGET_PACKAGES` 环境变量设置为 `false` 以禁用高速缓存。

# 相关链接
{: #rellinks notoc}
## 常规
{: #general notoc}
* [NuGet](https://docs.nuget.org/Consume/Overview){: new_window}
* [ASP.NET 核心概述](http://docs.asp.net/en/latest/conceptual-overview/aspnet.html){: new_window}
