---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# ASP.NET Core 빌드팩의 최신 업데이트
{: #latest_updates}

*마지막 업데이트 날짜: 2016년 6월 10일*

aspnet 빌드팩의 최신 업데이트 목록

## 2016년 6월 10일: 업데이트된 ASP.NET Core 빌드팩 v0.8.1-20160526-0957

이 버전의 빌드팩에 다음 변경사항이 포함되어 있습니다.

* 런타임의 이름이 ASP.NET 5에서 ASP.NET Core로 변경되었습니다.
* 빌드팩 버전 번호가 발견 스크립트 출력에 포함됩니다. 
* 이 버전의 빌드팩은 CoreCLR RC1 이하를 사용하는 DNX 기반 애플리케이션에 대한 지원이 제거되었습니다.
* 이 버전의 빌드팩은 .NET CLI 및 .NET Core RC2를 지원합니다.
* 빌드팩은 공개된 출력에서 project.json 파일 또는 *.runtimeconfig.json 파일로 프로젝트를 발견합니다. 

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
