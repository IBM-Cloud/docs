---

 

copyright:

  years: 2015, 2016

 

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# {{site.data.keyword.Bluemix_notm}} Admin CLI
{: #bluemixadmincli}

*Ultimo aggiornamento: 3 marzo 2016*

Puoi gestire gli utenti per il tuo ambiente
{{site.data.keyword.Bluemix_notm}} locale o {{site.data.keyword.Bluemix_notm}} dedicato
utilizzando l'interfaccia riga di comando Cloud Foundry insieme al plug-in
{{site.data.keyword.Bluemix_notm}} Admin CLI. Ad
esempio, puoi aggiungere utenti da un registro LDAP. Se stai cercando informazioni sulla gestione del tuo account {{site.data.keyword.Bluemix_notm}} pubblico, vedi [Amministrazione](../../../admin/adminpublic.html#administer).

Prima di iniziare, installa l'interfaccia riga di comando cf. Il plug-in {{site.data.keyword.Bluemix_notm}} Admin
CLI richiede cf versione 6.11.2 o successive. [Scarica
l'interfaccia riga di comando Cloud Foundry](https://github.com/cloudfoundry/cli/releases){: new_window}

**Limitazione:** l'interfaccia riga di comando Cloud Foundry non
è supportata da Cygwin. Utilizza l'interfaccia riga di comando Cloud Foundry
in una finestra riga di comando diversa da quella di Cygwin.

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
<dd class="pd">Dominio secondario dell'URL per la tua istanza {{site.data.keyword.Bluemix_notm}}.</dd>
</dl>
</li>
<li>Per installare il plug-in {{site.data.keyword.Bluemix_notm}} Admin CLI, esegui questo comando:<br/><br/>
<code>
cf install-plugin bluemix-admin-cli -r BluemixAdmin
</code>
</li>
</ol>

## Utilizzo del plug-in {{site.data.keyword.Bluemix_notm}} Admin
CLI

Puoi utilizzare il plug-in {{site.data.keyword.Bluemix_notm}} Admin CLI per aggiungere o rimuovere utenti, assegnare o annullare l'assegnazione degli utenti dalle organizzazioni ed
effettuare altre attività di gestione. Per visualizzare un elenco di comandi, immetti il seguente
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

Puoi aggiungere un utente al tuo ambiente {{site.data.keyword.Bluemix_notm}} da un registro LDAP. Immetti il seguente comando:

```
cf ba add-user <nome_utente> <organizzazione>
```
{: codeblock}

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

Puoi cercare un utente. Immetti il seguente comando:

```
cf ba search-users <nome_utente>
```
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">&lt;nome_utente&gt;</dt>
<dd class="pd">Il nome dell'utente in {{site.data.keyword.Bluemix_notm}}.</dd>

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
<dd class="pd">Imposta le autorizzazioni per l'utente: Ammin, Accesso, Catalogo (accesso in lettura o scrittura), Report (accesso in lettura o scrittura) o Utenti (accesso in lettura o scrittura).</dd>
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
<dd class="pd">Vedi [Ruoli](../../../admin/adminpublic.html#orgsandspaces) per i ruoli utente di {{site.data.keyword.Bluemix_notm}} e le relative
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
<dd class="pd">Vedi [Ruoli](../../../admin/adminpublic.html#orgsandspaces) per i ruoli utente di {{site.data.keyword.Bluemix_notm}} e le relative
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

### Aggiunta, eliminazione e recupero dei report

Puoi aggiungere, eliminare e richiamare report di sicurezza.
* Per aggiungere un report, immetti il seguente comando:

```
cf ba add-report <categoria> <date> <PDF|TXT|LOG> <RTF>
```
{: codeblock}

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
<dd class="pd">Il nome o GUID del servizio che vuoi abilitare. Se immetti un nome servizio non univoco,
ti verrà richiesto di scegliere tra dei piani di servizio.</dd>
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
<dd class="pd">Il nome o GUID del servizio che vuoi disabilitare. Se immetti un nome servizio non univoco,
ti verrà richiesto di scegliere tra dei piani di servizio.</dd>
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
<dd class="pd">Il nome o GUID del servizio per il quale vuoi aggiungere la visibilità. Se immetti un nome servizio non univoco,
ti verrà richiesto di scegliere tra dei piani di servizio.</dd>
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
<dd class="pd">Il nome o GUID del servizio per il quale vuoi rimuovere la visibilità. Se immetti un nome servizio non univoco,
ti verrà richiesto di scegliere tra dei piani di servizio.</dd>
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
<dd class="pd">Il nome o GUID del servizio che desideri rendere visibile. Se immetti un nome servizio non univoco,
ti verrà richiesto di scegliere tra dei piani di servizio.</dd>
<dt class="pt dlterm">&lt;organizzazione&gt;</dt>
<dd class="pd">Il nome o il GUID dell'organizzazione {{site.data.keyword.Bluemix_notm}} per cui aggiungere la visibilità. Puoi abilitare la visibilità del servizio per più di una singola organizzazione immettendo i GUID o i nomi organizzazione aggiuntivi nel comando.</dd>
</dl>

**Suggerimento:** puoi anche utilizzare **ba espv** come alias per il più lungo
nome comando **ba edit-service-plan-visibility**.

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

`cf ba update-service-broker <nome_broker> <nome_utente> <password> <url_broker>`
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
