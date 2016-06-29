---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# ASP.NET Core 
{: #dotnet_core}
*Letzte Aktualisierung: 30. Mai 2016*

Die Laufzeit von ASP.NET Core in {{site.data.keyword.Bluemix}} basiert auf dem Buildpack 'ASP.NET Core'. ASP.NET Core
ist ein modulares Open-Source-Framework zum Erstellen von .NET-Webanwendungen.
.Net Core ist eine kleine, plattformübergreifende Laufzeit, die von ASP.NET Core-Anwendungen als Ziel verwendet werden kann.
Gemeinsam ermöglichen sie moderne, cloudbasierte Webanwendungen.
{: shortdesc}

## Erkennung
{: #detection}
Das Bluemix-Buildpack 'ASP.NET Core' wird verwendet, wenn es irgendwo in der Anwendung mindestens eine Datei project.json gibt
 oder wenn die Anwendung mit einer Push-Operation aus dem Ausgabeverzeichnis des Befehls *dotnet publish* übertragen wird.

## Starteranwendung
{: #starter_application}

{{site.data.keyword.Bluemix}} stellt eine ASP.NET Core-Starteranwendung bereit. Die ASP.NET Core-Starteranwendung ist eine einfache App, die eine Schablone bereitstellt, die Sie verwenden können. Sie können mit der Starter-App experimentieren, Änderungen an der Bluemix-Umgebung vornehmen und diese mit einer Push-Operation übertragen.  Hilfe zur Verwendung der Starteranwendung finden Sie in [Starteranwendungen verwenden](../../cfapps/starter_app_usage.html).

## Laufzeitversionen
{: #runtime_versions}

### .NET-CLI-Version angeben

Steuern Sie die .NET-CLI-Version mit einer optionalen Datei global.json im Stammverzeichnis der Anwendung. Beispiel:
```
   {
      "projects": [ "src" ],
      "sdk": {
        "version": "1.0.0-preview1-002702"
      }
   }
```
{: codeblock}

Wenn keine Angabe erfolgt, wird die aktuellste stabile Vor-Releaseversion verwendet.

### NuGet-Paketquellen anpassen

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

## Veröffentlichte Anwendung mit einer Push-Operation übertragen

Wenn Sie möchten, dass Ihre Anwendung alle erforderlichen Binärdateien enthält, sodass das Buildpack keine
externen Binärdateien herunterlädt, können Sie eine veröffentlichte *eigenständige* Anwendung mit einer Push-Operation
übertragen. Weitere Informationen zu eigenständigen Anwendungen finden Sie in
[Portierbarkeitstypen in .Net Core](http://dotnet.github.io/docs/core-concepts/app-types.html){: new_window}.

Geben Sie zum Veröffentlichen einer Anwendung einen Befehl wie den folgenden ein:
```
  dotnet publish -r ubuntu.14.04-x64 
```
{: codeblock}
  
Die App kann dann mit einer Push-Operation aus dem Verzeichnis
```
  bin/<Debug|Release>/<framework>/<laufzeit>/publish
```
{: codeblock}
übertragen werden.

Beachten Sie auch, dass Sie, wenn Sie in Ihrer Anwendung eine Datei manifest.yml verwenden, den Pfad des Ausgabeordners 'publish' in Ihrer Datei manifest.yml angeben können. In diesem Fall müssen Sie sich nicht in diesem Ordner befinden, wenn Sie die Anwendung mit einer Push-Operation übertragen.

## Apps mit mehreren Projekten bereitstellen

Wenn Sie eine App bereitstellen, die mehrere Projekte enthält, müssen Sie angeben, welches Projekt das Buildpack als Hauptprojekt ausführen soll. Dies kann erfolgen, indem eine .deployment-Datei im Stammordner der Lösung erstellt wird, in der der Pfad für das Hauptprojekt angegeben wird. Der Pfad für das Hauptprojekt kann über den Projektordner oder die Projektdatei (.xproj bzw. .csproj) angegeben werden.

Wenn beispielsweise eine Lösung die drei Projekte *MyApp.DAL*, *MyApp.Services* und *MyApp.Web* im Ordner *src* enthält und *MyApp.Web* das Hauptprojekt ist, würde das Format der .deployment-Datei wie folgt aussehen:
```
  [config]
  project = src/MyApp.Web
```
{: codeblock}

In diesem Beispiel würde das Buildpack automatisch die Projekte *MyApp.DAL* und *MyApp.Services* kompilieren, wenn sie in der Datei project.json für *MyApp.Web* als Abhängigkeiten aufgelistet sind, aber das Buildpack würde nur versuchen, das Hauptprojekt, *MyApp.Web*, mit dotnet run -p src/MyApp.Web auszuführen. Der Pfad für *MyApp.Web* könnte, falls es sich bei diesem Projekt um ein xproj-Projekt handelt, auch wie folgt angegeben werden: 
```
  project = src/MyApp.Web/MyApp.Web.xproj 
```
{: codeblock}

## Beispiele aus dem Repository für CLI-Beispiele und Vorlagen von Visual Studio verwenden

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

Fügen Sie die folgende Abhängigkeit der Datei project.json hinzu: 
```
  "Microsoft.Extensions.Configuration.CommandLine": "1.0.0-rc2-final",
```
{: codeblock}

Fügen Sie der Datei, die Ihre Methode 'Main' enthält, eine Anweisung *using* hinzu: 
```
  using Microsoft.Extensions.Configuration;
```
{: codeblock}

# Zugehörige Links
{: #rellinks}
## Allgemein
{: #general}
* [Neueste Aktualisierungen für das Buildpack 'ASP.NET Core'](updates.html)
* [NuGet](https://docs.nuget.org/Consume/Overview){: new_window}
* [Übersicht über ASP.NET Core](http://docs.asp.net/en/latest/conceptual-overview/aspnet.html){: new_window}
