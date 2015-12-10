{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

#{{site.data.keyword.Bluemix_notm}} locale
{: #local}
*Ultimo aggiornamento: 13 novembre 2015*

{{site.data.keyword.Bluemix}} locale porta la potenza e l'agilità della piattaforma {{site.data.keyword.Bluemix_notm}} basata sul cloud al tuo centro dati. Con {{site.data.keyword.Bluemix_notm}} locale, puoi proteggere i tuoi carichi di lavoro più sensibili dietro il tuo firewall aziendale, continuando al tempo stesso a essere connesso in modo protetto e sincronizzato con {{site.data.keyword.Bluemix_notm}} pubblico.
{:shortdesc}

IBM® utilizza le operazioni cloud come un servizio per monitorare e gestire il tuo ambiente, consentendoti così di concentrarti sulla creazione di applicazioni e servizi che vengono eseguiti sull'ambiente. IBM gestisce anche gli aggiornamenti della piattaforma, in modo da consentirti di concentrarti sull'attività di business.

{{site.data.keyword.Bluemix_notm}} locale include un catalogo diffuso privato che visualizza i servizi locali disponibili in esclusiva per te. Sono compresi inoltre dei servizi aggiuntivi
che vengono diffusi e messi a disposizione da {{site.data.keyword.Bluemix_notm}} pubblico.

{{site.data.keyword.Bluemix_notm}} locale si trova su una macchina virtuale che è dietro il tuo firewall aziendale; in questo modo, l'infrastruttura cloud a tua disposizione offre le prestazioni più elevate e ha la massima protezione. IBM installa, esegue il monitoraggio in remoto e gestisce {{site.data.keyword.Bluemix_notm}} locale nel tuo centro dati tramite la tecnologia relay di IBM.

Relay è una funzionalità di consegna inclusa in {{site.data.keyword.Bluemix_notm}} locale che consente a IBM di offrire aggiornamenti in modo automatico e congruente a tutte le distribuzioni locali, in modo che tu abbia sempre un sistema aggiornato, stabile e sicuro. Relay ottiene la connettività protetta tramite un tunnel VP SSL in uscita e aperto che ha origine dalla macchina virtuale di inizio utilizzando i certificati specifici per ciascuna istanza di {{site.data.keyword.Bluemix_notm}} locale. Il traffico su questo tunnel è
l'automazione Urban Code Deployer per gestire la piattaforma, le risorse di elaborazione e i servizi per la tua istanza.

![Panoramica di {{site.data.keyword.Bluemix_notm}} locale](images/bluemixlocalarchitecture.png "Panoramica di Bluemix locale")

*Figura 1. Panoramica dettagliata di {{site.data.keyword.Bluemix_notm}} locale*

Gli ambienti {{site.data.keyword.Bluemix_notm}} locale hanno gli stessi standard di sicurezza di {{site.data.keyword.Bluemix_notm}} pubblico in termini di sicurezza operativa. Fornisci l'hardware e l'infrastruttura, che ti offre il controllo su infrastruttura e sicurezza fisica. L'accesso degli sviluppatori a {{site.data.keyword.Bluemix_notm}} locale è controllato dalle tue politiche LDAP, che possono essere configurate dal team {{site.data.keyword.Bluemix_notm}} quando configura il tuo ambiente. All'interno dell'ambiente locale, utilizzando la Console di gestione, puoi gestire i ruoli e le autorizzazioni degli utenti.

{{site.data.keyword.Bluemix_notm}} locale viene fornito con tutti i runtime {{site.data.keyword.Bluemix_notm}} inclusi e 64 GB di memoria di elaborazione.

Inoltre, per {{site.data.keyword.Bluemix_notm}} locale è disponibile una serie di servizi.

| **Tipo** | **Nome** | **Descrizione** |    
|----------|----------|-----------------|
|Incluso | Runtime {{site.data.keyword.Bluemix_notm}} | Utilizza i runtime per rendere rapidamente operativa la tua applicazione, senza dover configurare e gestire macchine virtuali e sistemi operativi. Tutti i runtime {{site.data.keyword.Bluemix_notm}} sono a tua disposizione per utilizzarli nella tua istanza di {{site.data.keyword.Bluemix_notm}} locale.|
|Incluso | {{site.data.keyword.autoscaling}}| Ti permette di aumentare o ridurre dinamicamente la capacità
di elaborazione della tua applicazione in base alle politiche. Con questo servizio, hai un uso illimitato nel tuo ambiente {{site.data.keyword.Bluemix}} locale.|
|Facoltativo |{{site.data.keyword.datacshort}}| Questo servizio fornisce una griglia di dati in memoria
che supporta scenari di cache distribuita per le tue applicazioni. Include 50 GB di cache in memoria. |
|Facoltativo | {{site.data.keyword.APIM}} | Utilizza il servizio {{site.data.keyword.APIMfull}}
per comporre, gestire e socializzare le API. Puoi importare delle API con risorse utilizzando un URL proxy o assemblando dati dalle origini dati HTTP. Il servizio {{site.data.keyword.APIM}} offre il vantaggio che puoi gestire la modalità di utilizzo delle tue API. |

*Tabella 1. Servizi locali*

##Configurazione dell'istanza di {{site.data.keyword.Bluemix_notm}} locale
{: #setuplocal}

{{site.data.keyword.Bluemix_notm}} locale è progettato per fornire una versione privata dell'offerta {{site.data.keyword.Bluemix_notm}} pubblico che è ospitata sul tuo hardware e da te gestita. Puoi utilizzare i servizi e i runtime {{site.data.keyword.Bluemix_notm}} per supportare le tue esigenze di elaborazione in un ambiente cloud protetto, ospitato e gestito dal cliente.

IBM ti fornisce l'accesso a {{site.data.keyword.Bluemix_notm}} locale utilizzando un accesso protetto da password. Puoi accedere a servizi, runtime
e risorse associate nonché distribuire e rimuovere applicazioni {{site.data.keyword.Bluemix_notm}}. Riesamina i seguenti passi per lavorare con il tuo
rappresentante IBM per configurare la tua istanza locale di {{site.data.keyword.Bluemix_notm}}.

Per configurare la tua versione privata di {{site.data.keyword.Bluemix_notm}}:

<ol>
<li>Riesamina i <a href="index.html#localinfra">Requisiti dell'infrastruttura {{site.data.keyword.Bluemix_notm}} locale</a> per configurare la tua istanza locale.</li>
<li>Contatta il tuo rappresentante dell'account designato IBM oppure contattare <a href="https://console.ng.bluemix.net/?direct=classic/#/contactUs/cloudOEPaneId=contactUs" target="_blank">{{site.data.keyword.Bluemix_notm}}</a> per iniziare.</li>
<li>Stabilisci un accordo per {{site.data.keyword.Bluemix_notm}} locale con IBM che includa le date cardine per la distribuzione.
<ol type="a">
	<li>Determina insieme a IBM la quota per la tua istanza di {{site.data.keyword.Bluemix_notm}} locale. La quota mensile ricorrente si basa sui servizi locali
che desideri utilizzare, oltre a una sottoscrizione a tutti i servizi pubblici {{site.data.keyword.Bluemix_notm}}. Riceverai quindi una fattura per tutto ciò che scegli di utilizzare
al di fuori di tale accordo di sottoscrizione.</li>
	<li>Identifica le scadenze per ogni fase di configurazione della tua istanza di {{site.data.keyword.Bluemix_notm}} locale.</li>
	</ol>
	</li>
<li>Dopo la creazione della tua piattaforma e del tuo account, identifichi le persone all'interno della tua organizzazione per i ruoli necessari per rendere operativa la tua istanza locale.<br />
<br />
<dl>
<dt>**Procurement focal**</dt>
<dd>Lavora con i rappresentanti IBM per organizzare il tuo ambiente {{site.data.keyword.Bluemix_notm}} locale,
includendo l'identificazione delle persone adeguate a gestire ogni aspetto del progetto all'interno della tua organizzazione. Questo ruolo supervisiona la selezione di pattern, le intese commerciali e l'organizzazione dell'accesso alle risorse cliente. Il Procurement focal è il contatto generale per la configurazione dell'istanza locale.</dd>
<dt>**Responsabile della conformità**</dt>
<dd>Lavora con i rappresentanti IBM per selezionare un'opzione di topologia e distribuzione che risponda ai tuoi requisiti di sicurezza. Questo ruolo lavora con i consulenti di conformità IBM per determinare quali pattern di distribuzione raggiungono le finalità e gli obiettivi di conformità.</dd>
<dt>**Specialista di rete**</dt>
<dd>Lavora con i rappresentanti IBM sui piani di rete per la distribuzione {{site.data.keyword.Bluemix_notm}}. Questo ruolo fornisce i requisiti ai rappresentanti IBM e lavora con i rappresentanti su un piano di implementazione. Alla fine della fase di installazione e verifica, questo ruolo "approverà" che la configurazione di rete è conforme agli standard aziendali.</dd>
<dt>**DevOps focal**</dt>
<dd>Lavora con i rappresentanti IBM per pianificare e applicare gli aggiornamenti di manutenzione necessari per i runtime, i servizi e la piattaforma {{site.data.keyword.Bluemix_notm}}. Questo ruolo lavora anche con i rappresentanti IBM sulla configurazione della tua istanza di {{site.data.keyword.Bluemix_notm}} locale.</dd>
</dl>
</li>
<li>Tu fornisci l'hardware e IBM ti aiuta a definire e stabilire la connettività di rete tra la tua rete aziendale e la tua istanza di {{site.data.keyword.Bluemix_notm}} locale. Per ulteriori informazioni sui requisiti dell'infrastruttura, vedi <a href="index.html#localinfra">Requisiti dell'infrastruttura {{site.data.keyword.Bluemix_notm}} locale</a>.
<ol type="a">
	<li>IBM configura l'accesso alla rete e il LDAP in base alle informazioni che hai fornito. L'accesso amministrativo
viene fornito ai contatti da te designati. Devi designare un
contatto anche per il supporto e la fatturazione.</li>
	<li>IBM configura un catalogo diffuso su diversi canali nell'ambiente locale per visualizzare i tuoi servizi locali e molti dei servizi {{site.data.keyword.Bluemix_notm}} pubblici.</li>
	<li>Convalida la configurazione di rete e del firewall e
l'accesso ed endpoint LDAP.</li>
	</ol>
</li>
</ol>
	
##Requisiti dell'infrastruttura {{site.data.keyword.Bluemix_notm}} locale
{: #localinfra}

Per {{site.data.keyword.Bluemix_notm}} locale, la sicurezza fisica e l'infrastruttura per ospitare l'istanza locale sono di tua competenza. IBM imposta i seguenti requisiti per configurare {{site.data.keyword.Bluemix_notm}} locale.
###Hardware
Anche se ci sono dei requisiti per il tipo e la dimensione di hardware disponibile, puoi scegliere qualsiasi combinazione per soddisfare i requisiti totali di risorse.
<dl>
<dt>**Hardware VMware ESXi**</dt>
<dd>
ESXi è un livello di virtualizzazione che viene eseguito sui server fisici e che astrae processore, memoria, archiviazione e risorse in più macchine virtuali. Scegli qualsiasi combinazione che soddisfi i seguenti totali di risorse, a condizione che il conteggio di core fisici minimo per ESXi sia otto. Le seguenti specifiche sono relative solo al runtime core di {{site.data.keyword.Bluemix_notm}}.
<ul>
<li>48 core fisici a 2.0 o più GHz ciascuno</li>
<li>756 GB di RAM fisica</li>
</li>Dimensione archivio dati totale di 7,5 TB
<ul>
<li>Archivio dati di 7 TB per contenere {{site.data.keyword.Bluemix_notm}}</li>
<li>Archivio dati di 500 GB per contenere la macchina virtuale di inizio</li>
</ul>
</ul>
<p><strong>Nota:</strong> se utilizzi più archivi dati, utilizza lo stesso prefisso per ognuno.</p>
</dd>
<dt>**Alta disponibilità**</dt>
<dd>
Per supportare il malfunzionamento di un singolo nodo, devi disporre di n+1 ESXi. Ad esempio, se vengono utilizzati due ESXi, il che significa 16x core ciascuno, ne occorre un terzo.
<p><strong>Nota:</strong> l'amministratore VMware del cliente può decidere di implementare un rigido failover dell'alta disponibilità nel cluster per garantire le risorse.</p>
</dd>
<dt>**Rete**</dt>
<dd>
I requisiti consigliati includono un gruppo di porte accessibili al cliente con 10 indirizzi IP di rete del cliente che hanno un accesso a Internet in uscita. Definisci quindi una seconda VLAN privata solo tra gli ESXi utilizzati per {{site.data.keyword.Bluemix_notm}} locale. Questa VLAN viene visualizzata come un gruppo di porte in VMware. {{site.data.keyword.Bluemix_notm}} locale la utilizza per la sottorete privata, che è più sicura e può aiutare a evitare problemi di instradamento.
</dd>
</dl>

###Configurazione del server vCenter
Riesamina i seguenti requisiti di versione, datacenter, pool di risorse e archivio dati.
<dl>
<dt>**Versioni VMware supportate**</dt>
<dd>vCenter e ESXi 5.1 e 5.5</dd>
<dt>**Tipi VMware supportati**</dt>
<dd>vSphere Enterprise<br />
vSphere Enterprise Plus, se intendi utilizzare gli switch virtuali distribuiti</dd>
<dt>**Datacenter**</dt>
<dd>Crea un datacenter, se non ne esiste uno.</dd>
<dt>**Cartella Datacenter**</dt>
<dd>Crea una cartella di macchina virtuale con lo stesso nome del cluster, se non intendi concedere l'accesso come amministratore propagato dal datacenter.</dd>
<dt>**Cluster**</dt>
<dd>Crea un cluster specificamente per l'utilizzo da parte di {{site.data.keyword.Bluemix_notm}} locale. Un esempio per il nome cluster è `bluemix`.</dd>
<dt>**Pool di risorse**</dt>
<dd>Crea un pool di risorse nel cluster {{site.data.keyword.Bluemix_notm}} locale. Un esempio per il nome di pool di risorse è `local`.</dd>
</dt>**Archivi dati**</dt>
<dd>Richiede 7,5 TB per la distribuzione iniziale di {{site.data.keyword.Bluemix_notm}}.<br />
<br />
**Nota**: quando utilizzi più di un archivio dati, assicurarti che ciascuno inizi con lo stesso prefisso. Degli esempi di più nomi di archivio dati con lo stesso prefisso sono `bluemix_datastore_01` e `bluemix_datastore_02`.</dd>
</dl>

###Larghezza di banda di rete
La velocità effettiva consigliata è 5 Mbps in upload e 5 Mbps in download, e puoi prevedere un utilizzo di dati mensile di 10 GB. IBM stabilisce delle finestre concordate di consegna di grossi bundle di file che possono avere una dimensione che arriva a 3 GB.
###Autorizzazioni VMware
Imposta i ruoli e le autorizzazioni di seguito indicati. La propagazione è impostata per ciascuna autorizzazione. Se l'autorizzazione viene propagata, viene passata verso il basso nella gerarchia degli oggetti. Tuttavia, le autorizzazioni per un oggetto secondario sovrascrivono sempre le autorizzazioni propagate da un oggetto principale.
<dl>
<dt>**v Center Server**</dt>
<dd>Imposta il ruolo come di sola lettura e non propagato.<br />
<br />
**Nota**: questo ruolo è necessario per richiamare lo stato attività per specifiche operazioni di disco.</dd>
<dt>**Datacenter**</dt>
<dd>Crea il ruolo "{{site.data.keyword.Bluemix_notm}}" e concedi le autorizzazioni per **Datastore**, includendo **Low level file operations** (operazioni file di basso livello) e **Update virtual machine files** (aggiorna file della macchina virtuale).<br />
<br />
**Nota**: questo ruolo è necessario per supportare gli inserimenti di file negli archivi dati.</dd>
<dt>**Cluster**</dt>
<dd>Imposta il ruolo come amministratore e propagato.</dd>
<dt>**Archivi dati**</dt>
<dd>Imposta il ruolo come amministratore e propagato per ciascun archivio dati {{site.data.keyword.Bluemix_notm}}.</dd>
<dt>**Rete**</dt>
<dd>Imposta i gruppi di porte pubblici e privati, con il ruolo amministratore, non propagato.</dd>
</dl>

###Pool DEA (Droplet Execution Agent)
Ciascun DEA è configurato con:
- 16 - 32 GB di RAM
- 2x - 4x vCPU
- 150 - 300 GB di archiviazione

Ad esempio, se la dimensione dell'host ESXi è 256 GB di memoria con 16x core, vengono aggiunti otto DEA. Se la dimensione dell'host ESXi è 64 GB di memoria con 8x core, è richiesta l'aggiunta di due ESXi e quattro DEA. Sono richiesti 1,5 TB di archiviazione aggiuntivi per ogni quattro DEA. Questo esempio è basato su un DEA configurato con 32 GB di RAM, 4x vCPU e 300 GB di archiviazione.

##Manutenzione dell'istanza locale
{: #maintainlocal}

IBM effettua la manutenzione e l'installazione di aggiornamenti e correzioni ogni qualvolta lo ritenga appropriato per la piattaforma, i runtime e i servizi di Bluemix locale. I servizi potrebbero non essere disponibili durante le finestre di manutenzione.

**Importante**: IBM si riserva il diritto di interrompere i servizi per applicare la manutenzione di emergenza a seconda delle necessità. IBM potrebbe modificare le ore di manutenzione pianificate, ma verrai avvisato di tali modifiche nonché di tutte le informazioni relative alla manutenzione di emergenza.

Per {{site.data.keyword.Bluemix_notm}} locale sono richiesti i seguenti tipi di manutenzione:
<dl>
<dt>**Finestre di manutenzione standard**</dt>
<dd>I servizi utilizzano delle finestre di manutenzione standard predefinite, che potrebbero causare la non disponibilità del servizi. IBM non richiede l'approvazione dei clienti per eseguire la manutenzione, ma prova a ridurre al minimo l'impatto sui tuoi servizi.<br />
<br />
IBM invia messaggi broadcast relativi alle modifiche pianificate per ciascuna finestra di manutenzione tramite email, telefono o altri metodi.<br />
<br />
**Importante**: alcuni servizi potrebbero non essere disponibili durante il periodo di manutenzione.</dd>

<dt>**Finestra di modifica mensile**</dt>
<dd>La finestra di manutenzione mensile viene applicata in base al coordinamento tra te e IBM entro una finestra di 21 giorni. Puoi fornire a IBM date od orari specifici entro la finestra di 21 giorni che potrebbero non andare bene per te. IBM prova a pianificare gli aggiornamenti tenendo conto di tali indicazioni temporali. In base alle richieste, IBM ti comunica la finestra di manutenzione pianificata. Non si prevede che le finestre di modifica mensili abbiano un impatto sull'ambiente Bluemix locale in esecuzione.<br />
<br />
**Nota**: se non richiedi una data/ora specifica per l'aggiornamento, la manutenzione viene applicata automaticamente alla fine della finestra.<br />
<br />
Vai a **AMMINISTRAZIONE > INFORMAZIONI DI SISTEMA** per visualizzare gli aggiornamenti in sospeso, impostare le date non disponibili e approvare gli aggiornamenti. Per ulteriori informazioni sulle notifiche e sulla pianificazione degli aggiornamenti in sospeso, vedi <a href="../admin/index.html#oc_system">Visualizzazione delle informazioni sul sistema</a>.</dd>

<dt>**Altro**</dt>
<dd>IBM intende limitare gli interventi di manutenzione che potrebbero influire sui servizi, in particolare sulla disponibilità dell'ambiente, dei runtime e dei servizi di Bluemix locale, alle finestre standard e mensili.
In via eccezionale, potrebbero essere utilizzate altre finestre di modifica per la gestione
dell'ambiente. IBM si impegna a ridurre al minimo l'impatto sul tuo lavoro durante tali finestre di modifica e ti avvisa anticipatamente.</dd>
</dl>

Per configurare la manutenzione della tua istanza locale, collabora con il rappresentante designato IBM per identificare una finestra concordata per la manutenzione standard.

##Ripristino della tua istanza locale
{: #restorelocal}

Il backup delle impostazioni e configurazioni di {{site.data.keyword.Bluemix_notm}} locale viene eseguito periodicamente in caso di interruzioni non pianificate nell'ambiente.

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
* [Scopri: {{site.data.keyword.Bluemix_notm}} locale](http://www.ibm.com/cloud-computing/bluemix/hybrid/local/)
