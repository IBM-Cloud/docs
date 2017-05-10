---



copyright:

  years: 2016, 2017
lastupdated: "2017-02-09"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Account standard beta di IBM {{site.data.keyword.Bluemix_notm}} 
{: #betaintro}

L'Account standard beta di {{site.data.keyword.Bluemix}} introduce un nuovo account gratuito, che offre un nuovo modo di lavorare in {{site.data.keyword.Bluemix_notm}} Public Cloud. A differenza della versione di prova di 30 giorni {{site.data.keyword.Bluemix_notm}}, l'Account standard non ha una scadenza. Puoi continuare a lavorare sulle tue applicazioni {{site.data.keyword.Bluemix_notm}} senza preoccuparti dei limiti di tempo. 
{:shortdesc}

La partecipazione all'utilizzo dell'Account standard beta è solo su invito. Dopo aver accettato l'invito e creato il tuo account standard, potrai invitare amici e colleghi a partecipare alla versione Beta.  

## Presentazione dell'Account standard {{site.data.keyword.Bluemix_notm}}
{: #standardaccount}

Potresti chiederti qual è la differenza tra l'Account standard e l'Account di prova. Nelle seguenti tabelle vengono riepilogati i dettagli chiave relativi all'account standard {{site.data.keyword.Bluemix_notm}}. 

|Novità in un account standard |    
|-----------------|
| L'account non scade mai. |
| Le applicazioni Cloud Foundry possono accedere fino a 256 MB di memoria di runtime immediata. |
| Puoi accedere ai piani Lite gratuiti per Cloudant NoSQL DB e la Piattaforma Internet delle cose con altri servizi in arrivo. |
| Le tue applicazioni verranno sospese se non vengono svolte attività di sviluppo per 10 giorni. |
| Le tue istanze del servizio vengono eliminate dopo 30 giorni di inattività. |
{:caption="Tabella 1. Novità in un account standard" caption-side="top"}

|Cosa rimane invariato quando si converte un account di prova? | 
|-----------------|
|L'account è gratuito -- non ti serve una carta di credito. |
|Tutte le istanze Lite di Cloudant NoSQL DB e della Piattaforma Internet delle cose. È possibile trasferire un'istanza Lite al tuo nuovo account per ognuno di questi servizi. |
|L'organizzazione, gli spazi e le impostazioni di accesso dei membri del team associate rimangono uguali. È possibile trasferire un'organizzazione al tuo nuovo account. |
|Il livello di supporto di {{site.data.keyword.Bluemix_notm}} rimane lo stesso. |
{:caption="Tabella 2. Cosa rimane invariato" caption-side="top"}

**Nota:** se il tuo account di prova non viene convertito, viene visualizzato un messaggio che ne spiega il motivo. Potresti avere più di un'organizzazione nel tuo account di prova esistente o applicazioni che non è possibile trasferire. Effettua l'operazione appropriata e prova a convertire di nuovo l'account.

Se hai eseguito la registrazione per un account standard, puoi invitare i membri del team a collaborare nella tua organizzazione e nei tuoi spazi, visualizzare il tuo utilizzo, creare gli spazi, aggiornare il profilo del tuo account e gestire la tua organizzazione. Per ulteriori
informazioni, vedi [Configurazione del tuo account](/docs/admin/adminpublic.html#account).

## Piani Lite
{: #liteplans}
   
I piani Lite, disponibili anche nell'account Pagamento a consumo, sono strutturati come quota gratuita. Puoi lavorare tranquillamente sui tuoi progetti senza il rischio di generare una fattura accidentale. La quota potrebbe essere applicata per uno specifico periodo di tempo, ad esempio un mese, oppure una tantum. Di seguito sono riportati alcuni esempi di quote dei piani Lite:

<ul>
<li>Numero massimo di dispositivi registrati.</li>
<li>Numero massimo di bind di applicazione.</li>
<li>Limite di archiviazione di dati crittografati, ad esempio 1 GB.</li>
<li>Capacità produttiva fornita.</li>
</ul> 

In un account standard, puoi utilizzare qualsiasi servizio del Catalogo {{site.data.keyword.Bluemix_notm}} che disponga di un piano Lite. I piani Lite sono facili da individuare. Per impostazione predefinita, quando apri il Catalogo, tutti i servizi con un piano Lite vengono visualizzati e identificati con una tag Lite ![tag Lite](../icons/Lite.svg). Seleziona un servizio per visualizzare i dettagli della quota per il piano Lite associato.

## Cosa è disponibile nell'account standard?
{: #whatsavailable}

In un account standard, le applicazioni Cloud Foundry possono accedere fino a un massimo di 256 MB di memoria di runtime immediata. Se superi la quota assegnata, puoi arrestare alcune delle tue applicazioni per liberare memoria di runtime. 

Nell'Account standard beta, i seguenti servizi offrono un piano Lite:

<ul>
<li>Cloudant NoSQL DB</li>
<li>Piattaforma Internet delle cose</li>
</ul>

Prossimamente l'elenco verrà aggiornato con altri servizi.

Quando si raggiungono i limiti di quota, la tua applicazione viene arrestata o il tuo servizio viene disabilitato. Se il piano Lite specifica che la quota viene fornita su base mensile, l'utilizzo delle risorse viene ripristinato il 1° di ogni mese, giorno in cui potrai riattivare il servizio. Quando stai per raggiungere il limite di quota o si già al limite, riceverai un'e-mail di notifica. 

Puoi eseguire il provisioning di 1 istanza per piano Lite. 

**Nota:** queste limitazioni si applicano solo all'account standard. In qualsiasi momento, puoi effettuare l'aggiornamento a un account Pagamento a consumo o con fatturazione di sottoscrizione. Paghi solo per ciò che utilizzi oltre i limiti concessi dalle franchigie. Per ulteriori informazioni sugli account Pagamento a consumo e Sottoscrizione, consulta [Modalità di fatturazione](/docs/pricing/index.html#pay-accounts).

## Attività di sviluppo
{: #devactivity}

Per aiutare gli utenti dell'Account standard a gestire al meglio le proprie risorse, abbiamo creato un paio di funzioni di efficienza che si basano sull'attività di sviluppo e sull'utilizzo:

 * Le applicazioni verranno sospese dopo 10 giorni di inattività dello sviluppo. Ciò è utile quando vuoi lavorare su una nuova applicazione perché non ti ritroverai a raggiungere il limite di 512 MB di quota di memoria. Per riattivare le tue applicazioni, inizia di nuovo a utilizzarle nella riga di comando Cloud Foundry o nella console {{site.data.keyword.Bluemix_notm}}. 
 
 Ecco un elenco di tutti i comandi che riattiveranno la tua applicazione.
  * push cf
  * cf restate
  * cf restart
  * cf ssh
  * cf scale
  * cf stop
  * cf start
  * cf create-route
  * cf map-route
  * cf unmap-route
  * cf delete-route
  * cf enable-ssh
  * cf disable-ssh

 **Nota:** se la tua applicazione è già abilitata a ssh, i comandi `cf enable-ssh` e `cf disable-sh` non riattiveranno la tua applicazione. 

 * I tuoi servizi con piano Lite verranno eliminati in assenza di attività per 30 giorni. Non dovrai quindi eliminare le istanze inattive quando desideri creare una nuova istanza. Al momento, questa funzione è utilizzata solo dalla Piattaforma Internet delle cose. 
 
 Mantieni attiva l'istanza Lite della Piattaforma Internet delle cose accedendo al dashboard dell'istanza del servizio di tale piattaforma.
 
## Partecipazione all'Account standard beta
{: #betainvitation}

Se sei stato selezionato per partecipare alla versione Beta, ti viene inviato un invito all'indirizzo e-mail associato al tuo Account di prova {{site.data.keyword.Bluemix_notm}}. Una volta ricevuto l'invito, completa le istruzioni riportate nell'e-mail per registrare l'account standard. 

Sei interessato a partecipare all'offerta dell'Account standard beta? Chiedi ai tuoi amici e colleghi. Se loro sono stati invitati a partecipare alla versione Beta e hanno creato il proprio account standard, potranno invitare anche te. 
