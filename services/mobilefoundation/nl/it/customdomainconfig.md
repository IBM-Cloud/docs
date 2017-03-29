---

copyright:
  years: 2016, 2017
lastupdated:  "2017-02-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Configurazione del dominio personalizzato per il server Mobile Foundation
{: #configcustomdomain}

{{site.data.keyword.mobilefoundation_short}} fornisce {{site.data.keyword.mfserver_short_notm}}, che è<!--on {{site.data.keyword.containerlong}} as a container group. The container group will be mapped to--> accessibile utilizzando un URL che dispone dei nomi del dominio in base alla **Regione** {{site.data.keyword.Bluemix_notm}}. Puoi anche configurare il tuo dominio personalizzato.
{:shortdesc}

L'<!--container group is created with a-->URL o la rotta creati con i nomi del dominio predefiniti in base alla `Regione` {{site.data.keyword.Bluemix_notm}}.

  |Dominio |  Regione  |    
  |:----- | :----- |    
  |`mybluemix.net` | Stati Uniti Sud |    
  |`eu-gb.mybluemix.net` | Regno Unito  |
  |`au-syd.mybluemix.net` | Sydney  |      
  {: caption="Table 1. Application domain names based on Region in {{site.data.keyword.Bluemix_notm}}" caption-side="top"}

Per poter utilizzare il tuo dominio, dovrai configurare il dominio personalizzato completando la seguente procedura:

1.	Crea un'istanza {{site.data.keyword.mfserver_short_notm}} creando l'istanza del servizio {{site.data.keyword.mobilefoundation_short}} scegliendo uno dei piani supportati.

+ Aggiungi il dominio personalizzato che vuoi utilizzare alla tua `Organizzazione` {{site.data.keyword.Bluemix_notm}}. Per aggiungere il tuo dominio, vai a **Gestisci organizzazioni > DOMINI > AGGIUNGI DOMINIO**.

+ Imposta una rotta per il server <!--container group--> per utilizzare il tuo dominio personalizzato.

+ Vai al provider DNS del tuo dominio e aggiungi una voce CNAME, che indirizzerà il traffico dal tuo dominio alla rotta {{site.data.keyword.Bluemix_notm}} predefinita, in cui è in esecuzione il server <!--container group-->.

+ Se vuoi configurare l'`https` per il dominio personalizzato, carica il certificato SSL per il tuo dominio in {{site.data.keyword.Bluemix_notm}}. Per farlo, vai a **Gestisci organizzazioni > DOMINI**, seleziona il dominio personalizzato per cui desideri configurare il certificato SSL e fai clic su **Carica certificato** per caricare il certificato SSL per il tuo dominio. Fai riferimento a [SSL Certificates and Bluemix Custom Domains ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://developer.ibm.com/bluemix/2014/09/28/ssl-certificates-bluemix-custom-domains/){: new_window} per ulteriori informazioni.
