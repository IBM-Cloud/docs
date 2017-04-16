---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-06"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# ASP.NET Core 빌드팩의 최신 업데이트
{: #latest_updates}


aspnet 빌드팩의 최신 업데이트 목록

## 2016년 10월 10일: 업데이트된 ASP.NET Core 빌드팩 v1.0.1-20161005-1225

* .NET Core 1.0.1 지원 추가
* NuGet 패키지를 캐시할 때 때때로 배치에 실패하는 문제 수정

## 2016년 8월 31일: 업데이트된 ASP.NET Core 빌드팩 v1.0-20160826-1345

* 프론트 엔드 javascript 및 css 라이브러리를 설치하기 위해 NPM 및 Bower를 사용하여 컴파일 전 및 후 스크립트를 실행하기 위한 지원을 추가합니다.
* 빌드팩을 베타 상태에서 GA 상태로 이동시킵니다.

## 2016년 7월 11일: 업데이트된 ASP.NET Core 빌드팩 v0.9-20160706-1603

이 버전의 빌드팩에 다음 변경사항이 포함되어 있습니다.

* 이 버전의 빌드팩은 .NET CLI 1.0 Preview 2 빌드 및 .NET Core 1.0 RTM을 지원합니다.
* 빌드팩이 계속해서 .NET CLI 1.0 Preview 1 및 .NET Core 1.0 RC2를 지원합니다.
* 설치될 기본 .NET CLI 버전이 현재 1.0.0-preview2-003121입니다.

## 2016년 6월 10일: 업데이트된 ASP.NET Core 빌드팩 v0.8.1-20160526-0957

이 버전의 빌드팩에 다음 변경사항이 포함되어 있습니다.

* 런타임의 이름이 ASP.NET 5에서 ASP.NET Core로 변경되었습니다.
* 빌드팩 버전 번호가 발견 스크립트 출력에 포함됩니다. 
* 이 버전의 빌드팩은 CoreCLR RC1 이하를 사용하는 DNX 기반 애플리케이션에 대한 지원이 제거되었습니다.
* 이 버전의 빌드팩은 .NET CLI 및 .NET Core RC2를 지원합니다.
* 빌드팩은 공개 출력에서 project.json 파일 또는 *.runtimeconfig.json 파일로 프로젝트를 발견합니다. 

## 2015년 10월 22일: 업데이트된 ASP.NET 5 빌드팩 v0.7-20151022-1257

* 이 버전의 빌드팩은 Mono를 제거했으며 그 대신 Beta 8 CoreCLR을 지원합니다.

## 2015년 9월 18일: 업데이트된 ASP.NET 5 빌드팩 v0.6-20150916-1220

* 이 버전의 빌드팩은 Beta 7 DNX 변경을 지원하며, 다음 사용자 정의 시작 명령으로 오래된 베타 릴리스에 종속되는 애플리케이션을 실행할 수 있습니다. 

```
   dnx src/dotnetstarter kestrel --server.urls http://${VCAP_APP_HOST}:${PORT}
```
{: codeblock}

* Nowin 웹 서버의 사용이 이 빌드팩에서 제거되었으며 그 대신 [Kestrel]{https://github.com/aspnet/KestrelHttpServer} 웹 서버가 사용됩니다.

# 관련 링크
{: #rellinks}
## 일반
{: #general}
* [Dotnet Core 런타임](index.html)
