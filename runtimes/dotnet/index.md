---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# ASP.NET Core 
{: #dotnet_core}
*Last updated: 30 May 2016*

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

{{site.data.keyword.Bluemix}} provides an ASP.NET Core starter application.  The ASP.NET Core starter application is a simple app that provides a template that you can use. You can experiment with the starter app, and make and push changes to the Bluemix environment.  See [Using the starter applications](../../cfapps/starter_app_usage.html) for help with using the starter application.

## Runtime versions
{: #runtime_versions}

### Specifying the .NET CLI version

Control the .NET CLI version with an optional global.json in the application's root directory. For example:
```
   {
      "projects": [ "src" ],
      "sdk": {
        "version": "1.0.0-preview1-002702"
      }
   }
```
{: codeblock}

If not specified, the most current stable Release Candidate is used.

### Customizing NuGet package sources

Control where your application's dependencies are downloaded from in the NuGet.Config file in the application's root directory. For example:
```
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
   <packageSources>
      <add key="NuGet.org" value="https://api.nuget.org/v3/index.json"/>
   </packageSources>
   </configuration>
```
{: codeblock}

## Developing applications locally
{: #developing_locally}

For more information about running an ASP.NET Core application locally, see
[Getting Started with ASP.NET](http://docs.asp.net/en/latest/getting-started/index.html).
To most closely match how the application runs in Bluemix, follow the Linux instructions for .NET Core, but developing the application on Linux is not required.

The Yeoman tool can be used to generate new project templates as described in
[Building Projects with Yeoman](http://docs.asp.net/en/latest/client-side/yeoman.html).

## Pushing a Published Application

If you want your application to contain all its required binaries so that the buildpack does not download any 
external binaries, you can push a published *self-contained* application.  See [Types of portability in .Net Core](http://dotnet.github.io/docs/core-concepts/app-types.html){: new_window}
for more information on self-contained applications.

To publish an application issue a command such as:
```
  dotnet publish -r ubuntu.14.04-x64 
```
{: codeblock}
  
The app can then be pushed from the
```
  bin/<Debug|Release>/<framework>/<runtime>/publish
```
{: codeblock}
directory.

Also note that if you are using a manifest.yml file in your application, you can specify the path to the publish output folder in your manifest.yml.  Then you don't have to be in that folder when you push the application.

## Deploying apps with multiple projects

To deploy an app which contains multiple projects, you will need to specify which project you want the buildpack to run as the main project. This can be done by creating a .deployment file in the root folder of the solution which sets the path to the main project. The path to the main project can be specified as the project folder or the project file (.xproj or .csproj).

For example if a solution which contains three projects, *MyApp.DAL*, *MyApp.Services*, and *MyApp.Web* in the *src* folder, and *MyApp.Web* is the main project, the format of the .deployment file would be as follows:
```
  [config]
  project = src/MyApp.Web
```
{: codeblock}

In this example, the buildpack would automatically compile the *MyApp.DAL* and *MyApp.Services* projects if they are listed as dependencies in the project.json file for *MyApp.Web*, but the buildpack would only attempt to execute the main project, *MyApp.Web*, with dotnet run -p src/MyApp.Web. The path to *MyApp.Web*, assuming this project is an xproj project, could also be specified as 
```
  project = src/MyApp.Web/MyApp.Web.xproj 
```
{: codeblock}

## Using samples from the cli-samples repository and Visual Studio template

The buildpack will run your application with the *dotnet run* command and pass the command-line argument that follows
```
  --server.urls http://0.0.0.0:${PORT}
```
{: codeblock}

Your application will need to pass this argument to kestrel to ensure that kestrel is listening on the correct port.

To implement the passing of this argument the samples provided in the cli-samples repository and templates provided by Visual Studio 
require slight modifications before deploying to Bluemix.

Modifications are required to the Main method as noted by the comments in the example below:

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

Add the following dependency to project.json: 
```
  "Microsoft.Extensions.Configuration.CommandLine": "1.0.0-rc2-final",
```
{: codeblock}

Add a *using* statement to the file which contains your Main method: 
```
  using Microsoft.Extensions.Configuration;
```
{: codeblock}

# rellinks
{: #rellinks}
## general
{: #general}
* [Latest Updates to the ASP.NET Core buildpack](updates.html)
* [NuGet](https://docs.nuget.org/Consume/Overview){: new_window}
* [ASP.NET Core Overview](http://docs.asp.net/en/latest/conceptual-overview/aspnet.html){: new_window}
