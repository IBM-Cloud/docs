---

copyright:
  years: 2015, 2016
  
---

# Utilizzo di Google per autenticare gli utenti
{: #google-auth}
Puoi configurare il servizio {{site.data.keyword.amashort}} per proteggere le risorse utilizzando Google come provider di identità. I tuoi utenti dell'applicazione mobile possono quindi utilizzare le loro credenziali Google per l'autenticazione.

**Importante:** non devi necessariamente installare separatamente l'SDK Google. L'SDK Google viene installato automaticamente dai gestori dipendenze quando configuri l'SDK client {{site.data.keyword.amashort}}.

## Flusso {{site.data.keyword.amashort}}
{: #google-auth-overview}

Consulta il seguente diagramma semplificato per comprendere in che modo {{site.data.keyword.amashort}} si integra con Google per l'autenticazione.

![immagine](images/mca-sequence-google.jpg)

1. Usa l'SDK {{site.data.keyword.amashort}} per effettuare una richiesta alle tue risorse di backend protette con l'SDK server {{site.data.keyword.amashort}}.
* L'SDK server {{site.data.keyword.amashort}} rileva la richiesta non autorizzata e restituisce un codice HTTP 401 e l'ambito di autorizzazione.
* L'SDK client {{site.data.keyword.amashort}} rileva automaticamente il codice HTTP 401 e avvia il processo di autenticazione.
* l'SDK client {{site.data.keyword.amashort}} contatta il servizio {{site.data.keyword.amashort}} e chiede di emettere un'intestazione di autorizzazione.
* Il servizio {{site.data.keyword.amashort}} chiede al client di eseguire prima l'autenticazione con Google fornendo una richiesta di verifica dell'autenticazione.
* L'SDK client {{site.data.keyword.amashort}} utilizza l'SDK Google per avviare il processo di autenticazione. Dopo un'autenticazione con esito positivo, l'SDK Google restituisce un token di accesso Google.
* Il token di accesso Google è considerato una risposta alla richiesta di verifica dell'autenticazione. Il token viene inviato al servizio {{site.data.keyword.amashort}}.
* Il servizio convalida la risposta alla richiesta di verifica dell'autenticazione presso i server Google.
* Se la convalida ha esito positivo, il servizio {{site.data.keyword.amashort}} genera un'intestazione di autorizzazione e la restituisce all'SDK client {{site.data.keyword.amashort}}. L'intestazione di autorizzazione contiene due token: un token di accesso che contiene le informazioni sulle autorizzazioni di accesso e il token ID che contiene le informazioni su utente, dispositivo e applicazione correnti.
* Da questo punto in avanti, tutte le richieste effettuate mediante l'SDK client {{site.data.keyword.amashort}} hanno un'intestazione di autorizzazione di nuova acquisizione.
* L'SDK client {{site.data.keyword.amashort}} reinvia automaticamente la richiesta originale che ha attivato il flusso di autorizzazione.
* L'SDK server {{site.data.keyword.amashort}} estrae l'intestazione di autorizzazione dalla richiesta, la convalida presso il servizio {{site.data.keyword.amashort}} e concede l'accesso a una risorsa di backend.

## Fasi successive
{: #google-auth-nextsteps}

* [Abilitazione dell'autenticazione Google nelle applicazioni Android](google-auth-android.html)
* [Abilitazione dell'autenticazione Google nelle applicazioni iOS](google-auth-ios.html)
* [Abilitazione dell'autenticazione Google nelle applicazioni Cordova](google-auth-cordova.html)
