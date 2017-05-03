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

{{site.data.keyword.Bluemix}}의 ASP.NET Core 런타임은 ASP.NET Core 빌드팩을 통해 제공됩니다.
ASP.NET Core는 .NET 웹 애플리케이션 빌드를 위한 모듈형 오픈 소스 프레임워크입니다.
.Net Core는 ASP.NET Core 애플리케이션이 대상화할 수 있는 소형의 크로스 플랫폼 런타임입니다.
이들은 함께 결합되어 최신의 클라우드 기반 웹 애플리케이션을 사용할 수 있게 합니다.
{: shortdesc}

## 발견
{: #detection}
Bluemix ASP.NET Core 빌드팩은 애플리케이션에 project.json 및 하나 이상의 .cs 파일이 둘 다 포함된 하나 이상의 폴더가 있거나
애플리케이션이 *dotnet publish* 명령의 출력 디렉토리에서 푸시되는 경우 사용됩니다.

## 스타터 애플리케이션
{: #starter_application}

{{site.data.keyword.Bluemix}}는 ASP.NET Core 스타터 애플리케이션을 제공합니다. ASP.NET Core 스타터 애플리케이션은 사용할 수 있는 템플리트를 제공하는 단순한 앱입니다. 스타터 앱을 사용하여 시험해 볼 수 있으며 Bluemix 환경을 변경하고 변경사항을 푸시할 수 있습니다. 스타터 애플리케이션 사용에 대한 도움말은 [스타터 애플리케이션 사용](/docs/cfapps/starter_app_usage.html)을 참조하십시오. 

## 런타임 버전
{: #runtime_versions}

### 지원되는 버전
{: #supported_versions}
이 빌드팩은 다음 버전을 지원하며, 더 이상 사용되지 않음으로 표시된 버전은 향후 빌드팩 릴리스에서 제거됩니다. [LTS 및 현재 릴리스에 대한 Microsoft의 지원 설명](https://www.microsoft.com/net/core/support)을 참조하십시오.

#### project.json 도구(더 이상 사용되지 않음)

| .NET SDK 버전        | 기본값 |
|-------------------------|---------|
| 1.0.0-preview2-003156   |   아니오    |
| 1.0.0-preview2-1-003177 |   아니오    |

#### MSBuild SDK 도구

| .NET SDK 버전        | 기본값 |
|-------------------------|---------|
| 1.0.0-preview4-004233   |   아니오    |
| 1.0.1                   |   예   |

#### .NET Core 런타임 버전

| .NET Core 런타임 버전 | 릴리스 유형 | 기본값 |
|---------------------------|--------------|---------|
| 1.0.0                     | LTS          |   아니오    |
| 1.0.1                     | LTS          |   아니오    |
| 1.0.3                     | LTS          |   아니오    |
| 1.0.4                     | LTS          |   예   |
| 1.1.0                     | 현재      |   아니오    |
| 1.1.1                     | 현재      |   아니오    |

### .NET SDK 버전 지정

애플리케이션의 루트 디렉토리에 있는 선택적인 global.json으로 .NET SDK 버전을 제어하십시오. 예: 
```
   {
      "projects": [ "src" ],
      "sdk": {
        "version": "1.0.1"
      }
   }
```
{: codeblock}

지정되지 않은 경우 최신 LTS(Long-term-support) 런타임의 MSBuild 도구가 사용됩니다. project.json 도구를 사용하기 위해 위에 나열된 project.json 버전 중 하나를 지정할 수 있지만 향후에 이러한 버전이 제거된다는 점에 유의해야 합니다.

## NuGet 패키지 소스 사용자 정의
{: #customizing_nuget_package_sources}

애플리케이션의 루트 디렉토리에 있는 NuGet.Config 파일에서 애플리케이션의 종속 항목이 다운로드되는 위치를 제어하십시오. 예: 
```
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
   <packageSources>
      <add key="NuGet.org" value="https://api.nuget.org/v3/index.json"/>
   </packageSources>
   </configuration>
```
{: codeblock}

## 애플리케이션을 로컬에서 개발
{: #developing_locally}

로컬에서 ASP.NET Core 애플리케이션을 실행하는 방법에 대한 자세한 정보는
[ASP.NET 시작하기](http://docs.asp.net/en/latest/getting-started/index.html)를 참조하십시오.
애플리케이션이 Bluemix에서 실행되는 방법에 가장 정확히 일치시키려면 .NET Core용 Linux 지침을 따르십시오. 하지만, Linux 상의 애플리케이션 개발은 필요하지 않습니다. 

[Yeoman으로 프로젝트 빌드](http://docs.asp.net/en/latest/client-side/yeoman.html)의 설명에 따라
Yeoman 도구를 사용하여 새 프로젝트 템플리트를 생성할 수 있습니다.

Visual Studio를 사용하여 로컬에서 개발하는 방법에 대한 정보는 [Visual Studio를 사용하여 개발](/docs/starters/deploy_vs.html){: new_window}을 참조하십시오. 

## 공개된 애플리케이션 푸시
{: #pushing_published_app}

빌드팩이 외부 바이너리를 다운로드하지 않도록 애플리케이션이 모든 필수 바이너리를 포함하게 하려는 경우,
공개된 *자체 포함* 애플리케이션을 푸시할 수 있습니다. 자체 포함 애플리케이션에 대한 자세한 정보는
[.NET Core 앱 유형](https://docs.microsoft.com/en-us/dotnet/articles/core/app-types){: new_window}을 참조하십시오. 

애플리케이션을 공개하려면 다음과 같이 명령을 발행하십시오. 
```
  dotnet publish -r ubuntu.14.04-x64
```
{: codeblock}

자체 포함된 애플리케이션의 경우 앱을 다음 디렉토리에서 푸시할 수 있습니다.
```
  bin/<Debug|Release>/<framework>/<runtime>/publish
```
{: codeblock}


휴대용 애플리케이션의 경우 앱을 다음 디렉토리에서 푸시할 수 있습니다.
```
  bin/<Debug|Release>/<framework>/publish
```
{:codeblock}


또한 애플리케이션에서 manifest.yml 파일을 사용 중인 경우 manifest.yml에 공개 출력 폴더에 대한 경로를 지정할 수 있음을 참고하십시오. 그런 다음에는 애플리케이션을 푸시할 때 해당 폴더 내에 있지 않아도 됩니다. 

## 다중 프로젝트가 있는 앱의 배치
{: #developing_apps_with_multiple_projects}

다중 프로젝트를 포함하는 앱을 배치하려면 빌드팩을 기본 프로젝트로 실행할 프로젝트를 지정해야 합니다. 이는 기본 프로젝트에 대한 경로를 설정하는 솔루션의 루트 폴더에 배치 파일을 작성하여 수행할 수 있습니다. 기본 프로젝트에 대한 경로는 프로젝트 폴더 또는 프로젝트 파일(.xproj 또는 .csproj)로 지정될 수 있습니다. 

예를 들어 세 개의 프로젝트, *MyApp.DAL*, *MyApp.Services*, *MyApp.Web*을 *src* 폴더에 포함하고 *MyApp.Web*이 기본 프로젝트인 솔루션의 경우 배치 파일의 형식은 다음과 같습니다. 
```
  [config]
  project = src/MyApp.Web/MyApp.Web.csproj
```
{: codeblock}

이 예제에서, *MyApp.DAL* 및 *MyApp.Services* 프로젝트가 *MyApp.Web*용 project.json 파일의 종속 항목으로 나열된 경우에 빌드팩은 자동으로 이 프로젝트들을 컴파일하지만 실행은 기본 프로젝트인 *MyApp.Web*에 대해서만 dotnet run -p src/MyApp.Web을 사용하여 시도합니다. 

## 애플리케이션 구성
{: #application_configuration}

### 적절한 포트에서 청취하도록 애플리케이션 구성
{: #configuring_listen_proper_port}

빌드팩은 *dotnet run* 명령으로 애플리케이션을 실행하고 뒤에 오는 명령행 인수를 전달합니다. 
```
  --server.urls http://0.0.0.0:${PORT}
```
{: codeblock}

애플리케이션은 이 인수를 kestrel에 전달하여 kestrel이 올바른 포트를 청취 중인지 확인해야 합니다. 

이 인수 전달을 구현하려면 Bluemix에 배치하기 전에 cli-samples 저장소에 제공된 샘플 및 Visual Studio가
제공한 템플리트를 약간 수정해야 합니다.

수정은 다음 예제의 주석에 표시된 대로 Main 메소드에 필요합니다. 

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

project.json 도구의 경우 project.json 파일에 다음 라인을 추가하십시오.
```
  "Microsoft.Extensions.Configuration.CommandLine": "1.0.1",
```
{: codeblock}

MSBuild 도구의 경우 .csproj 파일에 다음 행을 추가하십시오.
```
  <PackageReference Include="Microsoft.Extensions.Configuration.CommandLine" Version="1.0.1" />
```
{:codeblock}

Main 메소드를 포함하는 파일에 *using* 명령문을 추가하십시오. 
```
  using Microsoft.Extensions.Configuration;
```
{: codeblock}

### 애플리케이션의 빌드 출력 폴더에 필요한 모든 파일이 있는지 확인
{: #configure_output_files}

#### project.json 도구 사용

project.json의 `buildOptions` 섹션에 다음 특성을 추가하십시오. 
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

Startup.cs `Startup` 메소드에서 다음 행을 제거하십시오. 
```
  .SetBasePath(env.ContentRootPath)
```
{: codeblock}

Program.cs `Main` 메소드에서 다음 행을 제거하십시오. 
```
  .UseContentRoot(Directory.GetCurrentDirectory())
```
{: codeblock}

이렇게 변경하면 .NET CLI가 애플리케이션의 `Views`를 찾을 수 있게 됩니다. 이제 이러한 보기가 `dotnet run` 명령이 실행될 때 빌드 출력에 복사되기 때문입니다. 애플리케이션에 런타임 시 필요한 다른 파일(예: json 구성 파일)이 있는 경우에는 이러한 파일도 프로젝트의 project.json 파일에 있는 `copyToOutput`의 `include` 섹션에 추가해야 합니다.

#### MSBuild 도구 사용

`<Content>` 요소를 .csproj 파일의 `<ItemGroup>` 요소에 추가하십시오.
```
  <ItemGroup>
    <Content Include="wwwroot/**/*;Areas/**/Views/*;Views/*;appsettings.json">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
      <CopyToPublishDirectory>Always</CopyToPublishDirectory>
    </Content>
  </ItemGroup>
```
{: codeblock}

Startup.cs `Startup` 메소드에서 다음 행을 제거하십시오. 
```
  .SetBasePath(env.ContentRootPath)
```
{: codeblock}

Program.cs `Main` 메소드에서 다음 행을 제거하십시오. 
```
  .UseContentRoot(Directory.GetCurrentDirectory())
```
{: codeblock}

이렇게 변경하면 .NET CLI가 애플리케이션의 `Views`를 찾을 수 있게 됩니다. 이제 이러한 보기가 `dotnet publish` 명령이 실행될 때 빌드 출력에 복사되기 때문입니다. 애플리케이션에 런타임 시 필요한 다른 파일(예: json 구성 파일)이 있는 경우에는 이러한 파일도 프로젝트의 .csproj 파일에 있는 `Content` 요소의 `Include` 특성에 추가해야 하며, 세미콜론으로 구분합니다.

## 릴리스 구성의 애플리케이션 컴파일(MSBuild에만 해당)
{: #compiling_in_release_configuration}

MSBuild 기반 프로젝트는 스테이징 중에 `dotnet publish` 명령을 사용하여 공개됩니다. 기본적으로 빌드팩은 `Debug` 구성의 애플리케이션을 공개합니다.
`Release` 구성의 애플리케이션을 공개하려면 `PUBLISH_RELEASE_CONFIG` 환경 변수를 `true`로 설정하십시오.

다음 명령을 사용하여 CloudFoundry CLI에서 이를 수행할 수 있습니다.

```shell
  cf set-env <app_name> PUBLISH_RELEASE_CONFIG true
```

또는 애플리케이션의 manifest.yml 파일에서 변수를 설정할 수 있습니다.

```yml
---
applications:
- name: sample-aspnetcore-app
  memory: 512M
  env:
    PUBLISH_RELEASE_CONFIG: true
```

## NuGet 패키지 캐시 사용 안함
{: #disabling_the_nuget_package_cache}

일부 상황에서 애플리케이션의 NuGet 패키지 캐시를 지워야 할 수 있습니다. 이렇게 하면 캐시된 기존 NuGet 패키지가 지워지고 빌드팩이 새 패키지를 캐시하지 않게 됩니다.

CloudFoundry CLI를 통해 `CACHE_NUGET_PACKAGES` 환경 변수를 `false`로 설정하여 이를 수행할 수 있습니다.

```shell
  cf set-env <app_name> CACHE_NUGET_PACKAGES false
```

또는 애플리케이션 manifest.yml 파일에서 `CACHE_NUGET_PACKAGES` 환경 변수를 `false`로 설정할 수 있습니다.

```yml
---
applications:
- name: sample-aspnetcore-app
  memory: 512M
  env:
    CACHE_NUGET_PACKAGES: false
```

## 사용자 정의 네이티브 라이브러리 사용
{: #using_custom_native_libraries}

일부 라이브러리에서는 NuGet 패키지와 일부 네이티브 라이브러리 파일(.so 파일)을 둘 다 사용해야 합니다. 빌드팩에서 이러한 라이브러리를 사용하려면 애플리케이션의 루트 폴더에 "ld_library_path" 폴더를 보관해야 합니다.
빌드팩은 스테이징 중에 이 경로를 `LD_LIBRARY_PATH` 환경 변수에 자동 추가합니다. 또는 애플리케이션의 `manifest.yml` 파일에서 또는 `cf set-env` 명령으로 `LD_LIBRARY_PATH` 환경 변수를 지정하여 "ld_library_path"와 다른 폴더 이름을 사용할 수 있습니다. 이 경우 빌드팩은 이 사용자 정의 경로를 빌드팩에서 생성된 `LD_LIBRARY_PATH`에 추가합니다.

## 문제점 해결 FAQ
{: #troubleshooting_faq}

**질문**: 애플리케이션 배치에 실패하고 다음 메시지가 표시됩니다. `API/0App instance exited ... payload: {... "reason"=>"CRASHED", "exit_status"=>-1, ...}`.  이는 어떤 의미입니까? 

**답변**: 애플리케이션을 푸시할 때 이와 비슷한 메시지를 받는 경우 이는 애플리케이션이 메모리나 디스크 할당량 한계를 초과했기 때문일 가능성이 매우 높습니다. 애플리케이션의 할당량을 늘리면 해결됩니다. 

**질문**: 내 애플리케이션이 배치에 실패하며 다음 메시지가 나타납니다. `Failed to compress droplet: signal: broken pipe` 또는 `No space left on device`. 이 문제의 해결 방법은 무엇입니까?

**답변**: 많은 수의 NuGet 패키지 종속 항목이 포함된 소스 코드에서 푸시된 프로젝트로 인해 NuGet 패키지 캐시를 사용할 때 종종 이 오류가 발생합니다. 캐시를 사용 안함으로 설정하려면 `CACHE_NUGET_PACKAGES` 환경 변수를 `false`로 설정하십시오.

# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
* [NuGet](https://docs.nuget.org/Consume/Overview){: new_window}
* [ASP.NET Core 개요](http://docs.asp.net/en/latest/conceptual-overview/aspnet.html){: new_window}
