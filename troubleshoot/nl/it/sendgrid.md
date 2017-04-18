---

copyright:
  anni: 2015, 2015


---


{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}

# Risoluzione dei problemi di SendGrid
{: #ts_sendgrid}

*Ultimo aggiornamento: 9 dicembre 2015*
{: .last-updated}

Di seguito è riportata la risposta a una domanda relativa all'utilizzo di SendGrid di {{site.data.keyword.Bluemix}}.
{:shortdesc}


## Impossibile inviare email utilizzando SendGrid
{: #ts_sendgrid_email}

Se non riesci a inviare email utilizzando il servizio SendGrid, potresti aver raggiunto il limite di email consentite per ciascuna istanza del servizio.
{:shortdesc}


Dopo aver inviato il numero massimo di email consentite, non riesci a utilizzare il servizio SendGrid per inviare altre email.
{: tsSymptoms}


Quando invii email utilizzando il servizio SendGrid, esiste un limite di invio pari a 25.000 email per istanza del servizio al mese. Dopo che hai raggiunto il limite, SendGrid interrompe
l'invio delle email e non vengono applicati ulteriori addebiti per l'utilizzo di questo servizio.
{: tsCauses}

Per controllare il numero restante di email consentite, fai clic sulla tua istanza del servizio SendGrid dal Dashboard {{site.data.keyword.Bluemix_notm}} e fai clic su **APRI DASHBOARD SENDGRID**. Puoi
visualizzare il numero nel campo **Crediti rimanenti**.


Se desideri inviare altre email anche dopo aver raggiunto il limite
di 25.000 email per istanza del servizio al mese, puoi aggiungere un'altra
istanza del servizio. Per ulteriori informazioni su SendGrid, vedi [Introduzione a SendGrid](https://sendgrid.com/docs/index.html){: new_window}.    
{: tsResolve}
