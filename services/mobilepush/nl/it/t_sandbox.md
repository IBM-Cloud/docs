---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Modalità sandbox e di produzione
{: #push-sandboxandproduction-modes}
Ultimo aggiornamento: 11 gennaio 2017
{: .last-updated}

Puoi utilizzare {{site.data.keyword.mobilepushshort}} in una delle seguenti modalità: sandbox o produzione. Sandbox è un ambiente di test autonomo per sviluppare e testare l'integrazione
                della API di push con il servizio push dell'applicazione del server. 

Configura le modalità sandbox e di produzione utilizzando il dashboard Push. Puoi passare dalla modalità operativa sandbox alla modalità di produzione del servizio di push utilizzando l'[API REST Push](https://mobile.{DomainName}/imfpush/){: new_window}. Per impostazione predefinita, è abilitata la modalità sandbox. Tuttavia, quando passi da una modalità all'altra, le tag, i dispositivi e le sottoscrizioni non sono condivisi tra queste modalità.

Quando sei pronto a distribuire l'applicazione a un ambiente live, seleziona la modalità di PRODUZIONE utilizzando l'[API REST Push](https://mobile.{DomainName}/imfpush/){: new_window}. 

Per passare alla modalità di operazione del servizio di push dal sandbox alla produzione:

1. Utilizza la chiamata API REST delle impostazioni ApplicationID PUT
2. Nel corpo JSON, conferma che la modalità è stata passata utilizzando la chiamata API [REST delle impostazioni ApplicationID PUT](https://mobile.{DomainName}/imfpush/){: new_window} . La risposta prevista è "mode": "PRODUCTION
```{ 
    "mode": "PRODUCTION"
 }
```
	{: codeblock}
1. Dopo che è stata passata la tua modalità di ambiente, riesegui il tuo codice client per registrare il tuo dispositivo nella modalità di PRODUZIONE.

Per informazioni sull'API REST, consulta [Utilizzo delle API REST](t_restapi.html).
