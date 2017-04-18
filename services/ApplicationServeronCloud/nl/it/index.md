---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-01"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Introduzione a IBM WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}
{: #getting_started}

{{site.data.keyword.IBM}} WebSphere Application Server for {{site.data.keyword.Bluemix}} è un servizio che aiuta a impostare rapidamente un'istanza WebSphere Application Server Liberty, Traditional Network Deployment o un'istanza Traditional WebSphere Java EE in un ambiente cloud ospitato su {{site.data.keyword.Bluemix_notm}}.
{: shortdesc}

## Panoramica di WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}
{: #overview}

WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} fornisce ai consumatori i server WebSphere tradizionale e Liberty Profile preconfigurati. È ospitato su guest macchina virtuale con accesso root al
sistema operativo guest. Quando crei il tuo servizio, scegli tra *Liberty*, *Traditional ND* o *Traditional WebSphere*.

**Nota:** i clienti sono ora in grado di scegliere tra la V8.5 e la V9.0 quando creano una nuova istanza *Traditional ND* o *Traditional WebSphere*.

Ti verrà offerta una classica esperienza di amministrazione WebSphere e avrai accesso completo al sistema operativo
sottostante. Puoi riutilizzare i tuoi script esistenti e apportare quelle piccole modifiche al
sistema di cui hai bisogno per lavorare con il tuo framework o con quello di terze parti. Admin Center e Admin Console sono forniti per amministrare il tuo servizio WebSphere Application Server Liberty, ND o tradizionale, proprio come le tue configurazioni WebSphere installate in loco.

Il piano WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} Network Deployment consiste in un ambiente di cella WebSphere Application Server Network Deployment con due o più macchine virtuali. La prima macchina virtuale contiene il Deployment Manager e IBM HTTP Server e le restanti macchine virtuali contengono nodi personalizzati (agent nodo) federati al Deployment Manager. Utilizza i tuoi script wsadmin esistenti per creare la tua configurazione WebSphere o utilizza la console di gestione WebSphere per configurare manualmente l'ambiente. Queste nuove funzionalità consentono agli utenti di impostare un ambiente in cluster per l'elevata disponibilità, il che è un aspetto critico per ogni applicazione aziendale middleware. I clienti possono ora scegliere di organizzare in cluster una topologica per bilanciare il carico delle richieste tra due o più istanze. 

Il piano di WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} Liberty Core include l'utilizzo di un collettivo Liberty. Il collettivo Liberty è un dominio amministrativo per un gruppo di profili Liberty (server) e consiste in due o più macchine virtuali. La prima macchina virtuale contiene il server Collective Controller Liberty, che è un punto di controllo per il collettivo Liberty. Oltre al collettivo Liberty, questa macchina virtuale contiene anche IBM HTTP Server, che consente l'accesso alle tue applicazioni da un browser web. Le restanti macchine virtuali sono gli host di collettivo dove
si trovano i membri del collettivo (server Liberty Profile). La funzione Liberty Admin Center è anche abilitata sul server di controller Liberty.

La seguente figura mostra l'architettura degli ambienti WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} Network Deployment Cell e il collettivo Liberty.

Figura 1. Architettura di Network deployment cell e del collettivo Liberty

![Figura1. Architettura di Network deployment cell e del collettivo Liberty](images/CellCollectiveDiagram.gif)

**Nota**: nella precedente *Figura 1*, il pattern contiene descrizioni sulla collocazione del Deployment Manager o del Collective Controller con il IBM HTTP Server prevista per gli scopi di sviluppo e verifica. WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} ti fornisce inoltre la libertà di riconfigurare il software pre-installato per soddisfare i tuoi bisogni operativi e l'applicazione di produzione; come se fossi in loco. Inoltre, per rigorosi requisiti di produzione, contatta il rappresentante del settore Vendite di IBM in merito alla nostra offerta IBM WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} a singolo tenant, che offre risorse di calcolo e di rete isolate. 


## Ambiente operativo
{: #operational_environment}

IBM WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} è un servizio che restituisce i guest (macchine virtuali) in un ambiente condiviso per consentire agli utilizzatori di distribuire applicazioni. Una VPN
protegge il servizio pubblico da scansioni di porta generiche e altri attacchi indesiderati basati sulla rete. Tuttavia, è importante notare che la VPN del servizio che usi per accedere alla tua istanza del servizio potrebbe essere
condivisa tra più organizzazioni e utenti
{{site.data.keyword.Bluemix_notm}}. Le macchine virtuali
forniscono risorse di elaborazione, memoria e I/O, che provengono da un pool condiviso di
risorse IaaS.

