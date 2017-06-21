---

copyright:
  years: 2017
lastupdated: "2017-05-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Informazioni
{: #about}

{{site.data.keyword.bplong}} può essere utilizzato per creare i mattoni dell'infrastruttura. Puoi mettere insieme i servizi di {{site.data.keyword.IBM_notm}} Cloud per creare un'infrastruttura che sia distribuibile e riutilizzabile.
{:shortdesc}

{{site.data.keyword.bpshort}} utilizza Terraform per semplificare la gestione dell'infrastruttura. Ad esempio, se vuoi avviare più copie del tuo servizio che utilizza un cluster di server di applicazioni, un programma di bilanciamento del carico e un server di database, puoi scrivere uno script bash per eseguire comandi per avviare questi componenti. Tuttavia, è più facile, più veloce e più ordinato avere una configurazione con un'unità di esecuzione che prende la configurazione e la trasforma in risorse reali. Con Terraform, puoi avviare risorse diverse contemporaneamente, come gruppo collettivo, con le dipendenze associate all'interno. 

## Motivi per utilizzare {{site.data.keyword.bpshort}}
{: #reasons}

Potresti voler utilizzare l'infrastruttura codificata nei seguenti scenari:
{:shortdesc}

| Scenario     | Motivi    |
| :------------- | :------------- |
| Vuoi ricreare e riutilizzare la tua infrastruttura. | Puoi utilizzare {{site.data.keyword.bpshort}} per la gestione dell'infrastruttura. Con {{site.data.keyword.bpshort}}, puoi eseguire il provisioning, modificare ed eliminare le risorse a livello di programmazione. Quando codifichi e configuri le risorse, puoi creare una libreria di risorse che può essere riutilizzata più volte per ottenere gli stessi risultati.|
| Vuoi trasparenza su come vengono configurati gli ambienti. | {{site.data.keyword.bpshort}} funziona con le configurazioni del controllo sorgente, che abilita la collaborazione, la revisione e ti fornisce un audit trail per vedere come e quando sono state apportate delle modifiche. Puoi anche visualizzare le modifiche se devi eseguire il rollback a una configurazione precedente. |
| Vuoi semplificare l'esecuzione delle modifiche ambientali. | {{site.data.keyword.bpshort}} segue il modello dichiarativo che fornisce una singola fonte di verità. Quando pianifichi una modifica al tuo ambiente, indichi il risultato che vuoi ottenere.  |
| Utilizzi già uno strumento di gestione configurazione, ma vuoi un modo più automatizzato per impostare i tuoi ambienti.  | {{site.data.keyword.bpshort}} può lavorare con gli strumenti di gestione configurazione. Gli ambienti distribuiti con {{site.data.keyword.bpshort}} sono astrazioni di alto livello che possono creare le risorse dell'infrastruttura. Puoi quindi utilizzare gli strumenti di gestione configurazione per installare e configurare il software sulle risorse di cui {{site.data.keyword.bpshort}} ha eseguito il provisioning.  
  
## Come funziona
{: #how}

Puoi distribuire le risorse ai tuoi ambienti utilizzando {{site.data.keyword.bpshort}}.
{:shortdesc}

{{site.data.keyword.bpshort}} utilizza Terraform come strumento sottostante per abilitare l'infrastruttura come codice in modo che tu possa definire le risorse {{site.data.keyword.IBM}} Cloud come codice. Le risorse cloud possono essere componenti diversi della tua infrastruttura, ad esempio server bare metal, server virtuali, programmi di bilanciamento del carico e componenti di rete definiti da software. 

### Configurazioni per definire le risorse
{: #how-define}

Una configurazione, o una configurazione Terraform, è un file che definisce quali risorse compongono l'infrastruttura. Le configurazioni sono delle architetture distribuibili che possono essere applicate a uno o più ambienti. Il seguente diagramma mostra che cosa costituisce una configurazione e come i pezzi lavorano insieme per creare un ambiente distribuibile in {{site.data.keyword.bpshort}}.


![Diagramma dell'architettura {{site.data.keyword.bpshort}}](/images/anatomy_of_a_schematic.png)

Figura 1. Diagramma dell'architettura {{site.data.keyword.bpshort}}

### Controllo sorgente per abilitare la collaborazione
{: #how-collaborate}

Le configurazioni vengono memorizzate in GitHub in modo che i team possano esaminare il codice e collaborare. Con GitHub, disponi di un audit trail integrato e puoi visualizzare un'intera cronologia di commit delle modifiche apportate alle tue configurazioni. Puoi salvare le informazioni sull'utilizzo nei file readme in modo da rendere la configurazione condivisibile e riutilizzabile da più team. 

### Ambienti {{site.data.keyword.bpshort}} per il provisioning delle risorse
{: #how-provision}

Puoi utilizzare {{site.data.keyword.bpshort}} per eseguire la scansione del tuo codice in GitHub e distribuire le risorse a un ambiente. Gli ambienti possono condividere le configurazioni comuni. Ad esempio, puoi avviare un ambiente QA temporaneo che si presenti come di produzione ed eliminarlo una volta terminato con i test. Puoi creare una libreria di configurazioni di ambienti comuni che possono essere contrassegnate e ricercate da tutti gli utenti nel tuo account {{site.data.keyword.Bluemix_notm}}.
