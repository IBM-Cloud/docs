---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-03-15"

---

{:shortdesc: .shortdesc}
{:codeblock:.codeblock}

Il servizio {{site.data.keyword.amafull}} è stato sostituito con il servizio {{site.data.keyword.appid_full}}.

# Protezione delle risorse di back-end con il servizio {{site.data.keyword.amashort}}
{: #protecting-resources}


Con il servizio {{site.data.keyword.amafull}}, puoi proteggere le tue applicazioni di back-end basate su Java e Node.js in esecuzione su {{site.data.keyword.Bluemix_notm}} con monitoraggio e sicurezza OAth abilitati ai dispositivi mobili.
{:shortdesc}

## Prima di cominciare
{: #before-you-begin}
Prima di iniziare, assicurati che il servizio Node.js esista nella tua applicazione di backend {{site.data.keyword.Bluemix_notm}}.


## Filtro di autorizzazione
{: #auth-filter}
L'SDK server {{site.data.keyword.amashort}} ha dei filtri di autorizzazione che puoi utilizzare per proteggere le tue applicazioni di back-end.  Il filtro di autorizzazione intercetta le richieste in entrata e convalida se un'intestazione di autorizzazione è presente. Se l'intestazione di autorizzazione non è presente o non è valida, il filtro restituisce una risposta con HTTP 401. L'SDK client {{site.data.keyword.amashort}} sa come intercettare una risposta HTTP 401 restituita dall'SDK server {{site.data.keyword.amashort}} e attiva il flusso di autenticazione.
## Intestazione di autorizzazione
{: #auth-header}
L'intestazione di autorizzazione nella richiesta in entrata consiste di tre parti: Bearer, Token di accesso e Token ID, separate da spazi. Il `Token di accesso` è un componente obbligatorio mentre il `Token ID` è facoltativo.

L'intestazione di autorizzazione in entrata è elaborata dal rispettivo filtro di autorizzazione. Il filtro convalida l'integrità strutturale, la data di scadenza e le firme di token ID e token di accesso. Dopo che la convalida è stata superata, all'oggetto della richiesta viene aggiunto un oggetto di contesto di sicurezza. Puoi ottenere un riferimento al contesto di sicurezza utilizzando un'API pertinente.

Il contesto di sicurezza contiene le informazioni su oggetto, utente, dispositivo e applicazione, memorizzate con la seguente struttura:
```JSON
{
    "imf.sub":"myclientid",
    "imf.user": {
        "id":"user-name",
        "authBy":"myrealm",
        "displayName":"display-name"
    },
    "imf.device": {
        "id":"device-id",
        "platform":"iOSnative",
        "model":"device-model",
        "osVersion":"device-os"
    },
    "imf.application": {
        "id":"ios.bundle.id",
        "version":"1.0"
    }
}
```
{: codeblock}

* `imf.sub`: specifica l'oggetto del token ID o dell'ID univoco del client se non esiste alcun token ID.
* `imf.user`: specifica l'identità utente estratta dal token ID. Se non esiste alcun token ID, questo campo contiene un oggetto vuoto.
* `imf.device`: specifica l'identità dispositivo estratta dal token ID. Se non esiste alcun token ID, questo campo contiene un oggetto vuoto.
* `imf.application`: specifica l'identità applicazione estratta dal token ID. Se non esiste alcun token ID, questo campo contiene un oggetto vuoto.

## Fasi successive
{: #next-steps}
* [Protezione di risorse Node.js](protecting-resources-nodejs.html)
* [Protezione di risorse Liberty for Java&trade;](protecting-resources-java.html)
* [Sviluppo locale](protecting-resources-local.html)