Poiché le specifiche risorse di elaborazione, memoria e I/O sono eseguite da macchine virtuali in un ambiente condiviso, le configurazioni del servizio possono variare. Le configurazioni per ciascuna specifica istanza del servizio
possono essere visualizzate mediante i portali e i dashboard del servizio IBM WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}.

IBM WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} fornisce istanze della macchina virtuale. Con queste istanze, i clienti utilizzano un portale semplice per creare e gestire le distribuzioni di WebSphere Application Server aziendale in un modo coerente, ripetibile con flessibilità significativa per ottimizzare le loro applicazioni. Gli utenti possono iniziare a lavorare su un WebSphere Application Server Liberty preconfigurato, ND o su macchine virtuali tradizionali in un ambiente cloud ospitato. Gli utenti possono migrare le applicazioni WebSphere Application Server esistenti su {{site.data.keyword.Bluemix_notm}} e prendere il controllo completo del sottostante SO e middleware.

## Strategia sul prezzo
{: #pricing_strategy}

IBM WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} fornisce delle istanze con ridimensionamento T-Shirt per i clienti con applicazioni ad uso intensivo di memoria per dimensionare correttamente l'ambiente con macchine virtuali più grandi. I clienti possono selezionare la dimensione della risorsa specifica di un componente di WebSphere Application Server con provisioning o un singolo sistema fino a 32 GB RAM di macchine virtuali.

Le seguenti tabelle rappresentano i piani prezzi di IBM WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} a partire dal 1° aprile 2016 e sono indicati in dollari americani (USD).

*Tabella 1. Piano Liberty Core*

| **T-Shirt** | **vCPU** | **RAM (GB)** | **HD (GB)** | **Prezzo/Hr** |       
|:-------------:|:----------:|:--------------:|:-------------:|:--------------:|
| S | 1 | 2 | 12 | $0,21 |
| M | 2 | 4 | 25 | $0,42 |
| L | 4 | 8 | 50 | $0,84 |
| XL | 8 | 16 | 100 | $1,68 |
| XXL | 16 | 32 | 200 | $3,36 |

*Tabella 2. Piano base WebSphere Application Server*

| **T-Shirt** | **vCPU** | **RAM (GB)** | **HD (GB)** | **Prezzo/Hr** |       
|:-------------:|:----------:|:--------------:|:-------------:|:--------------:|
| S | 1 | 2 | 12 | $0,30 |
| M | 2 | 4 | 25 | $0,60 |
| L | 4 | 8 | 50 | $1,20 |
| XL | 8 | 16 | 100 | $2,40 |
| XXL | 16 | 32 | 200 | $4,80 |

*Tabella 3. Piano ND WebSphere Application Server*

| **T-Shirt** | **vCPU** | **RAM (GB)** | **HD (GB)** | **Prezzo/Hr** |       
|:-------------:|:----------:|:--------------:|:-------------:|:--------------:|
| S | 1 | 2 | 12 | $0,70 |
| M | 2 | 4 | 25 | $1,40 |
| L | 4 | 8 | 50 | $2,80 |
| XL | 8 | 16 | 100 | $5,60 |
| XXL | 16 | 32 | 200 | $11,20 |

<p></p>

IBM WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} è offerto in conformità alla seguente metrica di addebito:

*  *Istanza-ora*: un'istanza è definita come accesso a una configurazione specifica del servizio IBM WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}. I clienti vengono addebitati per ogni ora parziale o completa per ogni istanza del servizio distribuita durante il periodo di fatturazione. Ogni istanza-ora viene fatturata mensilmente e se un'istanza viene utilizzata solo una parte del mese, il tasso di utilizzo viene ripartito proporzionalmente.

Ad esempio, se utilizzi un piano ND, una istanza equivale a 1vCPU con 2 GB RAM e 12 GB HD. Così se scegli di configurare la tua cella con un nodo di controllo e otto nodi personalizzati, ti saranno addebitati nove nodi (istanze).

**Nota**: l'addebito minimo è impostato su 0.25 istanza-ora per nodo personalizzato o host Liberty. Nell'esempio sottostante, un nodo di controllo e un nodo personalizzato configurato per 15 minuti equivalgono a un addebito minimo di (.25 * # di istanze).

**Nota**: a causa di una specifica quantità di risorse I/O, calcolo e memoria, ai clienti vengono addebitate le istanze accumulate nello stato ARRESTATO a un tasso ridotto del 5%.  I clienti vengono gestiti fino a un numero fisso di istanze ARRESTATE con non più di 10 indirizzi IP o 64 GB di memoria.

# rellinks
{: #rellinks}
## general
{: #general}
* [WASdev](https://developer.ibm.com/wasdev/){: new_window}
* [Documentazione di WebSphere Application Server V9](http://www.ibm.com/support/knowledgecenter/SSEQTP_9.0.0/as_ditamaps/was900_welcome_base.html){: new_window}
