{:new_window: target="_blank"} 
{:shortdesc: .shortdesc}

#{{site.data.keyword.Bluemix_notm}} dedicato
{: #dedicated}

*Ultimo aggiornamento: 20 ottobre 2015*

{{site.data.keyword.Bluemix}} è
una piattaforma basata su cloud open standard per la creazione, esecuzione e
gestione delle applicazioni. Con {{site.data.keyword.Bluemix_notm}} dedicato, ottieni la potenza unita alla semplicità di {{site.data.keyword.Bluemix_notm}} nel tuo ambiente SoftLayer dedicato, che è connesso in modo protetto sia a {{site.data.keyword.Bluemix_notm}} pubblico sia alla tua rete.
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} dedicato
include un catalogo privato che consente di visualizzare i servizi dedicati
disponibili in esclusiva per te. Sono compresi inoltre dei servizi aggiuntivi
che vengono diffusi e messi a disposizione da {{site.data.keyword.Bluemix_notm}} pubblico.

{{site.data.keyword.Bluemix_notm}} dedicato è costruito su SoftLayer, così da permetterti di usufruire della struttura cloud dalle prestazioni più elevate. Ciascun data center fornisce rigorosi controlli di sicurezza 24 ore al giorno, 7
giorni a settimana. Tu e IBM accedete alla tua istanza di {{site.data.keyword.Bluemix_notm}} dedicato tramite un tunnel VPN e una VLAN privata.

![{{site.data.keyword.Bluemix_notm}} dedicato](images/detaileddedicated.png "{{site.data.keyword.Bluemix_notm}} dedicato")

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
| Facoltativo | {{site.data.keyword.sqldb}} | IBM {{site.data.keyword.sqldbfull}} Database for {{site.data.keyword.Bluemix_notm}} aggiunge alla tua applicazione un database relazione con provisioning completo. {{site.data.keyword.sqldb}} fornisce un database gestito per occuparsi degli impegnativi carichi di lavoro transazionali e web della tua attività di business. |
| Facoltativo | {{site.data.keyword.mql}} | IBM {{site.data.keyword.mqlfull}} for {{site.data.keyword.Bluemix_notm}} è un servizio di messaggistica basato sul cloud che fornisce una messaggistica flessibile e facile da usare per le applicazioni {{site.data.keyword.Bluemix_notm}}. {{site.data.keyword.mql}} fornisce una soluzione con ridotte esigenze gestionali alla messaggistica. Puoi utilizzare {{site.data.keyword.mql}} per rendere le tue applicazioni più reattive e scalabili e puoi condividere e scaricare lavoro tra le applicazioni con una semplice e potente API. |
| Facoltativo | {{site.data.keyword.dashdbshort}} | Usa dashDB per memorizzare dati relazionali, inclusi i tipi speciali quali i dati geospaziali. Quindi, analizza tali dati utilizzando l'analisi integrata SQL o avanzata come l'analisi predittiva e il data mining, l'analisi con R e l'analisi geospaziale. |

*Tabella 1. Servizi dedicati*

