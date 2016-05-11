<!-- Attribute definitions -->
{:codeblock: .codeblock}

# Introduzione all'esempio HelloWorld
{: #gettingstarted-android}
*Ultimo aggiornamento: 28 gennaio 2016*  

Se desideri iniziare a lavorare con una nuova applicazione Android, puoi utilizzare l'applicazione HelloWorld. Questa applicazione illustra come stabilire una connessione al tuo backend {{site.data.keyword.Bluemix}} da un'applicazione mobile senza autenticazione. Nell'applicazione è già installato l'SDK. Quando sei pronto, puoi ottenere le specifiche librerie
    che desideri utilizzare nella tua applicazione.

1. Crea il tuo backend mobile in {{site.data.keyword.Bluemix_notm}}.
    1. Nella sezione Contenitori tipo del catalogo {{site.data.keyword.Bluemix_notm}}, fai clic su MobileFirst Services Starter.
    2. Immetti un nome e un host per la tua applicazione e fai clic su **Crea**.
    3. Fai clic su **Fine**.
2. Ottieni il progetto da GitHub. Per ottenere il progetto puoi, facoltativamente, utilizzare il comando git clone. Dal tuo computer, apri il terminale e immetti quindi il seguente comando:
```
git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloworld.git
```
Prima di iniziare, scarica il file `Gradle.zip` e installa Gradle estraendo il file compresso scaricato nella directory che preferisci. Android Studio potrebbe chiedere un GRADLE HOME quando
importi l'esempio per la prima volta. Imposta tale percorso alla directory bin che si trova nel file `Gradle.zip` estratto. Il file `build.gradle` crea automaticamente
                        il tuo progetto introducendo le dipendenze richieste.
3. Inizializza il progetto.
Per inizializzare l'SDK, sostituisci &lt;ROTTA_APPLICAZIONE&gt; e &lt;ID_APPLICAZIONE&gt; con la rotta e il GUID della tua applicazione nel blocco try all'interno della funzione `BMSClient.getInstance().initialize()`:
```
// inizializza SDK con ID e rotta dell'applicazione IBM Bluemix
BMSClient.getInstance().initialize(this, "<ROTTA_APPLICAZIONE>", "<ID_APPLICAZIONE>");
```{: codeblock}

4. Esegui l'esempio nel tuo ambiente di sviluppo.
Dalla barra degli strumenti di Android Studio, fai clic sul pulsante di riproduzione (play) e seleziona un simulatore.
Nel simulatore,
                fai clic su **Ping {{site.data.keyword.Bluemix_notm}}**. L'applicazione di esempio invia una richiesta Get a una risorsa protetta sul runtime Node.js su {{site.data.keyword.Bluemix_notm}}. Se la richiesta ha esito
                            positivo, la connessione è verificata e il testo nel simulatore viene aggiornato.
<br/>**Nota:** il codice di runtime Node.js viene fornito nel contenitore tipo MobileFirst Services Starter. Se l'applicazione di backend non è stata creata con il contenitore tipo MobileFirst Services Starter, l'applicazione non stabilirà correttamente una connessione.<br/>
Quando stabilisci correttamente una connessione a {{site.data.keyword.Bluemix_notm}} dall'applicazione mobile in Android Studio, viene visualizzato un messaggio che indica che la connessione è stata stabilita ("Yay! You are connected"):<br/>
![Applicazione Hello World connessa correttamente a {{site.data.keyword.Bluemix_notm}}](images/yayconnected.jpg "Figura 1. Applicazione Hello World connessa correttamente a Bluemix")

5. Risolvere gli eventuali problemi.<br/>Quando la connessione non riesce, viene visualizzato un messaggio che indica che qualcosa è andato storto ("Bummer. Something went wrong"):</br>
![Applicazione Hello World non connessa a Bluemix](images/bummer_android.jpg "Figura 2. Applicazione Hello World non connessa a Bluemix")
<br/>
Controlla i seguenti elementi:
 * Verifica di aver incollato correttamente i valori di instradamento e GUID.
 * Puoi anche controllare il log di debug per ulteriori informazioni.

## Passi successivi:
{: #next}
Per informazioni su come ottenere l'SDK e integrarlo nella tua applicazione mobile, consulta le informazioni relative all'impostazione dei servizi Bluemix.
   * [Mobile Client Access](../../services/mobileaccess/index.html)
   * [Push](../../services/mobilepush/index.html)

# rellinks

## samples
   * [Esempio HelloWorld](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloworld)

## sdk
   * [Core SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core)

## api
   * [API Core](https://classicdocs.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html)
