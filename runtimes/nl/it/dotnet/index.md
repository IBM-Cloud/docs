---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# ASP.NET Core 
{: #dotnet_core}
*Ultimo aggiornamento: 30 maggio 2016*

Il runtime ASP.NET Core su {{site.data.keyword.Bluemix}} si avvale della tecnologia del pacchetto di build ASP.NET Core. ASP.NET Core
è un framework open source modulare per la creazione di applicazioni web .NET.
.Net Core è un runtime piccolo, multipiattaforma che può essere destinato alle applicazioni ASP.NET Core.
Forniscono un'abilitazione moderna, basata sul cloud per le applicazioni web.
{: shortdesc}

## Rilevamento
{: #detection}
Il pacchetto di build Bluemix ASP.NET Core viene utilizzato se sono presenti nell'applicazione uno o più file project.json o
 se l'applicazione viene trasmessa dalla directory di output del comando *dotnet publish*.

## Applicazione starter
{: #starter_application}

{{site.data.keyword.Bluemix}} fornisce un'applicazione starter ASP.NET Core.  L'applicazione starter ASP.NET Core è una semplice applicazione che fornisce un template che puoi utilizzare. Puoi fare delle prove con l'applicazione starter, apportare modifiche ed eseguirne il push all'ambiente Bluemix.  Consulta [Utilizzo di applicazioni starter](../../cfapps/starter_app_usage.html) per informazioni sull'utilizzo dell'applicazione starter.

## Versioni di runtime
{: #runtime_versions}

### Specifica della versione CLI .NET

Controlla la versione CLI .NET con un global.json facoltativo nella directory root dell'applicazione. Ad esempio:
```
   {
      "projects": [ "src" ],
      "sdk": {
        "version": "1.0.0-preview1-002702"
      }
   }
```
{: codeblock}

Se non specificata, viene utilizzata la più stabile e corrente versione di Release Candidate.

### Personalizzazione delle origini dei pacchetti NuGet

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

## Esecuzione del push di un'applicazione pubblicata

Se desideri che la tua applicazione contenga tutti i propri binari richiesti così che il pacchetto di build non scarichi
binari esterni, puoi eseguire il push di un'applicazione *self-contained* pubblicata.  Consulta [Types of portability in .Net Core](http://dotnet.github.io/docs/core-concepts/app-types.html){: new_window}
per ulteriori informazioni sulle applicazioni autonome.

Per pubblicare un'applicazione immetti un comando tipo:
```
  dotnet publish -r ubuntu.14.04-x64 
```
{: codeblock}
  
Dopodiché l'applicazione può essere trasmessa alla directory
```
  bin/<Debug|Release>/<framework>/<runtime>/publish
```
{: codeblock}
.

Inoltre tieni presente che se stai utilizzando un file manifest.yml nella tua applicazione, puoi specificare il percorso nella cartella di output di pubblicazione nel tuo manifest.yml.  Quindi non devi essere in tale cartella quando esegui il push dell'applicazione.

## Distribuzione di applicazioni con più progetti

Per distribuire un'applicazione che contiene più progetti, devi specificare su quale progetto eseguire il pacchetto di build come progetto principale. Ciò può essere eseguito creando un file .deployment nella cartella root della soluzione, che imposti il percorso per il progetto principale. Il percorso al progetto principale può essere specificato come la cartella del progetto o il file del progetto (.xproj o .csproj).

Ad esempio se una soluzione contiene tre progetti, *MyApp.DAL*, *MyApp.Services* e *MyApp.Web* nella cartella *src* e per cui *MyApp.Web* è il progetto principale, il formato del file .deployment deve essere come il seguente:
```
  [config]
  project = src/MyApp.Web
```
{: codeblock}

In questo esempio, il pacchetto di build compilerà automaticamente i progetti *MyApp.DAL* e *MyApp.Services* se sono elencati come dipendenze nel file project.json per *MyApp.Web*, ma il pacchetto di build tenterà soltanto di eseguire il progetto principale, *MyApp.Web*, con dotnet run -p src/MyApp.Web. Il percorso a *MyApp.Web*, assumendo che questo progetto sia un progetto xproj, può anche essere specificato come 
```
  project = src/MyApp.Web/MyApp.Web.xproj 
```
{: codeblock}

## Utilizzando gli esempi dal repository esempi-cli e dal template Visual Studio

Il pacchetto di build eseguirà la tua applicazione con il comando *dotnet run* e passerà il seguente argomento di riga di comando
```
  --server.urls http://0.0.0.0:${PORT}
```
{: codeblock}

La tua applicazione ha bisogno di passare questo argomento al kestrel per essere certi che kestrel sia in ascolto sulla porta corretta.

Per implementare il passaggio di questo argomento, gli esempi forniti nel repository esempi-cli e nei template forniti da Visual Studio,
richiedono lievi modifiche prima della distribuzione a Bluemix.

Le modifiche richieste al metodo principale sono annotate nei commenti nel seguente esempio:

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

Aggiungi la seguente dipendenza a project.json: 
```
  "Microsoft.Extensions.Configuration.CommandLine": "1.0.0-rc2-final",
```
{: codeblock}

Aggiungi un'istruzione *using* al file che contiene il metodo principale: 
```
  using Microsoft.Extensions.Configuration;
```
{: codeblock}

# rellinks
{: #rellinks}
## general
{: #general}
* [Aggiornamenti più recenti al pacchetto di build ASP.NET Core](updates.html)
* [NuGet](https://docs.nuget.org/Consume/Overview){: new_window}
* [Panoramica ASP.NET Core](http://docs.asp.net/en/latest/conceptual-overview/aspnet.html){: new_window}
