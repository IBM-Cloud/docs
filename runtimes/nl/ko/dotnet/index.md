---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# ASP.NET Core 
{: #dotnet_core}
*마지막 업데이트 날짜: 2016년 5월 30일*

{{site.data.keyword.Bluemix}}의 ASP.NET Core 런타임은 ASP.NET Core 빌드팩을 통해 제공됩니다.
ASP.NET Core는 .NET 웹 애플리케이션 빌드를 위한 모듈형 오픈 소스 프레임워크입니다.
.Net Core는 ASP.NET Core 애플리케이션이 대상화할 수 있는 소형의 크로스 플랫폼 런타임입니다.
이들은 함께 결합되어 최신의 클라우드 기반 웹 애플리케이션을 사용할 수 있게 합니다.
{: shortdesc}

## 발견
{: #detection}
Bluemix ASP.NET Core 빌드팩은 애플리케이션에 하나 이상의 project.json 파일이 있거나 *dotnet publish* 명령의 출력 디렉토리에서 애플리케이션이 푸시된 경우에 사용됩니다. 

## 스타터 애플리케이션
{: #starter_application}

{{site.data.keyword.Bluemix}}는 ASP.NET Core 스타터 애플리케이션을 제공합니다. ASP.NET Core 스타터 애플리케이션은 사용할 수 있는 템플리트를 제공하는 단순한 앱입니다. 스타터 앱을 사용하여 시험해 볼 수 있으며 Bluemix 환경을 변경하고 변경사항을 푸시할 수 있습니다. 스타터 애플리케이션 사용에 대한 도움말은 [스타터 애플리케이션 사용](../../cfapps/starter_app_usage.html)을 참조하십시오. 

## 런타임 버전
{: #runtime_versions}

### .NET CLI 버전 지정

애플리케이션의 루트 디렉토리에 있는 선택적인 global.json으로 .NET CLI 버전을 제어하십시오. 예: 
```
   {
      "projects": [ "src" ],
      "sdk": {
        "version": "1.0.0-preview1-002702"
      }
   }
```
{: codeblock}

지정하지 않으면 가장 최근의 안정적인 릴리스 후보가 사용됩니다. 

### NuGet 패키지 소스 사용자 정의

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

로컬에서 ASP.NET Core 애플리케이션을 실행하는 방법에 대한 자세한 정보는 [ASP.NET로 시작하기](http://docs.asp.net/en/latest/getting-started/index.html)를 참조하십시오.
애플리케이션이 Bluemix에서 실행되는 방법에 가장 정확히 일치시키려면 .NET Core용 Linux 지침을 따르십시오. 하지만, Linux 상의 애플리케이션 개발은 필요하지 않습니다. 

[Yeoman으로 프로젝트 빌드](http://docs.asp.net/en/latest/client-side/yeoman.html)의 설명에 따라 Yeoman 도구를 사용하여 새 프로젝트 템플리트를 생성할 수 있습니다.

## 공개된 애플리케이션 푸시

빌드팩이 외부 바이너리를 다운로드하지 않도록 애플리케이션이 모든 필수 바이너리를 포함하게 하려는 경우, 공개된 *자체 포함* 애플리케이션을 푸시할 수 있습니다. 자체 포함 애플리케이션에 대한 자세한 정보는 [.Net Core에서 이식성 유형](http://dotnet.github.io/docs/core-concepts/app-types.html){: new_window}을 참조하십시오. 

애플리케이션을 공개하려면 다음과 같이 명령을 발행하십시오. 
```
  dotnet publish -r ubuntu.14.04-x64 
```
{: codeblock}
  
그런 다음 다음 위치에서 앱을 푸시할 수 있습니다. 
```
  bin/<Debug|Release>/<framework>/<runtime>/publish 디렉토리.
```
{: codeblock}


또한 애플리케이션에서 manifest.yml 파일을 사용 중인 경우 manifest.yml에 공개 출력 폴더에 대한 경로를 지정할 수 있음을 참고하십시오. 그런 다음에는 애플리케이션을 푸시할 때 해당 폴더 내에 있지 않아도 됩니다. 

## 다중 프로젝트가 있는 앱의 배치

다중 프로젝트를 포함하는 앱을 배치하려면 빌드팩을 기본 프로젝트로 실행할 프로젝트를 지정해야 합니다. 이는 기본 프로젝트에 대한 경로를 설정하는 솔루션의 루트 폴더에 배치 파일을 작성하여 수행할 수 있습니다. 기본 프로젝트에 대한 경로는 프로젝트 폴더 또는 프로젝트 파일(.xproj 또는 .csproj)로 지정될 수 있습니다. 

예를 들어 세 개의 프로젝트, *MyApp.DAL*, *MyApp.Services*, *MyApp.Web*을 *src* 폴더에 포함하고 *MyApp.Web*이 기본 프로젝트인 솔루션의 경우 배치 파일의 형식은 다음과 같습니다. 
```
  [config]
  project = src/MyApp.Web
```
{: codeblock}

이 예제에서,
*MyApp.DAL* 및 *MyApp.Services* 프로젝트가 *MyApp.Web*용 project.json 파일의 종속 항목으로
나열된 경우에 빌드팩은 자동으로 이 프로젝트들을 컴파일하지만 실행은 기본 프로젝트인 *MyApp.Web*에 대해서만 dotnet run -p src/MyApp.Web을 사용하여
시도합니다. 이 프로젝트를 xproj 프로젝트라고 가정하고 *MyApp.Web*에 대한 경로를 다음과 같이 지정할 수도 있습니다.  
```
  project = src/MyApp.Web/MyApp.Web.xproj 
```
{: codeblock}

## cli-samples 저장소 및 Visual Studio 템플리트에서 샘플 사용

빌드팩은 *dotnet run* 명령으로 애플리케이션을 실행하고 뒤에 오는 명령행 인수를 전달합니다. 
```
  --server.urls http://0.0.0.0:${PORT}
```
{: codeblock}

애플리케이션은 이 인수를 kestrel에 전달하여 kestrel이 올바른 포트를 청취 중인지 확인해야 합니다. 

이 인수의 전달을 구현하려면 cli-samples 저장소에서 제공한 샘플과 Visual Studio에서 제공한 템플리트에 대해 Blumix로 배치 전에 약간의 수정이 필요합니다. 

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

다음 종속 항목을 project.json에 추가하십시오.  
```
  "Microsoft.Extensions.Configuration.CommandLine": "1.0.0-rc2-final",
```
{: codeblock}

Main 메소드를 포함하는 파일에 *using* 명령문을 추가하십시오.  
```
  using Microsoft.Extensions.Configuration;
```
{: codeblock}

# 관련 링크
{: #rellinks}
## 일반
{: #general}
* [ASP.NET Core 빌드팩의 최신 업데이트](updates.html)
* [NuGet](https://docs.nuget.org/Consume/Overview){: new_window}
* [ASP.NET Core 개요](http://docs.asp.net/en/latest/conceptual-overview/aspnet.html){: new_window}
