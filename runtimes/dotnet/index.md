---

copyright:
  years: 2015, 2017
lastupdated: "2017-05-19"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# ASP.NET Core
{: #dotnet_core}

The ASP.NET Core runtime on {{site.data.keyword.Bluemix}} is powered by the ASP.NET Core buildpack. ASP.NET Core
is a modular open source framework for building .NET web applications.
.Net Core is a small, cross-platform runtime that can be targeted by ASP.NET Core applications.
They combine to enable modern, cloud-based web applications.
{: shortdesc}

## Detection
{: #detection}
The Bluemix ASP.NET Core buildpack is used if there are one or more folders containing both a project.json and at least one .cs file anywhere in the application,
 or if the application is pushed from the output directory of the *dotnet publish* command.

## Starter application
{: #starter_application}

{{site.data.keyword.Bluemix}} provides an ASP.NET Core starter application.  The ASP.NET Core starter application is a simple app that provides a template that you can use. You can experiment with the starter app, and make and push changes to the Bluemix environment.  See [Using the starter applications](/docs/cfapps/starter_app_usage.html) for help with using the starter application.

# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
* [NuGet](https://docs.nuget.org/Consume/Overview){: new_window}
* [ASP.NET Core Overview](http://docs.asp.net/en/latest/conceptual-overview/aspnet.html){: new_window}
