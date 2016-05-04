---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Introduzione a IBM WebSphere Application Server for Bluemix
{: #getting_started}

*Ultimo aggiornamento: 08 aprile 2016*

{{site.data.keyword.IBM}} WebSphere Application Server for {{site.data.keyword.Bluemix}} è un servizio che facilita una rapida impostazione di un WebSphere Application Server Liberty, un Network Deployment o un'istanza tradizionale preconfigurati in un ambiente cloud ospitato su Bluemix.
{: shortdesc}

## Panoramica di WebSphere Application Server for Bluemix
{: #overview}

WebSphere Application Server for Bluemix fornisce ai consumatori dei server WebSphere e Liberty Profile tradizionali preconfigurati. È ospitato su guest macchina virtuale con accesso root al
sistema operativo guest. Quando crei il tuo servizio, scegli tra *Liberty*, *ND* o *WebSphere tradizionale*.

Ti verrà offerta una classica esperienza di amministrazione WebSphere e avrai accesso completo al sistema operativo
sottostante. Puoi riutilizzare i tuoi script esistenti e apportare quelle piccole modifiche al
sistema di cui hai bisogno per lavorare con il tuo framework o con quello di terze parti. Admin Center e Admin Console sono forniti per amministrare il tuo servizio tradizionale, WebSphere Application Server Liberty o ND, proprio come le tue configurazioni WebSphere installate in loco.

**Nota**: Il piano di WebSphere Application Server for Bluemix Network Deployment ora offre più funzionalità. Il piano consiste in un ambiente di cella WebSphere Application Server Network Deployment con due o più macchine virtuali. La prima macchina virtuale contiene il Deployment Manager e IBM HTTP Server e le restanti macchine virtuali contengono nodi personalizzati (agent nodo) federati al Deployment Manager. Utilizza i tuoi script wsadmin esistenti per creare la tua configurazione WebSphere o utilizza la console di gestione WebSphere per configurare manualmente l'ambiente. Queste nuove funzionalità consentono agli utenti di impostare un ambiente in cluster per l'elevata disponibilità, il failover e la scalabilità. Il clustering è un aspetto critico delle applicazioni aziendali
middleware e i clienti possono ora scegliere di organizzare in cluster una topologica per bilanciare il carico delle richieste tra due o più istanze.

Il piano di WebSphere Application Server for Bluemix Liberty Core offre anche ulteriori funzionalità. Il piano include l'utilizzo di un collettivo Liberty, che è un dominio amministrativo per un gruppo di profili Liberty (server) e consiste in due o più macchine virtuali. La prima macchina virtuale contiene il server Collective Controller Liberty, che è un punto di controllo per il collettivo Liberty. Oltre al collettivo Liberty, questa macchina virtuale contiene anche IBM HTTP Server, che consente l'accesso alle tue applicazioni da un browser web. Le restanti macchine virtuali sono gli host di collettivo dove
si trovano i membri del collettivo (server Liberty Profile). La funzione Liberty Admin Center è anche abilitata sul server di controller Liberty.

La seguente figura mostra l'architettura degli ambienti WebSphere Application Server for Bluemix Network Deployment Cell e il collettivo Liberty.

![Figura1. Architettura di Network deployment cell e del collettivo Liberty](images/CellCollectiveDiagram.gif)

## Ambiente operativo
{: #operational_environment}

IBM WebSphere Application Server for Bluemix è un servizio che restituisce i guest (macchine virtuali) in un ambiente condiviso per consentire agli utilizzatori di distribuire applicazioni. Una VPN
protegge il servizio pubblico da scansioni di porta generiche e altri attacchi indesiderati basati sulla rete. Tuttavia, è importante notare che la VPN del servizio che usi per accedere alla tua istanza del servizio potrebbe essere condivisa tra più organizzazioni e utenti Bluemix. Le macchine virtuali
forniscono risorse di elaborazione, memoria e I/O, che provengono da un pool condiviso di
risorse IaaS. Se vuoi eseguire le tue applicazioni in un ambiente privato, contatta il rappresentante del settore Vendite di IBM in merito alla nostra offerta IBM WebSphere Application Server for Bluemix dedicata.

Poiché le specifiche risorse di elaborazione, memoria e I/O sono eseguite da macchine virtuali in un ambiente condiviso, le configurazioni del servizio possono variare. Le configurazioni per ciascuna specifica istanza del servizio possono essere visualizzate mediante i portali e i dashboard del servizio IBM WebSphere Application Server for Bluemix.

**Nota**: IBM WebSphere Application Server for Bluemix fornisce ora un'opzione per i clienti con applicazioni intensive di memoria per dimensionare correttamente il loro ambiente con grandi macchine virtuali. I clienti possono selezionare la dimensione della risorsa specifica di un componente di WebSphere Application Server con provisioning o un singolo sistema fino a 32 GB RAM di macchine virtuali.

## Strategia sul prezzo
{: #pricing_strategy}

IBM WebSphere Application Server for Bluemix fornisce istanze della macchina virtuale. Con queste istanze, i clienti utilizzano un portale semplice per creare e gestire le distribuzioni di WebSphere Application Server aziendale in un modo coerente, ripetibile con flessibilità significativa per ottimizzare le loro applicazioni. Gli utenti possono iniziare a lavorare su un WebSphere Application Server Liberty preconfigurato, ND, o su macchine virtuali tradizionali in un ambiente cloud ospitato. Gli utenti possono migrare le applicazioni WebSphere Application Server esistenti su Bluemix e prendere il controllo completo del sottostante SO e middleware.

IBM WebSphere Application Server for Bluemix è offerto in conformità alla seguente metrica di addebito:

*  *Istanza-ora*: un'istanza è definita come accesso a una configurazione specifica del IBM WebSphere Application Server per un servizio Bluemix. I clienti vengono addebitati per ogni ora parziale o completa per ogni istanza del servizio distribuita durante il periodo di fatturazione. Ogni istanza-ora viene fatturata mensilmente e se un'istanza viene utilizzata solo una parte del mese, il tasso di utilizzo viene ripartito proporzionalmente.

Ad esempio, se utilizzi un piano ND, una istanza equivale a 1vCPU con 2 GB RAM e 12 GB HD. Così se scegli di configurare la tua cella con un nodo di controllo e otto nodi personalizzati, ti saranno addebitati nove nodi (istanze).

**Nota**: l'addebito minimo è impostato su 0.25 istanza-ora per nodo personalizzato o host Liberty. Nell'esempio sottostante, un nodo di controllo e un nodo personalizzato configurato per 15 minuti equivalgono a un addebito minimo di (.25 * # di istanze).

# rellinks
## general
* [WASdev](https://developer.ibm.com/wasdev/){: new_window}
* [Documentazione di WebSphere Application Server](http://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/as_ditamaps/was855_welcome_ndmp.html){: new_window}
* [Documentazione di WebSphere Application Server tradizionale v9 Beta](http://www.ibm.com/support/knowledgecenter/SSEQTP_9.0.0/as_ditamaps/was900_welcome_base.html){: new_window}
