---

copyright:
  years: 2016, 2017
lastupdated:  "2016-08-03"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Manutenzione e aggiornamenti
{: #maintupdates_mf}

{{site.data.keyword.mobilefoundation_short}} fornisce {{site.data.keyword.mfserver_short_notm}} <!--on {{site.data.keyword.containerlong}} as a container group-->. Gli aggiornamenti al server {{site.data.keyword.mobilefoundation_short}} vengono notificati agli utenti. Puoi scegliere di aggiornare il server {{site.data.keyword.mobilefoundation_short}} quando ti è più conveniente.
{:shortdesc}

## Strategia di manutenzione
{: #maintupdate_strategy_mf}

Quando è disponibile un aggiornamento per {{site.data.keyword.mobilefoundation_short}}, l'utente riceverà una notifica sulla disponibilità dell'aggiornamento.  Sarà visualizzata una notifica nel dashboard dell'istanza del servizio. L'utente può scegliere di applicare l'aggiornamento per {{site.data.keyword.mobilefoundation_short}} durante una finestra di manutenzione decisa da lui.

L'aggiornamento del servizio {{site.data.keyword.mobilefoundation_short}} sarà reso disponibile quando viene aggiornato uno dei seguenti componenti.

* {{site.data.keyword.mfserver_short_notm}}.
* Versione Liberty sottostante.
* Versione Java Developer Kit sottostante.


## Applicare gli aggiornamenti
{: #apply_update_mf}

L'aggiornamento per {{site.data.keyword.mobilefoundation_short}} può essere applicato facendo clic su **Ricrea**.

Durante l'applicazione dell'aggiornamento, la versione del server, come visto in {{site.data.keyword.mfp_oc_short_notm}}, sarà modificata per indicare la versione aggiornata del server.

**Nota:**
* Gli utenti non saranno in grado di applicare le loro modifiche e aggiornamenti alla loro istanza del servizio {{site.data.keyword.mobilefoundation_short}}.
* Consulta [Ricreare il server nel piano Developer](c_using_mfs_p1.html#recreate_mobilefoundation_p1) e [Ricreare il server nel piano Professional 1 Application](c_using_mfs_p2.html#recreate_mobilefoundation_p2) per comprendere la differenza nel comportamento dei piani quando viene fatto clic su **Ricrea**.
