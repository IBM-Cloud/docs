---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-13"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Risoluzione dei problemi di {{site.data.keyword.iot_short_notm}}
{: #ts}

Queste sono le risposte a domande sulla risoluzione dei problemi comuni riguardo l'utilizzo di {{site.data.keyword.iot_full}} su {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

## Problema di accesso alla tua organizzazione {{site.data.keyword.iot_short_notm}}
{: #access-expiry-problem}

Non puoi accedere all'organizzazione {{site.data.keyword.iot_short_notm}} che ti appartiene.
{:shortdesc}

Non puoi accedere alla tua organizzazione {{site.data.keyword.iot_short_notm}} direttamente utilizzando l'URL dell'organizzazione o utilizzando `https://internetofthings.ibmcloud.com`.
{: tsSymptoms}

Il tuo accesso alla tua organizzazione {{site.data.keyword.iot_short_notm}} potrebbe essere scaduto. Le organizzazioni {{site.data.keyword.iot_short_notm}} create utilizzando {{site.data.keyword.Bluemix}} utilizzano i profili utente temporanei per impostazione predefinita.
{: tsCauses}

Puoi risolvere questo problema accedendo alla tua organizzazione {{site.data.keyword.iot_short_notm}} utilizzando {{site.data.keyword.Bluemix_notm}} e modificando le impostazioni sulla scadenza del tuo profilo utente. Per modificare le tue impostazioni di scadenza utente:

1. Dal tuo dashboard {{site.data.keyword.Bluemix_notm}}, apri il tuo servizio {{site.data.keyword.iot_short_notm}}.
2. Fai clic su **Membri** dalla barra di navigazione.
3. Fai clic sull'icona **Modifica**.
4. Deseleziona la casella **Accesso con scadenza** e fai clic su **Salva**.
{: tsResolve}

## Problema di connessione a {{site.data.keyword.iot_short_notm}}
{: #connection_problem}

La tua connessione a {{site.data.keyword.iot_short_notm}} cade o si scollega in modo imprevisto.
{:shortdesc}

Quando tenti di collegarti a {{site.data.keyword.iot_short_notm}}, il tuo dispositivo o applicazione riceve un errore.
{: tsSymptoms}

Potresti avere due dispositivi che tentano di collegarsi con lo stesso clientID e credenziali. È consentita una sola connessione per clientID. Non puoi avere due connessioni simultanee utilizzando lo stesso ID. Le applicazioni possono condividere la stessa chiave API, ma MQTT richiede che l'ID sia sempre univoco.
{: tsCauses}

Puoi risolvere questo problema confermando che non hai due dispositivi che tentano di collegarsi utilizzando le stesse credenziali.
{: tsResolve}

## Il dispositivo si scollega a intermittenza da {{site.data.keyword.iot_short_notm}}
{: #disconnection_problem}

La connessione del tuo dispositivo a {{site.data.keyword.iot_short_notm}} cade a intermittenza in modo imprevisto.
{:shortdesc}

Un dispositivo collegato a un servizio {{site.data.keyword.iot_short_notm}} viene scollegato a intermittenza. Il dispositivo di ricollega ma viene di nuovo scollegato in modo imprevisto dopo un poco tempo.
{: tsSymptoms}

Potrebbe essere che quando ti colleghi, stai utilizzando un valore per un opzione di ping MQTT troppo piccola, che la rende simile a un timeout. Ad esempio, se il MQTT client è impostato in modo non corretto, i ping non vengono ricevuti in modo tempestivo e la connessione viene chiusa.
{: tsCauses}

Puoi risolvere questo problema confermando di aver correttamente impostato i parametri ping e KeepAlive per la tua connessione.   
{: tsResolve}


## Come ottenere aiuto e supporto per {{site.data.keyword.iot_short_notm}}
{: #gettinghelp}

Se hai dei problemi o delle domande quando utilizzi {{site.data.keyword.iot_short_notm}}, puoi ottenere aiuto ricercando le informazioni o facendo delle domande in un forum. Inoltre puoi aprire un ticket di supporto.

Quando utilizzi i forum per fare una domanda, contrassegnala con una tag in modo che sia visualizzabile dai team di sviluppo {{site.data.keyword.Bluemix_notm}}.

* Se hai domande tecniche sullo sviluppo o la distribuzione di un'applicazione con {{site.data.keyword.iot_short_notm}}, inserisci la tua domanda in [Stack Overflow ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://stackoverflow.com/search?q=watson-iot+ibm-bluemix){:new_window} e contrassegnala con le tag "ibm-bluemix" e "watson-iot".
<!--Insert the appropriate dW Answers tag for your service for <service_keyword> in URL below:  -->
* Per domande sul servizio e sulle istruzioni per l'utilizzo iniziale, utilizza il forum [IBM developerWorks dW Answers ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://developer.ibm.com/answers/topics/watson-iot/?smartspace=bluemix){:new_window}. Includi le tag  "watson-iot" e "bluemix".

Consulta [Come ottenere supporto](https://www.{DomainName}/docs/support/index.html#getting-help) per ulteriori dettagli sull'utilizzo dei forum.

Per informazioni su come aprire un ticket di supporto IBM o sui livelli di supporto e sulla gravità dei ticket, consulta [Come contattare il supporto ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.{DomainName}/docs/support/index.html#contacting-support).
