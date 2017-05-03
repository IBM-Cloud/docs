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

Il runtime ASP.NET Core su {{site.data.keyword.Bluemix}} si avvale della tecnologia del pacchetto di build ASP.NET Core. ASP.NET Core
è un framework open source modulare per la creazione di applicazioni web .NET.
.Net Core è un runtime piccolo, multipiattaforma che può essere destinato alle applicazioni ASP.NET Core.
Forniscono un'abilitazione moderna, basata sul cloud per le applicazioni web.
{: shortdesc}

## Rilevamento
{: #detection}
Il pacchetto di build Bluemix ASP.NET Core viene utilizzato se sono presenti nell'applicazione una più cartelle contenenti un file project.json o almeno un file .cs oppure
 se l'applicazione viene trasmessa dalla directory di output del comando *dotnet publish*.

## Applicazione starter
{: #starter_application}

{{site.data.keyword.Bluemix}} fornisce un'applicazione starter ASP.NET Core.  L'applicazione starter ASP.NET Core è una semplice applicazione che fornisce un template che puoi utilizzare. Puoi fare delle prove con l'applicazione starter, apportare modifiche ed eseguirne il push all'ambiente Bluemix.  Consulta [Utilizzo di applicazioni starter](/docs/cfapps/starter_app_usage.html) per informazioni sull'utilizzo dell'applicazione starter.

## Versioni di runtime
{: #runtime_versions}

### Versioni supportate
{: #supported_versions}
Questo pacchetto di build supporta le seguenti versioni, quelle contrassegnate come obsolete saranno rimosse in una futura release del pacchetto di build. Consulta [Microsoft's support statement for LTS and Current releases](https://www.microsoft.com/net/core/support).

#### Strumento project.json (obsoleto)

| Versione SDK .NET        | Predefinito |
|-------------------------|---------|
| 1.0.0-preview2-003156   |   No    |
| 1.0.0-preview2-1-003177 |   No    |

#### Strumento SDK MSBuild

| Versione SDK .NET        | Predefinito |
|-------------------------|---------|
| 1.0.0-preview4-004233   |   No    |
| 1.0.1                   |   Sì   |

#### Versioni runtime .NET Core

| Version runtime .NET Core | Tipo di rilascio | Predefinito |
|---------------------------|--------------|---------|
| 1.0.0                     | LTS          |   No    |
| 1.0.1                     | LTS          |   No    |
| 1.0.3                     | LTS          |   No    |
| 1.0.4                     | LTS          |   Sì   |
| 1.1.0                     | Corrente      |   No    |
| 1.1.1                     | Corrente      |   No    |

### Specifica della versione della SDK .NET

Controlla la versione della SDK .NET con un global.json facoltativo nella directory root dell'applicazione. Ad esempio:
```
   {
      "projects": [ "src" ],
      "sdk": {
        "version": "1.0.1"
      }
   }
```
{: codeblock}

Se non specificato, viene utilizzato lo strumento MSBuild per l'ultimo runtime Long-term-support (LTS).  Per utilizzare lo strumento project.json, puoi specificare una delle versioni project.json precedentemente elencate ma devi anche tenere presente che queste versioni saranno rimosse in futuro.

## Personalizzazione delle origini dei pacchetti NuGet
{: #customizing_nuget_package_sources}

Controlla dove le dipendenze della tua applicazione vengono scaricate dal file NuGet.Config nella directory root dell'applicazione. Ad esempio:
```
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
   <packageSources>
      <add key="NuGet.org" value="https://api.nuget.org/v3/index.json"/>
   </packageSources>
   </configuration>
```
{: codeblock}

## Sviluppo delle applicazioni localmente
{: #developing_locally}

Per ulteriori informazioni sull'esecuzione di un'applicazione ASP.NET Core localmente, consulta
[Getting Started with ASP.NET](http://docs.asp.net/en/latest/getting-started/index.html).
Per conoscere il più precisamente possibile come l'applicazione venga eseguita su Bluemix, seguire le istruzioni Linux per .NET Core, ma lo sviluppo dell'applicazione su Linux non è richiesto.

Lo strumento Yeoman può essere utilizzato per generare nuovi template del progetto come descritto in
[Building Projects with Yeoman](http://docs.asp.net/en/latest/client-side/yeoman.html).

Per informazioni sullo sviluppo locale utilizzando Visual Studio, consulta [Sviluppo con Visual Studio](/docs/starters/deploy_vs.html){: new_window}.

## Esecuzione del push di un'applicazione pubblicata
{: #pushing_published_app}

Se desideri che la tua applicazione contenga tutti i propri binari richiesti così che il pacchetto di build non scarichi
binari esterni, puoi eseguire il push di un'applicazione *self-contained* pubblicata.  Consulta
[.NET Core App Types](https://docs.microsoft.com/en-us/dotnet/articles/core/app-types){: new_window}
per ulteriori informazioni sulle applicazioni autonome.

Per pubblicare un'applicazione immetti un comando tipo:
```
  dotnet publish -r ubuntu.14.04-x64
```
{: codeblock}

Per le applicazioni autonome, l'applicazione può essere trasmessa alla directory
```
  bin/<Debug|Release>/<framework>/<runtime>/publish
```
{: codeblock}
.

Per le applicazioni portatili, l'applicazione può essere trasmessa da
```
  bin/<Debug|Release>/<framework>/publish
```
{:codeblock}
.

Inoltre tieni presente che se stai utilizzando un file manifest.yml nella tua applicazione, puoi specificare il percorso nella cartella di output di pubblicazione nel tuo manifest.yml.  Quindi non devi essere in tale cartella quando esegui il push dell'applicazione.

## Distribuzione di applicazioni con più progetti
{: #developing_apps_with_multiple_projects}

Per distribuire un'applicazione che contiene più progetti, devi specificare su quale progetto eseguire il pacchetto di build come progetto principale. Ciò può essere eseguito creando un file .deployment nella cartella root della soluzione, che imposti il percorso per il progetto principale. Il percorso al progetto principale può essere specificato come la cartella del progetto o il file del progetto (.xproj o .csproj).

Ad esempio se una soluzione contiene tre progetti, *MyApp.DAL*, *MyApp.Services* e *MyApp.Web* nella cartella *src* e per cui *MyApp.Web* è il progetto principale, il formato del file .deployment deve essere come il seguente:
```
  [config]
  project = src/MyApp.Web/MyApp.Web.csproj
```
{: codeblock}

In questo esempio, il pacchetto di build compilerà automaticamente i progetti *MyApp.DAL* e *MyApp.Services* se sono elencati come dipendenze nel file project.json per *MyApp.Web*, ma il pacchetto di build tenterà soltanto di eseguire il progetto principale, *MyApp.Web*, con dotnet run -p src/MyApp.Web.

## Configurazione dell'applicazione
{: #application_configuration}

### Configurazione della tua applicazione per ascoltare sulla porta appropriata
{: #configuring_listen_proper_port}

Il pacchetto di build eseguirà la tua applicazione con il comando *dotnet run* e passerà il seguente argomento di riga di comando
```
  --server.urls http://0.0.0.0:${PORT}
```
{: codeblock}

La tua applicazione ha bisogno di passare questo argomento al kestrel per essere certi che kestrel sia in ascolto sulla porta corretta.

Per implementare il passaggio di questo argomento, gli esempi forniti nel repository esempi-cli e nei template forniti da Visual Studio,
richiederanno lievi modifiche prima della distribuzione a Bluemix. 

Le modifiche richieste al metodo principale sono annotate nei commenti nel seguente esempio:

<pre>
  public static void Main(string[] args)
  {
    var config = new ConfigurationBuilder() //AGGIUNGI QUESTE 3 RIGHE ALL'INIZIO DEL METODO PRINCIPALE
        .AddCommandLine(args)
        .Build();

    var host = new WebHostBuilder()
        .UseKestrel()
        .UseConfiguration(config) //AGGIUNGI QUESTA RIGA PRIMA DI 'UseStartup'
        .UseStartup&lt;Startup&gt;()
        .Build();
    host.Run();
}
</pre>
{: codeblock}

Per lo strumento project.json, aggiungi questa riga al tuo file project.json:
```
  "Microsoft.Extensions.Configuration.CommandLine": "1.0.1",
```
{: codeblock}

Per lo strumento MSBuild, aggiungi questa riga al tuo file .csproj:
```
  <PackageReference Include="Microsoft.Extensions.Configuration.CommandLine" Version="1.0.1" />
```
{:codeblock}

Aggiungi un'istruzione *using* al file che contiene il metodo principale:
```
  using Microsoft.Extensions.Configuration;
```
{: codeblock}

### Assicurati che la tua applicazione abbia tutti i file necessari nella cartella di output della build.
{: #configure_output_files}

#### Utilizzo dello strumento project.json

Aggiungi la seguente proprietà alla sezione `buildOptions` di project.json:
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

Nel metodo `Startup` Startup.cs, rimuovi la seguente riga:
```
  .SetBasePath(env.ContentRootPath)
```
{: codeblock}

Nel metodo `Main` Program.cs, rimuovi la seguente riga:
```
  .UseContentRoot(Directory.GetCurrentDirectory())
```
{: codeblock}

Queste modifiche consentono alla CLI .NE di trovare le `Views` della tua applicazione che saranno ora copiate nell'output di build quando viene eseguito il comando `dotnet run`.  Se la tua applicazione dispone di altri file, come ad esempio dei file di configurazione json, richiesti durante il runtime, devi quindi aggiungerli nella sezione `include` di `copyToOutput` nel file project.json del tuo progetto. 

#### Utilizzo dello strumento MSBuild

Aggiungi un elemento `<Content>` all'elemento `<ItemGroup>` per il tuo file .csproj:
```
  <ItemGroup>
    <Content Include="wwwroot/**/*;Areas/**/Views/*;Views/*;appsettings.json">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
      <CopyToPublishDirectory>Always</CopyToPublishDirectory>
    </Content>
  </ItemGroup>
```
{: codeblock}

Nel metodo `Startup` Startup.cs, rimuovi la seguente riga:
```
  .SetBasePath(env.ContentRootPath)
```
{: codeblock}

Nel metodo `Main` Program.cs, rimuovi la seguente riga:
```
  .UseContentRoot(Directory.GetCurrentDirectory())
```
{: codeblock}

Queste modifiche consentono alla CLI .NE di trovare le `Views` della tua applicazione che saranno ora copiate nell'output di build quando viene eseguito il comando `dotnet publish`.  Se la tua applicazione dispone di altri file, come ad esempio dei file di configurazione json, richiesti durante il runtime, devi quindi aggiungerli nella proprietà `Include` dell'elemento `Content` nel file .csproj del tuo progetto, separati da punti e virgola.

## Compilazione della tua applicazione nella configurazione della release (solo MSBuild)
{: #compiling_in_release_configuration}

I progetti basati su MSBuild vengono ora pubblicati utilizzando il comando `dotnet publish` durante la fase di preparazione.  Per impostazione predefinita, il pacchetto di build pubblicherà la tua applicazione nella configurazione `Debug`.
Per pubblicare la tua applicazione nella configurazione `Release`, imposta la variabile di ambiente `PUBLISH_RELEASE_CONFIG` su `true`.

Puoi farlo con la CLI CloudFoundry con il seguente comando:

```shell
  cf set-env <app_name> PUBLISH_RELEASE_CONFIG true
```

In alternativa, puoi impostare la variabile nel file manifest.yml della tua applicazione:

```yml
---
applications:
- name: sample-aspnetcore-app
  memory: 512M
  env:
    PUBLISH_RELEASE_CONFIG: true
```

## Disabilitazione della cache del pacchetto NuGet
{: #disabling_the_nuget_package_cache}

In alcune situazioni potrebbe essere necessario cancellare la cache del pacchetto NuGet della tua applicazione.  In questo modo cancelli tutti i pacchetti NuGet nella cache esistenti ed eviti la memorizzazione nella cache del pacchetto di build per tutti i nuovi pacchetti.

Puoi farlo impostando la variabile di ambiente `CACHE_NUGET_PACKAGES` su `false` utilizzando la CLI CloudFoundry:

```shell
  cf set-env <app_name> CACHE_NUGET_PACKAGES false
```

In alternativa, puoi impostare la variabile di ambiente `CACHE_NUGET_PACKAGES` su `false` nel file manifest.yml della tua applicazione:

```yml
---
applications:
- name: sample-aspnetcore-app
  memory: 512M
  env:
    CACHE_NUGET_PACKAGES: false
```

## Utilizzo delle librerie native personalizzate.
{: #using_custom_native_libraries}

Alcune librerie possono richiederti di utilizzare sia un pacchetto NuGet che alcuni file della libraria nativa (file .so).  Per poter utilizzare queste librerie con il pacchetto di build, dovresti posizionarle in una cartella denominata "ld_library_path" nella cartella root della tua applicazione.
Il pacchetto di build aggiungerà automaticamente questo percorso alla variabile di ambiente `LD_LIBRARY_PATH` durante la fase di preparazione.  In alternativa, puoi specificare la variabile di ambiente `LD_LIBRARY_PATH` nel file `manifest.yml` della tua applicazione o utilizzando il comando `cf set-env` per utilizzare un nome della cartella differente da "ld_library_path".  In questo caso, il pacchetto di build accoderà questo percorso personalizzato alla variabile `LD_LIBRARY_PATH` generata dal pacchetto di build.

## Domande frequenti (FAQ) sulla risoluzione dei problemi
{: #troubleshooting_faq}

**Q**: la mia applicazione non può distribuire il messaggio: `API/0App instance exited ... payload: {... "reason"=>"CRASHED", "exit_status"=>-1, ...}`.  Cosa significa?

**A**: se stai ricevendo un messaggio simile quando esegui il push della tua applicazione, molto probabilmente la tua applicazione sta superando i limiti della quota di memoria o del disco.  Questo problema può essere risolto incrementando le quote della tua applicazione.

**Q**: impossibile eseguire la distribuzione della mia applicazione con il messaggio di errore: `Impossibile comprimere il droplet: segnale: pipe interrotta` o `Mancanza di spazio sul dispositivo`.  In che modo è possibile correggere l'errore? 

**A**: i progetti trasmessi dal codice di origine che contiene una grande numero di dipendenze del pacchetto NuGet può a volte causare questo errore quando viene abilitata la cache del pacchetto NuGet.  Imposta la variabile di ambiente `CACHE_NUGET_PACKAGES` su `false` per disabilitare la cache.

# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
* [NuGet](https://docs.nuget.org/Consume/Overview){: new_window}
* [Panoramica ASP.NET Core](http://docs.asp.net/en/latest/conceptual-overview/aspnet.html){: new_window}
