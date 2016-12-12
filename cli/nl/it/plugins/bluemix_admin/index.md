---



copyright:

  anni: 2015, 2016

lastupdated: "2016-11-08"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# {{site.data.keyword.Bluemix_notm}} Admin CLI
{: #bluemixadmincli}


Puoi gestire gli utenti per il tuo ambiente
{{site.data.keyword.Bluemix_notm}} locale o {{site.data.keyword.Bluemix_notm}} dedicato
utilizzando l'interfaccia riga di comando Cloud Foundry insieme al plug-in
{{site.data.keyword.Bluemix_notm}} Admin CLI. Ad
esempio, puoi aggiungere utenti da un registro LDAP. Se stai cercando informazioni sulla gestione del tuo account {{site.data.keyword.Bluemix_notm}} pubblico, vedi [Amministrazione](/docs/admin/adminpublic.html#administer).

Prima di iniziare, installa l'interfaccia riga di comando cf. Il plug-in {{site.data.keyword.Bluemix_notm}} Admin
CLI richiede cf versione 6.11.2 o successive. [Scarica
l'interfaccia riga di comando Cloud Foundry](https://github.com/cloudfoundry/cli/releases){: new_window}

**Limitazione:** l'interfaccia riga di comando Cloud Foundry non
è supportata da Cygwin. Utilizza l'interfaccia riga di comando Cloud Foundry
in una finestra riga di comando diversa da quella di Cygwin.

**Nota**: {{site.data.keyword.Bluemix_notm}} Admin CLI è utilizzato solo per gli ambienti {{site.data.keyword.Bluemix_notm}} locale e {{site.data.keyword.Bluemix_notm}} dedicato. Non è supportato in {{site.data.keyword.Bluemix_notm}} pubblico.

## Aggiunta del plug-in {{site.data.keyword.Bluemix_notm}} Admin
CLI

Dopo aver installato l'interfaccia riga di comandi cf, puoi
aggiungere il plug-in {{site.data.keyword.Bluemix_notm}} Admin
CLI.

**Nota**: se avevi già installato il plug-in Gestione {{site.data.keyword.Bluemix_notm}}, per ottenere gli ultimi aggiornamenti potresti doverlo disinstallare, eliminare il repository e reinstallare il plug-in.

Completa la seguente procedura per aggiungere il repository e installare il plug-in:

<ol>
<li>Per aggiungere il repository del plug-in {{site.data.keyword.Bluemix_notm}} Admin, esegui questo comando:<br/><br/>
<code>
cf add-plugin-repo BluemixAdmin https://console.&lt;dominiosecondario&gt;.bluemix.net/cli
</code><br/><br/>
<dl class="parml">
<dt class="pt dlterm">&lt;dominiosecondario&gt;</dt>
<dd class="pd">Dominio secondario dell'URL per la tua istanza {{site.data.keyword.Bluemix_notm}}. Ad esempio, <code>https://console.mycompany.bluemix.net/cli</code></dd>
</dl>
</li>
<li>Per installare il plug-in {{site.data.keyword.Bluemix_notm}} Admin CLI, immetti il seguente comando: <br/><br/>
<code>
cf install-plugin BluemixAdminCLI -r BluemixAdmin
</code>
</li>
</ol>

Se devi disinstallare il plug-in, puoi utilizzare i seguenti comandi e quindi aggiungere il repository aggiornato e installare l'ultimo plug-in:

* Disinstalla il plug-in: `cf uninstall-plugin BluemixAdminCLI`
* Rimuovi il repository di plug-in: `cf remove-plugin-repo BluemixAdmin`


## Utilizzo del plug-in {{site.data.keyword.Bluemix_notm}} Admin
CLI

Puoi utilizzare il plug-in {{site.data.keyword.Bluemix_notm}} Admin CLI per aggiungere o rimuovere utenti, assegnare o annullare l'assegnazione degli utenti dalle organizzazioni ed
effettuare altre attività di gestione.

Per visualizzare un elenco di comandi, immetti il seguente
comando:

```
cf plugins
```
{: codeblock}

Per ulteriore assistenza per un comando, utilizza l'opzione `-help`.

### Connessione e accesso a {{site.data.keyword.Bluemix_notm}}

Prima di poter utilizzare il plug-in Admin CLI per la gestione degli utenti,
devi connetterti ed effettuare l'accesso.

<ol>
<li>Per stabilire una connessione all'endpoint API {{site.data.keyword.Bluemix_notm}}, esegui il seguente comando:<br/><br/>
<code>
cf ba api https://console.&lt;subdomain&gt;.bluemix.net
</code>
<dl class="parml">
<dt class="pt dlterm">&lt;dominiosecondario&gt;</dt>
<dd class="pd">Dominio secondario dell'URL per la tua istanza {{site.data.keyword.Bluemix_notm}}.<br />
</dd>
</dl>
<p>Puoi controllare l'URL corretto nella pagina Risorse e informazioni della Console di gestione. L'URL viene mostrato
nella sezione Informazioni API all'interno del campo **URL API**.</p>
</li>
<li>Accedi a {{site.data.keyword.Bluemix_notm}} con il seguente comando:<br/><br/>
<code>
cf login
</code>
</li>
</ol>

### Aggiunta di un utente

Puoi aggiungere un utente al tuo
ambiente {{site.data.keyword.Bluemix_notm}} dal
registro utenti dell'ambiente. Immetti il seguente comando:

```
cf ba add-user <nome_utente> <organizzazione>
```
{: codeblock}

**Nota**: per aggiungere un utente a un'organizzazione specifica, devi essere un **Ammin** con autorizzazione **users.write** (o **Superuser**). Se sei un gestore organizzazione, ti può essere data la possibilità di aggiungere utenti alla tua organizzazione da un Superuser che esegue il comando **enable-managers-add-users**.  Vedi [Abilitazione dei gestori all'aggiunta di utenti](index.html#clius_emau) per ulteriori informazioni.

<dl class="parml">
<dt class="pt dlterm">&lt;nome_utente&gt;</dt>
<dd class="pd">Il nome dell'utente nel registro LDAP.</dd>
<dt class="pt dlterm">&lt;organizzazione&gt;</dt>
<dd class="pd">Il nome o GUID dell'organizzazione {{site.data.keyword.Bluemix_notm}} a cui aggiungere l'utente.</dd>
</dl>

**Suggerimento: ** puoi anche utilizzare **ba au** come alias per
il più lungo nome comando **ba add-user**.

<!-- staging-only commands start. Live for interconnect -->

### Ricerca un utente

Puoi cercare un utente. Immetti il seguente comando insieme ai parametri di filtro di ricerca facoltativi (nome, autorizzazione, organizzazione e ruolo) in base alle esigenze:

```
cf ba search-users -name=<valore_nome_utente> -permission=<valore_autorizzazione> -organization=<valore_organizzazione> -role=<valore_ruolo>
```
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">&lt;valore_nome_utente&gt;</dt>
<dd class="pd">Il nome dell'utente in {{site.data.keyword.Bluemix_notm}}. </dd>
<dt class="pt dlterm">&lt;valore_autorizzazione&gt;</dt>
<dd class="pd">L'autorizzazione assegnata all'utente. Ad esempio, superuser, di base, catalogo, utente e report. Per ulteriori informazioni sulle autorizzazioni da assegnare all'utente, vedi [Autorizzazioni](/docs/admin/index.html#permissions). Non puoi utilizzare questo parametro insieme al parametro organizzazione nella stessa query. </dd>
<dt class="pt dlterm">&lt;valore_organizzazione&gt;</dt>
<dd class="pd">Il nome dell'organizzazione a cui appartiene l'utente. Non puoi utilizzare questo parametro insieme al parametro organizzazione nella stessa query.</dd>
<dt class="pt dlterm">&lt;valore_ruolo&gt;</dt>
<dd class="pd">Il ruolo dell'organizzazione assegnato all'utente. Ad esempio, gestore, gestore fatturazione o revisore dell'organizzazione. Con questo parametro devi specificare l'organizzazione. Per ulteriori informazioni sui ruoli, vedi [Ruoli utente](/docs/admin/users_roles.html#userrolesinfo).</dd>

</dl>

**Suggerimento: ** puoi anche utilizzare **ba su** come alias per
il più lungo nome comando **ba search-users**.

### Impostazione di autorizzazioni per un utente

Puoi impostare autorizzazioni per un utente specificato. Immetti il seguente comando:

```
cf ba set-permissions <nome_utente> <autorizzazione> <accesso>
```
{: codeblock}

**Nota**: puoi impostare una sola autorizzazione alla volta.

<dl class="parml">
<dt class="pt dlterm">&lt;nome_utente&gt;</dt>
<dd class="pd">Il nome dell'utente in {{site.data.keyword.Bluemix_notm}}.</dd>
<dt class="pt dlterm">&lt;autorizzazione&gt;</dt>
<dd class="pd">Imposta le autorizzazioni per l'utente: Ammin (in alternativa Superuser), Accesso (in alternativa Di base), Catalogo (accesso in lettura o scrittura), Report (accesso in lettura o scrittura) o Utenti (accesso in lettura o scrittura).</dd>
<dt class="pt dlterm">&lt;accesso&gt;</dt>
<dd class="pd">Per le autorizzazioni Catalogo, Report e Utenti, devi inoltre impostare il livello di accesso su <code>lettura</code> o <code>scrittura</code>.</dd>
</dl>

**Suggerimento: ** puoi anche utilizzare **ba sp** come alias per
il più lungo nome comando **ba set-permissions**.

<!-- staging-only commands end -->

### Rimozione di un utente

Puoi rimuovere un utente dal tuo ambiente {{site.data.keyword.Bluemix_notm}}
immettendo il seguente comando:

```
cf ba remove-user <nome_utente>
```
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">&lt;nome_utente&gt;</dt>
<dd class="pd">Il nome dell'utente in {{site.data.keyword.Bluemix_notm}}.</dd>

</dl>

**Suggerimento: ** puoi anche utilizzare **ba ru** come alias per
il più lungo nome comando **ba remove-user**.

### Abilitazione dei gestori all'aggiunta di utenti
{: #clius_emau}

Se disponi dell'autorizzazione **Superuser** nel tuo ambiente {{site.data.keyword.Bluemix_notm}}, puoi abilitare i gestori organizzazione ad aggiungere utenti alle organizzazioni che essi gestiscono. Immetti il seguente comando:

```
cf ba enable-managers-add-users
```
{: codeblock}

**Suggerimento:** puoi anche utilizzare **ba emau** come alias per il più lungo
nome comando **ba enable-managers-add-users**.

### Disabilitazione dei gestori all'aggiunta di utenti
{: #clius_dmau}

Se i gestori organizzazione sono stati abilitati ad aggiungere utenti alle organizzazioni che essi gestiscono nel tuo ambiente {{site.data.keyword.Bluemix_notm}} con il comando **enable-managers-add-users** e disponi dell'autorizzazione **Superuser**, puoi rimuovere questa impostazione.  Immetti il seguente comando:

```
cf ba disable-managers-add-users
```
{: codeblock}

**Suggerimento:** puoi anche utilizzare **ba dmau** come alias per il più lungo
nome comando **ba disable-managers-add-users**.

### Aggiunta ed eliminazione di un'organizzazione

Puoi aggiungere ed eliminare un'organizzazione.

* Per aggiungere un'organizzazione, immetti il seguente comando:

```
cf ba create-organization <organizzazione> <gestore>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organizzazione&gt;</dt>
<dd class="pd">Il nome o il GUID dell'organizzazione {{site.data.keyword.Bluemix_notm}} da aggiungere.</dd>
<dt class="pt dlterm">&lt;gestore&gt;</dt>
<dd class="pd">Il nome utente del gestore per l'organizzazione.</dd>
</dl>

**Suggerimento: ** puoi anche utilizzare **ba co** come alias per
il più lungo nome comando **ba create-organization**.

* Per eliminare un'organizzazione, immetti il seguente comando:

```
cf ba delete-organization <organizzazione>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organizzazione&gt;</dt>
<dd class="pd">Il nome o il GUID dell'organizzazione {{site.data.keyword.Bluemix_notm}} da eliminare.</dd>
</dl>

**Suggerimento: ** puoi anche utilizzare **ba do** come alias per
il più lungo nome comando **ba delete-organization**.

### Assegnazione di un utente a un'organizzazione

Puoi assegnare un utente nel tuo ambiente {{site.data.keyword.Bluemix_notm}} a una
specifica organizzazione. Immetti il seguente comando:

```
cf ba set-org <nome_utente> <organizzazione> [<ruolo>]
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;nome_utente&gt;</dt>
<dd class="pd">Il nome dell'utente in {{site.data.keyword.Bluemix_notm}}.</dd>
<dt class="pt dlterm">&lt;organizzazione&gt;</dt>
<dd class="pd">Il nome o GUID dell'organizzazione {{site.data.keyword.Bluemix_notm}} a cui assegnare l'utente.</dd>
<dt class="pt dlterm">&lt;ruolo&gt;</dt>
<dd class="pd">Vedi [Ruoli](/docs/admin/users_roles.html) per i ruoli utente di {{site.data.keyword.Bluemix_notm}} e le relative
descrizioni.</dd>
</dl>

**Suggerimento: ** puoi anche utilizzare **ba so** come alias per
il più lungo nome comando **ba set-org**.

### Annullamento dell'assegnazione di un utente da un'organizzazione

Puoi annullare l'assegnazione di un utente del tuo ambiente {{site.data.keyword.Bluemix_notm}}
da una specifica organizzazione. Immetti il seguente comando:

```
cf ba unset-org <nome_utente> <organizzazione> [<ruolo>]
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;nome_utente&gt;</dt>
<dd class="pd">Il nome dell'utente in {{site.data.keyword.Bluemix_notm}}.</dd>
<dt class="pt dlterm">&lt;organizzazione&gt;</dt>
<dd class="pd">Il nome o GUID dell'organizzazione {{site.data.keyword.Bluemix_notm}} a cui assegnare l'utente.</dd>
<dt class="pt dlterm">&lt;ruolo&gt;</dt>
<dd class="pd">Vedi [Ruoli](/docs/admin/users_roles.html) per i ruoli utente di {{site.data.keyword.Bluemix_notm}} e le relative
descrizioni.</dd>
</dl>

**Suggerimento: ** puoi anche utilizzare **ba uo** come alias per
il più lungo nome comando **ba unset-org**.

### Ruoli

<dl class="parml">
<dt class="pt dlterm">OrgManager</dt>
<dd class="pd">Gestore organizzazione. Un gestore organizzazione ha l'autorità per svolgere le seguenti azioni:
<ul>
<li>Creare o eliminare spazi all'interno dell'organizzazione.</li>
<li>Invitare gli utenti all'organizzazione e gestirli.</li>
<li>Gestire i domini dell'organizzazione.</li>
</ul>
</dd>
<dt class="pt dlterm">BillingManager</dt>
<dd class="pd">Gestore fatturazione. Un gestore fatturazione può visualizzare le informazioni relative all'utilizzo di runtime e servizi
per l'organizzazione.</dd>
<dt class="pt dlterm">OrgAuditor</dt>
<dd class="pd">Revisore organizzazione. Un revisore organizzazione può visualizzare i contenuti di applicazioni e servizi in uno
spazio.</dd>
</dl>

### Impostazione di una quota per un'organizzazione

Puoi impostare la quota di utilizzo per una specifica organizzazione.

```
cf ba set-quota <organizzazione> <piano>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organizzazione&gt;</dt>
<dd class="pd">Il nome o il GUID dell'organizzazione {{site.data.keyword.Bluemix_notm}} per cui impostare la quota.</dd>
<dt class="pt dlterm">&lt;piano&gt;</dt>
<dd class="pd">Il piano di quota per un'organizzazione.</dd>
</dl>

**Suggerimento: ** puoi anche utilizzare **ba sq** come alias per
il più lungo nome comando **ba set-quota**.


### Ricerca e impostazione delle quote del contenitore per un'organizzazione.
{: #containquotas}

Puoi trovare e impostare le quote per i contenitore in un'organizzazione.

Per trovare la quota per i contenitori in un'organizzazione, immetti il seguente comando:

```
cf bluemix-admin containers-quota <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organizzazione&gt;</dt>
<dd class="pd">Il nome o l'ID dell'organizzazione in Bluemix. Questo parametro è obbligatorio.</dd>
</dl>

**Suggerimento:** puoi anche utilizzare **ba cq** come alias per il più lungo
nome comando **bluemix-admin containers-quota**.

Per impostare la quota per i contenitori in un'organizzazione, immetti il seguente comando con inclusa almeno una delle opzioni:

```
cf bluemix-admin set-containers-quota <organization> <options>
```
{: codeblock}

**Nota**: puoi includere più opzioni, ma ne devi includere almeno una.

<dl class="parml">
<dt class="pt dlterm">&lt;organizzazione&gt;</dt>
<dd class="pd">Il nome o l'ID dell'organizzaizone in Bluemix. Questo parametro è obbligatorio.</dd>
<dt class="pt dlterm">&lt;opzioni&gt;</dt>
<dd class="pd">Includi una o più delle seguenti opzioni in cui il valore deve essere un numero intero:
<ul>
<li>floating-ips-max &lt;value&gt;</li>
<li>floating-ips-space-default &lt;value&gt;</li>
<li>memory-max &lt;value&gt;</li>
<li>memory-space-default &lt;value&gt;</li>
<li>image-limit &lt;value&gt;</li>
</ul>
</dd>
</dl>

**Suggerimento:** puoi anche utilizzare i seguenti nomi brevi come un alias per i nomi delle opzioni più
lunghi: 
<dl class="parml">
<dt class="pt dlterm">floating-ips-max &lt;value&gt;</dt>
<dd class="pd"><strong>fim</strong></dd>
<dt class="pt dlterm">floating-ips-space-default &lt;value&gt;</dt>
<dd class="pd"><strong>fisd</strong></dd>
<dt class="pt dlterm">memory-max &lt;value&gt;</dt>
<dd class="pd"><strong>mm</strong></dd>
<dt class="pt dlterm">memory-space-default &lt;value&gt;</dt>
<dd class="pd"><strong>msd</strong></dd>
<dt class="pt dlterm">image-limit &lt;value&gt;</dt>
<dd class="pd"><strong>il</strong></dd>
</dl>

Facoltativamente, puoi fornire un file che contiene i parametri di configurazione specifici in un oggetto JSON valido. Se utilizzi l'opzione **-file**, ha la precedenza e le altre opzioni vengono ignorate. Per fornire un file invece di impostare le opzioni, immetti il seguente comando:

```
cf bluemix-admin set-containers-quota <organization> <-file path_to_JSON_file>
```
{: codeblock}

Il file JSON deve avere il formato mostrato nel seguente esempio:

```
{
  "floating_ips_max": 10,
  "floating_ips_space_default": 0,
  "ram_max": 4096,
  "ram_space_default": 0,
  "image_limit": 10
}  
```
{: codeblock}

**Suggerimento:** puoi anche utilizzare **ba scq** come alias per il più lungo
nome comando **bluemix-admin set-containers-quota**.

### Aggiunta, eliminazione e recupero dei report

Puoi aggiungere, eliminare e richiamare report di sicurezza.
* Per aggiungere un report, immetti il seguente comando:

```
cf ba add-report <category> <date> <PDF|TXT|LOG> <RTF>
```
{: codeblock}

**Nota**: se hai accesso in scrittura per l'autorizzazione dei report, puoi creare una nuova categoria e aggiungere un report in uno qualsiasi dei formati accettati per i tuoi utenti. Immetti il nome della nuova categoria per il parametro `categoria` o aggiungi il nuovo report a una categoria esistente.

<dl class="parml">
<dt class="pt dlterm">&lt;categoria&gt;</dt>
<dd class="pd">La categoria per il report. Se nel nome è presente uno spazio, racchiudi il nome
tra virgolette.</dd>
<dt class="pt dlterm">&lt;data&gt;</dt>
<dd class="pd">La data del report nel formato <samp class="ph codeph">AAAAMMGG</samp>.</dd>
<dt class="pt dlterm">&lt;PDF|TXT|LOG&gt;</dt>
<dd class="pd">Il percorso del PDF, file di testo o file di log del report da caricare.</dd>
<dt class="pt dlterm">&lt;RTF&gt;</dt>
<dd class="pd">Un'opzione per includere una versione RTF (Rich Text Format) del PDF. Questa opzione si applica solo se
hai incluso il percorso del PDF del report. La versione RTF è utilizzata per l'indicizzazione e la ricerca.</dd>
</dl>

**Suggerimento: ** puoi anche utilizzare **ba ar** come alias per
il più lungo nome comando **ba add-report**.

* Per eliminare un report, immetti il seguente comando:

```
cf ba delete-report <categoria> <data> <nome>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;categoria&gt;</dt>
<dd class="pd">La categoria per il report. Se nel nome è presente uno spazio, racchiudi il nome
tra virgolette.</dd>
<dt class="pt dlterm">&lt;data&gt;</dt>
<dd class="pd">La data del report nel formato <samp class="ph codeph">AAAAMMGG</samp>.</dd>
<dt class="pt dlterm">&lt;nome&gt;</dt>
<dd class="pd">Il nome del report.</dd>
</dl>

**Suggerimento: ** puoi anche utilizzare **ba dr** come alias per
il più lungo nome comando **ba delete-report**.

* Per recuperare un report, immetti il seguente comando:

```
cf ba retrieve-report <categoria> <data> <nome>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;categoria&gt;</dt>
<dd class="pd">La categoria per il report. Se nel nome è presente uno spazio, racchiudi il nome
tra virgolette.</dd>
<dt class="pt dlterm">&lt;data&gt;</dt>
<dd class="pd">La data del report nel formato <samp class="ph codeph">AAAAMMGG</samp>.</dd>
<dt class="pt dlterm">&lt;nome&gt;</dt>
<dd class="pd">Il nome del report.</dd>
</dl>

**Suggerimento: ** puoi anche utilizzare **ba rr** come alias per il più lungo nome comando **ba retrieve-report**.

### Abilitazione e disabilitazione dei servizi per tutte le organizzazioni

Puoi abilitare o disabilitare la visualizzazione di un servizio nel Catalogo {{site.data.keyword.Bluemix_notm}} per tutte le organizzazioni.

* Per abilitare la visibilità di un servizio nel Catalogo {{site.data.keyword.Bluemix_notm}} per tutte le organizzazioni, immetti il seguente comando:

```
cf ba enable-service-plan <identificativo_piano>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;identificativo_piano&gt;</dt>
<dd class="pd">Il nome o il GUID del piano di servizio che desideri abilitare. Se immetti un nome del piano di servizio non univoco, ad esempio "Standard" o "Di base," ti verrà richiesto di scegliere tra dei piani di servizio. Per identificare il nome di un piano di servizio, seleziona la categoria di servizio dalla homepage, quindi fai clic su **Aggiungi** per visualizzarne i servizi. Fai clic sul nome del servizio per aprire la vista Dettagli, da cui puoi visualizzare i nomi dei piani di servizi disponibili per il servizio. </dd>
</dl>

**Suggerimento:** puoi anche utilizzare **ba esp** come alias per il più lungo
nome comando **ba enable-service-plan**.

* Per disabilitare la visualizzazione di un servizio nel Catalogo {{site.data.keyword.Bluemix_notm}} per tutte le organizzazioni, immetti questo comando:

```
cf ba disable-service-plan <identificativo_piano>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;identificativo_piano&gt;</dt>
<dd class="pd">Il nome o il GUID del piano di servizio che desideri abilitare. Se immetti un nome del piano di servizio non univoco, ad esempio "Standard" o "Di base," ti verrà richiesto di scegliere tra dei piani di servizio. Per identificare il nome di un piano di servizio, seleziona la categoria di servizio dalla homepage, quindi fai clic su **Aggiungi** per visualizzarne i servizi. Fai clic sul nome del servizio per aprire la vista Dettagli, da cui puoi visualizzare i nomi dei piani di servizi disponibili per il servizio.</dd>
</dl>

**Suggerimento: ** puoi anche utilizzare **ba dsp** come alias per il più
lungo nome comando **ba disable-service-plan**.

### Aggiunta, rimozione e modifica della visibilità dei servizi per le organizzazioni

Puoi aggiungere o rimuovere un'organizzazione dall'elenco di organizzazioni che possono vedere uno specifico servizio nel Catalogo {{site.data.keyword.Bluemix_notm}}. Puoi anche modificare e sostituire l'elenco di servizi che specifiche organizzazioni possono vedere nel Catalogo {{site.data.keyword.Bluemix_notm}}.

* Per consentire a un'organizzazione di visualizzare uno specifico servizio nel Catalogo {{site.data.keyword.Bluemix_notm}}, immetti questo comando:

```
cf ba add-service-plan-visibility <identificativo_piano> <organizzazione>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;identificativo_piano&gt;</dt>
<dd class="pd">Il nome o il GUID del piano di servizio che desideri abilitare. Se immetti un nome del piano di servizio non univoco, ad esempio "Standard" o "Di base," ti verrà richiesto di scegliere tra dei piani di servizio. Per identificare il nome di un piano di servizio, seleziona la categoria di servizio dalla homepage, quindi fai clic su **Aggiungi** per visualizzarne i servizi. Fai clic sul nome del servizio per aprire la vista Dettagli, da cui puoi visualizzare i nomi dei piani di servizi disponibili per il servizio.</dd>
<dt class="pt dlterm">&lt;organizzazione&gt;</dt>
<dd class="pd">Il nome o il GUID dell'organizzazione {{site.data.keyword.Bluemix_notm}} da aggiungere all'elenco di visibilità del servizio.</dd>
</dl>

**Suggerimento:** puoi anche utilizzare **ba aspv** come alias per il più lungo
nome comando **ba add-service-plan-visibility**.

* Per rimuovere la visibilità di un servizio nel Catalogo {{site.data.keyword.Bluemix_notm}} per
un'organizzazione, immetti il seguente comando:

```
cf ba remove-service-plan-visibility <identificativo_piano> <organizzazione>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;identificativo_piano&gt;</dt>
<dd class="pd">Il nome o il GUID del piano di servizio che desideri abilitare. Se immetti un nome del piano di servizio non univoco, ad esempio "Standard" o "Di base," ti verrà richiesto di scegliere tra dei piani di servizio. Per identificare il nome di un piano di servizio, seleziona la categoria di servizio dalla homepage, quindi fai clic su **Aggiungi** per visualizzarne i servizi. Fai clic sul nome del servizio per aprire la vista Dettagli, da cui puoi visualizzare i nomi dei piani di servizi disponibili per il servizio.</dd>
<dt class="pt dlterm">&lt;organizzazione&gt;</dt>
<dd class="pd">Il nome o il GUID dell'organizzazione {{site.data.keyword.Bluemix_notm}} da rimuovere dall'elenco di visibilità del servizio.</dd>
</dl>

**Suggerimento: ** puoi anche utilizzare **ba rspv** come alias per il più
lungo nome comando **ba remove-service-plan-visibility**.

* Per sostituire tutti i servizi visibili esistenti per un'organizzazione o più organizzazioni, utilizza questo comando.

```
cf ba edit-service-plan-visibilities <identificativo_piano> <organizzazione_1> <organizzazione_facoltativa_2>
```
{: codeblock}

**Nota:** questo comando sostituisce i servizi visibili esistenti per le organizzazioni specificate con il servizio da te specificato nel comando.

<dl class="parml">
<dt class="pt dlterm">&lt;identificativo_piano&gt;</dt>
<dd class="pd">Il nome o il GUID del piano di servizio che desideri abilitare. Se immetti un nome del piano di servizio non univoco, ad esempio "Standard" o "Di base," ti verrà richiesto di scegliere tra dei piani di servizio. Per identificare il nome di un piano di servizio, seleziona la categoria di servizio dalla homepage, quindi fai clic su **Aggiungi** per visualizzarne i servizi. Fai clic sul nome del servizio per aprire la vista Dettagli, da cui puoi visualizzare i nomi dei piani di servizi disponibili per il servizio.</dd>
<dt class="pt dlterm">&lt;organizzazione&gt;</dt>
<dd class="pd">Il nome o il GUID dell'organizzazione {{site.data.keyword.Bluemix_notm}} per cui aggiungere la visibilità. Puoi abilitare la visibilità del servizio per più di una singola organizzazione immettendo i GUID o i nomi organizzazione aggiuntivi nel comando.</dd>
</dl>

**Suggerimento:** puoi anche utilizzare **ba espv** come alias per il più lungo
nome comando **ba edit-service-plan-visibility**.

### Visualizzazione delle informazioni sulle metriche della risorsa 
{: #cliresourceusage}

Puoi visualizzare le informazioni sulle metriche della risorsa, tra cui l'utilizzo di memoria, disco e CPU.  Oltre all'utilizzo di tali risorse, puoi vedere un riepilogo delle risorse fisiche e riservate disponibili. Inoltre, puoi vedere i dati di utilizzo dei DEA (Droplet Execution Agent) e i dati cronologici per l'utilizzo di memoria e disco. Per impostazione predefinita, i dati cronologici per l'utilizzo di memoria e disco vengono visualizzati settimanalmente e in ordine decrescente. Per visualizzare le informazioni sulle metriche della risorsa, utilizza il seguente comando: 

```
cf ba resource-metrics <monthly> <weekly>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;mensile&gt;</dt>
<dd class="pd">Visualizzare i dati cronologici per la memoria e lo spazio su disco un mese alla volta.</dd>
<dt class="pt dlterm">&lt;settimanale&gt;</dt>
<dd class="pd">Visualizzare i dati cronologici per la memoria e lo spazio su disco una settimana alla volta. Questo è il valore predefinito.</dd>
</dl>

**Suggerimento:** puoi anche utilizzare **ba rsm** come alias per il più lungo
nome comando **ba resource-metrics**.

### Utilizzo dei broker dei servizi

Utilizza i seguenti comandi per elencare tutti i broker dei servizi, aggiungere o eliminare un broker dei servizi o aggiornare un broker di servizi.

* Puoi elencare i broker dei servizi
immettendo il seguente comando:

```
cf ba service-brokers <nome_broker>
```
{: codeblock}

**Nota**: per elencare tutti i broker dei servizi, immetti il comando omettendo il parametro `nome_broker`.

<dl class="parml">
<dt class="pt dlterm">&lt;nome_broker&gt;</dt>
<dd class="pd">Facoltativo: nome del broker dei servizi personalizzato. Utilizza questo parametro per ottenere informazioni per un broker dei servizi specifico.</dd>
</dl>

**Suggerimento: ** puoi anche utilizzare **ba sb** come alias per il più
lungo nome comando **ba service-brokers**.

* Puoi aggiungere un broker dei servizi, in modo da poter aggiungere un servizio personalizzato al tuo catalogo
{{site.data.keyword.Bluemix_notm}}
immettendo il seguente comando:

```
cf ba add-service-broker <nome_broker> <nome_utente> <password> <url_broker>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;nome_broker&gt;</dt>
<dd class="pd">Nome del broker dei servizi personalizzato.</dd>
<dt class="pt dlterm">&lt;nome_utente&gt;</dt>
<dd class="pd">Nome utente per l'account con accesso al broker dei servizi.</dd>
<dt class="pt dlterm">&lt;password&gt;</dt>
<dd class="pd">Password per l'account con accesso al broker dei servizi.</dd>
<dt class="pt dlterm">&lt;url_broker&gt;</dt>
<dd class="pd">URL per il broker dei servizi.</dd>
</dl>

**Suggerimento:** puoi anche utilizzare **ba asb** come alias per il più lungo
nome comando **ba add-service-broker**.

* Puoi eliminare un broker dei servizi per rimuovere il servizio personalizzato dal tuo catalogo
{{site.data.keyword.Bluemix_notm}},
immettendo il seguente comando:

```
cf ba delete-service-broker <broker_servizi>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;broker_servizi&gt;</dt>
<dd class="pd">Nome o GUID del broker dei servizi personalizzato.</dd>
</dl>

**Suggerimento: ** puoi anche utilizzare **ba dsb** come alias per il più
lungo nome comando **ba delete-service-broker**.

* Puoi aggiornare un broker dei servizi
immettendo il seguente comando:

```
cf ba update-service-broker <broker_name> <user_name> <password> <broker_url>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;nome_broker&gt;</dt>
<dd class="pd">Nome del broker dei servizi personalizzato.</dd>
<dt class="pt dlterm">&lt;nome_utente&gt;</dt>
<dd class="pd">Nome utente per l'account con accesso al broker dei servizi.</dd>
<dt class="pt dlterm">&lt;password&gt;</dt>
<dd class="pd">Password per l'account con accesso al broker dei servizi.</dd>
<dt class="pt dlterm">&lt;url_broker&gt;</dt>
<dd class="pd">URL per il broker dei servizi.</dd>
</dl>

**Suggerimento:** puoi anche utilizzare **ba usb** come alias per il più lungo
nome comando **ba update-service-broker**.


### Gestione dei gruppi di sicurezza dell'applicazione

Per gestire i gruppi di sicurezza dell'applicazione (ASG), devi essere un amministratore con accesso completo all'ambiente locale o dedicato. Tutti gli utenti dell'ambiente possono elencare gli ASG disponibili per l'organizzazione a cui si fa riferimento con il comando. Tuttavia, per creare, aggiornare o associare gli ASG, devi essere l'amministratore dell'ambiente {{site.data.keyword.Bluemix_notm}}.

I gruppi ASG funzionano come firewall virtuali che controllano il traffico dall'applicazione presente nel tuo ambiente {{site.data.keyword.Bluemix_notm}}. Ogni ASG è costituito da un elenco di regole che consentono un traffico specifico e la comunicazione da e verso la rete esterna. Puoi associare uno o più ASG a una specifica serie di gruppi di sicurezza, ad esempio a una serie di gruppi utilizzata per applicare l'accesso globale, oppure associarli agli spazi all'interno di un'organizzazione nel tuo ambiente {{site.data.keyword.Bluemix_notm}}.

{{site.data.keyword.Bluemix_notm}} è inizialmente impostato con limitazioni a tutti gli accessi alla rete esterna. Due gruppi di sicurezza creati da IBM, `public_networks` e `dns`, abilitano l'accesso globale alla rete esterna quando esegui il bind di tali gruppi alla serie di gruppi di sicurezza Cloud Foundry predefinita. Le due serie di gruppi di sicurezza in Cloud Foundry utilizzate per applicare l'accesso globale sono **Preparazione predefinita** ed **Esecuzione predefinita**. Queste serie di gruppi applicano le regole per consentire il traffico a tutte le applicazioni in esecuzione o a tutte le applicazioni in fase di preparazione. Se non vuoi eseguire il bind a queste due serie di gruppi di sicurezza, puoi annullare il bind alle serie di gruppi Cloud Foundry e quindi associare il gruppo a uno specifico spazio. Per ulteriori informazioni, vedi [Binding Application Security Groups](https://docs.cloudfoundry.org/adminguide/app-sec-groups.html#binding-groups){: new_window}.

**Nota**: i seguenti comandi che consentono di gestire i gruppi di sicurezza, si basano su Cloud Foundry versione 1.6.

#### Elenco, creazione, aggiornamento ed eliminazione dei gruppi di sicurezza

Per ulteriori informazioni sulla creazione di gruppi di sicurezza e sulle regole che definiscono il traffico in uscita, vedi [Creating Application Security Groups](https://docs.cloudfoundry.org/adminguide/app-sec-groups.html#creating-groups){: new_window}.

* Puoi elencare tutti i gruppi di sicurezza
immettendo il seguente comando:

```
cf ba security-groups
```
{: codeblock}

**Suggerimento:** puoi anche utilizzare **ba sgs** come alias per il più lungo nome comando
**ba security-groups**.

* Puoi visualizzare i dettagli di uno specifico gruppo di sicurezza
immettendo il seguente comando:

```
cf ba security-groups <gruppo-di-sicurezza>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Gruppo di sicurezza&gt;</dt>
<dd class="pd">Nome del gruppo di sicurezza</dd>
</dl>

**Suggerimento:** puoi anche utilizzare **ba sg** come alias per il più lungo nome comando
**ba security-groups** con il parametro `security-group`.


* Puoi creare un gruppo di sicurezza
immettendo il seguente comando. Al nome di ciascun gruppo di sicurezza creato, viene aggiunto il prefisso `adminconsole_` per distinguerlo dai gruppi di sicurezza creati da IBM.

```
cf ba create-security-group <gruppo-di-sicurezza> <percorso-del-file-di-regole>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Gruppo di sicurezza&gt;</dt>
<dd class="pd">Nome del tuo gruppo di sicurezza</dd>
<dt class="pt dlterm">&lt;Percorso del file di regole&gt;</dt>
<dd class="pd">Percorso assoluto o relativo a un file di regole</dd>
</dl>

**Suggerimento:** puoi anche utilizzare **ba csg** come alias per il più lungo nome comando
**ba create-security-group**.

* Puoi aggiornare un gruppo di sicurezza
immettendo il seguente comando:

```
cf ba update-security-group <gruppo-di-sicurezza> <percorso-del-file-di-regole>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Gruppo di sicurezza&gt;</dt>
<dd class="pd">Nome del tuo gruppo di sicurezza</dd>
<dt class="pt dlterm">&lt;Percorso del file di regole&gt;</dt>
<dd class="pd">Percorso assoluto o relativo a un file di regole</dd>
</dl>

**Suggerimento:** puoi anche utilizzare **ba usg** come alias per il più lungo nome comando
**ba update-security-group**.

* Puoi eliminare un gruppo di sicurezza
immettendo il seguente comando:

```
cf ba delete-security-group <gruppo-di-sicurezza>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Gruppo di sicurezza&gt;</dt>
<dd class="pd">Nome del tuo gruppo di sicurezza</dd>
</dl>

**Suggerimento:** puoi anche utilizzare **ba dsg** come alias per il più lungo nome comando
**ba delete-security-group**.


#### Bind, annullamento del bind ed elenco dei gruppi di sicurezza associati

Per ulteriori informazioni su bind e annullamento del bind dei gruppi di sicurezza, vedi [Binding Application Security Groups](https://docs.cloudfoundry.org/adminguide/app-sec-groups.html#binding-groups){: new_window} e [Unbinding Application Security Groups](https://docs.cloudfoundry.org/adminguide/app-sec-groups.html#unbinding-groups){: new_window}.

* Puoi eseguire il bind alla serie di gruppi di sicurezza Preparazione predefinita
immettendo il seguente comando:

```
cf ba bind-staging-security-group <gruppo-di-sicurezza>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Gruppo di sicurezza&gt;</dt>
<dd class="pd">Nome del tuo gruppo di sicurezza</dd>
</dl>

**Suggerimento:** puoi anche utilizzare **ba bssg** come alias per il più lungo nome comando
**ba bind-staging-security-group**.

* Puoi eseguire il bind alla serie di gruppi di sicurezza Esecuzione predefinita
immettendo il seguente comando:

```
cf ba bind-running-security-group <gruppo-di-sicurezza>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Gruppo di sicurezza&gt;</dt>
<dd class="pd">Nome del tuo gruppo di sicurezza</dd>
</dl>

**Suggerimento:** puoi anche utilizzare **ba brsg** come alias per il più lungo nome comando
**ba bind-running-security-group**.

* Puoi annullare il bind alla serie di gruppi di sicurezza Preparazione predefinita
immettendo il seguente comando:

```
cf ba cf ba unbind-staging-security-group <gruppo-di-sicurezza>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Gruppo di sicurezza&gt;</dt>
<dd class="pd">Nome del tuo gruppo di sicurezza</dd>
</dl>

**Suggerimento:** puoi anche utilizzare **ba ussg** come alias per il più lungo nome comando
**ba unbind-staging-security-group**.

* Puoi annullare il bind alla serie di gruppi di sicurezza Esecuzione predefinita
immettendo il seguente comando:

```
cf ba unbind-running-security-group <gruppo-di-sicurezza>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Gruppo di sicurezza&gt;</dt>
<dd class="pd">Nome del tuo gruppo di sicurezza</dd>
</dl>

**Suggerimento:** puoi anche utilizzare **ba brsg** come alias per il più lungo nome comando
**ba bind-running-security-group**.

* Puoi eseguire il bind di un gruppo di sicurezza a uno spazio
immettendo il seguente comando:

```
cf ba bind-security-group <gruppo-di-sicurezza> <organizzazione> <spazio>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Gruppo di sicurezza&gt;</dt>
<dd class="pd">Nome del tuo gruppo di sicurezza</dd>
<dt class="pt dlterm">&lt;Organizzazione&gt;</dt>
<dd class="pd">Nome dell'organizzazione a cui eseguire il bind del gruppo di sicurezza</dd>
<dt class="pt dlterm">&lt;Spazio&gt;</dt>
<dd class="pd">Nome dello spazio all'interno dell'organizzazione a cui eseguire il bind del gruppo di sicurezza</dd>
</dl>

**Suggerimento:** puoi anche utilizzare **ba bsg** come alias per il più lungo nome comando
**ba bind-security-group**.

* Puoi annullare il bind di un gruppo di sicurezza a uno spazio
immettendo il seguente comando:

```
cf ba unbind-security-group <gruppo-di-sicurezza> <organizzazione> <spazio>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Gruppo di sicurezza&gt;</dt>
<dd class="pd">Nome del tuo gruppo di sicurezza</dd>
<dt class="pt dlterm">&lt;Organizzazione&gt;</dt>
<dd class="pd">Nome dell'organizzazione a cui eseguire il bind del gruppo di sicurezza</dd>
<dt class="pt dlterm">&lt;Spazio&gt;</dt>
<dd class="pd">Nome dello spazio all'interno dell'organizzazione a cui eseguire il bind del gruppo di sicurezza</dd>
</dl>

**Suggerimento:** puoi anche utilizzare **ba usg** come alias per il più lungo nome comando
**ba unbind-staging-security-group**.

### Gestione dei pacchetti di build
{: #buildpacks}

Se disponi di autorizzazioni di scrittura nel catalogo di applicazioni, puoi elencare, creare, aggiornare o eliminare i pacchetti di build.  
#### Elenca tutti i pacchetti di build

Utilizza il seguente comando per elencare tutti i pacchetti di build o visualizzare un pacchetto specifico:

```
cf ba buildpacks <nome_pacchettodibuild>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;nome_pacchettodibuild&gt;</dt>
<dd class="pd">Un parametro facoltativo per specificare un determinato pacchetto di build da visualizzare.</dd>
</dl>

**Suggerimento:** puoi anche utilizzare **ba lb** come alias per il più lungo
nome comando **ba buildpacks**.

#### Crea e carica un pacchetto di build

Puoi creare e caricare un pacchetto di build. Puoi caricare qualsiasi file compresso che presenta un tipo di file .zip.  Utilizza il seguente comando per caricare un pacchetto di build:

```
cf ba create-buildpack <nome_pacchettodibuild> <percorso_file> <posizione>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;nome_pacchettodibuild&gt;</dt>
<dd class="pd">Il nome del pacchetto di build da caricare.</dd>
<dt class="pt dlterm">&lt;percorso_file&gt;</dt>
<dd class="pd">Il percorso del file compresso del pacchetto di build.</dd>
<dt class="pt dlterm">&lt;posizione&gt;</dt>
<dd class="pd">L'ordine in cui vengono controllati i pacchetti di build durante il rilevamento automatico.</dd>
</dl>

**Suggerimento: ** puoi anche utilizzare **ba cb** come alias per il più lungo
nome comando **ba create-buildpack**.

#### Aggiorna un pacchetto di build

Per aggiornare un pacchetto di build esistente, utilizza il seguente comando:

```
cf ba update-buildpack <nome_pacchettodibuild> <posizione> <abilitato> <bloccato>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;nome_pacchettodibuild&gt;</dt>
<dd class="pd">Il nome del pacchetto di build da aggiornare.</dd>
<dt class="pt dlterm">&lt;posizione&gt;</dt>
<dd class="pd">L'ordine in cui vengono controllati i pacchetti di build durante il rilevamento automatico.</dd>
<dt class="pt dlterm">&lt;abilitato&gt;</dt>
<dd class="pd">Indica se il pacchetto di build è utilizzato per la fase di preparazione.</dd>
<dt class="pt dlterm">&lt;bloccato&gt;</dt>
<dd class="pd">Indica se il pacchetto di build è bloccato per impedire gli aggiornamenti.</dd>
</dl>

**Suggerimento:** puoi anche utilizzare **ba ub** come alias per il più lungo
nome comando **ba update-buildpack**.

#### Elimina un pacchetto di build

Per eliminare un pacchetto di build esistente, utilizza il seguente comando:

```
cf ba delete-buildpack <nome_pacchettodibuild>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;nome_pacchettodibuild&gt;</dt>
<dd class="pd">Il nome del pacchetto di build da eliminare.</dd>
</dl>

**Suggerimento: ** puoi anche utilizzare **ba db** come alias per il più lungo
nome comando **ba delete-buildpack**.
