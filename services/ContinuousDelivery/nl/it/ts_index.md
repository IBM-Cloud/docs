---

copyright:
  years: 2015, 2017
lastupdated: "2017-2-9"

---
<!-- Common attributes used in the template are defined as follows: -->
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Risoluzione dei problemi {{site.data.keyword.contdelivery_short}}
{: #ts_cd}

Ottieni le risposte alle domande di risoluzione dei problemi comuni sull'utilizzo di {{site.data.keyword.contdelivery_full}}.
{:shortdesc}


## Impossibile eseguire l'autorizzazione con GitHub
{: #cannot_authorize_github}

Non sei autorizzato con GitHub.
{:shortdesc}

Se non sei autorizzato con {{site.data.keyword.Bluemix_notm}} ad accedere al tuo account GitHub, si può verificare uno qualsiasi di questi problemi:
{: tsSymptoms}

 * Quando tenti di aggiungere un'integrazione dello strumento GitHub alla tua toolchain, l'integrazione dello strumento non viene aggiunta.
 * La pipeline non viene eseguita automaticamente quando trasmetti le modifiche al tuo repository GitHub o GitHub Enterprise.

{{site.data.keyword.Bluemix_notm}} non è autorizzato ad accedere a GitHub.  
{: tsCauses}
 
Se stai configurando l'integrazione dello strumento GitHub mentre stai creando la tua toolchain, segui questi passi:
{: tsResolve}
 
  1. Nella sezione delle integrazioni configurabili, fai clic su **GitHub**.  
  1. Se stai creando la toolchain in {{site.data.keyword.Bluemix_notm}} pubblico e non hai autorizzato {{site.data.keyword.Bluemix_notm}} ad accedere a GitHub, fai clic su **Autorizza** per andare al sito web GitHub. 
  1. Se non disponi di una sessione GitHub attiva, ti viene richiesto di accedere. Fai clic su **Authorize Application** per consentire a {{site.data.keyword.Bluemix_notm}} di accedere al tuo account GitHub. Se disponi di una sessione GitHub attiva ma non hai immesso la tua password recentemente, ti potrebbe essere richiesto di immettere la tua password GitHub per la conferma.
  
Se già disponi di una toolchain, aggiorna la configurazione dell'integrazione dello strumento GitHub:

 1. Nel dashboard DevOps, nella pagina **Toolchain**, fai clic sulla toolchain per aprirne la pagina Panoramica. In alternativa, nella pagina della panoramica dell'applicazione, nella scheda di fornitura continua, fai clic su **Visualizza toolchain** e quindi su **Panoramica**.
 1. Nella scheda GitHub, fai clic sul menu e su **Configure**.
 1. Aggiorna le impostazioni di configurazione per autorizzare {{site.data.keyword.Bluemix_notm}} ad accedere a GitHub. Fai clic su **Authorize** per andare al sito web GitHub. Se non disponi di una sessione GitHub attiva, ti viene richiesto di accedere. Fai clic su **Authorize Application** per consentire a {{site.data.keyword.Bluemix_notm}} di accedere al tuo account GitHub. Se disponi di una sessione GitHub attiva ma non hai immesso la tua password recentemente, ti potrebbe essere richiesto di immettere la tua password GitHub per la conferma.
 1. Quando hai terminato di aggiornare le impostazioni, fai clic su **Save Integration**.


## L'integrazione dello strumento non è configurata
{: #tool_integration_error}

Dopo aver configurato un'integrazione dello strumento per la tua toolchain, viene visualizzato l'errore `Setup failed` nella scheda dello strumento.
{:shortdesc}

Dopo aver configurato un'integrazione dello strumento, ne visualizzi la scheda dello strumento nella pagina della panoramica della toolchain e noti che la configurazione ha avuto esito negativo.
{: tsSymptoms}

 ![Errore configurazione non riuscita](images/tool_setup_failed.png)
 
Quando aggiungi un'integrazione dello strumento, la toolchain comunica con lo strumento rappresentato dall'integrazione dello strumento per eseguire il provisioning di tutte le risorse e le associa alla toolchain. Se si verifica un errore nel processo di configurazione o se la comunicazione tra la toolchain e lo strumento non viene completata correttamente, l'integrazione dello strumento viene messa in uno stato di errore.
{: tsCauses}

Configura nuovamente l'integrazione dello strumento:
{: tsResolve}

1. Nella relativa scheda, passa con il mouse sul messaggio `Setup failed` e fai clic su **Reconfigure**.

 ![Pulsante riconfigura](images/tool_reconfigure.png)
 
1. Assicurati di stare utilizzando dei parametri di configurazione validi. Se l'errore è stato causato da una configurazione non valida, viene visualizzato un messaggio di errore; ad esempio, `Impossibile configurare l'integrazione. Controlla le impostazione e riprova. Motivo: Invalid api_key:fakeKey`. Aggiorna le impostazioni per l'integrazione dello strumento e fai clic su **Save integration**.
1. Se l'errore è stato causato da un problema di comunicazione, fai clic su **Save integration** per ritentare.
