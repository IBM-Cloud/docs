---

copyright:
  anni: 2016

---


<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Configurazione della connettività e sicurezza mobile
{: #iot4e_configureMCA}

*Ultimo aggiornamento: 19 settembre 2016*
{: .last-updated}

Abilita le comunicazioni e la sicurezza mobile configurando {{site.data.keyword.amafull}}. Questa attività è necessaria per utilizzare l'applicazione mobile di esempio e deve essere eseguita solo una volta.
{:shortdesc}

## Prima di iniziare

Prima di iniziare, devi completare le seguenti attività:
  - Distribuisci un'istanza dello starter {{site.data.keyword.iotelectronics}} nella tua organizzazione
{{site.data.keyword.Bluemix_notm}}. La distribuzione di un'istanza dello starter distribuisce automaticamente le applicazioni e i servizi del componente, incluso {{site.data.keyword.amafull}}.

  - Poiché il processo di configurazione varia leggermente a seconda della versione della console {{site.data.keyword.Bluemix_notm}} in uso, devi leggere le istruzioni per la versione appropriata.

  Per determinare la versione che stai utilizzando, puoi controllare le seguenti opzioni:
    - [Nuovo {{site.data.keyword.Bluemix_notm}}](#configMCAnew). Se stai utilizzando la nuova esperienza {{site.data.keyword.Bluemix_notm}}, nella sezione dell'intestazione del dashboard viene visualizzata l'opzione **Vai a Esperienza classica**.
    - [{{site.data.keyword.Bluemix_notm}} classico](#configMCAclassic). Se stai utilizzando l'esperienza classica di {{site.data.keyword.Bluemix_notm}}, nella sezione dell'intestazione viene visualizzata l'opzione **Prova il nuovo Bluemix**.

## Configurazione di {{site.data.keyword.amashort}} nella nuova esperienza {{site.data.keyword.Bluemix_notm}}
{: #configMCAnew}

  1. Se hai appena distribuito lo starter {{site.data.keyword.iotelectronics}}, viene visualizzata la scheda Introduzione dell'applicazione starter e dovrai procedere al passo successivo di queste istruzioni. Se l'applicazione starter non viene visualizzata, apri il dashboard {{site.data.keyword.Bluemix_notm}} e avvia la tua applicazione starter {{site.data.keyword.iotelectronics}} facendo clic sul tile relativo.

    ![{{site.data.keyword.iotelectronics}} nel dashboard, Nuova esperienza](images/IoT4E_bm_dashboard.png "{{site.data.keyword.iotelectronics}} nel dashboard, Nuova esperienza")

  2. Nella scheda **Connessioni**, fai clic sul servizio {{site.data.keyword.amashort}} per aprirlo.

    ![Come trovare {{site.data.keyword.amashort}}.](images/IoT4E_Connections.png "{{site.data.keyword.iotelectronics}} connections")

  3. Nella pagina **Imposta autenticazione**, individua l'URL della tua applicazione starter {{site.data.keyword.iotelectronics}} facendo clic su **Opzioni mobili**. Copia l'URL che si trova nel campo **Rotta**.

    ![ Opzioni mobili {{site.data.keyword.amashort}}](images/MCA_config_mobileoptions.png "Opzioni mobili {{site.data.keyword.amashort}}")  

  4. Nella sezione **Personalizza della pagina **Imposta autenticazione**, fai clic su **Configura**.

       ![Configura {{site.data.keyword.amashort}}.](images/MCA_config_pg.png "{{site.data.keyword.amashort}} Pagina Imposta autenticazione")  

  5. Immetti le seguenti credenziali di autenticazione e fai clic su **Salva**:
    - **Nome realm**: immetti **myRealm**.
    - **URL provider di identità personalizzato**: immetti l'URL che hai copiato precedentemente per identificare la tua applicazione starter {{site.data.keyword.iotelectronics}} nel seguente formato: **https://<*myIoT4eStarterApp*>.mybluemix.net**
    - **URI di reindirizzamento dell'applicazione Web**: lascia vuoto questo campo.

      ![{{site.data.keyword.amashort}} Voce autenticazione personalizzata.](images/MCA_config_pg2.png "{{site.data.keyword.amashort}} Voce autenticazione personalizzata")  

  6. Torna alla scheda Connessioni della console starter {{site.data.keyword.iotelectronics}} facendo clic sul nome dell'applicazione starter, che si trova nella sezione dell'intestazione.

   ![Navigazione {{site.data.keyword.amashort}}.](images/MCA_breadcrumb.png "Navigazione {{site.data.keyword.amashort}}")

## Configurazione di {{site.data.keyword.amashort}} nell'esperienza classica {{site.data.keyword.Bluemix_notm}}
{: #configMCAclassic}

1. Nel dashboard {{site.data.keyword.Bluemix_notm}}, avvia la tua applicazione starter {{site.data.keyword.iotelectronics}} facendo clic sul tile relativo.

    ![{{site.data.keyword.iotelectronics}} nel dashboard, Classico.](images/IoT4E_bm_dashboard_c.png "{{site.data.keyword.iotelectronics}} nel dashboard, Classico")

2. Nella tua istanza di {{site.data.keyword.iotelectronics}}, fai clic sul servizio {{site.data.keyword.amashort}} per aprirlo.   

  ![Come trovare {{site.data.keyword.amashort}}.](images/IoT4E_Connections_c.png "{{site.data.keyword.iotelectronics}} connections")

2. Nella pagina **Imposta autenticazione**, individua l'URL della tua applicazione starter {{site.data.keyword.iotelectronics}} facendo clic su **Opzioni mobili**. Copia l'URL che si trova nel campo **Rotta**.

  ![ Opzioni mobili {{site.data.keyword.amashort}}](images/MCA_config_mobileoptions.png "Opzioni mobili {{site.data.keyword.amashort}}")  

3. Nella sezione **Personalizza della pagina **Imposta autenticazione**, fai clic su **Configura**.

 ![Configura {{site.data.keyword.amashort}}.](images/MCA_config_pg.png "{{site.data.keyword.amashort}} Pagina Imposta autenticazione")  

4. Immetti le seguenti credenziali di autenticazione e fai clic su **Salva**:
   - **Nome realm**: immetti **myRealm**.
   - **URL provider di identità personalizzato**: immetti l'URL che hai copiato precedentemente per identificare la tua applicazione starter {{site.data.keyword.iotelectronics}} nel seguente formato: **https://<*myIoT4eStarterApp*>.mybluemix.net**
   - **URI di reindirizzamento dell'applicazione Web**: lascia vuoto questo campo.

    ![{{site.data.keyword.amashort}} Voce autenticazione personalizzata.](images/MCA_config_pg2.png "{{site.data.keyword.amashort}} Voce autenticazione personalizzata")  

5. Torna alla scheda Connessioni della console starter {{site.data.keyword.iotelectronics}} nel seguente modo:
  1. Visualizza il menu facendo clic sulle doppie frecce accanto all'opzione **Torna al Dashboard** nella sezione dell'intestazione.
  2. Fai clic su **Panoramica** per tornare alla console starter.  

    ![Navigazione {{site.data.keyword.amashort}}.](images/MCA_breadcrumb_c.png "Navigazione {{site.data.keyword.amashort}}")
