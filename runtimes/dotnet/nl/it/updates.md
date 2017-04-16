---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-06"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Aggiornamenti più recenti al pacchetto di build ASP.NET Core
{: #latest_updates}


Un elenco degli aggiornamenti più recenti nel pacchetto di build aspnet.

## 10 ottobre, 2016: aggiornamento del pacchetto di build ASP.NET Core v1.0.1-20161005-1225 

* Aggiunto il supporto per .NET Core 1.0.1
* Risolto un problema intermittente che causava un malfunzionamento della distribuzione durante la memorizzazione nella cache dei pacchetti NuGet

## 31 agosto, 2016: aggiornamento del pacchetto di build ASP.NET Core v1.0-20160826-1345

* Aggiunto supporto per l'esecuzione pre e post compilazione degli script utilizzando NPM e Bower per installare le librerie css e javascript di front-end.
* Spostato il pacchetto di build dallo stato Beta allo stato GA

## 11 luglio, 2016: aggiornamento del pacchetto di build ASP.NET Core v0.9-20160706-1603

Questa versione del pacchetto di build include le seguenti modifiche:

* Questa versione del pacchetto di build supporta la CLI .NET 1.0 Preview 2 build e .NET Core 1.0 RTM
* Il pacchetto di build continua a supportare la CLI .NET 1.0 Preview 1 e .NET Core 1.0 RC2
* La versione della CLI .NET predefinita da installare è ora 1.0.0-preview2-003121

## 10 giugno, 2016: aggiornamento del pacchetto di build ASP.NET Core v0.8.1-20160526-0957

Questa versione del pacchetto di build include le seguenti modifiche:

* Il nome del runtime è stato modificato da ASP.NET 5 a ASP.NET Core.
* Il numero della versione del pacchetto di build è incluso nell'output dello script di rilevamento.
* Questa versione del pacchetto di build rimuove il supporto per le applicazioni basate su DNX utilizzando CoreCLR RC1 e precedenti.
* Questa versione del pacchetto di build supporta la CLI .NET e .NET Core RC2.
* Il pacchetto di build individua i progetti tramite il file project.json o i file *.runtimeconfig.json dall'output di pubblicazione.

## 22 ottobre 2015: pacchetto di build ASP.NET 5 aggiornato v0.7-20151022-1257

* Questa versione del pacchetto di build rimuove Mono e supporta invece CoreCLR Beta 8.

## 18 settembre 2015: aggiornato il pacchetto di build ASP.NET 5 v0.6-20150916-1220

* Questa versione del pacchetto di build supporta le modifiche DNX della Beta 7 e può eseguire applicazioni che dipendono da release beta precedenti, attraverso il seguente comando di avvio personalizzato:

```
   dnx src/dotnetstarter kestrel --server.urls http://${VCAP_APP_HOST}:${PORT}
```
{: codeblock}

* L'utilizzo del server web Nowin è stato rimosso da questo pacchetto di build e viene invece utilizzato il server [Kestrel]{https://github.com/aspnet/KestrelHttpServer}.

# rellinks
{: #rellinks}
## general
{: #general}
* [Runtime Dotnet core](index.html)
