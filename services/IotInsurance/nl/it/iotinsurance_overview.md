---

copyright:
  years: 2016
lastupdated: "2016-10-26"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}


# Informazioni su {{site.data.keyword.iotinsurance_short}}
{: #about}
Ultimo aggiornamento: 21 ottobre 2016
{: .last-updated}

{{site.data.keyword.iotinsurance_full}} è un'istanza di produzione IoT integrata che raccoglie e analizza i dati di contesto completo dai possessori della polizza per fornire valutazioni del rischio, protezione in tempo reale e riduzione dei costi della politica personalizzati.
{: shortdesc}

{{site.data.keyword.iotinsurance_short}} fornisce una visualizzazione di contesto completo dei beni e della situazione del possessore della polizza, incluse informazioni come l'ubicazione, il meteo, il traffico e il benessere generale. Le analisi approfondite di queste informazioni consentono all'assicuratore di fornire valutazioni del rischio e protezione in tempo reale per il possessore della polizza. I benefici per il possessore della polizza includono la possibilità di evitare i rischi con avvisi anticipati, avvertenze personalizzate e un accordo e elaborazione dei reclami accelerato. I benefici per l'assicuratore includono la soddisfazione del cliente, la fedeltà del cliente e la riduzione delle spese utilizzando il contenimento dei reclami e l'automazione del processo.

## Architettura
{: #architecture}

![{{site.data.keyword.iotinsurance_short}} Architettura. Questo diagramma è descritto nel corpo principale dell'argomento.](images/IoT4I_architecture.svg "{{site.data.keyword.iotinsurance_short}} architettura")

I componenti {{site.data.keyword.iotinsurance_short}} funzionano insieme come descritto in questa sezione. Questa organizzazione viene anche mostrata nel diagramma dell'architettura. Il dashboard {{site.data.keyword.iotinsurance_short}} visualizza i dati archiviati in {{site.data.keyword.iot_short_notm}} e nel database {{site.data.keyword.cloudantfull}}. I dispositivi intelligenti dell'utente, collegati tramite il cloud Wink, inviano i dati al trasformatore, che li elabora ed invia a {{site.data.keyword.iot_short_notm}}. I dati vengono elaborati dal motore dello scudo e se soddisfano i criteri dello scudo vengono inviati tramite le API al motore delle azioni. Il motore delle azioni utilizza {{site.data.keyword.mobilepushfull}} per inviare notifiche all'applicazione mobile dell'utente. L'utente può inoltre utilizzare l'applicazione mobile per rispondere agli avvisi o alle offerte. La risposta viene elaborata dal servizio {{site.data.keyword.amafull}} e restituita tramite le API a {{site.data.keyword.iot_short_notm}} e quindi al dashboard {{site.data.keyword.iotinsurance_short}}.

## Dashboard assicurazione
{: #insurance_dashboard}
Il dashboard dell'assicurazione fornisce agli utenti della compagnia assicurativa, come gli agenti, un visuale completa di cosa sta succedendo con i beni assicurati dei propri clienti. Possono visualizzare gli scudi e gli eventi a livello nazionale, statale o dell'account.

Il dashboard dell'assicurazione di esempio è caricato con dati simulati per mostrarti un esempio del tipo di informazioni che puoi raccogliere e analizzare.

## Applicazione mobile di esempio
{: #mobileapp}
L'applicazione mobile di esempio è dove i possessori della polizza d'assicurazione, come i proprietari di casa, visualizzano e rispondono alle informazioni che {{site.data.keyword.iotinsurance_short}} invia dai sensori nelle loro case.

Utilizzando un dispositivo mobile, i proprietari di casi autorizzano il servizio a collegarsi al cloud del provider dei sensori per inviare e ricevere dati. Ad esempio, un proprietario di casa può ricevere una notifica nell'applicazione starter mobile quando il sensore rileva una fuoriuscita d'acqua. Per ulteriori informazioni, consulta [Installazione e collegamento dell'applicazione mobile di esempio](iotinsurance_mobile_app.html}). 

## API REST e in tempo reale
{: #rest_api}
Le API REST vengono utilizzate dall'applicazione starter mobile, dal dashboard dell'assicurazione, dal motore della protezione e dal controllore del pericolo. Consentono agli utenti di conoscere le associazioni che esistono tra i dispositivi e gli scudi e le azioni. Utilizzando queste API, i programmatori possono creare nuovi utenti, generare dati di eventi, creare e registrare nuovi scudi e richiamare i dati dell'evento. 

L'API a cui accedi dalla console del servizio viene personalizzata per la tua assicurazione di {{site.data.keyword.iotinsurance_short}}.

Nella pagina dell'API, puoi  
  - Visualizzare le chiamate API disponibili e la documentazione associata.
  - Tentare chiamate API individuali.  Selezionare una chiamata API per visualizzare tutte le informazioni e quindi fare clic su **Provalo adesso!**.

Gli esempi API sono disponibili per aiutarti ad iniziare ad utilizzare gli scenari comuni. Per ulteriori informazioni, vedi [Esempi di API {{site.data.keyword.iotinsurance_short}}](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs).


## Trasformatore
{: #transformer}
Il trasformatore richiede nuove informazioni dall'API del server cloud e le trasforma per corrispondere ai dati in {{site.data.keyword.iotinsurance_short}}. I dati sono quindi pubblicati per il resto dell'implementazione {{site.data.keyword.iotinsurance_short}} da utilizzare. Gli utenti devono autorizzare il componente Trasformatore ad accedere ai dati cloud del sensore e ad elaborare i dati registrati. L'autorizzazione viene concessa utilizzando l'applicazione starter mobile. Wink è l'unico fornitore cloud che è supportato in questo momento.

## Motore dello scudo
{: #shield_engine}
In base alle informazioni archiviate in un evento, il motore dello scudo determina se si verifica una pericolo come una fuoriuscita d'acqua. Se viene identificato un pericolo, viene trasmesso al motore dello scudo 

## Motore delle azioni
{: #action_engine}
Il motore delle azioni determina le azioni da intraprendere in base alle informazioni specificate nello scudo. 

Puoi creare nuovi scudi in JavaScript utilizzando l'API {{site.data.keyword.iotinsurance_short}}.

## Scudi
{: #shields}
Uno scudo è una protezione che un cliente compra dal provider dell'assicurazione. Ad esempio, un proprietario di casa acquista un'assicurazione sulla propria casa per proteggerlo in caso di incendio, danni dovuti a perdite d'acqua, a furti con scasso o ad altri pericoli. La soluzione {{site.data.keyword.iotinsurance_short}} fornisce uno scudo integrato contro l'acqua. I clienti vengono avvertiti e possono rispondere quando un evento che coinvolge l'acqua minaccia la loro casa. Utilizzando l'API REST, gli sviluppatori possono aggiungere altri scudi.
Gli scudi sono eseguiti nel motore di analisi {{site.data.keyword.iotinsurance_short}}. Il motore di analisi identifica il tipo di pericolo (ad esempio *Acqua rilavata*), l'account utente del sensore che invia il pericolo e gli scudi associati con l'account. Possono essere intraprese delle azioni in base a tali informazioni.

# Link correlati
{: #rellinks}

## Esercitazioni ed esempi
{: #samples}
* [Sample mobile app code on GitHub](https://github.com/ibm-watson-iot/ioti-mobile){:new_window}

## Riferimento API
{: #api}
* [{{site.data.keyword.iotinsurance_short}} API](https://iot4i-api-docs.mybluemix.net/){:new_window}
* [{{site.data.keyword.iotinsurance_short}} API Examples](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/#iot-for-insurance-api-examples){:new_window}

## Link correlati
{: #general}
* [Documentazione {{site.data.keyword.iot_full}}](https://console.ng.bluemix.net/docs/services/IoT/index.html)
* [Developer support forum](https://developer.ibm.com/answers/search.html?f=&type=question&redirect=search%2Fsearch&sort=relevance&q=%2B[iot]%20%2B[bluemix])
* [Stack overflow support forum](http://stackoverflow.com/questions/tagged/ibm-bluemix)
