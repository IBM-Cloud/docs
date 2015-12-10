{:new_window: target="_blank"} 
{:shortdesc: .shortdesc}

#{{site.data.keyword.Bluemix_notm}} dedicato
{: #dedicated}

*Ultimo aggiornamento: 3 novembre 2015*

{{site.data.keyword.Bluemix}} è
una piattaforma basata su cloud open standard per la creazione, esecuzione e
gestione delle applicazioni. Con {{site.data.keyword.Bluemix_notm}} dedicato, ottieni la potenza unita alla semplicità di {{site.data.keyword.Bluemix_notm}} nel tuo ambiente SoftLayer dedicato che è connesso in modo protetto sia all'ambiente {{site.data.keyword.Bluemix_notm}} pubblico sia alla tua rete.
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} dedicato
include un catalogo privato che visualizza i servizi dedicati
disponibili in esclusiva per te. Sono compresi inoltre dei servizi aggiuntivi
che vengono diffusi e messi a disposizione da {{site.data.keyword.Bluemix_notm}} pubblico.

{{site.data.keyword.Bluemix_notm}} dedicato è costruito su SoftLayer, così da permetterti di usufruire della struttura cloud dalle prestazioni più elevate. Ciascun data center fornisce rigorosi controlli di sicurezza 24 ore al giorno, 7
giorni a settimana. Tu e IBM accedete all'istanza di {{site.data.keyword.Bluemix_notm}} dedicato tramite un tunnel VPN e una VLAN privata.

![{{site.data.keyword.Bluemix_notm}} Dedicato](images/detaileddedicated.png "{{site.data.keyword.Bluemix_notm}} dedicato")

*Figura 1. Diagramma dettagliato di {{site.data.keyword.Bluemix_notm}} dedicato*

