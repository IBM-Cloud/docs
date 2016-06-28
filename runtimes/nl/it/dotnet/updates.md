---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Aggiornamenti più recenti al pacchetto di build ASP.NET Core 
{: #latest_updates}

*Ultimo aggiornamento: 10 giugno 2016*

Un elenco degli aggiornamenti più recenti nel pacchetto di build aspnet.

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
