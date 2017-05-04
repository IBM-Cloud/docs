---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Raccolta di dati di log non predefiniti da un contenitore
{: #logging_containers_collect_data}

Per acquisire i dati da ubicazioni log non predefinite in un contenitore, configura la variabile di ambiente **LOG_LOCATIONS** quando crei un contenitore.
{:shortdesc}

* Aggiungi la variabile di ambiente **LOG_LOCATIONS** con un percorso al file di log quando crei il contenitore. 
* Puoi aggiungere più file di log separandoli con le virgole. 

## Raccolta di dati di log non predefiniti tramite la console Bluemix
{: #logging_containers_collect_data_ui}

Completa le seguenti istruzioni per raccogliere i dati non predefiniti tramite la console:

1. Dal catalogo, seleziona **Contenitori** e scegli un'immagine. 

    L'elenco di immagini visualizzate include le immagini fornite da {{site.data.keyword.IBM}} e le immagini archiviate nel tuo registro {{site.data.keyword.Bluemix_notm}} privato. 

2. Definisci il tuo contenitore. Scegli il tipo, immetti un nome per il contenitore, selezionane la dimensione e definisci altri attributi come i dettagli dell'indirizzo IP e le porte. Per ulteriori informazioni, consulta [Crea e distribuisci un singolo contenitore tramite la IU {{site.data.keyword.Bluemix_notm}}](/docs/containers/container_single_ui.html). 

3. Espandi la sezione **Opzioni avanzate** e seleziona **Aggiungi una nuova variabile di ambiente**.

4. Aggiungi la variabile **LOG_LOCATIONS** e impostane il valore sul log che desideri analizzare.

    Ad esempio, quando aggiungi un contenitore che si basa sull'ultima immagine Liberty, per analizzare il file di log *dpkg.log*, imposta il valore dell'ambiente sul seguente valore:
    
    <table>
      <tbody>
        <tr>
          <th align="center">Nome variabile </th>
          <th align="center">Valore</th>
        </tr>
        <tr>
          <td align="left">LOG_LOCATIONS</td>
          <td align="left">/var/log/dpkg.log</td>
        </tr>
      </tbody>
    </table>

4. Fai clic su **Crea**.

Viene visualizzato il dashboard del contenitore. Controlla che lo stato del contenitore sia *In esecuzione*, quindi controlla i log nella scheda **Monitoraggio e log**.


## Raccolta di dati di log non predefiniti tramite la CLI
{: #logging_containers_collect_data_cli}

Completa le seguenti istruzioni per raccogliere i dati di log non predefiniti tramite la CLI: 

1. Configura un terminale per utilizzare la CLI {{site.data.keyword.containershort}}. Per ulteriori informazioni, consulta [Configurazione della CLI del servizio IBM Bluemix Container](/docs/containers/container_cli_cfic_install.html).

2. Accedi alla CLI Cloud Foundry utilizzando il seguente comando: `cf login`. Immetti i tuoi ID, password, organizzazione e spazio {{site.data.keyword.Bluemix_notm}} quando ti viene richiesto. 

    Per impostazione predefinita, sei collegato dalla regione Stati Uniti Sud o o dall'ultima regione da cui hai eseguito l'accesso.  
    
    Puoi includere l'opzione **–a** per accedere a una regione specifica in {{site.data.keyword.Bluemix_notm}}. Ad esempio, la seguente tabella elenca i comandi per regione:

    <table>
      <tbody>
        <tr>
          <th align="center">Regione</th>
          <th align="center">Comando</th>
        </tr>
        <tr>
          <td align="left">Stati Uniti Sud</td>
          <td align="left"> cf login -a api.ng.bluemix.net</td>
        </tr>
        <tr>
          <td align="left">Regno Unito</td>
          <td align="left">cf login -a api.eu-gb.bluemix.net</td>
        </tr>
        <tr>
          <td align="left">Sydney</td>
          <td align="left">cf login -a api.au-syd.bluemix.net</td>
        </tr>
      </tbody>
    </table>
    

3. Accedi a {{site.data.keyword.containershort}} utilizzando il seguente comando: `cf ic login`

4. Crea un singolo contenitore da un'immagine. Includi la variabile di ambiente LOG_LOCATIONS per includere le ubicazioni log non predefinite.  

    Per aggiungere un'ubicazione log personalizzata per poter visualizzare le informazioni log in Kibana, aggiungi la variabile di ambiente **LOG_LOCATIONS** quando crei il contenitore. Immetti il seguente comando:
    
    `docker run -p portNumber -e "LOG_LOCATIONS=log1,log2" --name containerName registry.domain_name/imageName:imageTag`
    
    dove
    
     <table>
      <tbody>
        <tr>
          <th align="center">Opzione </th>
          <th align="center">Descrizione</th>
        </tr>
        <tr>
          <td align="left">-p</td>
          <td align="left"> Se desideri rendere la tua applicazione accessibile da internet, devi esporre una porta pubblica. Includi le porte specificate nel Dockerfile per l'immagine che stai utilizzando. <br> Puoi scegliere tra UDP e TCP per indicare il protocollo IP che vuoi utilizzare. Se non specifichi un protocollo, la tua porta viene automaticamente esposta per il traffico TCP. <br> Quando esponi una porta pubblica, crei un gruppo di sicurezza di rete pubblico per il tuo contenitore che ti consente di inviare e ricevere dati pubblici solo nella porta esposta. Tutte le altre porte pubbliche sono chiuse e non possono essere utilizzate per accedere alla tua applicazione da internet. <br> Puoi includere più porte con più opzioni -p. </td>
        </tr>
        <tr>
          <td align="left">-e</td>
          <td align="left">Imposta una variabile di ambiente. <br> Puoi elencare più chiavi separatamente. Racchiudi tra virgolette sia il valore che il nome della variabile di ambiente. <br> Per aggiungere un file di log da monitorare nel contenitore, includi la variabile di ambiente LOG_LOCATIONS con un percorso al file di log.</td>
        </tr>
        <tr>
          <td align="left">--name</td>
          <td align="left">Definisce il nome del contenitore. </td>
        </tr>
	<tr>
          <td align="left">registry.domain_name</td>
          <td align="left">Registro nella regione pubblica. Ad esempio, per la regione Stati Uniti Sud, il nome del dominio predefinito è: `ng.bluemix.net` per Regno Unito è: `eu-gb.bluemix.net` </td>
        </tr>
        <tr>
          <td align="left">imageName</td>
          <td align="left">Nome dell'immagine che desideri aggiungere.</td>
        </tr>
	<tr>
          <td align="left">imageTag</td>
          <td align="left">Tag dell'immagine che desideri aggiungere.</td>
        </tr>
      </tbody>
    </table>
    
    Ad esempio, per creare un contenitore basato sull'ultima immagine Liberty e includere il file di log `/var/log/dpkg.log`, utilizza il seguente comando: 
    
    `docker run -p 9080 -e "LOG_LOCATIONS=/var/log/dpkg.log" --name MyContainer registry.ng.bluemix.net/ibmliberty:latest`
    
    Il file dpkg.log è un file di log Ubuntu standard che viene comunemente generato durante la creazione di un contenitore, ma non viene trasmesso automaticamente a Kibana.

Per controllare lo stato del contenitore, esegui il comando `docker ps`. Quando lo stato è *In esecuzione*, controlla i log nella console {{site.data.keyword.Bluemix_notm}}, tramite la riga di comando o Kibana.



