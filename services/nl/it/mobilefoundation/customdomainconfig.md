---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Configurazione del dominio personalizzato per il server  {{site.data.keyword.mobilefoundation_short}}
{: #configcustomdomain}

*Ultimo aggiornamento: 15 giugno 2016*
{: .last-updated}

{{site.data.keyword.mobilefoundation_short}} fornisce un {{site.data.keyword.mfserver_short_notm}} su {{site.data.keyword.containerlong}} come gruppo di contenitori. Il gruppo di contenitori verrà associato a un URL che ha i nomi dominio basati sulla **Regione** {{site.data.keyword.Bluemix_notm}}. Puoi anche configurare il tuo dominio personalizzato.
{:shortdesc}

Un gruppo di contenitori viene creato con un URL o rotta che ha i nomi domino predefiniti basati sulla `Regione` {{site.data.keyword.Bluemix_notm}}.

*Tabella 1. Nomi dominio dell'applicazione basati sulla 'Regione' in  {{site.data.keyword.Bluemix_notm}}*

  |Dominio |  Regione  |    
  |:----- | :----- |    
  |`mybluemix.net` | Dallas, USA  |    
  |`eu-gb.mybluemix.net` | Londra, UK  |    
  |`au-syd.mybluemix.net`  | Sydney, Australia |  

Per poter utilizzare il tuo dominio, dovrai configurare il dominio personalizzato completando la seguente procedura:

1.	Crea un'istanza {{site.data.keyword.mfserver_short_notm}} creando l'istanza del servizio {{site.data.keyword.mobilefoundation_short}} scegliendo uno dei piani supportati.

+ Aggiungi il dominio personalizzato che vuoi utilizzare alla tua `Organizzazione` {{site.data.keyword.Bluemix_notm}}. Per aggiungere il tuo dominio, vai a **Gestisci organizzazioni > DOMINI > AGGIUNGI DOMINIO**.

+ Imposta una rotta per il gruppo di contenitori per utilizzare il tuo dominio personalizzato.

+ Vai al provider DNS del tuo dominio e aggiungi una voce CNAME, che indirizzerà il traffico dal tuo dominio alla rotta {{site.data.keyword.Bluemix_notm}} predefinita, in cui è in esecuzione il gruppo di contenitori.

+ Se vuoi configurare l'`https` per il dominio personalizzato, carica il certificato SSL per il tuo dominio in {{site.data.keyword.Bluemix_notm}}. Per farlo, vai a **Gestisci organizzazioni > DOMINI**, seleziona il dominio personalizzato per cui desideri configurare il certificato SSL e fai clic su **Carica certificato** per caricare il certificato SSL per il tuo dominio. Fai riferimento a [SSL Certificates and Bluemix Custom Domains](https://developer.ibm.com/bluemix/2014/09/28/ssl-certificates-bluemix-custom-domains/) per ulteriori informazioni.
