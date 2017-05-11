---



copyright:

  years: 2015, 2017
lastupdated: "2017-01-09"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# {{site.data.keyword.Bluemix_notm}}-Konto verwalten
{: #mngacct}

Klicken Sie auf den Link **Konto**, um Einstellungen für Benachrichtigungen festzulegen, Ihre Kontonutzung oder Ihre Rechnung anzuzeigen.
{:shortdesc}

## {{site.data.keyword.Bluemix_notm}}-Anmeldung
{: #signup}

Sie können sich unter Verwendung einer vorhandenen IBMid, durch Erstellung einer neuen IBMid oder unter Verwendung einer eingebundenen ID für ein {{site.data.keyword.Bluemix_notm}}-Konto anmelden. Eine eingebundene ID ist eine ID innerhalb einer Unternehmensdomäne, die für IBM registriert wurde, um über die Domäne und die Benutzerberechtigungsnachweise auf IBM Webanwendungen zugreifen zu können.  

Die Anmeldung an {{site.data.keyword.Bluemix_notm}} mit einer eingebundenen ID ist nur dann möglich, wenn Ihr Unternehmen bereits bei IBM registriert wurde.  Nach der Registrierung der Unternehmensdomäne bei IBM können sich die Benutzer unter Verwendung der bestehenden Benutzerberechtigungsnachweise des Unternehmens bei IBM Produkten und Services anmelden. Die Authentifizierung erfolgt über den Identitätsprovider Ihres Unternehmens. Bei der Anmeldung an {{site.data.keyword.Bluemix_notm}} mit einer eingebundenen ID werden Sie zur Anmeldung über die Anmeldeseite Ihres Unternehmens aufgefordert. Weitere Informationen zum Anfordern der Registrierung der Domäne Ihres Unternehmens oder Ihrer Organisation bei IBM und zu den hierfür erforderlichen Schritten finden Sie in der Veröffentlichung [IBMid Enterprise Federation Adoption Guide ![Symbol für externen Link](../icons/launch-glyph.svg)](https://ibm.box.com/v/IBMid-Federation-Guide){: new_window}. Für die Registrierung eingebundener IDs muss ein IBM Sponsor, wie beispielsweise ein Angebotsmanager oder Kundenansprechpartner, kontaktiert werden.

| Anmeldemethoden | Details |    
|-----------------|---------|
|Vorhandene IBMid | Wenn Sie bereits über eine IBMid verfügen, können Sie sich mit Ihren bestehenden Berechtigungsnachweisen für andere IBM Produkte und Services bei {{site.data.keyword.Bluemix_notm}} anmelden. Bei der Anmeldung ist die Eingabe einer Telefonnummer erforderlich. |
|Neue IBMid | Wenn Sie noch keine IBMid besitzen, können Sie diese erstellen. Mit einer IBMid können Sie sich mit nur einem Benutzernamen für alle IBM Produkte und Services, einschließlich {{site.data.keyword.Bluemix_notm}}, anmelden. Für die neuen Berechtigungsnachweise müssen Sie Ihre persönlichen Daten (Vor- und Nachname, Telefonnummer und Kennwort) eingeben. Sie können sich mit dieser IBMid anmelden, wenn Sie andere IBM Produkte oder Services verwenden.  |
|Eingebundene ID | Wenn Ihr Unternehmen die Registrierung der Benutzerberechtigungsnachweise für die Unternehmensdomäne bei IBM angefordert hat, können Sie sich mit den Benutzerberechtigungsnachweisen bei {{site.data.keyword.Bluemix_notm}} anmelden, die Sie bereits für die Unternehmensanmeldung verwenden. Bei der Anmeldung ist die Eingabe einer Telefonnummer erforderlich. |
{:caption="Tabelle 1. Anmeldemethoden" caption-side="top"}

## Benachrichtigungen einstellen
{: #notifications}

Klicken Sie auf **Konto** &gt; **Benachrichtigungen**, um allgemeine Benachrichtigungen über Konten und Ausgaben festzulegen. Ausgabebenachrichtigungen sind nur für Eigener eines nutzungsabhängigen {{site.data.keyword.Bluemix_notm}}-Kontos oder -Abonnementkontos verfügbar.

Sie können Plattform-E-Mail-Benachrichtigungen für {{site.data.keyword.Bluemix_notm}}-Vorfälle und die geplante Instandhaltung festlegen und Sie können Ausgabebenachrichtigungen definieren, durch die Sie gewarnt werden, wenn sich die Ausgaben für Ihr Konto dem festgelegten Schwellenwert nähern. Führen Sie die folgenden Tasks aus, um unterschiedliche Benachrichtigungstypen für Ihr Konto festzulegen.

### Plattformbenachrichtigungen einstellen

Klicken Sie auf **Konto** &gt; **Benachrichtigungen** &gt; **Plattform**, um den Erhalt von E-Mail-Benachrichtigungen für {{site.data.keyword.Bluemix_notm}}-Vorfälle und geplante Wartungsmaßnahmen festzulegen. Sie können jede einzelne Option auswählen oder abwählen, um die E-Mail-Benachrichtigung zu aktivieren oder zu inaktivieren.

<!-- staging only

**Note**: You are always alerted by email about emergencies and pricing changes.

On the **Platform** tab you can also customize notifications for your orgs, spaces, or applications. Complete the following steps to add a customized notification:

<ol>
<li>Select **Add a Notification**.</li>
<li>Use the search field to find the org, application, service, or resource that you want to set a notification for, or expand the item in the pre-populated list.</li>
<li>Select *Email* to set the notification type.</li>
</ol>

staging only end -->

### Ausgabebenachrichtigungen einstellen
{: #spendingnotifications}

Wenn Sie Eigner eines {{site.data.keyword.Bluemix_notm}}-Abonnementkontos oder eines nutzungsabhängigen Kontos sind, können Sie E-Mail-Benachrichtigungen über Ausgaben konfigurieren. Legen Sie Benachrichtigungen über Gesamtsumme, Laufzeit, Container und Serviceausgaben sowie Ausgaben für einzelne Services ausschließlich der Services anderer Anbieter fest. Sie erhalten Benachrichtigungen, wenn Sie 80 %, 90 % und 100 % des angegebenen Schwellenwerts für die Ausgaben erreicht haben. Sie können jede Benachrichtigung über Ausgaben jederzeit bearbeiten, wenn sich Ihre Anforderungen ändern.

Führen Sie die folgenden Schritte aus, um E-Mail-Benachrichtigungen für Ausgabenlimits einzurichten:

<ol>
<li>Klicken Sie auf **Konto** &gt; **Benachrichtigungen** &gt; **Ausgaben**.</li>
<li>Geben Sie einen numerischen Wert ein, um das Ausgabelimit für das Auslösen einer Benachrichtigung für jeden Typ der Benachrichtigung festzulegen:<br />
<ul>
<li>Gesamtausgaben - Konto</li>
<li>Gesamtausgaben - Laufzeit</li>
<li>Gesamtausgaben - Services</li>
<li>Gesamtausgaben - Container</li>
<li>Ausgaben für einen bestimmten Service</li>
</ul>
</li>
<li>Wenn Sie damit fertig sind, klicken Sie auf **Speichern**.</li>
</ol>

**Hinweis:** Wenn Sie über ein Testkonto verfügen, können Sie ein Upgrade auf ein Abonnementkonto oder ein nutzungsabhängiges Konto durchführen, um Ausgabelimits festzulegen. Weitere Informationen zu nutzungsabhängigen Konten und Abonnementkonten finden Sie unter [Wie wird abgerechnet?](/docs/pricing/index.html#pay-accounts).

## Nutzung anzeigen
{: #acctusage}

Als Kontoeigner oder Abrechnungsmanager einer Organisation können Sie die Seite 'Nutzungsdashboard' verwenden, um die Gebühren für die Laufzeiten, Container, Services und den Support, die monatlich in Ihrer Organisation genutzt werden, in Echtzeit anzuzeigen. Sie können die GB-Stunden für Laufzeiten und die Servicenutzung in allen Regionen anzeigen oder eine bestimmte Region für die Anzeige auswählen.

Um die Seite 'Nutzungsdashboard' zu öffnen, klicken Sie auf **Konto** &gt; *Name_des_eigenen_Kontos* &gt; **Nutzungsdashboard**. Abrechnungsmanager können nur die Details für die Organisationen anzeigen, in denen ihnen die Rolle des Abrechnungsmanagers zugewiesen ist.

Dem Kontoeigner werden die Gebühren für die Gesamtnutzung, die für alle Organisationen anfallen, am Ende jedes Abrechnungszyklus in Rechnung gestellt. Als Kontoeigner können Sie die Nutzungszusammenfassung nach Region und Organisation filtern. Sie können ferner auf einen bestimmten Monat klicken, um die Nutzung für diesen Monat anzuzeigen. Wählen Sie in der Liste **Organisation** die Option **Alle Organisationen** aus, um die Nutzung für alle Organisationen im Konto anzuzeigen.

## Abrechnungsdaten aktualisieren
{: #account_billing}

Als Kontoeigner können Sie gespeicherte Kreditkarteninformationen, die zu Ihrem {{site.data.keyword.Bluemix_notm}}-Konto gehören, bearbeiten, hinzufügen oder entfernen. Klicken Sie auf **Konto** &gt; *Name_des_eigenen_Kontos* &gt; **Abrechnung**.

Wenn Sie ein SoftLayer-Konto mit Ihrem {{site.data.keyword.Bluemix_notm}}-Konto verknüpft haben, lesen Sie den Abschnitt [Rechnungsstellung für {{site.data.keyword.Bluemix_notm}}-Nutzung bei verknüpften Konten](/docs/admin/softlayerlink.html#bill_usage). Dort finden Sie weitere Informationen zur Abrechnung.
