---

copyright:
  years: 2017
lastupdated: "2017-02-28"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note:.deprecated}

# Introduzione a {{site.data.keyword.mqa}} (Obsoleto)
{: #gettingstartedtemplate}

**Il servizio {{site.data.keyword.mqafull}} è obsoleto.** Per ulteriori informazioni sullo stato e le date, consulta la [Voce del blog Retirement of Bluemix Mobile Quality Assurance ![icona link esterno](../../icons/launch-glyph.svg "icona link esterno")](https://www.ibm.com/blogs/bluemix/?p=72728){: new_window}.
{:deprecated}

{{site.data.keyword.mqafull}} fornisce
ai team gli strumenti necessari all'acquisizione di esperienze di tester e utenti in tempo reale per creare
e distribuire applicazioni mobili di alta qualità.
{: shortdesc}

Per iniziare a lavorare rapidamente con il servizio {{site.data.keyword.mqa}}, attieniti alla seguente procedura:

1. Dopo che hai creato un'istanza <!--[create an instance](https://console.{DomainName}/docs/services/reqnsi.html#req_instance)-->del servizio {{site.data.keyword.mqa}}, puoi accedere alla console {{site.data.keyword.mqa}} facendo clic sul tuo tile nella sezione **Servizi** del dashboard {{site.data.keyword.Bluemix}}.

	Il servizio {{site.data.keyword.mqa}} viene avviato.

2. Aggiungi un'applicazione mobile all'istanza {{site.data.keyword.mqa}} selezionando **Add MQA App** e fornendo un nome per l'applicazione.

3. Scarica le {{site.data.keyword.mqa}}SDK client [ ![icona link esterno](../../icons/launch-glyph.svg "icona link esterno")](http://www.ibm.com/support/docview.wss?uid=swg27044490){: new_window} e completa la strumentazione della tua applicazione continuando con una delle seguenti procedure:

	* [Strumenta MQA con un'applicazione Android](mqa_inst_app_android.html)
	* [Strumenta MQA con un'applicazione iOS](mqa_inst_app_ios.html)
	* [Strumenta MQA con un'applicazione Cordova](mqa_inst_app_cord.html)

	Per dotare di strumentazione le applicazioni di pre-produzione e di produzione viene utilizzato un unico SDK. Puoi
utilizzare il parametro `MODE:` per specificare *QA* per la modalità di pre-produzione
oppure specificare *MARKET* per la modalità di produzione. Specifica la modalità di pre-produzione in modo che i tester interni possano fornire informazioni dettagliate relative ai bug e agli arresti anomali che si verificano con la tua applicazione. Se la tua applicazione è in produzione, {{site.data.keyword.mqa}} facilita l'ottenimento del feedback dagli utenti nell'applicazione.

4. Dopo aver strumentato la tua applicazione, puoi visualizzare ulteriori informazioni sulla qualità dettagliate per essa selezionando una delle seguenti opzioni sull'interfaccia della tua istanza del servizio {{site.data.keyword.mqa}}:

	<dl>
		<dt><strong>Sessioni</strong></dt>
		<dd>Riesamina le informazioni relative ad arresti anomali, bug, feedback e lo stato del dispositivo durante la sessione.  Consulta [Viewing session details ![icona link esterno](../../icons/launch-glyph.svg "icona link esterno")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/t_ViewingSessionDetails.html){: new_window} nel IBM Knowledge Center per ulteriori informazioni.</dd>
		<dt>![](/images/cap_crashicon.jpg) <strong>Arresti anomali</strong></dt>
		<dd>Riesamina le informazioni relative alla causa degli arresti anomali. Consulta [Crash reports ![icona link esterno](../../icons/launch-glyph.svg "icona link esterno")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/c_CrashReports.html){: new_window} nel IBM Knowledge Center per ulteriori informazioni.</dd>
		<dt>![](/images/cap_bugicon.jpg) <strong>Bug</strong></dt>
		<dd>Riesamina le informazioni riportate dagli utenti, ad esempio i report sui bug, le acquisizioni schermo e i dettagli del dispositivo. Consulta [Bug reports ![icona link esterno](../../icons/launch-glyph.svg "icona link esterno")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/c_BugReports.html){: new_window} nel IBM Knowledge Center per ulteriori informazioni.</dd>
		<dt>![](/images/cap_feedbackicon.jpg) <strong>Feedback</strong></dt>
		<dd>Riesamina le risposte ai feedback dell'utente per vedere chi e quando ha scritto il feedback. Consulta [User feedback ![icona link esterno](../../icons/launch-glyph.svg "icona link esterno")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/c_UserFeedback.html){: new_window} nel IBM Knowledge Center per ulteriori informazioni.</dd>
		<dt><strong>Punteggio delle sensazioni (se configurato)</strong></dt>
		<dd>Riesamina il punteggio delle sensazioni utente nel corso del tempo e delle versioni per monitorare, misurare e migliorare la qualità dell'applicazione. Consulta [User sentiment ![icona link esterno](../../icons/launch-glyph.svg "icona link esterno")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/UserSentiment.html){: new_window} nel IBM Knowledge Center per ulteriori informazioni.</dd>
		<dt><strong>Dispositivi registrati</strong></dt>
		<dd>Riesamina l'elenco dei dispositivi utilizzati durante una sessione di test e le informazioni su questi dispositivi. Consulta [Viewing device information ![icona link esterno](../../icons/launch-glyph.svg "icona link esterno")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/t_ManagingDevices.html){: new_window} nel IBM Knowledge Center per ulteriori informazioni.</dd>
	</dl>

	Queste metriche includono
i seguenti dati:

	* Dati di pre-produzione relativi ad arresti anomali, bug, feedback e sessioni.
	* Dati di produzioni relativi ad arresti anomali, feedback, sensazioni e sessioni.

	![Acquisizione schermo dell'interfaccia in cui puoi visualizzare le metriche di qualità per un'applicazione.](images/quality_metrics_saas4.gif)

	Visualizzando queste informazioni per le applicazioni, puoi stabilire se
analizzare ulteriormente gli specifici problemi. Ad esempio,
se la frequenza di arresti anomali per un'applicazione aumenta in modo significativo, puoi fare clic sulla frequenza
per visualizzare informazioni più dettagliate sui report dell'arresto anomalo di tale applicazione.

5. Per visualizzare il punteggio complessivo delle sensazioni
per l'applicazione, devi configurare l'analisi delle sensazioni:

	1. Nella sezione *Punteggio sensazioni*,
fai clic sul link per configurare l'analisi delle sensazioni per l'applicazione selezionata.

	2. Nella pagina Dettagli applicazione, [configura l'analisi delle sensazioni ![icona link esterno](../../icons/launch-glyph.svg "icona link esterno")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/tEnablingUserSentiment.html){: new_window} e salva le le tue modifiche.


# Link correlati
{: #rellinks notoc}

## Esercitazioni ed esempi
{: #samples notoc}

* [Video: Introduzione a Mobile Quality Assurance in Bluemix ![icona link esterno](../../icons/launch-glyph.svg "icona link esterno")](https://www.youtube.com/watch?v=zHRfGatcKPM){: new_window}  
* [Video: Analisi delle sensazioni in Mobile Quality Assurance ![icona link esterno](../../icons/launch-glyph.svg "icona link esterno")](https://www.youtube.com/watch?v=uhkqb8BIn6k){: new_window}
* [developerWorks: Add IBM Mobile Quality Assurance to your mobile quality regimen ![icona link esterno](../../icons/launch-glyph.svg "icona link esterno")](http://www.ibm.com/developerworks/library/mo-mqa/index.html){: new_window}
* [developerWorks: Build mobile apps that work: Five tips from an expert panel ![icona link esterno](../../icons/launch-glyph.svg "icona link esterno")](http://www.ibm.com/developerworks/library/mo-mqa-tips/index.html){: new_window}
* [developerWorks: Build a mobile app that isn't perfect ![icona link esterno](../../icons/launch-glyph.svg "icona link esterno")](http://www.ibm.com/developerworks/library/mo-build-imperfect-mobile-app/){: new_window}
* [developerWorks: DevOps for mobile apps challenges and best practices ![icona link esterno](../../icons/launch-glyph.svg "icona link esterno")](http://www.ibm.com/developerworks/library/mo-bestdevops-mobileapps/index.html){: new_window}
* [Sample: bluelist-mqa ![icona link esterno](../../icons/launch-glyph.svg "icona link esterno")](https://hub.jazz.net/project/mobilecloud/bluelist-mqa/overview){: new_window}
