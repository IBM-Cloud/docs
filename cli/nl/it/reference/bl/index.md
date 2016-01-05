# comandi bl

*Ultimo aggiornamento:* 13 novembre 2015

Se stai creando un'applicazione Node.js, puoi utilizzare Bluemix™ Live Sync per aggiornare rapidamente l'istanza dell'applicazione in esecuzione su Bluemix e sviluppare
come faresti sul desktop senza rieseguire la distribuzione. Quando apporti una modifica, puoi vedere tale modifica nella tua applicazione Bluemix in esecuzione
immediatamente. L'interfaccia riga di comando Bluemix Live Sync è denominata *bl*.

Puoi utilizzare i comandi dell'interfaccia riga di comando **bl** per completare le seguenti attività:

* Avviare e arrestare un'applicazione in esecuzione su Bluemix.
* Creare un nuovo progetto basato sul cloud dal tuo desktop.
* Sincronizzare le modifiche dal tuo desktop allo spazio di lavoro del progetto basato sul cloud e all'applicazione in esecuzione su Bluemix.
* Visualizzare l'elenco di progetti disponibili per la sincronizzazione.
* Visualizzare lo stato delle applicazioni in esecuzione.

Per ulteriori informazioni sul download e l'utilizzo del comando bl, vedi [Bluemix Live Sync](https://www.ng.bluemix.net/docs/manageapps/bluemixlive.html#bluemixlive).

## comandi bl

La riga di comando Bluemix Live Sync, **bl**, ha la seguente sintassi:

``` bl comando [argomenti][options] [--help]```

### Comandi
<dl>
<dt>login, l</dt>
<dd>Eseguire l'accesso a Bluemix.</dd>
<dt>logout, lo</dt>
<dd>Disconnettere l'utente.</dd>
<dt>sync, s</dt>
<dd>Avviare il processo di sincronizzazione tra il desktop e il server.</dd>
<dt>create, c</dt>
<dd>Creare un progetto privato, collegarlo al repository Git in questa directory e distribuire il contenuto a Bluemix.</dd>
<dt>projects, p</dt>
<dd>Elencare tutti i progetti disponibili per la sincronizzazione.</dd>
<dt>start, st</dt>
<dd>Avviare l'istanza dell'applicazione in Bluemix.</dd>
<dt>stop, sp</dt>
<dd>Arrestare l'istanza dell'applicazione in Bluemix.</dd>
<dt>status, ss</dt>
<dd>Elencare lo stato dell'istanza dell'applicazione in esecuzione in Bluemix.</dd>
</dl>

### Argomenti
<dl>
<dd>Argomenti per il comando.</dd>
</dl>

### Opzioni
<dl>
<dd>Opzioni per il comando.</dd>
</dl>

### Opzioni globali
<dl>
<dt>--help</dt>
<dd>Visualizzare la pagina di guida per lo specifico comando</dd>
<dt>--verbose</dt>
<dd>Abilitare la registrazione dettagliata.</dd>
</dl>

**Nota:** se qualche argomento od opzione contiene uno spazio, racchiudi il valore tra virgolette doppie.
