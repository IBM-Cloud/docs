---

copyright:
  years: 2016, 2017
lastupdated: "2016-11-29"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Protezione del tuo server delle schede personalizzate
{: #securing_custom_cards}

I server delle schede personalizzate sono server web standard che ospitano il codice javascript delle schede personalizzate. Per assicurare l'integrità del tuo ambiente {{site.data.keyword.iot_short_notm}} devi proteggere il tuo server delle schede personalizzate per proteggere l'origine della scheda come descritto in questo argomento.
{:shortdesc}

**Importante:** le schede personalizzate vengono al momento offerte come una funzione sperimentale e l'estensione delle schede personalizzate è abilitata per la sessione browser. La configurazione della connessione delle schede personalizzate e i pacchetti della scheda non sono condivisi globalmente nella tua organizzazione {{site.data.keyword.iot_short_notm}}.

## Requisito ruolo {{site.data.keyword.Bluemix_notm}}
{: #roles_requirements}

Devi disporre dei diritti da amministratore {{site.data.keyword.iot_short_notm}} per creare una connessione al server delle schede personalizzate.

## Considerazioni sulla sicurezza server delle schede personalizzate
{: #server_requirements}

I seguenti requisiti vengono impostati da {{site.data.keyword.iot_short_notm}}:
- La directory che utilizza il contenuto della scheda personalizzata sul server non deve richiedere credenziali di accesso.  
Nessuna autenticazione richiesta al server delle schede personalizzate durante il collegamento per accedere e caricare le schede personalizzate.
- Il server deve utilizzare il protocollo di sicurezza HTTP (HTTPS).
- Il server deve supportare le connessioni CORS (Cross-origin resource sharing).  

Per proteggere il codice delle schede personalizzate e il server delle schede stesso, il server delle schede deve essere individuato e protetto utilizzando delle misure difensive valide. Questo include la protezione firewall per limitare l'accesso al server delle schede personalizzate.

L'elaborazione della scheda personalizzata viene sempre effettuata tra un browser dell'utente e il server delle schede personalizzate. Il backend {{site.data.keyword.iot_short_notm}} non viene mai coinvolto nell'elaborazione o nella modifica del codice e delle informazioni delle schede personalizzate.

Non esistono restrizioni nel codice JavaScript che scegli di distribuire nelle tue schede nel tuo server delle schede personalizzate. Il codice Javascript nelle schede personalizzate ha accesso a tutte le informazioni detenute dal browser, così come a qualsiasi scheda in esecuzione nel dashboard.  Assicurati che il server delle schede personalizzato corretto stia fornendo il codice al browser per visualizzare ed elaborare le schede personalizzate.

Le schede eseguono il loro codice nella tua sessione del browser {{site.data.keyword.iot_short_notm}} esattamente come è scritto. Inoltre, la connessione al server delle schede personalizzate viene creata senza credenziali fornite al server delle schede personalizzate. Un browser dell'utente può collegarsi a un qualsiasi server delle schede personalizzate configurato.

È importante che configuri solo i server delle schede personalizzate sicuri e conosciuti per fornire le schede personalizzate ai dashboard dei tuoi utenti.   
