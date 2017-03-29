---

copyright:
  years: 2015, 2017
  
lastupdated: "2017-01-10"

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 


# Fehlerbehebung für die Verwaltung von Konten
{: #managingaccounts}

Allgemeine Probleme bei der Verwaltung Ihres Kontos können sein, dass verschiedene Apps denselben Domänennamen verwenden oder Administratoren nicht alle Organisationen anzeigen können. In vielen Fällen können Sie diese Probleme durch Ausführen weniger einfacher Schritte beheben.
{:shortdesc}


## Konto ist inaktiv
{: #ts_accnt_inactive}

Wenn Ihr Konto inaktiv ist, können Sie keine App in {{site.data.keyword.Bluemix_notm}} erstellen. Wenden Sie sich zur Lösung dieses Problems an das Support-Team.

Bei dem Versuch, in {{site.data.keyword.Bluemix_notm}} eine App zu erstellen, wird die folgende Fehlernachricht angezeigt:
{: tsSymptoms} 

`BXNUI0096E: Die App wurde nicht erstellt. Ihr Konto ist inaktiv, da es storniert oder ausgesetzt wurde.`

Der Status Ihres {{site.data.keyword.Bluemix_notm}}-Kontos verändert sich in 'Inaktiv', wenn es storniert oder ausgesetzt wurde.
{: tsCauses}


Setzen Sie sich zur Reaktivierung Ihres Kontos mit dem [{{site.data.keyword.Bluemix_notm}}-Support ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](http://ibm.biz/bluemixsupport.com){: new_window} in Verbindung. Geben Sie in der E-Mail die folgenden Informationen an:
{: tsResolve}

  * Die IBMid, mit der Sie sich bei {{site.data.keyword.Bluemix_notm}} anmelden.
  * Der Name der Organisation, in der Ihre App erstellt wird. Mithilfe dieser Informationen kann das Support-Team feststellen, ob Ihnen die richtigen Rollen bzw. die richtige Zugehörigkeit in Ihrer Organisation zugewiesen wurden.


## Der momentanen Organisation ist kein Bereich zugeordnet
{: #ts_no_space}

Wenn Ihrer momentanen Organisation kein Bereich zugeordnet ist, können Sie keine Anwendung erstellen.

Bei dem Versuch, in {{site.data.keyword.Bluemix_notm}} eine App zu erstellen, wird die folgende Fehlernachricht angezeigt:
{: tsSymptoms} 

`BXNUI0097E: Bevor Sie eine App hinzufügen können, muss Ihrer Organisation und Ihrer Region mindestens ein Bereich zugeordnet sein. Klicken Sie auf dem Dashboard auf die Option 'Bereich erstellen'. Wiederholen Sie den Vorgang, wenn der Bereich erstellt worden ist. `

Apps in {{site.data.keyword.Bluemix_notm}} müssen in Ihrer Organisation innerhalb eines Bereichs erstellt werden.
{: tsCauses} 

Wenden Sie eine der folgenden Methoden an,
um einen Bereich zu erstellen: 
{: tsResolve}
 
  * Wählen Sie auf dem Dashboard von {{site.data.keyword.Bluemix_notm}} die Organisation aus, in der Sie den Bereich erstellen möchten;
klicken Sie anschließend auf **Bereich erstellen**.
  * Geben Sie in der Befehlszeilenschnittstelle 'cf' Folgendes ein: `cf create-space <Name des Bereichs> -o <Name der Organisation>`.

  
## Apps verwenden denselben Domänennamen gemeinsam
{: #ts_domain_diff}

Es kann vorkommen, dass in {{site.data.keyword.Bluemix_notm}} von mehreren Apps dieselbe URL gemeinsam genutzt wird.

Dieses Problem kann auftreten, wenn Sie unterschiedlichen Apps in einem Bereich dieselbe URL-Route zuweisen.
{: tsCauses}

Beispiel: Sie übertragen die App 'myApp1' per Push-Operation an {{site.data.keyword.Bluemix_notm}} und legen als Domäne 'mynewapp.stage1.mybluemix.net' fest. Anschließend übertragen Sie eine weitere App mit dem Namen 'myApp2' per Push-Operation in denselben Bereich und legen für eine der URL-Routen den Namen 'mynewapp.stage1.mybluemix.net' fest. Die Route ist jetzt beiden Apps zugeordnet.

Hierbei handelt es sich um ein unterstütztes Verhalten von {{site.data.keyword.Bluemix_notm}}; Sie können dieses Verfahren verwenden, um beim Upgrade einer App Ausfallzeiten vollständig zu vermeiden. Weitere Informationen finden Sie unter [Using Blue-Green Deployment to Reduce Downtime and Risk ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://docs.cloudfoundry.org/devguide/deploy-apps/blue-green.html){: new_window}.
{: tsResolve}
  

## Administratoren können über die {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle nicht alle Organisationen anzeigen
{: #ts_ui_org}

Wenn Sie die {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle als Administrator verwenden, können Sie nicht alle Organisationen zu Verwaltungszwecken anzeigen. Sie können nur die Organisationen anzeigen und verwalten, zu denen Sie gehören.

Als Administrator können Sie nicht alle Organisationen über die {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle anzeigen.
{: tsSymptoms}

Dies ist eine Einschränkung der {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle.
{: tsCauses}

Sie können über die Befehlszeilenschnittstelle 'cf' Befehle wie `cf orgs`, `cf create-org` oder `cf delete-org` verwenden, um alle Organisationen zu verwalten. Für eine vollständige Liste der cf-Befehle geben Sie `cf help` ein.
{: tsResolve}
	
## Kreditkarte kann nicht hinzugefügt werden
{: #ts_addcc}

Sie können Ihre Kreditkarteninformationen nicht übergeben, um Ihr Testkonto in ein Konto für nutzungsabhängige Zahlung umzuwandeln.

Die Schaltfläche **Übergeben** auf der Seite 'Kreditkarte' hinzufügen ist inaktiviert.
{: tsSymptoms}

Dieses Problem tritt auf, wenn Sie auf der Seite 'Kreditkarte hinzufügen' nicht die korrekten Informationen eingegeben haben.
{: tsCauses}


Führen Sie die folgenden Schritte aus:
{: tsResolve}

  1. Füllen Sie auf der Seite 'Kreditkarte hinzufügen' alle erforderlichen Felder in den Abschnitten für die Kontaktinformationen, die Kontaktadresse und die Rechnungsadresse aus.
  2. Wählen Sie das Kontrollkästchen unter **Ich habe die allgemeinen Geschäftsbedingungen von IBM gelesen und stimme ihnen zu** aus und klicken Sie auf **Übergeben**. Der Abschnitt **Wählen Sie eine Zahlungsmethode aus** wird angezeigt.
  3. Geben Sie Ihre Kreditkartennummer, das Ablaufdatum Ihrer Karte und den Sicherheitscode auf Ihrer Karte ein. Anschließend klicken Sie auf **Übergeben**.
