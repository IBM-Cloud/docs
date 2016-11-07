---

copyright:
  years: 2016

---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}


# Informazioni su {{site.data.keyword.iotinsurance_short}}
{: #about_servicename}
Ultimo aggiornamento: 15 settembre 2016
{: .last-updated}

{{site.data.keyword.iotinsurance_full}} è un'istanza di produzione IoT integrata che raccoglie e analizza i dati di contesto completo dai possessori della polizza per fornire valutazioni del rischio, protezione in tempo reale e riduzione dei costi della politica personalizzati.
{: shortdesc}

{{site.data.keyword.iotinsurance_short}} fornisce una visualizzazione di contesto completo dei beni e della situazione del possessore della polizza, incluse informazioni come l'ubicazione, il meteo, il traffico e il benessere generale. Le analisi approfondite di queste informazioni consentono all'assicuratore di fornire valutazioni del rischio e protezione in tempo reale per il possessore della polizza. I benefici per il possessore della polizza includono la possibilità di evitare i rischi con avvisi anticipati, avvertenze personalizzate e un accordo e elaborazione dei reclami accelerato. I benefici per l'assicuratore includono la soddisfazione del cliente, la fedeltà del cliente e la riduzione delle spese utilizzando il contenimento dei reclami e l'automazione del processo.

## Flusso del processo
{: #processFlow}
Il provider dell'assicurazione dispone di un'istanza nel broker del servizio {{site.data.keyword.Bluemix_notm}}. I clienti dell'assicuratore dispongono di sensori nelle loro case, collegati al cloud del provider dei sensori. Per i loro dispositivi mobili, i proprietari di casa autorizzano il servizio {{site.data.keyword.iotinsurance_short}} a ricevere i dati dai sensori da {{site.data.keyword.iotinsurance_short}}. Il servizio {{site.data.keyword.iotinsurance_short}} si collega al cloud del provider dei sensori e trasmette i dati di ogni utente e li invia al server IoT. Se il sensore mostra che i parametri specificati negli scudi dell'assicuratore vengono soddisfatti nella casa del cliente, le notifiche vengono inviate al dashboard dell'assicuratore e al dispositivo del cliente.

## Componenti
{: #components}

### Dashboard assicurazione
{: #insurance_dashboard}
Il dashboard dell'assicurazione fornisce agli utenti della compagnia assicurativa, come gli agenti, un visuale completa di cosa sta succedendo con i beni assicurati dei propri clienti. Possono visualizzare gli scudi e gli eventi a livello nazionale, statale o dell'account.

Il dashboard dell'assicurazione di esempio è caricato con dati simulati per mostrarti un esempio del tipo di informazioni che puoi raccogliere e analizzare.

### Applicazione starter mobile
{: #mobileapp}
L'applicazione starter mobile è dove i possessori della polizza d'assicurazione, come i proprietari di casa, visualizzano e rispondono alle informazioni che {{site.data.keyword.iotinsurance_short}} invia dai sensori nelle loro case.

Utilizzando un dispositivo mobile, i proprietari di casi autorizzano il servizio a collegarsi al cloud del provider dei sensori per inviare e ricevere dati. Ad esempio, un proprietario di casa può ricevere una notifica nell'applicazione starter mobile quando il sensore rileva una fuoriuscita d'acqua. Per ulteriori informazioni, consulta [Installazione e collegamento di un'applicazione starter mobile](iotinsurance_mobile_app.html).

### API REST
{: #rest_api}
L'API REST viene utilizzata dall'applicazione starter mobile, dal dashboard dell'assicurazione, dal motore della protezione e dal controllore del pericolo. Consente agli utenti di conoscere le associazioni che esistono tra i dispositivi e gli scudi e le azioni. Utilizzando questa API, i programmatori possono creare nuovi utenti, generare dati di eventi, creare e registrare nuovi scudi e richiamare i dati dell'evento.

L'API a cui accedi dalla console del servizio viene personalizzata per la tua assicurazione di {{site.data.keyword.iotinsurance_short}}.

Nella pagina dell'API, puoi  
  - Visualizzare le chiamate API disponibili e la documentazione associata.
  - Tentare chiamate API individuali.  Selezionare una chiamata API per visualizzare tutte le informazioni e quindi fare clic su **Provalo adesso!**.

Gli esempi API sono disponibili per aiutarti ad iniziare ad utilizzare gli scenari comuni. Per ulteriori informazioni, vedi [Esempi di API {{site.data.keyword.iotinsurance_short}}](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs).

### provider cloud
{: #cloudprovider}
Gli utenti devono autorizzare il componente Trasformatore ad accedere ai dati cloud del sensore e ad elaborare i dati registrati. L'autorizzazione viene concessa utilizzando l'applicazione starter mobile. Wink è l'unico fornitore cloud che è supportato in questo momento.

### Trasformatore
{: #transformer}
Il trasformatore richiede nuove informazioni dall'API del server cloud e le trasforma per corrispondere ai dati in {{site.data.keyword.iotinsurance_short}}. I dati sono quindi pubblicati per il resto dell'implementazione {{site.data.keyword.iotinsurance_short}} da utilizzare.

### Motore di analisi
{: #analytics_engine}
In base alle informazioni archiviate in un evento, il motore di analisi determina se si verifica una pericolo come una fuoriuscita d'acqua. Se viene identificato un pericolo, viene trasmesso al controllore del pericolo. Il motore delle azioni visualizza i dati nel database per determinare l'azione da intraprendere in base alle informazioni specificate nello scudo.

Puoi creare nuovi scudi in JavaScript utilizzando l'API {{site.data.keyword.iotinsurance_short}}.

### Scudi
{: #shields}
Uno scudo è una protezione che un cliente compra dal provider dell'assicurazione. Ad esempio, un proprietario di casa acquista un'assicurazione sulla propria casa per proteggerlo in caso di incendio, danni dovuti a perdite d'acqua, a furti con scasso o ad altri pericoli. La soluzione {{site.data.keyword.iotinsurance_short}} fornisce uno scudo integrato contro l'acqua. I clienti vengono avvertiti e possono rispondere quando un evento che coinvolge l'acqua minaccia la loro casa. Utilizzando l'API REST, gli sviluppatori possono aggiungere altri scudi.
Gli scudi sono eseguiti nel motore di analisi {{site.data.keyword.iotinsurance_short}}. Il motore di analisi identifica il tipo di pericolo (ad esempio *Acqua rilavata*), l'account utente del sensore che invia il pericolo e gli scudi associati con l'account. Possono essere intraprese delle azioni in base a tali informazioni.
