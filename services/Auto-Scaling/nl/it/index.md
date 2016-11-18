---

 

copyright:

  anni: 2015，2016
ultimo aggiornamento: "02-11-2016"  
 

---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Introduzione al servizio {{site.data.keyword.autoscaling}}
{: #autoscaling}
Ultimo aggiornamento: 02 novembre 2016
{: .last-updated}

In {{site.data.keyword.Bluemix_notm}}, puoi gestire automaticamente
la capacità della tua applicazione. Utilizza il servizio {{site.data.keyword.autoscaling}} per aumentare o ridurre
		automaticamente la capacità di calcolo della tua applicazione. Il numero di istanze
		dell'applicazione viene regolato in modo dinamico in base alla politica {{site.data.keyword.autoscaling}} da te definita.
{:shortdesc} 

## Sommario
  * [Utilizzo del servizio {{site.data.keyword.autoscaling}} in {{site.data.keyword.Bluemix_notm}}](#as-service)
  * [Configurazione delle applicazioni Node.js con il servizio {{site.data.keyword.autoscaling}}](#node-asagent)
  * [Gestire il servizio {{site.data.keyword.autoscaling}} tramite la API RESTful](#RESTAPI)
  * [Gestire il servizio {{site.data.keyword.autoscaling}} tramite la CLI {{site.data.keyword.autoscaling}}](#CLI)
  * [Campi della politica per il servizio {{site.data.keyword.autoscaling}}](#policy_fields)
  * [Messaggi di errore](#err_smsg)

## Utilizzo del servizio {{site.data.keyword.autoscaling}} in {{site.data.keyword.Bluemix_notm}}
{: #as-service}

Per utilizzare il servizio {{site.data.keyword.autoscaling}}, completa la seguente procedura:

1. Sul Dashboard {{site.data.keyword.Bluemix_notm}}, fai clic su *Aggiungi un servizio o una API* e seleziona quindi il servizio {{site.data.keyword.autoscaling}} dalla sezione DevOps del catalogo del servizio. Viene visualizzata una nuova finestra con una panoramica del servizio {{site.data.keyword.autoscaling}}.
2. Seleziona l'applicazione di cui vuoi eseguire il bind al servizio {{site.data.keyword.autoscaling}} e fai clic su
*Crea*. <br/>
*Ricorda:* puoi associare UN SOLO servizio {{site.data.keyword.autoscaling}} a un'applicazione. Se l'applicazione è già associata a un altro servizio {{site.data.keyword.autoscaling}},
      non selezionare l'applicazione in questo passo. In caso contrario, otterrai l'errore CWSCV2004E.<br/>Viene visualizzata la finestra Prepara di nuovo applicazione.
3. Nella finestra Prepara di nuovo applicazione, fai clic su *Riprepara* per ripreparare l'applicazione prima di utilizzare il nuovo servizio {{site.data.keyword.autoscaling}} appena aggiunto. <br/><ul><li>Per l'applicazione Liberty, il servizio {{site.data.keyword.autoscaling}} è configurato automaticamente ed è pronto per l'utilizzo dopo la ripreparazione dell'applicazione.</li> <li>Per le applicazioni Node.js, devi aggiornare il tuo codice dell'applicazione per abilitare il servizio {{site.data.keyword.autoscaling}} prima di eseguire il push dell'applicazione a {{site.data.keyword.Bluemix_notm}}. Per ulteriori dettagli, vedi [Configurazione delle applicazioni Node.js con il servizio {{site.data.keyword.autoscaling}}](index.html#node_asagent).</ul><br/>
Una volta completata la ripreparazione dell'applicazione, puoi iniziare a configurare il servizio {{site.data.keyword.autoscaling}} per la tua applicazione.
4. Per configurare il servizio {{site.data.keyword.autoscaling}} per
un'applicazione, nell'interfaccia utente {{site.data.keyword.Bluemix_notm}},
fai clic su questa applicazione a cui è associato il servizio {{site.data.keyword.autoscaling}}.
5. Nella sezione dei servizi presente sul Dashboard, fai clic
						sull'icona *Auto-Scaling*.
6. Se non lo hai già fatto, definisci la politica {{site.data.keyword.autoscaling}} per l'applicazione facendo clic su *Crea politica {{site.data.keyword.autoscaling}}*.

Adesso puoi configurare la politica di {{site.data.keyword.autoscaling}},
consultare le statistiche delle metriche o visualizzare la cronologia di scaling dell'applicazione.
<dl>
<dt>Configurazione della politica</dt>
<dd>Utilizza questa sezione per creare o modificare le regole di scalabilità per specificare le condizioni in cui alcune attività di scaling devono essere attivate.<ul>
<li> Per le applicazioni Liberty for Java™, puoi definire le regole di scalabilità per Heap, Memoria, Tempo di risposta e Velocità effettiva.  
<li> Per le applicazioni Node.js, puoi definire le regole di scalabilità per Heap, Memoria e Velocità effettiva.
<li> Per le applicazioni Ruby, puoi definire le regole di scalabilità per la
Memoria.</ul>
*Nota:* puoi definire più regole di scalabilità per più di un tipo di metrica. Tuttavia, il servizio {{site.data.keyword.autoscaling}}
non rileva i conflitti tra le politiche di scalabilità. Quando definisci la politica di scalabilità, devi accertarti che
le diverse regole di scalabilità non siano in conflitto tra di loro. In caso contrario, potresti notare delle oscillazioni nel numero totale di istanze in quanto l'applicazione esegue in un primo minuto lo scaling decrementale e in quello successivo lo scaling incrementale.<br/><br/>
Se il carico di lavoro della tua applicazione cambia notevolmente tra l'ora di utilizzo massimo e l'ora di utilizzo minimo, puoi creare una pianificazione di scalabilità per gestirne i diversi requisiti durante i vari periodi di tempo. Utilizza il parametro Numero minimo di istanze specificato in una pianificazione per definire la linea di base del numero di istanze dell'applicazione, mentre le regole di scalabilità dinamica si applicano ancora alla pianificazione per attivare le azioni di scaling decrementale e incrementale.</dd>
<dt>Statistiche delle metriche</dt>
<dd>Visualizza le statistiche delle metriche per le istanze della tua applicazione. Puoi visualizzare le statistiche medie e selezionare una specifica istanza per
visualizzarne le statistiche.</dd>
<dt>Cronologia ridimensionamenti</dt>
<dd>Visualizza la cronologia dei ridimensionamenti delle tue applicazioni.<ul>
<li> Settimana scorsa:
visualizza la cronologia dei ridimensionamenti della settimana scorsa.
<li> Mese scorso:
visualizza la cronologia dei ridimensionamenti del mese scorso.
<li> Intervallo personalizzato:
puoi impostare l'intervallo di tempo.</ul>
*Nota:* puoi filtrare il record di cronologia selezionando Stato scaling o Scaling decrementale/incrementale.</dd>
</dl>


## Configurazione delle applicazioni Node.js con il servizio {{site.data.keyword.autoscaling}}
{: #node-asagent}

Per abilitare il servizio {{site.data.keyword.autoscaling}} con le tue applicazioni Node.js, oltre al provisioning del servizio e ai passi di bind, devi completare anche la seguente procedura prima di eseguire il push dell'applicazione a {{site.data.keyword.Bluemix_notm}}.

1. Aggiorna il file package.json con la seguente procedura: <ol><li>Crea una voce di dipendenza per `blumix-autoscaling-agent`, ad esempio `"bluemix-autoscaling-agent": "*"`.<br/><li>(Facoltativo) Imposta il limite di heap nella sezione `scripts` sulla base della memoria da te allocata per la tua applicazione,
ad esempio `"start": "node --max-old-space-size=600 app.js"`. .<br/>*Nota:* imposta un valore per `max-old-space-size` se vuoi attivare lo scaling in base all'utilizzo dell'heap. Se il valore non è impostato quando avvii la tua applicazione, viene utilizzato il limite di heap di Node.js predefinito, indipendentemente dalla quantità di memoria allocata alla tua applicazione, il che potrebbe portare a decisioni di scaling automatico non corrette.<br/>
```
{
	"name": "NodejsStarterApp",
	"version": "0.0.1",
	"description": "Una applicazione nodejs di esempio per Bluemix",
	"scripts": {
		"start": "node --max-old-space-size=600 app.js"
	},
	"dependencies": {
		"bluemix-autoscaling-agent": "*"
	},
	"repository": {},
	"engines": {
		"node": "0.12.x"
	} 
}
```
</ol>
2. Aggiorna il tuo file principale per aggiungere la dichiarazione di agent `var as_agent = require('bluemix-autoscaling-agent');`. Il seguente frammento di codice mostra un file js con voci complete con la dichiarazione di agent di scaling automatico.<br/>
```
var agent = require('bluemix-autoscaling-agent');
var http = require('http');
var server = http.createServer(function handler(req, res) {
	console.log("Hello!");
	
	}).listen(process.env.PORT || 3000);
console.log('App is listening on port 3000');
```

## Gestire il servizio {{site.data.keyword.autoscaling}} tramite la API RESTful 
{: #RESTAPI}

La API RESTful {{site.data.keyword.autoscaling}} fornisce un modo alternativo per gestire il servizio {{site.data.keyword.autoscaling}} oltre all'interfaccia utente Bluemix, e supporta anche il recupero e l'analisi dei dati di scaling. Fornisce delle funzionalità analoghe a quelle dell'interfaccia utente {{site.data.keyword.Bluemix_notm}} con l'API, come la creazione di una politica e l'acquisizione della cronologia dei ridimensionamenti.

Per utilizzare la API RESTful {{site.data.keyword.autoscaling}} per gestire il servizio {{site.data.keyword.autoscaling}}, completa i
seguenti prerequisiti: associa il servizio {{site.data.keyword.autoscaling}} alla tua applicazione come specificato nella sezione precedente, acquisisci l'`AccessToken`, l'URL del
server API {{site.data.keyword.autoscaling}} e l'`app_id` dell'applicazione di cui vuoi eseguire lo scaling decrementale o incrementale:

1. Per motivi di sicurezza, in ciascuna intestazione di richiesta della API RESTful {{site.data.keyword.autoscaling}}, deve essere fornito un `AccessToken` ottenuto tramite la procedura UAA CloudFoundry nell'intestazione `Authorization` per indicare l'obbligatorietà della convalida della richiesta. La mancata conformità a questo `AccessToken` causa una risposta 401 non autorizzato. Puoi ottenere questo `AccessToken` in due modi dopo che hai installato lo strumento riga di comando Cloud Foundry e hai eseguito l'accesso a {{site.data.keyword.Bluemix_notm}}:<ul><li>puoi ottenere questo token tramite il comando `cf oauth-token`:
   ```
   > cf oauth-token
   Getting OAuth token...
   OK

     bearer eyJhbGciOiJIUzI1NiJ9.eyJqdGkiOiJhNjIzMGE1YS1mNzE3LTQ0YjItOWM3Yi1kNGJkYThhZGU0NjkiLCJzdWIiOiI4OGViNjM2My1hMjkzLTRlZTItYWQ1MS0yOGVkMTZmZjMwNzQiLCJzY29wZSI6WyJjbG91ZF9jb250cm9sbGVyLnJlYWQiLCJwYXNzd29yZC53cml0ZSIsImNsb3VkX2NvbnRyb2xsZXIud3JpdGUiLCJvcGVuaWQiXSwiY2xpZW50X2lkIjoiY2YiLCJjaWQiOiJjZiIsImF6cCI6ImNmIiwiZ3JhbnRfdHlwZSI6InBhc3N3b3JkIiwidXNlcl9pZCI6Ijg4ZWI2MzYzLWEyOTMtNGVlMi1hZDUxLTI4ZWQxNmZmMzA3NCIsIm9yaWdpbiI6InVhYSIsInVzZXJfbmFtZSI6Imtqa29uZ2tqQGNuLmlibS5jb20iLCJlbWFpbCI6Imtqa29uZ2tqQGNuLmlibS5jb20iLCJyZXZfc2lnIjoiZDhlNGY0MDIiLCJpYXQiOjE0NTU2MDc1NDUsImV4cCI6MTQ1NTY1MDc0NSwiaXNzIjoiaHR0cHM6Ly91YWEuc3RhZ2UxLm5nLmJsdWVtaXgubmV0L29hdXRoL3Rva2VuIiwiemlkIjoidWFhIiwiYXVkIjpbImNsb3VkX2NvbnRyb2xsZXIiLCJwYXNzd29yZCIsImNmIiwib3BlbmlkIl19.nrzsEAZmGXNOWjX8r5Xf7U8Hj5-CE1rtHg8_C-jZKSk
   ```
 La lunga stringa restituita con “bearer” è l'AccessToken che può essere utilizzato nella richiesta della API RESTful {{site.data.keyword.autoscaling}}. Se riscontri degli errori quali “Command not found”, puoi aggiornare il tuo strumento riga di comando Cloud Foundry a una versione più recente.</li><li>Puoi anche trovare questo AccessToken nella directory home. Dopo che hai eseguito l'accesso a {{site.data.keyword.Bluemix_notm}} dall'interfaccia riga di comando, viene creata una cartella `.cf` nella tua cartella home, dove
puoi trovare un nome file JSON `config.json` che contiene un elenco di informazioni sull'ambiente della tua registrazione corrente, come l'organizzazione, lo spazio, l'endpoint di autenticazione e la versione. Puoi individuare una voce `AccessToken` simile alla seguente : 
    ```
   >cat ~/.cf/config.json
 {
  "ConfigVersion": 3,
  "Target": "https://api.ng.bluemix.net",
  "ApiVersion": "2.40.0",
  "AuthorizationEndpoint": "https://login.ng.bluemix.net/UAALoginServerWAR",
  "LoggregatorEndPoint": "wss://loggregator.ng.bluemix.net:443",
  "DopplerEndPoint": "wss://doppler.ng.bluemix.net:443",
  "UaaEndpoint": "https://uaa.ng.bluemix.net",
  "RoutingApiEndpoint": "https://api.ng.bluemix.net/routing",
  "AccessToken": "bearer eyJhbGciOiJIUzI1NiJ9.eyJqdGkiOiJhNjIzMGE1YS1mNzE3LTQ0YjItOWM3Yi1kNGJkYThhZGU0NjkiLCJzdWIiOiI4OGViNjM2My1hMjkzLTRlZTItYWQ1MS0yOGVkMTZmZjMwNzQiLCJzY29wZSI6WyJjbG91ZF9jb250cm9sbGVyLnJlYWQiLCJwYXNzd29yZC53cml0ZSIsImNsb3VkX2NvbnRyb2xsZXIud3JpdGUiLCJvcGVuaWQiXSwiY2xpZW50X2lkIjoiY2YiLCJjaWQiOiJjZiIsImF6cCI6ImNmIiwiZ3JhbnRfdHlwZSI6InBhc3N3b3JkIiwidXNlcl9pZCI6Ijg4ZWI2MzYzLWEyOTMtNGVlMi1hZDUxLTI4ZWQxNmZmMzA3NCIsIm9yaWdpbiI6InVhYSIsInVzZXJfbmFtZSI6Imtqa29uZ2tqQGNuLmlibS5jb20iLCJlbWFpbCI6Imtqa29uZ2tqQGNuLmlibS5jb20iLCJyZXZfc2lnIjoiZDhlNGY0MDIiLCJpYXQiOjE0NTU2MDc1NDUsImV4cCI6MTQ1NTY1MDc0NSwiaXNzIjoiaHR0cHM6Ly91YWEuc3RhZ2UxLm5nLmJsdWVtaXgubmV0L29hdXRoL3Rva2VuIiwiemlkIjoidWFhIiwiYXVkIjpbImNsb3VkX2NvbnRyb2xsZXIiLCJwYXNzd29yZCIsImNmIiwib3BlbmlkIl19.nrzsEAZmGXNOWjX8r5Xf7U8Hj5-CE1rtHg8_C-jZKSk",
  "SSHOAuthClient": "ssh-proxy",
 .....
 }
   ```
L'`AccessToken` nel `config.json` è valido solo per un periodo di tempo. Se ottieni una risposta 401 non autorizzato per la richiesta API REST, è possibile che tu debba eseguire nuovamente l'accesso dall'interfaccia riga di comando per aggiornare il file e ottenere il nuovo `AcessToken`. </li></ul>
 
2.  Puoi ottenere l'URL del server API {{site.data.keyword.autoscaling}} controllando la variabile di ambiente `VCAP_SERVICE` dopo
che hai associato la tua applicazione al servizio {{site.data.keyword.autoscaling}}. In `VCAP_SERVICE`, puoi trovare la sezione
del servizio {{site.data.keyword.autoscaling}} e l'`api_url` è l'URL del server API a cui è associata la tua applicazione. Questo URL di server API ti serve per stabilire una connessione al servizio API RESTful {{site.data.keyword.autoscaling}}:
   ```
    {
      "Auto-Scaling": [
      {
         "name": "Auto-Scaling-iw",
         "label": "Auto-Scaling",
         "plan": "free",
         "credentials": {
            "agentUsername": "agent",
            "api_url": "https://ScalingAPI.ng.bluemix.net",
            "service_id": "3f42b7ff-d939-4ff2-9a55-cb09cef9ab9e",
            "app_id": "2287f442-a7f3-4799-8919-d3908c386fa3",
            "url": "https://Scaling3.ng.bluemix.net",
            "agentPassword": "0cddf80b-37e1-4cfd-b648-83a6c8wee69f"
         }
      }
     ]
   }
   ``` 
  Nota che questo URL può essere trovato tramite il comando `cf env NOMEAPPLICAZIONE`:
   ```
   > cf env Hello
   Getting env variables for app Hello in org OE_Runtimes_SVT / space RT_SVT as Alice...
   OK

   System-Provided:
   {
     "VCAP_SERVICES": {
     "Auto-Scaling": [
     {
      "credentials": {
       "agentPassword": "b626b064-7d26-417a-b954-41c6d3cb5200",
       "agentUsername": "agent",
       "api_url": "https://ScalingAPI.ng.bluemix.net",
       "app_id": "aa8d19b6-eceb-4b6e-b034-926a87e98a51",
       "service_id": "8f482f78-58d8-493c-829b-635e4cbfd817",
       "url": "https://Scaling.ng.bluemix.net"
      },
      "label": "Auto-Scaling",
      "name": "ScalingService",
      "plan": "free",
      "tags": [
       "bluemix_extensions",
       "ibm_created",
       "dev_ops"
      ]
     }
   ...
   ```  
3.  Puoi ottenere l'`app_id` dalla variabile di ambiente `VCAP_SERVICES` oppure eseguire semplicemente il comando `cf app NOMEAPPLICAZIONE --guid`:

   ```
   > cf app Hello --guid
   aa8d19b6-eceb-4b6e-b034-926a87e98a51
   > 
   ```

Con tutti i prerequisiti sopra indicati, puoi ora fare una richiesta API REST utilizzando l'add-on RestClient nel browser oppure semplicemente tramite qualche strumento come `curl`. 

Con l'add-on di client REST, come quelli per Firefox o Chrome, puoi attivare la richiesta REST al server API {{site.data.keyword.autoscaling}} per
eseguire il tuo comando. Fornisci semplicemente questi add-on con l'URL dell'API REST, il metodo e le intestazioni richiesti da questa API REST e i parametri nella
parte del corpo. Per ulteriori dettagli su ciascuna API, vedi [API Rest di IBM {{site.data.keyword.autoscaling}} per {{site.data.keyword.Bluemix_notm}}](https://new-console.ng.bluemix.net/apidocs/48){:new_window}.

Con strumenti come `curl`, puoi gestire il servizio {{site.data.keyword.autoscaling}} in uno script nel seguente modo:    
```
    cf login -a http://api.ng.bluemix.net -u Alice -p pa55w0rd --skip-ssl-validation
    accessToken=$(cf oauth-token | grep bearer | sed -e s/bearer/Bearer/g)
    API_url=$(cf env Hello | grep "api_url" | awk '{print $2}' | cut -d "," -f1 | cut -d "\"" -f2 )
    policyJson="./policy.json"
    appId=$(cf app Hello --guid)

    echo  -e "\nCreate scaling policy using API :"
    createPolicyUrl="${API_url}/v1/autoscaler/apps/${appId}/policy"
    curl_cmd="curl $createPolicyUrl -X 'PUT' -H 'Content-Type:application/json'  -H 'Accept:application/json' -H 'Authorization:$accessToken' --data-binary @${policyJson} -s -o response.txt -w '%{http_code}\n'"
    eval status_code=$($curl_cmd)
    if [[ $status_code -eq 201 ]]; then
         echo "looks good"
    else
         echo "error happens"
         exit 255
    fi
  ```

## Gestire il servizio {{site.data.keyword.autoscaling}} tramite la CLI {{site.data.keyword.autoscaling}} 
{: #CLI}

La CLI {{site.data.keyword.autoscaling}} fornisce una funzionalità analoga alla API RESTful {{site.data.keyword.autoscaling}} ma è un
modo più pratico per configurare il servizio {{site.data.keyword.autoscaling}}. Con la CLI {{site.data.keyword.autoscaling}}, non ti devi preoccupare dei
dettagli nella API RESTful {{site.data.keyword.autoscaling}}, come l'`AccessToken` e l'URL del server API. Ti basta attenerti alle indicazioni dettagliate fornite dalla CLI. Per ulteriori dettagli su come installare e utilizzare la API {{site.data.keyword.autoscaling}}, vedi [{{site.data.keyword.autoscaling}} CLI](../../cli/plugins/auto-scaling/index.html){:new_window}



## Campi della politica per il servizio {{site.data.keyword.autoscaling}}
{: #policy_fields}

| Nome campo  | Descrizione |
|-------------|----------------------|
|*Numero massimo di istanze
consentito* |	Numero massimo di istanze dell'applicazione che è possibile
avviare. Se il numero corrente di istanze dell'applicazione è uguale a questo valore, il servizio {{site.data.keyword.autoscaling}} non eseguirà più lo scaling
incrementale dell'applicazione. Numero minimo di istanze predefinito	Numero minimo di istanze dell'applicazione che è possibile avviare. Se il numero di istanze è uguale a questo valore, il servizio {{site.data.keyword.autoscaling}} non eseguirà più lo scaling decrementale
dell'applicazione. |
| *Tipo di metrica*	| 	I tipi di metrica supportati che è possibile
monitorare. Per ulteriori informazioni, vedi la Tabella 2. |
| *Scaling incrementale* | 	Specifica la soglia che attiva un'azione di scaling incrementale e il numero di
istanze che vengono incrementate quando si attiva l'azione di scaling incrementale. |
| *Scaling decrementale* |	Specifica una soglia che attiva un'azione di scaling decrementale e il numero di
istanze che vengono diminuite quando si attiva l'azione di scaling decrementale. |
| *Finestra statistica* |	La durata del periodo di tempo trascorso in cui
i valori di metrica ricevuti vengono riconosciuti come validi. I valori di metrica sono validi solo se le date/ore rientrano in questo periodo. L'unità del parametro Finestra statistica è il secondo. |
| *Durata violazione*	| La durata del periodo di tempo trascorso in cui potrebbe essere attivata un'azione di
scaling. Un'azione di scaling viene attivata quando i valori di metrica raccolti si trovano al di sopra della soglia
superiore o al di sotto della soglia inferiore più lunga del tempo specificato. L'unità del parametro Durata violazione è il secondo. |
| *Periodo di raffreddamento per lo scaling decrementale* | Dopo che si è verificata un'azione di scaling decrementale, le altre richieste di scaling vengono ignorate durante il periodo di tempo specificato dal parametro Periodo di raffreddamento per lo scaling decrementale. L'unità di questo parametro è il secondo. |
| *Periodo di raffreddamento per lo scaling incrementale*	| Dopo che si è verificata un'azione di scaling incrementale, le altre richieste di scaling vengono ignorate durante il periodo di tempo specificato dal parametro Periodo di raffreddamento per lo scaling incrementale. L'unità di questo parametro è il secondo. |
| *Fuso orario*	| Il fuso orario in cui si applica la pianificazione. |
| *Ora di inizio*  |	L'ora di inizio di una pianificazione ricorrente. |
| *Ora di fine*    |	L'ora di fine di una pianificazione ricorrente.	|
| *Ripetere per*	|	Il giorno in una settimana in cui si applica una pianificazione ricorrente. |
| *Numero minimo di istanze* |	Il numero di minimo di istanze che è possibile avviare per un'applicazione
durante il periodo di tempo specificato nella pianificazione. |
| *Data e ora di inizio* |	La data e ora di inizio della pianificazione impostata su una specifica
data. |
| *Data e ora di fine* |	La data e ora di fine della pianificazione impostata su una specifica data.	|

Tabella 1. Campi di politica nella politica di scalabilità

| Nome metrica | Descrizione | Tipo di metrica
supportata |
|-------------|----------------------| ------------------- |
| *Heap* |	La percentuale di utilizzo della memoria heap.	| SDK Liberty for Java, Node.js |
| *Memoria*   |	La percentuale di utilizzo della memoria.	|  Tutto |
| *Velocità effettiva* | Il numero di richieste
elaborate al secondo.| SDK Liberty for Java, Node.js |
| *Tempo di risposta* |	Il tempo di risposta delle
richieste elaborate.	| Liberty for Java |

Tabella 2. Nomi delle metriche supportate

*Nota:* per raccogliere i dati delle metriche Auto-Scaling, la tua applicazione deve essere distribuita come applicazione Web Liberty in modo che le richieste HTTP/HTTPS di misurazione vengano elaborate tramite il contenitore Web Liberty.
Ad esempio, se esegui un'applicazione Spring Boot come applicazione "Main-Classs", il pacchetto di build Liberty ti fornisce solo l'ambiente java e l'applicazione viene eseguita in realtà nel contenitore Tomcat integrato in Spring, pertanto il servizio Auto-Scaling non raccoglierà alcun dato delle metriche. Devi eseguire l'applicazione come WAR Liberty WAR affinché possa operare con il servizio Auto-Scaling.

## Messaggi di errore
{: #err_msg}
Questa sezione elenca i messaggi di avvertenza e di errore prodotti dal servizio {{site.data.keyword.autoscaling}}.
 
### CWSCV2004E Un altro servizio {{site.data.keyword.autoscaling}} è
già associato all'applicazione.
**Puoi associare un solo servizio {{site.data.keyword.autoscaling}} a un'applicazione. Questo errore si verifica quando vuoi associare il servizio {{site.data.keyword.autoscaling}} a un'applicazione già associata a un altro servizio {{site.data.keyword.autoscaling}}.**

Seleziona un'altra applicazione non associata a un altro servizio {{site.data.keyword.autoscaling}} e associa il
servizio {{site.data.keyword.autoscaling}} di destinazione a questa applicazione.
Se riscontri questo errore in tutti gli altri casi, contatta il supporto IBM.

### CWSCV6001E Il server API non è in grado di analizzare le stringhe JSON di input per la API: {0}.
**Si è verificato un problema durante l'analisi delle stringhe JSON di input.**

Controllare il documento relativo al JSON di input con la API e correggere l'errore in esso.

### CWSCV6002E Il server API non è in grado di analizzare le stringhe JSON di output per la API: {0}.
**Si è verificato un problema durante l'analisi delle stringhe JSON di input.**

Per ulteriori informazioni, rivolgersi all'amministratore di Cloud.

### CWSCV6003E Errore del formato delle stringhe JSON di input: {0} nel
JSON di input per la API: {1}.
**È stato rilevato un errore di formato durante l'analisi delle stringhe JSON di input.**

Controllare il documento relativo al JSON di input con la API e correggere l'errore in esso.

### CWSCV6004E Errore di formato delle stringhe JSON di output: {0}
nel JSON di output per la API: {1}.
**È stato rilevato un errore di formato durante l'analisi delle stringhe JSON di output.**

Per ulteriori informazioni, rivolgersi all'amministratore di Cloud.

### CWSCV6005E Si è verificato un errore server interno durante: {0}.
**Durante l'elaborazione della richiesta, si è verificato un errore server interno.**

Per ulteriori informazioni, rivolgersi all'amministratore di Cloud.

### CWSCV6006E Richiamo delle API CloudFoundry non riuscito: {0}
**Si è verificato un errore durante il richiamo delle API CloudFoundry.**

Per ulteriori informazioni, rivolgersi all'amministratore di Cloud.

### CWSCV6007E L'applicazione non è stata trovata: {0}
**L'applicazione non è stata trovata.**

Per ulteriori dettagli, controllare le informazioni sull'applicazione.

### CWSCV6008E Durante il recupero delle informazioni per l'applicazione
{0} si è verificato il seguente errore: {1}
**Recupero delle informazioni sull'applicazione non riuscito con qualche errore.**

Per ulteriori dettagli, controllare le informazioni sull'applicazione.

### CWSCV6009E Il servizio: {0} per l'applicazione {1} non è stato trovato.
**Non è stato possibile trovare il servizio per questa applicazione.**

Per ulteriori informazioni, controllare il binding di servizio per questa applicazione.

### CWSCV6010E Non è stato possibile trovare la politica per l'applicazione {0}
**Non è stato possibile trovare la politica per questa applicazione.**

Per ulteriori informazioni, controllare la configurazione dell'applicazione.

### CWSCV6011E L'autenticazione interna non è riuscita durante:
{0}
**Autenticazione interna non riuscita.**

Per ulteriori informazioni, rivolgersi all'amministratore di Cloud.


# rellinks
{: #rellinks}

## esempi
{: #samples}

* [Esercitazione: Make your application elastic on {{site.data.keyword.Bluemix_notm}}](http://www.ibm.com/developerworks/cloud/library/cl-autoscale-app/index.html){:new_window}
* [Laboratori sull'architettura Cloud Foundry](https://developer.ibm.com/bluemix/docs/category/cloud-foundry-docs/){:new_window}

## sdk
{: #sdk}

* [API Rest di IBM {{site.data.keyword.autoscaling}} per {{site.data.keyword.Bluemix_notm}}](https://new-console.{DomainName}/apidocs/48){:new_window}

## generale
{: #general}

* [Scaling dei contenitori](https://www.{DomainName}/docs/containers/container_creating_ov.html#container_group_ov){:new_window}
* [Scaling dei server virtuali](https://www.{DomainName}/docs/virtualmachines/vm_index.html#vm_manage_instances){:new_window}
* [CLI {{site.data.keyword.autoscaling}}](../../cli/plugins/auto-scaling/index.html){:new_window}
* [Agent {{site.data.keyword.autoscaling}} per Node.js](https://www.npmjs.com/package/bluemix-autoscaling-agent){:new_window}

