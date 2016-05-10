---

copyright:
 years: 2015, 2016

---

# Utilizzo delle API REST
{: #push-api-rest}

Puoi utilizzare una API (application program interface) REST (Representational State Transfer) per le notifiche di push. Puoi anche utilizzare l'SDK e le [Push API](https://mobile.{DomainName}/imfpushrestapidocs/) per sviluppare ulteriormente le tue applicazioni client.

Con la API REST
                Push, i client e le applicazioni server di backend possono accedere alle funzioni Push.

- Registrazioni di dispositivi
- Registrazioni
- messaggi
- Sottoscrizioni
- Tag

Per ottenere l'URL di base per la API REST:

1. Crea un'applicazione di backend nella sezione Contenitori tipo del catalogo Bluemix®, che esegue automaticamente il bind del servizio Push a questa applicazione. Se già hai
                        creato un'applicazione di backend, assicurati di eseguirne il bind al Push
                        Notification Service. 

1. Nella pagina principale del dashboard Bluemix, vai nell'area **Applicazioni** e quindi fai clic sulla tua applicazione.

3. Fai clic su OPZIONI MOBILI. I valori GUID di applicazione e instradamento sono
                            visualizzati nella parte superiore della pagina dei dettagli per la tua                             applicazione.



## Intestazione Accept-Language
{: #push-api-rest-accept}

L'intestazione "Accept-Language" specifica quale lingua utilizzare per i messaggi di errore generati in output dalla [API REST di Push](https://mobile.{DomainName}/imfpushrestapidocs/){: new_window}. Per i messaggi di errore sono supportate le
                seguenti lingue: cinese (semplificato), cinese, (tradizionale), inglese (US), tedesco, francese,
                italiano, giapponese, coreano, portoghese e spagnolo.

## appSecret
{: #push-api-rest-secret}

Quando un'applicazione esegue il bind alle notifiche di push, il servizio genera
                 una appSecret (una chiave univoca) e la passa nell'intestazione di risposta. Se stai utilizzando IBM® Push Notifications per la API Rest Bluemix, utilizza la guida di riferimento alle API REST per ottenere informazioni su quali API devi proteggere. Per informazioni sull'API REST, consulta la Guida di riferimento per la API REST.

L'intestazione di richiesta deve contenere l'appSecret. In caso contrario, il server restituisce un codice di errore
                401 Non autorizzato. Quando la notifica di push viene aggiunta a un'applicazione,
                viene creato uno specifico AppID. Come parte della risposta, ottieni un'intestazione denominata appSecret che viene utilizzata per la creazione di tag o l'invio di messaggi. L'operazione viene eseguita tramite i servizi nel catalogo o
                nel contenitore tipo.

Per ottenere il valore appSecret:

1. Fai clic sul * nome-applicazione* associato al servizio push.
2. Fai clic sul link **Visualizza credenziali** per visualizzare
                        l'appSecret (AppID).

La schermata **Visualizza credenziali** mostra le informazioni sull'AppSecret:

```
{
 "imfpush_Dev": [
   {
     "name": "testapp1",
     "label": "imfpush_Dev",
     "plan": "Basic",
     "credentials": {
       "url": "http://imfpush.ng.bluemix.net/imfpush/v1/apps/b615b280-b37e-4042-8815-38a758f234e2",
       "admin_url": "//mobile.ng.bluemix.net/imfpushdashboard/?appGuid=b615b280-b37e-4042-8815-38a758f234e2",
       "appSecret": "8dac71a5-2219-42b3-a9f3-dbb828ba1f04"  
       }
   }
 ]
}
``` 

##Filtri API REST di Push
{: #push-api-rest-filters}

I filtri definiscono un criterio di ricerca che limita i dati restituiti da una API GET di Push. Applica i filtri sul risultato dell'operazione Get che desideri filtrare. Il filtro limita il numero di voci incluse nel risultato. Ad esempio, puoi utilizzare un filtro per cercare una tag il cui nome inizia con "test". Puoi generare
                un filtro utilizzando la seguente sintassi.

**name**
Il nome campo su cui viene applicato il filtro.

**operator**
== (corrispondenza esatta) oppure =@ (contiene la sottostringa) che descrive la corrispondenza di filtro da utilizzare.

**expression**
I valori da includere nel risultato.

Quando in un'espressione vengono visualizzati una virgola o una barra rovesciata, è necessario eseguirne l'escape
                con una barra rovesciata.

Quando utilizzi più filtri, puoi combinarli utilizzando la logica AND e OR.\

- Per la logica AND, utilizza più filtri nella query.
- Per la logica OR, utilizza una virgola nell'espressione di filtro.
- Sia per la logica AND che per quella OR: una singola query può avere sia la logica AND sia quella OR. Ogni filtro viene valutato singolarmente prima che i filtri vengano combinati
                        in un'espressione AND.

Per l'API GET di dispositivo, sono supportate le seguenti combinazioni:
-Il nome è il campo piattaforma.
- Fatta eccezione per la piattaforma, l'operatore può essere == oppure =@
- Per la piattaforma, l'operatore deve essere ==. Se viene utilizzato l'operatore =@, il valore può essere una sottostringa.
- Se viene utilizzato ==, il valore deve essere una stringa di corrispondenza esatta.

Per la API GET di sottoscrizione, sono supportate le seguenti combinazioni:

- Il nome può essere uno di questi campi: tagName o deviceId
- Fatta eccezione per la piattaforma, l'operatore può essere == oppure =@
- Per la piattaforma, l'operatore deve essere ==
- Se viene utilizzato l'operatore =@, il valore può essere una sottostringa. Se viene utilizzato l'operatore ==, il valore deve essere una stringa di corrispondenza esatta.
- Per la API GET di tag, sono supportate le seguenti combinazioni:
- Il nome può essere uno dei seguenti campi: “name” o “description”
- Se viene utilizzato l'operatore =@, il valore può essere una sottostringa.
- Se viene utilizzato ==, il valore deve essere una stringa di corrispondenza esatta.
