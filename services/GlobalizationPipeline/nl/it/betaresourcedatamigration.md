---

copyright:
  years: 2015, 2017
lastupdated: "2016-10-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Migrazione dei dati di risorsa dalla versione beta
{: #globalizationpipeline_betaresourcedatamigration}


La versione beta di {{site.data.keyword.GlobalizationPipeline_full}} sarà interrotta dopo un determinato periodo di tempo dall'uscita della versione GA. I dati utente nelle istanze beta non saranno spostati alle istanze del servizio GAS. Per mantenere i dati dopo lo spostamento alla GA, puoi esportare i dati della risorsa nei file, quindi importali nella nuova istanza. Tieni presente che non puoi eseguire questa operazione utilizzando il dashboard del servizio. Inoltre, l'esportazione dei dati della risorsa in un formato file di risorsa non conserverà gli altri metadati associati con le voci della risorsa.

Per supportare la migrazione dei dati dalla beta alla GA, è stata aggiunta una funzione allo strumento della riga di comando della {{site.data.keyword.GlobalizationPipeline_short}}. L'origine dello strumento viene ospitata all'indirizzo https://github.com/IBM-Bluemix/gp-java-tools e la sua release binaria sarà anche disponibile nel repository github. Viene pubblicata l'ultima istantanea di sviluppo. [Scarica.](https://w3-connections.ibm.com/communities/service/html/communityview?communityUuid=589d87cf-d0c7-4e06-ab95-4108547f90aa#fullpageWidgetId=Wa22bb771e29b_4aa9_a114_cfe53fda2cc8&file=5cdaf089-ec7c-4881-b5a0-7ab651491237)

Lo strumento utilizza una API REST migliorata dopo la release beta per il ***caricamento delle voci della risorsa***, quindi, l'istanza del servizio di destinazione deve essere alla versione GA. 
* Origine: beta o GA
* Destinazione: solo GA

Per copiare tutti i dati di bundle in un'istanza del servizio Globalization a un'altra istanza, utilizza il seguente comando:

```> java -jar gp-cli.jar copy-all-bundles -s <source-service-url> -i <source-instance-id> -u <source-user-id> -p <source-password> --dest-url <dest-service-url> --dest-instance-id <dest-instance-id> --dest-user-id <dest-user-id> --dest-password <dest-password>```


`source/target-service-url`, e altri valori dei parametri trovati nelle credenziali del servizio di origine/destinazione, ad esempio: 

```
{
  "gp-beta": [
    {
      "name": "Globalization Pipeline-7x",
      "label": "gp-beta",
      "plan": "gp-beta-plan",
      "credentials": {
 

      "url": "https://gp-beta-rest.ng.bluemix.net/translate/rest",
        "userId": "bd0b84362c6934d222c3a0a40fc1443b",
        "password": "OGxp6jDqCLCL1ui8kQSPTt1mZDi4EQwu",
        "instanceId": "bd0b84362c6934d222c3a0a40fc1233e"
      }
    }
  ]
}
```
Inoltre, tutta la CLI GP è aggiornata per supportare le credenziali nel formato json in aggiunta alle opzioni individuali `(-s / -i / -u / -p)`. Puoi creare un file json con dei contenuti simile al seguente: 

creds.json 
```
 {

        "url": "https://gp-rest.stage1.ng.bluemix.net/translate/rest",
        "userId": "36cad58b3a65dc9fe0183208305be137",
        "password": "43F9MRMu9Q8BWRXMLctunUsAe8LTdwq1",
        "instanceId": "b157e3fc63e62d76c50d9f689d7fc965"

} 
```
Quindi, puoi specificare il file con `-j <json-file>`. Nel comando `copy/copy-all-bundles`, puoi sostituire

```-s https://gp-rest.stage1.ng.bluemix.net/translate/rest -i b157e3fc63e62d76c50d9f689d7fc965 -u 36cad58b3a65dc9fe0183208305be137 -p 43F9MRMu9Q8BWRXMLctunUsAe8LTdwq1```

con

`-j creds.json `
 
In alternativa, puoi copiare il bundle da un posto ad un altro utilizzando il comando: 

```> java -jar gp-cli.jar copy -s <source-service-url> -i <source-instance-id> -u <source-user-id> -p <source-password> -b <source-bundle-id> --dest-url <dest-service-url> --dest-instance-id <dest-instance-id> --dest-user-id <dest-user-id> --dest-password <dest-password> -d <dest-bundle-id>```


**Nota:** Puoi utilizzare due ulteriori parametri: `-b <source-bundle-id>` e `-d <dest-bundle-id>` in aggiunta al comando copy-all-bundles. Questo comando può essere utilizzato per copiare un bundle nella stessa istanza. In questo caso, puoi rilasciare i parametri delle credenziali del servizio `(--dest-*)`.


I precedenti comandi estraggono i dati del bundle esistente e i dati della voce della risorsa e li caricano nella nuova ubicazione. Durante il processo, alcuni campi controllati dal server REST saranno aggiornati (come ad esempio il campo updatedBy/updatedAt). Inoltre, poiché questi comandi non copiano il bind del servizio e i dati di configurazione, devi configurare i servizi MT nell'istanza di destinazione.


Ad esempio, la versione beta supporta la traduzione in arabo con Watson Language Translator. Nella versione GA, la traduzione in arabo non è più offerta gratuitamente. Quando passi i dati beta alla nuova istanza GA, i contenuti già tradotti in arabo saranno conservati. Nessuna modifica nella lingua di origine attiverà la traduzione in arabo automaticamente, a meno che non imposti il bind di Watson per abilitare la traduzione dall'arabo. Questo è inoltre il caso in cui l'istanza di origine è la versione GA. Il bind del servizio MT esterno è specifico di un'istanza GP; il bind/configurazione di un'altra istanza non sarà passato automaticamente. 