##Configurazione dell'istanza di {{site.data.keyword.Bluemix_notm}} dedicato
{: #setupdedicated}

{{site.data.keyword.Bluemix_notm}} dedicato
è progettato per fornire una versione privata dell'offerta {{site.data.keyword.Bluemix_notm}}
pubblico. Puoi utilizzare i servizi e i runtime {{site.data.keyword.Bluemix_notm}} per supportare le tue esigenze di elaborazione in un account SoftLayer su host IBM. 

IBM ti fornisce l'accesso a {{site.data.keyword.Bluemix_notm}} dedicato utilizzando un accesso protetto da password. Puoi accedere a servizi, runtime
e risorse associate nonché distribuire e rimuovere applicazioni {{site.data.keyword.Bluemix_notm}}. IBM si avvale di più sedi SoftLayer per la distribuzione di {{site.data.keyword.Bluemix_notm}} dedicato, il che ti permette di ottenere la tua versione privata in una sede a te vicina.

Per configurare la tua versione privata di {{site.data.keyword.Bluemix_notm}}:

<ol>
<li>Contatta il tuo rappresentante dell'account designato IBM oppure <a href="https://console.ng.bluemix.net/?direct=classic/#/contactUs/cloudOEPaneId=contactUs" target="_blank">{{site.data.keyword.Bluemix_notm}}</a> per iniziare.</li>
<li>La quota mensile ricorrente si basa sui servizi dedicati
che desideri utilizzare, oltre a una sottoscrizione a tutti i servizi pubblici
{{site.data.keyword.Bluemix_notm}}. Riceverai quindi una fattura per tutto ciò che scegli di utilizzare
al di fuori di tale accordo di sottoscrizione.
	<ol type="a">
	<li>Determina insieme a IBM la quota per la tua istanza di {{site.data.keyword.Bluemix_notm}} dedicato.
	La quota mensile ricorrente si basa sui servizi dedicati
che desideri utilizzare, oltre a una sottoscrizione a tutti i servizi pubblici
{{site.data.keyword.Bluemix_notm}}. Riceverai quindi una fattura per tutto ciò che scegli di utilizzare
al di fuori di tale accordo di sottoscrizione.</li>
	<li>Identifica le scadenze per ogni fase di configurazione
della tua istanza di {{site.data.keyword.Bluemix_notm}}
dedicato.</li>
	</ol>
	</li>
<li>Seleziona la <a href="http://www.softlayer.com/data-centers" target="_blank">sede data center SoftLayer</a> la tua istanza dedicata. Verranno creati, quindi, la piattaforma dedicata e
l'account. Per l'account, devi identificare le persone all'interno della tua organizzazione
a cui assegnare i ruoli necessari per rendere operativa la tua istanza
dedicata. Per ciascun ruolo, esiste un rappresentante IBM corrispondente.<br />
<p>Ruoli cliente:</p>
<dl>
<dt>**Procurement focal**</dt>
<dd>Lavora con il rappresentante IBM per organizzare il tuo ambiente {{site.data.keyword.Bluemix_notm}} dedicato, occupandosi inoltre dell'identificazione delle persone adeguate a gestire ogni aspetto del progetto all'interno della tua organizzazione. Questo ruolo controlla la selezione del modello, gli accordi commerciali e la disposizione dell'accesso alle risorse dei clienti. Il Procurement focal rappresenta il contatto generale per la configurazione dell'istanza dedicata.</dd>
<dt>**Compliance officer**</dt>
<dd>Lavora con il rappresentante IBM per selezionare un'opzione di topologia e distribuzione che risponda ai tuoi requisiti di sicurezza. Questo ruolo collabora con il Compliance consultant di IBM per determinare quali modelli di distribuzione raggiungono gli obiettivi di conformità.</dd>
<dt>**Network Specialist**</dt>
<dd>Lavora con il rappresentante IBM per identificare i piani di rete per la distribuzione di {{site.data.keyword.Bluemix_notm}}. Questo ruolo fornisce i requisiti al rappresentante IBM e collabora a un piano di implementazione. Al termine della fase di installazione e verifica, questo ruolo dovrà confermare che la configurazione di rete è in conformità con gli standard aziendali.</dd>
<dt>**DevOps focal**</dt>
<dd>Lavora con il rappresentante IBM per pianificare e applicare gli aggiornamenti di manutenzione necessari per la piattaforma, i servizi e i runtime {{site.data.keyword.Bluemix_notm}}. Inoltre, questo ruolo collabora con il rappresentante IBM alla configurazione della tua istanza di {{site.data.keyword.Bluemix_notm}} dedicato.</dd>
</dl>
<p>Ruoli IBM:</p>
<dl>
<dt>**IBM provisioning manager**</dt>
<dd>Lavora con il Customer procurement focal per organizzare l'ambiente del cliente.</dd>
<dt>**IBM compliance consultant**</dt>
<dd>Lavora con il Customer compliance officer per selezionare un'opzione di topologia e distribuzione che risponda ai tuoi requisiti di sicurezza.</dd>
<dt>**IBM network specialist**</dt>
<dd>Lavora con il Customer network specialist per identificare i piani di rete per la distribuzione. Questo ruolo collabora con il cliente per raccogliere disposizioni e creare un piano di implementazione. Effettua inoltre dei test automatizzati per verificare il risultato fisico del piano di implementazione.</dd>	
<dt>**IBM DevOps focal**</dt>
<dd>Lavora con il Customer DevOps focal sull'installazione e manutenzione continua della topologia di distribuzione. Questo ruolo collabora con il cliente per pianificare ed effettuare aggiornamenti necessari per la piattaforma e i servizi.</dd>
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
<dd>I servizi utilizzano finestre di manutenzione standard predefinite che potrebbero comportare la mancata disponibilità dei servizi. IBM non richiede l'approvazione del cliente per effettuare la manutenzione, ma tenta di minimizzare l'impatto sui tuoi servizi.<br />
<br />
IBM invia messaggi broadcast relativi alle modifiche pianificate per ciascuna finestra di manutenzione tramite e-mail, telefono o altri metodi.<br />
<br />
**Importante**: alcuni servizi potrebbero non essere disponibili durante il periodo di manutenzione.</dd>

<dt>**Finestra di modifica mensile**</dt>
<dd>La finestra di manutenzione mensile si applica in base al coordinamento tra te e IBM all'interno di una finestra di 21 giorni. Puoi fornire a IBM specifiche date o ore nella finestra di 21 giorni che potrebbero non andar bene per te. IBM tenta di pianificare gli aggiornamenti lontano da quei periodi. In base alle richieste, IBM ti comunica la finestra di manutenzione pianificata. Le finestre di modifica mensile non dovrebbero influire sull'ambiente Bluemix dedicato in esecuzione.<br />
<br />
**Nota:** se non richiedi un periodo specifico per l'aggiornamento, la manutenzione viene applicata automaticamente allo scadere della finestra.<br />
<br />
Passa a **AMMINISTRAZIONE > INFORMAZIONI DI SISTEMA** per visualizzare gli aggiornamenti in sospeso, impostare le date non disponibili e approvare gli aggiornamenti. Per ulteriori informazioni sulle notifiche e sulla pianificazione degli aggiornamenti in sospeso, vedi <a href="../admin/index.html#oc_system">Visualizzazione delle informazioni di sistema</a>.</dd>
	
<dt>**Altro**</dt>
<dd>IBM intende limitare gli interventi di manutenzione che potrebbero influire sui servizi, in particolare sulla disponibilità dell'ambiente, dei runtime e dei servizi di {{site.data.keyword.Bluemix_notm}} dedicato, ad aggiornamenti standard e mensili. In via eccezionale, potrebbero essere utilizzate altre finestre di modifica per la gestione
dell'ambiente. IBM si impegnerà a ridurre al minimo l'impatto sul tuo lavoro durante tali finestre di modifica e ti avviserà anticipatamente. </dd>
</dl>

Per configurare la manutenzione della tua istanza dedicata, collabora con il rappresentante designato IBM per identificare una finestra concordata per la manutenzione standard.
