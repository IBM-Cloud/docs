---

copyright:
  years: 2015-2016

---

<!-- Attribute definitions -->
{:codeblock: .codeblock}

# Introduzione all'esempio Hello Bluemix per Android
{: #gettingstarted-android}
*Ultimo aggiornamento: 27 maggio 2016*
{: .last-updated}  

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

3. Inizializza il progetto sostituendo &lt;APPLICATION_ROUTE&gt; e &lt;APPLICATION_ID&gt; con la rotta e il GUID della tua applicazione nel blocco `try` all'interno della funzione `BMSClient.getInstance().initialize()`:
```
// inizializza SDK con ID e rotta dell'applicazione IBM Bluemix
BMSClient.getInstance().initialize(this, "<ROTTA_APPLICAZIONE>", "<ID_APPLICAZIONE>");
```
4. Esegui l'esempio nel tuo ambiente di sviluppo.
Dalla barra degli strumenti di Android Studio, fai clic sul pulsante di riproduzione **Play** e seleziona un simulatore.
5. Nel simulatore,
                fai clic su **Ping {{site.data.keyword.Bluemix_notm}}**. L'applicazione di esempio invia una richiesta Get al runtime `Node.js` su {{site.data.keyword.Bluemix_notm}}. Se la richiesta ha esito
                            positivo, la connessione è verificata e il testo nel simulatore viene aggiornato.

  **Nota:** il codice di runtime `Node.js` viene fornito nel contenitore tipo MobileFirst Services Starter. Se l'applicazione di backend non è stata creata con il contenitore tipo MobileFirst Services Starter, l'applicazione non stabilirà correttamente una connessione.

  Dopo che hai stabilito correttamente una connessione a {{site.data.keyword.Bluemix_notm}} dall'applicazione mobile in Android Studio, viene visualizzato il seguente messaggio:

  `Yay! You are connected`
  {: screen}

  ![Applicazione Hello World connessa correttamente a {{site.data.keyword.Bluemix_notm}}](images/yayconnected.jpg "Figura 1. Applicazione Hello World connessa correttamente a Bluemix")

  Se la connessione non riesce, visualizzerai:
  `Bummer. Something went wrong`
  {: screen}

  ![Applicazione Hello World non connessa a Bluemix](images/bummer_android.jpg "Figura 2. Applicazione Hello World non connessa a Bluemix")

  Puoi risolvere il problema riguardo la connessione non riuscita nel seguente modo:
   * Verifica di aver incollato correttamente i valori di instradamento e GUID.
   * Rivedi il log di debug per ulteriori informazioni.


## Passi successivi:
{: #next}
Per informazioni su come ottenere l'SDK e integrarlo nella tua applicazione mobile, consulta le informazioni relative all'impostazione dei servizi Bluemix.
   * [Mobile Client Access](../../services/mobileaccess/index.html)
   * [Push](../../services/mobilepush/index.html)

# rellinks

## samples
   * [Esempio Hello Bluemix](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloworld)

## sdk
   * [Core SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core)

## api
   * [API Core](https://www.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html)
