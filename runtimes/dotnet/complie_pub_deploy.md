---

copyright:
  years: 2015, 2017
lastupdated: "2017-05-31"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


#Compile, Publish, and Deploy Applications
{: #publish_configure_deploy}

## Compiling your application in Release configuration (MSBuild only)
{: #compiling_in_release_configuration}

MSBuild based projects are now published using the `dotnet publish` command during staging.  By default, the buildpack will publish your application in `Debug` configuration.
To publish your application in `Release` configuration, set the `PUBLISH_RELEASE_CONFIG` environment variable to `true`.

You can do this with the CloudFoundry CLI with the following command:

```shell
  cf set-env <app_name> PUBLISH_RELEASE_CONFIG true
```

Alternatively, you can set the variable in your application's manifest.yml file:

```yml
---
applications:
- name: sample-aspnetcore-app
  memory: 512M
  env:
    PUBLISH_RELEASE_CONFIG: true
```

## Pushing a Published Application
{: #pushing_published_app}

If you want your application to contain all its required binaries so that the buildpack does not download any
external binaries, you can push a published *self-contained* application.  See [.NET Core App Types](https://docs.microsoft.com/en-us/dotnet/articles/core/app-types){: new_window}
for more information on self-contained applications.

To publish an application issue a command such as:
```
  dotnet publish -r ubuntu.14.04-x64
```
{: codeblock}

For self-contained applications, the app can then be pushed from the
```
  bin/<Debug|Release>/<framework>/<runtime>/publish
```
{: codeblock}
directory.

For portable applications, the app can be pushed from the
```
  bin/<Debug|Release>/<framework>/publish
```
{:codeblock}
directory.

Also note that if you are using a manifest.yml file in your application, you can specify the path to the publish output folder in your manifest.yml.  Then you don't have to be in that folder when you push the application.

## Deploying apps with multiple projects
{: #developing_apps_with_multiple_projects}

To deploy an app which contains multiple projects, you will need to specify which project you want the buildpack to run as the main project. This can be done by creating a .deployment file in the root folder of the solution which sets the path to the main project. The path to the main project can be specified as the project folder or the project file (.xproj or .csproj).

For example if a solution which contains three projects, *MyApp.DAL*, *MyApp.Services*, and *MyApp.Web* in the *src* folder, and *MyApp.Web* is the main project, the format of the .deployment file would be as follows:
```
  [config]
  project = src/MyApp.Web/MyApp.Web.csproj
```
{: codeblock}

In this example, the buildpack would automatically compile the *MyApp.DAL* and *MyApp.Services* projects if they are listed as dependencies in the project.json file for *MyApp.Web*, but the buildpack would only attempt to execute the main project, *MyApp.Web*, with dotnet run -p src/MyApp.Web.
