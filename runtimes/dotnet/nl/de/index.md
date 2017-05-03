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

Die Laufzeit von ASP.NET Core in {{site.data.keyword.Bluemix}} basiert auf dem Buildpack 'ASP.NET Core'. ASP.NET Core
ist ein modulares Open-Source-Framework zum Erstellen von .NET-Webanwendungen.
.Net Core ist eine kleine, plattformübergreifende Laufzeit, die von ASP.NET Core-Anwendungen als Ziel verwendet werden kann. 
Gemeinsam ermöglichen sie moderne, cloudbasierte Webanwendungen.
{: shortdesc}

## Erkennung
{: #detection}
Das Bluemix-Buildpack 'ASP.NET Core' wird verwendet, wenn mindestens ein Ordner sowohl eine Datei 'project.json' und mindestens eine Datei mit der Erweiterung .cs in der Anwendung enthält wenn die Anwendung mit einer Push-Operation aus dem Ausgabeverzeichnis des Befehls *dotnet publish* übertragen wird.

## Starteranwendung
{: #starter_application}

{{site.data.keyword.Bluemix}} stellt eine ASP.NET Core-Starteranwendung bereit.  Die ASP.NET Core-Starteranwendung ist eine einfache App, die eine Schablone bereitstellt, die Sie verwenden können. Sie können mit der Starter-App experimentieren, Änderungen an der Bluemix-Umgebung vornehmen und diese mit einer Push-Operation übertragen.  Hilfe zur Verwendung der Starteranwendung finden Sie in [Starteranwendungen verwenden](/docs/cfapps/starter_app_usage.html).

## Laufzeitversionen
{: #runtime_versions}

### Unterstützte Versionen
{: #supported_versions}
Dieses Buildpack unterstützt die folgenden Versionen. Versionen, die als veraltet markiert sind, werden in einem künftigen Release des Buildpacks entfernt. Siehe [Microsoft Support Statement für LTS- und Current-Releases](https://www.microsoft.com/net/core/support).

#### project.json-Tools (nicht mehr verwendet)

| .NET SDK-Version        | Standard  |
|-------------------------|-----------|
| 1.0.0-preview2-003156   |   Nein    |
| 1.0.0-preview2-1-003177 |   Nein    |

#### MSBuild SDK-Tools

| .NET SDK-Version        | Standard  |
|-------------------------|-----------|
| 1.0.0-preview4-004233   |   Nein    |
| 1.0.1                   |   Ja      |

#### .NET Core-Laufzeitversionen

| .NET Core-Laufzeitversion | Releasetyp   | Standard  |
|---------------------------|--------------|-----------|
| 1.0.0                     | LTS          |   Nein    |
| 1.0.1                     | LTS          |   Nein    |
| 1.0.3                     | LTS          |   Nein    |
| 1.0.4                     | LTS          |   Ja      |
| 1.1.0                     | Current      |   Nein    |
| 1.1.1                     | Current      |   Nein    |

### .NET SDK-Version angeben

Steuern Sie die .NET SDK-Version mit der optionalen Datei 'global.json' im Stammverzeichnis der Anwendung. Beispiel:
```
   {
      "projects": [ "src" ],
      "sdk": {
        "version": "1.0.1"
      }
   }
```
{: codeblock}

Falls nicht anders angegeben, wird das MSBuild-Tool für die letzte LTS-Laufzeit (LTS, Long-term-support) verwendet. Um das Tool 'project.json' zu verwenden, können Sie eine der oben aufgelisteten Versionen von 'project.json' angeben. Sie sollten dabei jedoch beachten, dass diese Versionen in Zukunft entfernt werden. 

## NuGet-Paketquellen anpassen
{: #customizing_nuget_package_sources}

Steuern Sie, von wo die Abhängigkeiten Ihrer Anwendung heruntergeladen werden, in der Datei NuGet.Config im Stammverzeichnis der Anwendung. Beispiel:
```
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
   <packageSources>
      <add key="NuGet.org" value="https://api.nuget.org/v3/index.json"/>
   </packageSources>
   </configuration>
```
{: codeblock}

## Anwendungen lokal entwickeln
{: #developing_locally}

Weitere Informationen zum lokalen Ausführen einer ASP.NET Core-Anwendung, finden Sie in
[Einführung in ASP.NET](http://docs.asp.net/en/latest/getting-started/index.html)
Um der Ausführung der Anwendung in Bluemix am nächsten zu kommen, führen Sie die Linux-Anweisungen für .NET Core aus, wobei aber die Entwicklung der Anwendung unter Linux nicht erforderlich ist.

Das Tool Yeoman kann zum Generieren neuer Projektvorlagen verwendet werden, wie in
[Projekte mit Yeoman erstellen](http://docs.asp.net/en/latest/client-side/yeoman.html) beschrieben.

Informationen zur lokalen Entwicklung mit Visual Studio finden Sie im Abschnitt zum Thema [Mit Visual Studio entwickeln](/docs/starters/deploy_vs.html){: new_window}.

## Veröffentlichte Anwendung mit einer Push-Operation übertragen
{: #pushing_published_app}

Wenn Sie möchten, dass Ihre Anwendung alle erforderlichen Binärdateien enthält, sodass das Buildpack keine
externen Binärdateien herunterlädt, können Sie eine veröffentlichte *eigenständige* Anwendung mit einer Push-Operation
übertragen.  Weitere Informationen zu eigenständigen Anwendungen finden Sie unter dem Thema [.NET Core App-Typen](https://docs.microsoft.com/en-us/dotnet/articles/core/app-types){: new_window}.

Geben Sie zum Veröffentlichen einer Anwendung einen Befehl wie den folgenden ein:
```
  dotnet publish -r ubuntu.14.04-x64 
```
{: codeblock}

Bei eigenständigen Anwendungen kann die App mit einer Push-Operation aus dem Verzeichnis 
```
  bin/<Debug|Release>/<framework>/<runtime>/publish
```
{: codeblock}
übertragen werden.

Bei portierbaren Anwendungen kann die App mit einer Push-Operation aus dem Verzeichnis 
```
  bin/<Debug|Release>/<framework>/publish
```
{:codeblock}
übertragen werden.

Beachten Sie auch, dass Sie, wenn Sie in Ihrer Anwendung eine Datei manifest.yml verwenden, den Pfad des Ausgabeordners 'publish' in Ihrer Datei manifest.yml angeben können.  In diesem Fall müssen Sie sich nicht in diesem Ordner befinden, wenn Sie die Anwendung mit einer Push-Operation übertragen.

## Apps mit mehreren Projekten bereitstellen
{: #developing_apps_with_multiple_projects}

Wenn Sie eine App bereitstellen, die mehrere Projekte enthält, müssen Sie angeben, welches Projekt das Buildpack als Hauptprojekt ausführen soll. Dies kann erfolgen, indem eine .deployment-Datei im Stammordner der Lösung erstellt wird, in der der Pfad für das Hauptprojekt angegeben wird. Der Pfad für das Hauptprojekt kann über den Projektordner oder die Projektdatei (.xproj bzw. .csproj) angegeben werden.

Wenn beispielsweise eine Lösung die drei Projekte *MyApp.DAL*, *MyApp.Services* und *MyApp.Web* im Ordner *src* enthält und *MyApp.Web* das Hauptprojekt ist, würde das Format der .deployment-Datei wie folgt aussehen:
```
  [config]
  project = src/MyApp.Web/MyApp.Web.csproj
```
{: codeblock}

In diesem Beispiel würde das Buildpack automatisch die Projekte *MyApp.DAL* und *MyApp.Services* kompilieren, wenn sie in der Datei 'project.json' für *MyApp.Web* als Abhängigkeiten aufgelistet sind, aber das Buildpack würde nur versuchen, das Hauptprojekt, *MyApp.Web*, mit dotnet run -p src/MyApp.Web auszuführen. 

## Anwendungskonfiguration
{: #application_configuration}

### Ihre Anwendung für die Überwachung des richtigen Ports konfigurieren
{: #configuring_listen_proper_port}

Das Buildpack führt Ihre Anwendung mit dem Befehl *dotnet run* aus und übergibt das folgende Befehlszeilenargument:
```
  --server.urls http://0.0.0.0:${PORT}
```
{: codeblock}

Ihre Anwendung muss dieses Argument an Kestrel übergeben, damit Kestrel am korrekten Port empfangsbereit ist.

Damit die Übergabe dieses Arguments implementiert wird, müssen die im Repository für CLI-Beispiele bereitgestellten Beispiele
und die von Visual Studio bereitgestellten Vorlagen vor der Bereitstellung für Bluemix leicht geändert werden.

Änderungen der Methode 'Main' sind entsprechend den Kommentaren im folgenden Beispiel erforderlich:

<pre>
  public static void Main(string[] args)
  {
    var config = new ConfigurationBuilder() //FÜGEN SIE DIESE 3 ZEILEN AM ANFANG DER METHODE MAIN HINZU
        .AddCommandLine(args)
        .Build();

    var host = new WebHostBuilder()
        .UseKestrel()
        .UseConfiguration(config) //FÜGEN SIE DIESE ZEILE VOR 'UseStartup' HINZU
        .UseStartup&lt;Startup&gt;()
        .Build();
    host.Run();
}
</pre>
{: codeblock}

Fügen Sie die folgende Zeile für das Tool 'project.json' in Ihrer Datei 'project.json' hinzu: 
```
  "Microsoft.Extensions.Configuration.CommandLine": "1.0.1",
```
{: codeblock}

Fügen Sie die folgende Zeile für das Tool 'MSBuild' in Ihrer '.csproj'-Datei hinzu: 
```
  <PackageReference Include="Microsoft.Extensions.Configuration.CommandLine" Version="1.0.1" />
```
{:codeblock}

Fügen Sie der Datei, die Ihre Methode 'Main' enthält, eine Anweisung *using* hinzu:
```
  using Microsoft.Extensions.Configuration;
```
{: codeblock}

### Stellen Sie sicher, dass Ihre Anwendung im Buildausgabeordner über alle erforderlichen Dateien verfügt. 
{: #configure_output_files}

#### Tool project.json verwenden

Fügen Sie die folgende Eigenschaft zum Abschnitt `buildOptions` in der Datei 'project.json' hinzu:
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

Entfernen Sie folgende Zeile in der `Startup`-Methode Startup.cs:
```
  .SetBasePath(env.ContentRootPath)
```
{: codeblock}

Entfernen Sie folgende Zeile in der `Main`-Methode Program.cs:
```
  .UseContentRoot(Directory.GetCurrentDirectory())
```
{: codeblock}

Diese Änderungen sollte der .NET-CLI ermöglichen, die `Sichten` Ihrer Anwendung zu finden, da diese jetzt in die Buildausgabe kopiert werden, wenn der Befehl `dotnet run` ausgeführt wird.  Wenn Ihre Anwendung über andere Dateien wie beispielsweise json-Konfigurationsdateien verfügt, die zur Laufzeit erforderlich sind, dann sollten Sie auch diese zum Abschnitt `include` von `copyToOutput` in der Datei 'project.json' für Ihr Projekt hinzufügen.

#### Tool MSBuild verwenden

Fügen Sie ein Element `<Content>` zum Element `<ItemGroup>` Ihrer .csproj-Datei hinzu: 
```
  <ItemGroup>
    <Content Include="wwwroot/**/*;Areas/**/Views/*;Views/*;appsettings.json">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
      <CopyToPublishDirectory>Always</CopyToPublishDirectory>
    </Content>
  </ItemGroup>
```
{: codeblock}

Entfernen Sie folgende Zeile in der `Startup`-Methode Startup.cs:
```
  .SetBasePath(env.ContentRootPath)
```
{: codeblock}

Entfernen Sie folgende Zeile in der `Main`-Methode Program.cs:
```
  .UseContentRoot(Directory.GetCurrentDirectory())
```
{: codeblock}

Diese Änderungen sollte der .NET-CLI ermöglichen, die `Sichten` Ihrer Anwendung zu finden, da diese jetzt in die Buildausgabe kopiert werden, wenn der Befehl `dotnet publish` ausgeführt wird. Wenn Ihre Anwendung über andere Dateien wie beispielsweise json-Konfigurationsdateien verfügt, die zur Laufzeit erforderlich sind, dann sollten Sie auch diese durch Semikolons getrennt zur Eigenschaft `Include` des Elements `Content` in der .csproj-Datei Ihres Projekts hinzufügen.

## Anwendung in der Releasekonfiguration kompilieren (nur MSBuild)
{: #compiling_in_release_configuration}

Auf MSBuild basierende Projekte werden jetzt während des Stagings mithilfe des Befehls `dotnet publish` veröffentlicht. Standardmäßig veröffentlicht das Buildpack Ihre Anwendung in der `Debug`-Konfiguration.
Um Ihre Anwendung in der `Release`-Konfiguration zu veröffentlichen, legen Sie für die Umgebungsvariable `PUBLISH_RELEASE_CONFIG` den Wert `true` fest.

Sie können dies über die CloudFoundry-CLI mit folgendem Befehl tun: 

```shell
  cf set-env <app_name> PUBLISH_RELEASE_CONFIG true
```

Alternativ können Sie die Variable in der Datei 'manifest.yml' Ihrer Anwendung festlegen: 

```yml
---
applications:
- name: sample-aspnetcore-app
  memory: 512M
  env:
    PUBLISH_RELEASE_CONFIG: true
```

## NuGet-Paketcache inaktivieren
{: #disabling_the_nuget_package_cache}

In einigen Situationen ist es möglicherweise erforderlich, den NuGet-Paketcache für Ihre Anwendung zu bereinigen. Bei diesem Vorgang werden alle vorhandenen NuGet-Pakete, die im Cache gespeichert sind, bereinigt und es wird verhindert, dass das Buildpack neue Pakete im Cache speichert. 

Sie können dies durch die Angabe des Wertes `false` für die Umgebungsvariable `CACHE_NUGET_PACKAGES` erreichen. Dazu verwenden Sie die CloudFoundry-CLI:

```shell
  cf set-env <app_name> CACHE_NUGET_PACKAGES false
```

Alternativ können Sie für die Umgebungsvariable `CACHE_NUGET_PACKAGES` in der Datei 'manifest.yml' Ihrer Anwendung den Wert `false` festlegen: 

```yml
---
applications:
- name: sample-aspnetcore-app
  memory: 512M
  env:
    CACHE_NUGET_PACKAGES: false
```

## Angepasste native Bibliotheken verwenden
{: #using_custom_native_libraries}

Einige Bibliotheken erfordern möglicherweise die Verwendung eines NuGet-Pakets und einiger nativer Bibliotheksdateien (.so-Dateien). Um diese Bibliotheken mit dem Buildpack zu verwenden, sollten Sie diese in einen Ordner mit dem Namen "ld_library_path" in den Stammordner Ihrer Anwendung stellen.
Das Buildpack fügt diesen Pfad automatisch während des Stagings zur Umgebungsvariablen `LD_LIBRARY_PATH` hinzu. Alternativ können Sie die Umgebungsvariable `LD_LIBRARY_PATH` in der Datei `manifest.yml` Ihrer Anwendung angeben oder den Befehl `cf set-env` verwenden, um einen anderen Ordnernamen als "ld_library_path" anzugeben. In diesem Fall hängt das Buildpack diesen angepassten Pfad an den vom Buildpack generierten `LD_LIBRARY_PATH` an. 

## Fehlerbehebung - Häufig gestellte Fragen (FAQ)
{: #troubleshooting_faq}

**F**: Meine Anwendung schlägt bei der Bereitstellung mit folgender Nachricht fehl: `API/0App instance exited ... payload: {... "reason"=>"CRASHED", "exit_status"=>-1, . ..}`.  Was bedeutet das? 

**A**: Falls Sie eine ähnliche Nachricht erhalten, wenn Sie eine Push-Operation für Ihre Anwendung durchführen, wird dies vermutlich dadurch verursacht, dass Ihre Anwendung entweder den Grenzwert für den Speicher oder für das Datenträgerkontingent überschreitet. Dieses Problem kann durch Erhöhung der Größenbeschränkung für Ihre Anwendung behoben werden. 

**F**: Meine Anwendung schlägt bei der Bereitstellung mit folgender Nachricht fehl: `Failed to compress droplet: signal: broken pipe` oder `No space left on device`. Wie kann ich den Fehler beheben? 

**A**: Projekte, die mit einer Push-Operation von einem Quellcode mit einer großen Anzahl an NuGet-Paketabhängigkeiten übertragen wurden, können diesen Fehler verursachen, wenn der NuGet-Paketcache aktiviert ist. Legen Sie für die Umgebungsvariable `CACHE_NUGET_PACKAGES` den Wert `false` fest, um das Zwischenspeichern im Cache zu inaktivieren. 

# Zugehörige Links
{: #rellinks notoc}
## Allgemein
{: #general notoc}
* [NuGet](https://docs.nuget.org/Consume/Overview){: new_window}
* [Übersicht über ASP.NET Core](http://docs.asp.net/en/latest/conceptual-overview/aspnet.html){: new_window}
