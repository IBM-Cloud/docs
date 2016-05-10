---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}
# Modalità sandbox e di produzione

{: #push-sandboxandproduction-modes}

Puoi utilizzare le notifiche di push in una delle seguenti modalità: sandbox o
                produzione. Sandbox è un ambiente di test autonomo per sviluppare e testare l'integrazione
                della API di push con il servizio push dell'applicazione del server. Per prima cosa configura il sandbox e le modalità di produzione utilizzando il dashboard Push. Passa alla modalità dell'operazione per eseguire il servizio di push tra il sandbox e la produzione utilizzando l'[API REST di Push](https://mobile.{DomainName}/imfpushrestapidocs/){: new_window} . Per impostazione predefinita,
                la modalità sandbox è abilitata. Tuttavia, quando passi da una modalità all'altra, le tag, i dispositivi e le sottoscrizioni non sono condivisi tra queste modalità.


Quando sei pronto a distribuire l'applicazione a un ambiente live, seleziona la modalità di PRODUZIONE utilizzando l'API REST di push. Per informazioni sulla API REST, consulta l'API REST.

Per passare alla modalità di operazione del servizio di push dal sandbox alla produzione:

1. Utilizza la chiamata API REST delle impostazioni ApplicationID PUT
2. Nel corpo JSON, conferma che la modalità è stata passata utilizzando la chiamata API [REST delle impostazioni ApplicationID PUT](https://mobile.{DomainName}/imfpushrestapidocs/){: new_window} . La risposta prevista è "mode": "PRODUCTION
 
 ```
 { 
 "mode": "PRODUCTION"
 }
 ```
1. Dopo che è stata passata la tua modalità di ambiente, riesegui il tuo codice client per registrare il tuo dispositivo nella modalità di PRODUZIONE.

Per informazioni sulla API REST, consulta l'API REST.
