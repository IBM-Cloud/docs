
{:shortdesc: .shortdesc}

# Servizi VCAP

*Ultimo aggiornamento: 9 novembre 2015*


La variabile di ambiente VCAP_SERVICES è un oggetto JSON che contiene le informazioni che puoi utilizzare per interagire con un'istanza del servizio in {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}


## Richiamo del valore della variabile di ambiente VCAP_SERVICES
{:retrieving}

La variabile di ambiente VCAP_SERVICES è un oggetto JSON che contiene le informazioni che puoi utilizzare per interagire con un'istanza del servizio in {{site.data.keyword.Bluemix_notm}}. Le informazioni includono il nome dell'istanza del servizio, le credenziali e l'URL di connessione all'istanza del servizio. Questi valori vengono inseriti nella variabile di ambiente VCAP_SERVICES quando la tua applicazione viene associata a un'istanza del servizio in {{site.data.keyword.Bluemix_notm}}.

Il valore della variabile di ambiente VCAP_SERVICES è disponibile solo quando esegui il bind di un'istanza del servizio alla tua applicazione. Puoi visualizzare le variabili di ambiente dell'applicazione utilizzando il driver della console WebSocket. Il seguente esempio mostra come utilizzare il driver della console WebSocket per visualizzare le variabili di ambiente di un'applicazione Node.js.

Esegui innanzitutto il comando per eseguire nuovamente la distribuzione della tua applicazione Node.js.
```
cf push -c "curl -s https://raw.githubusercontent.com/dmikusa-pivotal/cf-debug-tools/master/debug-console.sh | bash" yourapp
```
Immetti ora il seguente URL:
```
https://yourapp.{APPDomain}/bash.sh
```
Nella pagina che viene visualizzata, fai clic sul segno di spunta per connettere lo strumento ed immetti quindi il comando env per visualizzare le variabili di ambiente della tua applicazione. Per ulteriori
informazioni su cf-debug-tools, vedi il documento relativo agli [strumenti di debug per Cloud Foundry](https://github.com/dmikusa-pivotal/cf-debug-tools).


## Visualizzazione dei livelli dell'infrastruttura Bluemix
{:viewinfra}


{{site.data.keyword.Bluemix_notm}} astrae e nasconde i
livelli di sistema operativo e infrastruttura in modo che tu non debba occuparti della loro gestione. Tuttavia, potrebbe capitare che
tu voglia saperne di più sul sistema operativo e sul middleware per la tua applicazione.

Puoi eseguire il comando cf stacks per visualizzare gli stack disponibili, o filesystem root, a cui devono essere distribuite le tue applicazioni. Puoi anche specificare lo stack quando utilizzi il comando cf push con l'opzione *-s* e il *nome_stack*, dove il nome_stack è il filesystem root, come `lucid64` o `cflinuxfs2`:
```
cf push appName -s nome_stack
```
Puoi utilizzare il comando `cf buildpacks` per visualizzare i componenti middleware, come il profilo WebSphere Liberty ed SDK for Node.js, disponibili come runtime in cui eseguire la tua applicazione. Puoi anche specificare l'ambiente di runtime per la tua applicazione utilizzando il seguente comando:
```
cf push nomeapplicazione -b nomepacchettodibuild
```
