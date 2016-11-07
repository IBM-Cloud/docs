---

copyright:
  anni: 2016

---


<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Utilizzo dell'applicazione mobile
{: #iot4e_using_mobile}
*Ultimo aggiornamento: 19 settembre 2016*
{: .last-updated}

Introduzione all'applicazione mobile {{site.data.keyword.iotelectronics_full}} per vedere come ricevere avvisi, inviare comandi e controllare lo stato delle tue applicazioni collegate.
{:shortdesc}

## Prima di iniziare

Prima di poter utilizzare l'applicazione mobile, devi completare le seguenti attività:
  - Distribuisci un'istanza dello starter {{site.data.keyword.iotelectronics}} nella tua organizzazione {{site.data.keyword.Bluemix_notm}}. La distribuzione di un'istanza dello starter distribuisce automaticamente le applicazioni e i servizi componenti dello starter.
  - [Abilita le comunicazioni e la sicurezza mobile](iotelectronics_config_mca.html) configurando {{site.data.keyword.amafull}}.

## Introduzione all'applicazione mobile
Per iniziare a utilizzare l'applicazione mobile, completa le seguenti attività:
1. [Scarica l'applicazione mobile](#iot4e_downloadmobile) nel tuo dispositivo mobile.
2. [Connetti l'applicazione mobile all'ambiente {{site.data.keyword.iotelectronics}}](#iot4e_connecting_mobile) e registra le tue applicazioni.


 ### Scaricamento dell'applicazione mobile
 {: #iot4e_downloadmobile}
 Per ottenere l'applicazione mobile, scaricala e installala sul tuo telefono dall'Apple App store.  Sul tuo telefono, apri l'App store e cerca "ibm iot". Scegli **IBM IoT for Electronics** e installa.

 In alternativa, puoi installarla nel tuo telefono utilizzando [iTunes](https://itunes.apple.com/us/app/ibm-iot-for-electronics/id1103404928?ls=1&mt=8).


### Connessione dell'applicazione mobile
{: #iot4e_connecting_mobile}

Per connettere l'applicazione mobile al tuo ambiente e registrare le tue applicazioni, completa le seguenti attività:

1. Apri la tua applicazione starter {{site.data.keyword.itoelectronics}}. Per istruzioni, vedi [Apertura dell'applicazione starter](iot4ecreatingappliances.html#iot4e_openAppMain).

2. Seleziona **Controlla in remoto le tue applicazioni collegate**.

    ![{{site.data.keyword.iotelectronics}} esperienza starter](images/IoT4E_remotely_option.png "{{site.data.keyword.iotelectronics}} esperienza starter")

3. Crea una o più rondelle scorrendo alla sezione etichettata **Successivamente, scegli o aggiungi una nuova rondella simulata** e fai clic sull'icona +. Viene creata una nuova rondella.

    ![Aggiungi rondella](images/IoT4E_add_washer.png "Aggiungi rondella")

4.	Passa al codice QR di connessione e scansionalo utilizzando il tuo dispositivo mobile. Il codice QR di connessione è posizionato nella sezione etichettata **Per collegare l'applicazione all'ambiente, ti verrà richiesto di scansionare questo codice QR**.

  ![Codice QR di connessione.](images/iot4e_mobile_connect_QR.png "{{site.data.keyword.iotelectronics}} Codice QR di connessione")

5. Nel tuo dispositivo mobile, immetti le credenziali di accesso. I tuoi ID e password possono essere di qualsiasi lunghezza. Ricorda le tue credenziali di accesso per sessioni future. Il dispositivo mobile è ora registrato al tuo ambiente {{site.data.keyword.iotelectronics}} e sei pronto per registrare le singole applicazioni.

6. Sul tuo computer, passa a una rondella simulata e fai clic su di essa per visualizzarne i dati e il codice QR dell'applicazione.

  ![Seleziona una rondella.](images/IoT4E_mobile_washer_QR.png "Seleziona una rondella.")

7.	Utilizza il tuo dispositivo mobile per eseguire la scansione del codice QR della rondella. La rondella viene registrata e il suo stato viene visualizzato sul tuo cellulare.

#### Operazioni successive
Puoi ora visualizzare gli avvisi e controllare la rondella mediante il tuo dispositivo mobile. Per farlo, completa questa procedura:
  - Sul tuo computer, seleziona un problema con la rondella, come Board Failure o Strong Vibration. Il problema invia un avviso al tuo cellulare.
  - Sul tuo dispositivo mobile, fai clic su **Avvia lavaggio** per avviare la macchina. Puoi vedere la modifica dello stato della rondella sul tuo computer man mano si procede con il ciclo di lavaggio.
