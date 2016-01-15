# Introduzione all'esempio HelloWorld
{: #gettingstarted-cordova}

Se desideri iniziare a lavorare con una nuova applicazione Cordova, puoi utilizzare l'applicazione HelloWorld. Questa applicazione illustra come stabilire una connessione al tuo backend Bluemix da un'applicazione mobile senza autenticazione. Nell'applicazione è già installato l'SDK. Quando sei pronto, puoi ottenere le specifiche librerie
    che desideri utilizzare nella tua applicazione.

1. Crea il tuo backend mobile in Bluemix.
<ol>
	<li>Nella sezione Contenitori tipo del catalogo Bluemix, fai clic su MobileFirst Services Starter.</li>
    	<li>Immetti un nome e un host per la tua applicazione e fai clic su **Crea**.</li>
    	<li>Fai clic su **Fine**. </li>
</ol>
2. Ottieni il progetto da GitHub. Per ottenere il progetto puoi, facoltativamente, utilizzare il comando git clone. Dal tuo computer, apri il terminale e immetti quindi il seguente comando:
```
git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-Cordova-helloworld.git
```
Prima di iniziare, scarica il file Gradle.zip e installa Gradle estraendo il file compresso scaricato nella directory che preferisci. Android Studio potrebbe chiedere un GRADLE HOME quando
importi l'esempio per la prima volta. Imposta tale percorso alla directory bin che si trova nel file Gradle.zip estratto. Il file build.gradle crea automaticamente il tuo progetto introducendo le dipendenze richieste.

3. Inizializza il progetto.
Per inizializzare l'SDK, sostituisci &lt;ROTTA_APPLICAZIONE&gt; e &lt;ID_APPLICAZIONE&gt; con la rotta e il GUID della tua applicazione nel blocco try all'interno della funzione BMSClient.getInstance().initialize():
```
// inizializza SDK con ID e rotta dell'applicazione IBM Bluemix
BMSClient.getInstance().initialize(this, "<ROTTA_APPLICAZIONE>", "<ID_APPLICAZIONE>");
```
4. Esegui l'esempio nel tuo ambiente di sviluppo.
Dalla barra degli strumenti di Android Studio, fai clic sul pulsante di riproduzione (play) e seleziona un simulatore.
Nel simulatore, fai clic su **Ping Bluemix**. L'applicazione di esempio invia una richiesta Get a una risorsa protetta sul runtime Node.js su Bluemix. Se la richiesta ha esito
                            positivo, la connessione è verificata e il testo nel simulatore viene aggiornato.
Nota: il codice di runtime Node.js viene fornito nel contenitore tipo MobileFirst Services Starter. Se l'applicazione di backend non è stata creata con il contenitore tipo MobileFirst Services Starter, l'applicazione non stabilirà la connessione correttamente. 


![Applicazione Hello World connessa correttamente a Bluemix](images/yayconnected.jpg "Figura 1. Applicazione Hello World connessa correttamente a Bluemix")

Dopo che hai stabilito correttamente una connessione a Bluemix dall'applicazione mobile in Android Studio, viene visualizzato un messaggio che indica che la connessione è stata stabilita ("Yay! You are connected").
5. Risolvi gli eventuali problemi.

![Applicazione Hello World non connessa a Bluemix](images/bummer_android.jpg "Figura 2. Applicazione Hello World non connessa a Bluemix")

Quando la connessione non riesce, viene visualizzato un messaggio che indica che qualcosa è andato storto ("Bummer Something went wrong"). Sono incluse delle ulteriori informazioni sull'errore.
Controlla i seguenti elementi:
 * Verifica di aver incollato correttamente i valori di instradamento e GUID.
 * Puoi anche controllare il log di debug per ulteriori informazioni.

## Passi successivi:
{: #next}
Per informazioni su come ottenere l'SDK e integrarlo nella tua applicazione mobile, vedi la sezione relativa all'impostazione dell'SDK del client Android.