Gli ambienti di {{site.data.keyword.Bluemix_notm}} dedicato
hanno gli stessi standard di sicurezza di {{site.data.keyword.Bluemix_notm}} pubblico in
termini di sicurezza fisica, operativa e di infrastruttura. Tuttavia,
l'accesso degli sviluppatori a {{site.data.keyword.Bluemix_notm}} dedicato è
controllato dalle tue politiche LDAP, che possono essere configurate dal team di {{site.data.keyword.Bluemix_notm}}
nel momento in cui configurano il tuo ambiente. All'interno dell'ambiente dedicato,
puoi gestire i ruoli e le autorizzazioni degli utenti. Per i dettagli, vedi [Gestione di utenti e autorizzazioni](../admin/index.html#oc_useradmin).

{{site.data.keyword.Bluemix_notm}} dedicato
viene fornito con tutti i runtime {{site.data.keyword.Bluemix_notm}} inclusi
e 128 GB di memoria per le applicazioni.

È inoltre disponibile una serie di servizi inclusi per impostazione predefinita e altri facoltativi che puoi scegliere per la tua istanza dedicata. 

| **Tipo**        | **Nome**            | **Descrizione** |      
|-----------------|-------------------|-------------------|
| Incluso | {{site.data.keyword.autoscaling}} | Ti permette di aumentare o ridurre dinamicamente la capacità
di elaborazione della tua applicazione in base alle politiche. Con questo servizio,
avrai un uso illimitato nel tuo ambiente {{site.data.keyword.Bluemix_notm}}
dedicato. |
| Incluso | {{site.data.keyword.datacshort}} | Questo servizio fornisce una griglia di dati in memoria
che supporta scenari di cache distribuita per le tue applicazioni. Include
50 GB di cache in memoria. |
| Incluso | {{site.data.keyword.cloudant}} | Database NoSQL IBM che fornisce un livello di dati JSON ad elevate prestazioni (compatibile con CouchDB). Include 1,6 TB e fino a 3.000 richieste API al secondo. |
| Facoltativo | {{site.data.keyword.sqldb}} | IBM {{site.data.keyword.sqldbfull}} Database per {{site.data.keyword.Bluemix_notm}} aggiunge
un database relazionale con provisioning completo alla tua applicazione. {{site.data.keyword.sqldb}} fornisce un database gestito per occuparsi degli impegnativi carichi di lavoro transazionali e web della tua attività di business.  |
| Facoltativo | {{site.data.keyword.mql}} | IBM {{site.data.keyword.mqlfull}} per {{site.data.keyword.Bluemix_notm}} è
un servizio di messaggistica basato sul cloud che fornisce una messaggistica flessibile e facile da usare per le applicazioni {{site.data.keyword.Bluemix_notm}}. {{site.data.keyword.mql}} fornisce una soluzione con ridotte esigenze gestionali alla messaggistica. Puoi utilizzare {{site.data.keyword.mql}} per rendere le tue applicazioni più reattive e ridimensionabili e puoi condividere e scaricare lavoro tra le applicazioni con una semplice e potente API.  |
| Facoltativo | {{site.data.keyword.dashdbshort}} | Usa dashDB per memorizzare dati relazionali, inclusi i tipi speciali quali i dati geospaziali. Quindi, analizza tali dati utilizzando l'analisi integrata SQL o avanzata come l'analisi predittiva e il data mining, l'analisi con R e l'analisi geospaziale. |

*Tabella 1. Servizi dedicati*

##Configurazione dell'istanza di {{site.data.keyword.Bluemix_notm}} dedicato
{: #setupdedicated}

{{site.data.keyword.Bluemix_notm}} dedicato
è progettato per fornire una versione privata dell'offerta {{site.data.keyword.Bluemix_notm}}
pubblico. Puoi utilizzare i servizi e i runtime {{site.data.keyword.Bluemix_notm}} per supportare le tue esigenze di elaborazione in un account SoftLayer ospitato da IBM.

IBM ti fornisce l'accesso a {{site.data.keyword.Bluemix_notm}} dedicato, utilizzando un accesso protetto da password. Puoi accedere a servizi, runtime
e risorse associate nonché distribuire e rimuovere applicazioni {{site.data.keyword.Bluemix_notm}}. IBM si avvale di più sedi SoftLayer per la distribuzione di {{site.data.keyword.Bluemix_notm}} dedicato, il che ti permette di ottenere la tua versione privata in una sede a te vicina.

Per configurare la tua versione privata di {{site.data.keyword.Bluemix_notm}}:

<ol>
<li>Contatta il tuo rappresentante dell'account designato IBM oppure contattare <a href="https://console.ng.bluemix.net/?direct=classic/#/contactUs/cloudOEPaneId=contactUs" target="_blank">{{site.data.keyword.Bluemix_notm}}</a> per iniziare.</li>
<li>La quota mensile ricorrente si basa sui servizi dedicati
che desideri utilizzare, oltre a una sottoscrizione a tutti i servizi pubblici
{{site.data.keyword.Bluemix_notm}}. Riceverai quindi una fattura per tutto ciò che scegli di utilizzare
al di fuori di tale accordo di sottoscrizione.
	<ol type="a">
	<li>Determina insieme a IBM la quota per la tua istanza di {{site.data.keyword.Bluemix_notm}} dedicato.	La quota mensile ricorrente si basa sui servizi dedicati
che desideri utilizzare, oltre a una sottoscrizione a tutti i servizi pubblici
{{site.data.keyword.Bluemix_notm}}. Riceverai quindi una fattura per tutto ciò che scegli di utilizzare
al di fuori di tale accordo di sottoscrizione.</li>
	<li>Identifica le scadenze per ogni fase di configurazione
della tua istanza di {{site.data.keyword.Bluemix_notm}}
dedicato.</li>
	</ol>
	</li>
<li>Seleziona la <a href="http://www.softlayer.com/data-centers" target="_blank">sede data center SoftLayer</a> per la tua istanza dedicata. Verranno creati, quindi, la piattaforma dedicata e
l'account. Per l'account, devi identificare le persone all'interno della tua organizzazione
a cui assegnare i ruoli necessari per rendere operativa la tua istanza
dedicata.<br />
<br />
<dl>
<dt>**Procurement focal**</dt>
<dd>Lavora con i rappresentanti IBM per organizzare il tuo ambiente {{site.data.keyword.Bluemix_notm}} dedicato,
includendo l'identificazione delle persone adeguate a gestire
ogni aspetto del progetto all'interno della tua organizzazione. Questo ruolo supervisiona la selezione di pattern, le intese commerciali e l'organizzazione dell'accesso alle risorse cliente. Il Procurement focal è il contatto generale per la configurazione dell'istanza dedicata.</dd>
<dt>**Responsabile della conformità**</dt>
<dd>Lavora con i rappresentanti IBM per selezionare un'opzione di topologia e distribuzione che risponda ai tuoi requisiti
di sicurezza. Questo ruolo lavora con i consulenti di conformità IBM per determinare quali pattern di distribuzione raggiungono le finalità e gli obiettivi di conformità.</dd>
<dt>**Specialista di rete**</dt>
<dd>Lavora con i rappresentanti IBM sui piani di rete per la distribuzione {{site.data.keyword.Bluemix_notm}}. Questo ruolo fornisce i requisiti ai rappresentanti IBM e lavora con i rappresentanti su un piano di implementazione. Alla fine della fase di installazione e verifica, questo ruolo "approverà" che la configurazione di rete è conforme agli standard aziendali.</dd>
<dt>**DevOps focal**</dt>
<dd>Lavora con i rappresentanti IBM per pianificare e applicare gli aggiornamenti di manutenzione necessari per i runtime, i servizi e la piattaforma {{site.data.keyword.Bluemix_notm}}. Questo ruolo lavora anche con i rappresentanti IBM sulla configurazione della tua istanza di {{site.data.keyword.Bluemix_notm}} dedicato.</dd>
</dl>
</li>
<li>Definisci e stabilisci la connettività di rete tra la rete
aziendale e l'istanza di {{site.data.keyword.Bluemix_notm}}
dedicato.
	<ol type="a">
	<li>IBM installa l'infrastruttura di monitoraggio e di sicurezza per l'istanza dedicata.</li>
	<li>IBM installa i servizi dedicati a singolo tenant che hai selezionato.</li>
	<li>Fornisci gli endpoint e la configurazione di rete
per cose come indirizzi IP o firewall e accedi al tuo LDAP per
l'integrazione in {{site.data.keyword.Bluemix_notm}}.</li>
	</ol>
</li>
<li>Identifica e assegna i ruoli per il team amministrativo
dell'ambiente.
	<ol type="a">
	<li>IBM configura l'accesso alla rete e il LDAP in base alle informazioni che hai fornito. L'accesso amministrativo
viene fornito ai contatti da te designati. Devi designare un
contatto anche per il supporto e la fatturazione.</li>
	<li>IBM configura un catalogo diffuso su diversi canali nell'ambiente dedicato per visualizzare i tuoi servizi dedicati e molti dei servizi {{site.data.keyword.Bluemix_notm}} pubblici.</li>
	<li>Convalida la configurazione di rete e del firewall e
l'accesso ed endpoint LDAP.</li>
	</ol>
</li>
</ol>

##Manutenzione dell'istanza dedicata
{: #maintaindedicated}

IBM effettua la manutenzione e l'installazione di aggiornamenti e correzioni ogni qualvolta lo ritenga appropriato per la piattaforma, i runtime e i servizi di {{site.data.keyword.Bluemix_notm}} dedicato.

**Importante**: IBM si riserva il diritto di interrompere i servizi per applicare la manutenzione di emergenza a seconda delle necessità. IBM potrebbe modificare le ore di manutenzione pianificate, ma verrai avvisato di tali modifiche nonché di tutte le informazioni relative alla manutenzione di emergenza.

Per
{{site.data.keyword.Bluemix_notm}} dedicato sono richiesti i seguenti tipi di manutenzione:
<dl>
<dt>**Finestre di manutenzione standard**</dt>
<dd>I servizi utilizzano delle finestre di manutenzione standard predefinite, che potrebbero causare la non disponibilità del servizi. IBM non richiede l'approvazione dei clienti per eseguire la manutenzione, ma prova a ridurre al minimo l'impatto sui tuoi servizi.<br />
<br />
IBM invia messaggi broadcast relativi alle modifiche pianificate per ciascuna finestra di manutenzione tramite email, telefono o altri metodi.<br />
<br />
**Importante**: alcuni servizi potrebbero non essere disponibili durante il periodo di manutenzione.</dd>

<dt>**Finestra di modifica mensile**</dt>
<dd>La finestra di manutenzione mensile viene applicata in base al coordinamento tra te e IBM entro una finestra di 21 giorni. Puoi fornire a IBM date od orari specifici entro la finestra di 21 giorni che potrebbero non andare bene per te. IBM prova a pianificare gli aggiornamenti tenendo conto di tali indicazioni temporali. In base alle richieste, IBM ti comunica la finestra di manutenzione pianificata. Non si prevede che le finestre di modifica mensili abbiano un impatto sull'ambiente Bluemix dedicato in esecuzione.<br />
<br />
**Nota:** se non richiedi una data/ora specifica per l'aggiornamento, la manutenzione viene applicata automaticamente alla fine della finestra.<br />
<br />
Vai a **AMMINISTRAZIONE > INFORMAZIONI DI SISTEMA** per visualizzare gli aggiornamenti in sospeso, impostare le date non disponibili e approvare gli aggiornamenti. Per ulteriori informazioni sulle notifiche e sulla pianificazione degli aggiornamenti in sospeso, vedi <a href="../admin/index.html#oc_system">Visualizzazione delle informazioni sul sistema</a>.</dd>
	
<dt>**Altro**</dt>
<dd>IBM intende limitare gli interventi di manutenzione che potrebbero influire sui servizi, in particolare sulla disponibilità dell'ambiente, dei runtime e dei servizi di {{site.data.keyword.Bluemix_notm}} dedicato, agli aggiornamenti standard e mensili. In via eccezionale, potrebbero essere utilizzate altre finestre di modifica per la gestione
dell'ambiente. IBM si impegnerà a ridurre al minimo l'impatto sul tuo lavoro durante tali finestre di modifica e ti avviserà anticipatamente.</dd>
</dl>

Per configurare la manutenzione della tua istanza dedicata, collabora con il rappresentante designato IBM per identificare una finestra concordata per la manutenzione standard.

##Ripristino dell'istanza dedicata
{: #restorededicated}

Il backup delle impostazioni e configurazioni di {{site.data.keyword.Bluemix_notm}} dedicato viene eseguito periodicamente in caso di interruzioni non pianificate nell'ambiente.

Come parte del backup dei dati, IBM completa le seguenti attività:

<ul>
<li>Crittografa tutte le copie di backup e gestisce le chiavi di crittografia</li>
<li>Monitora e gestisce l'attività di backup</li>
<li>Fornisce i file di backup crittografati</li>
<li>Ripristina i dati richiesti</li>
<li>Gestisce i conflitti di pianificazione tra le operazioni di gestione dei backup e delle correzioni</li>
</ul>

Poiché la protezione dei dati privati è di importanza critica, IBM ha bisogno della tua collaborazione quando si occupa della gestione dei file di backup in modo che i file non vengano spostati all'esterno dei tuoi data center. Nello specifico, IBM richiede che tu completi le seguenti attività:

<ul>
<li>Spostare una copia dei tuoi dati di backup crittografati fuori sede, proprio come faresti per qualsiasi altro dato di backup da te gestito.</li>
<li>Fornire i file di backup per l'operatore IBM nel caso occorra eseguire un ripristino.</li>
</ul>

# rellinks
## general 
* [Scopri: {{site.data.keyword.Bluemix_notm}} dedicato](http://www.ibm.com/cloud-computing/bluemix/hybrid/dedicated/)
