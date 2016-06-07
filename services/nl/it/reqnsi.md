---

copyright:
  years: 2015, 2016

---


{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}


#Servizi
{: #services}
*Ultimo aggiornamento: 20 gennaio 2016*

I servizi disponibili sono elencati nel **catalogo** sotto **Servizi**
nell'interfaccia utente
di {{site.data.keyword.Bluemix}}.
{:shortdesc}


I servizi predefiniti sono disponibili in {{site.data.keyword.Bluemix_notm}} per
le applicazioni mobili. {{site.data.keyword.Bluemix_notm}}
ti consente di implementare, ospitare o ingrandire facilmente questi servizi mobili per le tue applicazioni mobili. Potrai così concentrarti sulla logica e
sulla progettazione dell'applicazione.

{{site.data.keyword.Bluemix_notm}} ospita
e gestisce servizi middleware per le applicazioni Web. Gli sviluppatori
delle applicazioni possono specificare i servizi middleware di cui hanno bisogno. {{site.data.keyword.Bluemix_notm}} esegue quindi
automaticamente il provisioning di nuove istanze dei servizi middleware
specificati ed esegue il bind delle istanze del servizio all'applicazione.

{{site.data.keyword.Bluemix_notm}} visualizza i servizi in due modi: per categoria del servizio e per tipo di supporto del servizio.



<dl>
<dt><strong>Categoria</strong></dt>
<dd>I servizi {{site.data.keyword.Bluemix_notm}}
sono organizzati in diverse categorie. In ciascuna categoria del servizio,
i servizi creati da IBM vengono elencati per primi, seguiti dai servizi di terze parti e, infine,
dai servizi della community.</dd>
<dt><strong>Supporto</strong></dt>
<dd>Per i servizi {{site.data.keyword.Bluemix_notm}} vengono forniti più livelli di supporto. La seguente tabella descrive le informazioni di supporto generali per i servizi {{site.data.keyword.Bluemix_notm}}:

</dd>
</dl>



|Tipo	|Descrizione	|Dettagli sul supporto|
|:------|:--------------|:--------------|
|IBM	|Un servizio fornito da IBM e che è generalmente disponibile.	|Viene fornito supporto per i problemi considerati come un difetto
in un servizio fornito da IBM generalmente disponibile. Il supporto viene fornito in base alla severità da te impostata. Per ulteriori informazioni sulla severità del ticket, vedi [Come contattare il supporto](../support/index.html#contacting-bluemix-support){: new_window}.|
|Terze parti	|Un servizio fornito da un'azienda diversa da IBM.	|Il supporto per i servizi di terze parti è fornito dal
fornitore del servizio. Se un problema viene analizzato da IBM e tale problema viene considerato come un difetto in un servizio di terze parti, IBM non è tenuto a fornire una correzione. IBM condividerà l'analisi con il fornitore del servizio di terze parti laddove necessario.|
|Community	|Un servizio fornito da una community
open source.	|Il supporto per i servizi di community viene fornito dalla Community di sviluppatori {{site.data.keyword.Bluemix_notm}}. Se un problema viene analizzato da IBM e tale problema viene considerato come un difetto in un servizio di community, IBM non è tenuto a fornire una correzione.|
|Beta	|Un servizio che non è pronto per la produzione e che è un una
fase di sviluppo di prova. Un servizio beta può aiutare i team di sviluppo
e di marketing a valutare la qualità dei servizi prima di
renderli generalmente disponibili.	|Viene fornito supporto per i problemi considerati come un difetto in un servizio beta fornito da IBM, tuttavia  IBM non è tenuto a fornire una correzione. Inoltre,
laddove applicabile, al ticket del problema verrà assegnata una severità 3 o 4. Per informazioni sulla severità del ticket, vedi [Come contattare il supporto](../support/index.html#contacting-bluemix-support){: new_window}.|
*Tabella 1. Informazioni sul supporto dei servizi {{site.data.keyword.Bluemix_notm}}*




{{site.data.keyword.Bluemix_notm}} offre anche dei servizi sperimentali che puoi provare. Per visualizzare tutti i servizi sperimentali, i contenitori tipo e i runtime disponibili, accedi a {{site.data.keyword.Bluemix_notm}}, scorri fino alla parte inferiore del Catalogo e fai quindi clic su **Catalogo Lab {{site.data.keyword.Bluemix_notm}}**.

I servizi sperimentali potrebbero non essere stabili e possono cambiare secondo modalità non compatibili con le versioni precedenti. L'uso di questi servizi negli ambienti di produzione è sconsigliato. Il supporto per i servizi sperimentali viene fornito tramite la Community di sviluppatori {{site.data.keyword.Bluemix_notm}}. Se un problema viene analizzato da IBM
e tale problema viene considerato come un difetto in un servizio sperimentale,
IBM non è tenuto a fornire una correzione.

Per utilizzare un servizio nell'interfaccia utente di {{site.data.keyword.Bluemix_notm}}, nell'interfaccia riga di comando cf, in IBM {{site.data.keyword.Bluemix_notm}} DevOps Services o in qualsiasi strumento supportato, attieniti alla seguente procedura:

1. Crea un'istanza del servizio. Nella maggior parte dei casi,
l'istanza del servizio può essere creata quando crei l'applicazione.

2. Identifica l'applicazione che utilizza la nuova istanza del servizio. Per le applicazioni Web, puoi specificare più di un'applicazione per
utilizzare la stessa istanza del servizio, in genere per la condivisione dei dati.

3. Scrivi il codice nella tua applicazione per consentire l'integrazione con il
servizio.

##Servizi per regione

Non tutti i servizi sono
disponibili in ogni regione {{site.data.keyword.Bluemix_notm}}. La seguente tabella mostra i servizi forniti da IBM.



|Servizio	|Disponibile nella regione Stati Uniti Sud	|Disponibile nella regione Europa Regno Unito |Disponibile nella regione di Sydney in Australia|
|:----------|:------------------------------|:------------------|:------------------|
|{{site.data.keyword.activedeployshort}}	|Sì		|Sì		|No|
|{{site.data.keyword.alchemyapishort}} 		|Sì	   	|Sì  		|Sì|
|{{site.data.keyword.appsecshort}}		|Sì		|No		|No|
|{{site.data.keyword.alertnotificationshort}}|Sì		|No			|No		|
|{{site.data.keyword.APS_DA}}			|Sì		|No		|No|
|{{site.data.keyword.APS_MA}}			|Sì		|No		|No|
|{{site.data.keyword.amashort}}			|Sì		|Sì		|Sì|
|{{site.data.keyword.hadoopst}}			|Sì		|No		|No|
|{{site.data.keyword.APIM}}			|Sì		|Sì		|No|
|{{site.data.keyword.autoscaling}}		|Sì		|Sì		|Sì|
|{{site.data.keyword.bigicloudst}}		|Sì		|No		|No|
|{{site.data.keyword.rules_short}}		|Sì		|Sì		|No|
|{{site.data.keyword.cloudint}}			|Sì		|Sì		|No|
|{{site.data.keyword.cloudant}}			|Sì		|Sì		|No|
|{{site.data.keyword.conceptexpansionshort}}	|Sì		|Sì		|Sì|
|{{site.data.keyword.conceptinsightsshort}}	|Sì		|Sì		|Sì|
|{{site.data.keyword.dashdbshort}}		|Sì		|Sì		|No|
|{{site.data.keyword.datacshort}}		|Sì		|Sì		|Sì|
|{{site.data.keyword.DB2OnCloud_short}}		|Sì		|Sì		|Sì|
|{{site.data.keyword.deliverypipeline}}		|Sì		|Sì		|No|
|{{site.data.keyword.dialogshort}}		|Sì		|Sì		|Sì|
|{{site.data.keyword.documentconversionshort}}	|Sì		|Sì		|Sì|
|{{site.data.keyword.creshort}}			|Sì		|No		|No|
|{{site.data.keyword.game}}			|Sì		|Sì		|Sì|
|{{site.data.keyword.geospatialshort_Geospatial}}	|Sì	|Sì		|No|
|{{site.data.keyword.globalizationshort}}	|Sì		|No		|No|
|{{site.data.keyword.dataworks_short}}		|Sì		|Sì		|No|
|{{site.data.keyword.twittershort}}		|Sì		|Sì		|Sì|
|{{site.data.keyword.weather_short}}		|Sì		|Sì		|Sì|
|{{site.data.keyword.IntegrationTestingshort}}	|Sì		|Sì		|No|
|{{site.data.keyword.iot_short}}		|Sì		|No		|No|
|{{site.data.keyword.keymanagementserviceshort}}|No		|Sì		|No|
|{{site.data.keyword.languagetranslationshort}}	|Sì		|Sì		|No|
|{{site.data.keyword.messagehub}}		|Sì		|Sì		|No|
|{{site.data.keyword.messageresonanceshort}}	|Sì		|Sì		|No|
|{{site.data.keyword.APS_MAiOS}} 		|Sì		|No		|No|
|{{site.data.keyword.macm_short}}		|Sì		|Sì		|Sì|
|{{site.data.keyword.mobilemam}}		|Sì		|Sì		|No|
|{{site.data.keyword.mobiledata}}		|Sì		|Sì		|No|
|{{site.data.keyword.manda}}			|Sì		|Sì		|No|
|{{site.data.keyword.mqa}}			|Sì		|Sì		|No|
|{{site.data.keyword.mql}}			|Sì		|Sì		|No|
|{{site.data.keyword.nlclassifierlshort}} 	|Sì 		|Sì 		|Sì|
|{{site.data.keyword.objectstorageshort}}	|Sì		|No		|No|
|{{site.data.keyword.personalityinsightsshort}}	|Sì		|Sì		|Sì|
|{{site.data.keyword.mobilepush}}Push		|Sì		|Sì		|No|
|Push for iOS 8					|Sì		|Sì		|No|
|{{site.data.keyword.questionandanswershort}}	|Sì		|Sì		|Sì|
|{{site.data.keyword.rapidApps}}		|Sì		|Sì		|No|
|{{site.data.keyword.relationshipextractionshort}}	|Sì	|Sì		|Sì|
|{{site.data.keyword.retrieveandrankshort}}	|Sì 		|Sì 		|Sì|
|{{site.data.keyword.SecureGateway}}		|Sì		|Sì		|No|
|{{site.data.keyword.servicediscoveryshort}}	|Sì		|No		|No|
|{{site.data.keyword.sescashort}}		|Sì		|Sì		|Sì|
|{{site.data.keyword.ssofull}}			|Sì		|No		|No|
|{{site.data.keyword.speechtotextshort}}	|Sì 		|Sì	 	|Sì|
|{{site.data.keyword.sqldb}}			|Sì		|Sì		|No|
|{{site.data.keyword.staticanalyzershort}}	|Sì		|Sì		|No|
|{{site.data.keyword.streaminganalyticsshort}}	|Sì		|No		|No|
|{{site.data.keyword.texttospeechshort}} 	|Sì 		|Sì	 	|Sì|
|{{site.data.keyword.times}}			|Sì		|Sì		|No|
|{{site.data.keyword.toneanalyzershort}} 	|Sì 		|Sì 		|Sì|
|{{site.data.keyword.trackplan}}		|Sì		|Sì		|No|
|{{site.data.keyword.tradeoffanalyticsshort}}	|Sì		|Sì		|Sì|
|{{site.data.keyword.visualinsightsshort}}	|Sì		|Sì		|Sì|
|{{site.data.keyword.visualizationrenderingshort}} |Sì		|Sì		|No|
|{{site.data.keyword.workflow}}			|Sì		|Sì		|No|
|{{site.data.keyword.workloadscheduler}}	|Sì		|Sì		|No|
|{{site.data.keyword.xpagesservice_short}}	|Sì		|Sì		|No|
*Tabella 2. Disponibilità dei servizi*


# Aggiunta di un servizio alla tua applicazione
{: #add_service}
*Ultimo aggiornamento: 8 marzo 2016*

{{site.data.keyword.Bluemix}} ha un elenco di servizi e
li gestisce per conto degli sviluppatori. Per aggiungere un servizio a
un'applicazione da utilizzare, devi richiedere un'istanza di tale servizio e configurare l'applicazione in modo
che interagisca con il servizio.

Puoi visualizzare tutti i servizi disponibili in {{site.data.keyword.Bluemix_notm}}
nei seguenti modi:

* Dall'interfaccia utente {{site.data.keyword.Bluemix_notm}}. Visualizza il catalogo {{site.data.keyword.Bluemix_notm}}.
* Dall'interfaccia riga di comando cf. Utilizza il comando **cf marketplace**.
* Dalla tua applicazione. Utilizza la [API di servizi GET /v2/services](http://apidocs.cloudfoundry.org/197/services/list_all_services.html){: new_window}.

Puoi selezionare il servizio di cui hai bisogno quando sviluppi le applicazioni. Dopo la tua selezione, {{site.data.keyword.Bluemix_notm}} interagisce con il servizio ed
effettua le operazioni necessarie per eseguire il provisioning delle risorse del servizio. Il processo di provisioning può essere
differente per i diversi tipi di servizi. Ad esempio, un servizio database crea un database e un
servizio di notifiche di push per le applicazioni mobili genera le informazioni di configurazione.

{{site.data.keyword.Bluemix_notm}} fornisce le risorse di un servizio alla tua applicazione utilizzando un'istanza del servizio. Un'istanza del servizio può essere condivisa tra le
applicazioni Web.

Se vi sono dei servizi disponibili in altre regioni, potrai utilizzare anche tali
servizi. Questi servizi devono essere accessibili da Internet e avere degli endpoint API. Per utilizzare
questi servizi, devi codificare manualmente l'applicazione nello stesso modo in cui codifichi le applicazioni
esterne o gli strumenti di terze parti per utilizzare i servizi {{site.data.keyword.Bluemix_notm}}. Per ulteriori informazioni, vedi [Abilitazione di applicazioni esterne e strumenti di terze parti all'utilizzo di servizi {{site.data.keyword.Bluemix_notm}}](#accser_external).



## Richiesta di una nuova istanza del servizio
{: #req_instance}

Per richiedere una nuova istanza del servizio, devi utilizzare l'interfaccia utente di {{site.data.keyword.Bluemix_notm}} oppure
l'interfaccia riga di comando cf.

**Nota:** quando specifichi il nome servizio, evita di utilizzare caratteri che non siano alfabetici o numerici; in caso contrario, i risultati potrebbero essere imprevedibili.

Se utilizzi l'interfaccia utente di {{site.data.keyword.Bluemix_notm}}
per richiedere un'istanza del servizio, completa la seguente procedura:

1. Nel {{site.data.keyword.Bluemix_notm}} **Catalogo**, fai clic sul tile per il servizio che vuoi aggiungere. Viene visualizzata la pagina dei dettagli.

2. Nel riquadro Aggiungi servizio, seleziona un'applicazione di cui desideri eseguire il bind a questa istanza del servizio dall'elenco **Applicazione**.

3. Immetti un nome nel campo **Nome servizio**. Viene fornito un nome servizio predefinito. Puoi modificare il nome nel campo o lasciarlo invariato.

4. Completa le selezioni o i campi aggiuntivi e fai quindi clic su **CREA**.

Se utilizzi l'interfaccia riga di comando cf per richiedere un'istanza del servizio, completa la seguente procedura:

1. Utilizza il comando **cf marketplace** per trovare il nome e il piano del servizio di cui hai bisogno.

2. Utilizza il seguente comando per creare un'istanza del servizio, dove nome_servizio è il nome del servizio, piano_servizio è il piano del servizio e istanza_servizio è il nome da utilizzare per questa istanza del servizio.

    ```
    cf create-service nome_servizio piano_servizio istanza_servizio
    ```

3. Utilizza il seguente comando per eseguire il bind dell'istanza del servizio a un'applicazione, dove nomeapplicazione è il nome dell'applicazione e istanza_servizio è il nome dell'istanza del servizio.

    ```
    cf bind-service nomeapplicazione istanza_servizio
    ```

Puoi eseguire il bind a un'istanza del servizio per le sole istanze dell'applicazione che si trovano nello stesso spazio od organizzazione. Tuttavia, puoi utilizzare istanze di servizio provenienti da altri spazi od organizzazioni seguendo le modalità adottate dalle applicazioni esterne. Invece di creare un bind, utilizza le credenziali per configurare direttamente l'istanza della tua applicazione. Per ulteriori informazioni sull'uso dei servizi {{site.data.keyword.Bluemix_notm}} da parte delle applicazioni esterne, vedi [Abilitazione di applicazioni esterne all'utilizzo dei servizi {{site.data.keyword.Bluemix_notm}} ](#accser_external){: new_window}.


## Configurazione della tua applicazione per l'interazione con un servizio 
{: #config}

Dopo aver eseguito il bind di un'istanza del servizio all'applicazione, devi configurare
l'applicazione in modo da interagire con il servizio.

Ciascun servizio potrebbe richiedere un meccanismo differente per comunicare con le applicazioni. Questi
meccanismi sono documentati come parte della definizione del servizio a scopo informativo quando sviluppi le
applicazioni. Per congruenza, i meccanismi sono richiesti perché la tua applicazione interagisca con il
servizio.

* Per interagire con i servizi del database, utilizza le informazioni fornite da {{site.data.keyword.Bluemix_notm}}, quali ID utente, password
e l'URI di accesso per l'applicazione.
* Per interagire con i servizi di back-end mobili, utilizza le informazioni fornite da {{site.data.keyword.Bluemix_notm}}, quali l'identità dell'applicazione
(ID applicazione), le informazioni di sicurezza specifiche per il client e l'URI di accesso per
l'applicazione. I servizi mobili di norma operano in contesto reciproco e, pertanto, le informazioni
di contesto, come il nome dello sviluppatore dell'applicazione e l'utente che utilizza l'applicazione,
possono essere condivise tra la serie di servizi.
* Per interagire con le applicazioni Web o il codice cloud lato server per le applicazioni mobili, utilizza le
informazioni fornite da {{site.data.keyword.Bluemix_notm}}, quali le
credenziali di runtime nella variabile di ambiente *VCAP_SERVICES*
dell'applicazione. Il valore della variabile di ambiente *VCAP_SERVICES* è la
serializzazione di un oggetto JSON. La variabile contiene i dati di runtime richiesti per interagire con i servizi
a cui è associata l'applicazione. Il formato dei dati è differente per i
diversi servizi. Potresti dover leggere la documentazione del servizio in merito a cosa aspettarsi
e come interpretare ogni elemento di informazione.

Se si verifica un arresto anomalo di un servizio di cui esegui il bind a un'applicazione,
l'esecuzione dell'applicazione potrebbe essere arrestata oppure potrebbero verificarsi per essa delle condizioni di errore. {{site.data.keyword.Bluemix_notm}} non riavvia automaticamente l'applicazione per eseguire un ripristino da tali problemi. Valuta una codifica della tua applicazione per identificare interruzioni, eccezioni ed errori di connessione e per eseguire il ripristino da tali condizioni. Per ulteriori informazioni, consulta l'argomento di risoluzione dei problemi relativo al fatto che [le applicazioni non verranno riavviate automaticamente](../troubleshoot/index.html#ts_topmenubar).

## Abilitazione di applicazioni esterne all'utilizzo dei servizi {{site.data.keyword.Bluemix_notm}}
{: #accser_external}

Potresti disporre di applicazioni create ed eseguite
all'esterno di {{site.data.keyword.Bluemix_notm}},
o utilizzare strumenti di terze parti. Se i servizi {{site.data.keyword.Bluemix_notm}}
forniscono degli endpoint accessibili da Internet, puoi utilizzare
questi servizi con le tue applicazioni locali e con gli strumenti di terze parti.

Per abilitare un'applicazione esterna o uno strumento di terze parti
a utilizzare un servizio {{site.data.keyword.Bluemix_notm}},
completa la seguente procedura:

1. Richiedi un'istanza del servizio.
    1. Nel Dashboard nell'interfaccia utente {{site.data.keyword.Bluemix_notm}}, fai clic su **Utilizza servizi o API**. Viene visualizzato il Catalogo.
    2. Dal Catalogo, seleziona il servizio che vuoi facendo clic sul relativo tile. Viene visualizzata la pagina dei dettagli.
    3. Nella finestra Aggiungi servizio, mantieni la selezione dell'elenco **Applicazione**: come **Lascia senza binding**. Questa selezione significa che
il servizio non sarà connesso a un'applicazione {{site.data.keyword.Bluemix_notm}}.
    4. Opera le altre selezioni come necessario. Fai quindi clic su **CREA**. Viene creata un'istanza del servizio e viene visualizzato il dashboard del servizio.
2. Nel riquadro di navigazione di sinistra del dashboard del servizio, puoi selezionare **Credenziali del servizio** per visualizzare o aggiungere credenziali nel formato JSON. Utilizza la chiave API visualizzata come credenziali per stabilire una
connessione all'istanza del servizio.

La tua applicazione che viene eseguita esternamente a {{site.data.keyword.Bluemix_notm}} può
ora accedere al servizio {{site.data.keyword.Bluemix_notm}}.

**Nota:** se vuoi eliminare delle istanze del servizio oppure controllare le informazioni di fatturazione, devi tornare indietro al Dashboard nell'interfaccia utente per gestire le istanze del servizio.

## Creazione di un'istanza del servizio fornito dall'utente
{: #user_provide_services}

Puoi avere delle risorse che sono gestite esternamente a {{site.data.keyword.Bluemix_notm}}. Se hai delle credenziali per accedere a queste risorse esterne da Internet, puoi creare delle istanze del servizio fornito dall'utente {{site.data.keyword.Bluemix_notm}} per rappresentare le risorse esterne e comunicare con esse.

Per creare un'istanza del servizio fornito dall'utente ed eseguirne il bind a un'applicazione, completa la seguente procedura:

1. Crea un'istanza del servizio fornito dall'utente utilizzando il comando **cf create-user-provided-service** oppure il comando **cf cups**:
    * Per creare un'istanza del servizio fornito dall'utente generale, utilizza l'opzione **-p** e
separa i nomi parametro con delle virgole. L'interfaccia riga di comando cf ti chiede quindi ciascun
parametro, uno alla volta. Ad
                                    esempio:
        ```
        cf cups testups1 -p "host, port, dbname, username, password"
        host> pubsub01.example.com
        port> 1234
        dbname> sampledb01
        username> pubsubuser
        password> p@$$w0rd
        Creating user provided service testups1 in org my-org / space dev as user@sample.com...
        OK
        ```

    * Per creare un'istanza del servizio che scarica informazioni in un software di gestione di log di terze parti,
utilizza l'opzione **-l** e specifica la destinazione fornita dal software di gestione di log di terze parti. Ad
esempio:

        ```
        cf cups testups2 -l syslog://example.com
        Creating user provided service testups2 in org my-org / space dev as user@sample.com...
        OK
        ```

    Se vuoi aggiornare uno o più parametri dell'istanza del servizio fornito dall'utente, utilizza il comando **cf update-user-provided-service** oppure
il comando **cf uups**.

    * Per aggiornare un'istanza del servizio fornito dall'utente, utilizza l'opzione **-p**
e specifica le chiavi e i valori di parametro in un oggetto json. Ad
esempio:

        ```
        cf uups testups1 -p "{\"username\":\"pubsubuser2\",\"password\":\"p@$$w0rd2\"}"
        Updating user provided service testups1 in org my-org / space dev as user@sample.com...
        OK
        ```

    * Per creare un'istanza del servizio che scarica informazioni in un software di gestione di log di terze parti, utilizza l'opzione -l. Ad
esempio:

        ```
        cf uups testups2 -l syslog://example2.com
        Updating user provided service testups2 in org my-org / space dev as user@sample.com...
        OK
        ```

2. Esegui il bind dell'istanza del servizio alla tua applicazione utilizzando il comando cf bind-service. Ad
esempio:

	```
	cf bind-service myapp testups1
	Binding service testups1 to app myapp in org my-org / space dev as user@sample.com...
	OK
	```

Ora puoi configurare la tua applicazione per utilizzare le risorse esterne. Per informazioni su come configurare la tua applicazione per interagire con un servizio, vedi [Configurazione della tua applicazione per l'interazione con un servizio](#config){: new_window}.

## Utilizzo dei servizi in un'altra regione
{: #cross_region_service}

Se disponi di un'istanza di servizio creata e associata mediante bind ad applicazioni in un'unica regione, puoi utilizzare questa istanza in un'altra regione utilizzando uno dei seguenti metodi:

  * Utilizza le credenziali del servizio per configurare direttamente l'istanza della tua applicazione. Per i dettagli, vedi [Abilitazione di applicazioni esterne all'utilizzo dei servizi {{site.data.keyword.Bluemix_notm}}](#accser_external){: new_window}.
  * Crea come ponte un servizio fornito dall'utente.
    
	Supponiamo di iniziare nella regione in cui
desideri utilizzare l'istanza del servizio. Per utilizzare un'istanza del servizio che si trova
in un'altra regione, completa la seguente procedura:

      1. Passa alla regione in cui si trova l'istanza del servizio. Nella barra dei menu principale di {{site.data.keyword.Bluemix_notm}},
espandi **Regione** o fai clic sull'icona **Regione**,
quindi seleziona la regione in cui si trova l'istanza del servizio.

      2. Recupera le credenziali e i parametri di connessione dalla variabile di ambiente VCAP_SERVICES dell'istanza del servizio nella regione in cui si trova il servizio. Completa la seguente
procedura:

	       1. Nel Dashboard {{site.data.keyword.Bluemix_notm}}, fai clic sul tile dell'applicazione. Viene visualizzata la pagina Panoramica.
	       2. Nel riquadro di navigazione a sinistra,  fai clic su **Variabili di ambiente**. I dettagli della variabile di ambiente *VCAP_SERVICES*
vengono visualizzati nel riquadro a destra. Registra il contenuto JSON per l'istanza
del servizio.

      3. Passa alla regione in cui desideri utilizzare l'istanza del
servizio. Nella barra dei menu principale di {{site.data.keyword.Bluemix_notm}},
espandi **Regione** o fai clic sull'icona **Regione**,
quindi seleziona la regione in cui desideri utilizzare l'istanza del servizio.

      4. Crea un'istanza del servizio fornito dall'utente utilizzando le credenziali
e i parametri di connessione che hai registrato dalla variabile di ambiente
*VCAP_SERVICES*. Per informazioni su come creare un'istanza
del servizio fornito dall'utente, vedi [Creazione di un'istanza
del servizio fornito dall'utente](#user_provide_services){: new_window}.

      5. Esegui il bind dell'istanza del servizio fornito dall'utente alla tua applicazione
utilizzando il seguente comando:

	     ```
	     cf bind-service myapp user-provided_service_instance
	     ```






## Utilizzo di servizi in un altro servizio
{: #s2s_binding}

Autorizzazione accesso al servizio consente a un servizio di accedere a un altro servizio direttamente. Puoi autorizzare e configurare l'accesso di un'istanza del servizio ad altre istanze del servizio sul Dashboard {{site.data.keyword.Bluemix_notm}}.

Per utilizzare un'istanza del servizio da un altro servizio, completa la seguente procedura:

1. Nel Dashboard {{site.data.keyword.Bluemix_notm}}, fai clic sul tile per il servizio a
cui vuoi accedere. Viene visualizzato il dashboard per il servizio.
2. Nel riquadro di navigazione a sinistra,  fai clic su *Gestisci* per autorizzare il binding da altre istanze del servizio utilizzando la console dell'istanza del servizio.
3. Se vuoi negare ad altri servizi l'accesso all'istanza del servizio, fai clic su *Autorizzazione accesso al servizio* nel riquadro di navigazione a sinistra e utilizza quindi *Revoca* per rimuovere il bind di servizio. 

# rellinks
{: #rellinks}

## general
{: #general}

* [Esecuzione del bind di un servizio utilizzando l'interfaccia utente {{site.data.keyword.Bluemix_notm}}](../cfapps/ee.html#ee_bindui)
* [Richiamo di VCAP_SERVICES](../cli/vcapsvc.html#retrieving)


