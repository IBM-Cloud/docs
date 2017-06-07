---



copyright:

  years: 2016, 2017
lastupdated: "2017-03-17"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Zur IBMid wechseln
Für die Authentifizierung in SoftLayer wird jetzt eine IBMid verwendet, die eine einzige Anmeldung bei allen {{site.data.keyword.Bluemix_notm}}-Komponenten ermöglicht. Es wird ein Wechsel für vorhandene SoftLayer-Konten zur Authentifizierung mit IBMid ermöglicht. Sie werden von einem Migrationsassistenten durch diesen Wechsel geführt. 
{:shortdesc}

Sie können diesen Wechsel zur IBMid jederzeit abbrechen, solange der Prozess noch nicht abgeschlossen ist. Bei jeder Anmeldung wird jedoch die Auffordung zum Wechsel zur IBMid angezeigt. Jedes SoftLayer-Konto, das mit einem {{site.data.keyword.Bluemix_notm}}-Konto verknüpft werden soll, muss zu einer eindeutigen IBMid mit einer eindeutigen E-Mail-Adresse gehören.

Führen Sie folgende Schritte aus, um von Ihrem bisherigen SoftLayer-Konto zu einer IBMid zu wechseln:
1. Melden Sie sich bei Ihrem SoftLayer-Konto an und klicken Sie auf **OK**, wenn die Eingabeaufforderung zum Wechseln zu einem IBMid angezeigt wird.

   Wenn Sie Masterbenutzer sind und keine Eingabeaufforderung zum Wechseln zur IBMid im {{site.data.keyword.slportal}} angezeigt wird, [wenden Sie sich an den IBM Support](/docs/support/index.html#contacting-support), um Hilfe zu erhalten.
  
   Falls Sie bereits angemeldet sind und bei der Eingabeaufforderung auf **Später** geklickt haben, jedoch in der aktuellen Sitzung zur Authentifizierung mit IBMid wechseln möchten, rufen Sie die Seite für die Bearbeitung des Benutzerprofils auf und klicken Sie auf **Zu IBM ID wechseln**.

2. Befolgen Sie die Anweisungen im Assistenten, um Ihre IBMid zu erstellen. 

   Geben Sie eine E-Mail-Adresse ein, die aktuell nicht von einer IBMid verwendet wird. Diese E-Mail-Adresse wird als Benutzername für die neue IBMid verwendet; an diese Adresse wird Ihr Registrierungscode gesendet, nachdem die IBMid erstellt wurde. Sie können die E-Mail-Adresse, die der IBMid zugeordnet ist, zu einem späteren Zeitpunkt aktualisieren, jedoch nicht den Benutzernamen ändern.

3. Wenn Sie Ihren Registrierungscode erhalten, klicken Sie auf den Link in der E-Mail oder kopieren Sie die URL in einen Browser und geben Sie Ihren Registrierungscode ein.

   Der Registrierungscode ist sieben Tage lang gültig und kann nur einmal verwendet werden.
  
4. Nachdem Sie Ihren Registrierungscode übergeben haben, melden Sie sich mit Ihrer IBMid am {{site.data.keyword.slportal}} an.

   Wechseln Sie bei der Eingabeaufforderung 'Kontoanmeldung' in den Abschnitt für die **Kontoanmeldung mit IBMid** und klicken Sie auf **Mit IBM ID anmelden**. Verwenden Sie nicht die Felder **Benutzername** und **Kennwort**, die Sie zuvor mit Ihrer SoftLayer-ID verwendet haben.

Wenn Sie ein neuer Kunde sind, werden Sie beim Überprüfen Ihrer Bestellung nach Ihrer vorhandenen IBMid gefragt oder zum Erstellen einer neuen IBMid aufgefordert. 
  * Zur Verwendung einer bestehenden IBMid geben Sie den Benutzernamen oder die E-Mail-Adresse der IBMid ein, falls diese eindeutig ist (also nicht von mehreren IBMids gemeinsam genutzt wird).
  
  * Geben Sie zum Erstellen einer neuen IBMid eine E-Mail-Adresse ein, die noch nicht von einer IBMid verwendet wird. Diese E-Mail-Adresse ist der Benutzername für die IBMid; an diese Adresse wird Ihr Registrierungscode gesendet, nachdem die IBMid erstellt wurde. Sie können die E-Mail-Adresse, die der IBMid zugeordnet ist, zu einem späteren Zeitpunkt aktualisieren, jedoch nicht den Benutzernamen ändern. 
  
Informationen zur Lösung von Problemen, die bei der Anmeldung mit Ihrer IBMid auftreten könnten, finden Sie unter [Fehlerbehebung für den Zugriff auf Bluemix](/docs/troubleshoot/ts_accessing.html#accessing).

## Benutzerkonten für die Authentifizierung mit IBMid aktivieren
{: #link_accounts_resellers}

In einigen Fällen muss ein Reseller oder Distributor aktivieren, dass die Authentifizierung mit IBMid für ein Konto verwendet werden kann, bevor ein Benutzer zu einer IBMid wechseln kann. 

  * Die Authentifizierung mit IBMid ist für jedes vorhandene Benutzerkonto erforderlich, das mit einem Bluemix-Konto verknüpft werden soll. Anschließend muss jeder Benutzer den Prozess abschließen, um mithilfe des Migrationsassistenten zu einer IBMid zu wechseln, wie im vorherigen Abschnitt beschrieben. Wenden Sie sich an den [IBM Support](/docs/support/index.html#contacting-support), um ein vorhandenes SoftLayer-Konto für die Verwendung der Authentifizierung mit IBMid zu aktivieren. 
  
  * Um sicherzustellen, dass neue Benutzerkonten mit einer IBMid erstellt werden, muss das Attribut `CREATE_NEW_ACCOUNT_WITH_IBMid_AUTHENTICATION` auf das direkte Masterbenutzerkonto festgelegt werden. Wenden Sie sich an den [ IBM Support ](/docs/support/index.html#contacting-support) oder Ihren Anbieter, um das Attribut für Ihre Konten festzulegen.  

## IBMid-Benutzerkonten verknüpfen
{: #link_user_accounts}

Nachdem die Benutzerkonten zur Authentifizierung mit IBMid gewechselt haben, können Reseller und Distributoren SoftLayer- und {{site.data.keyword.Bluemix_notm}}-Konten verknüpfen, um die kombinierten Infrastruktur- und Plattformressourcen zu nutzen. 

**Hinweis**:
  * Der Masterbenutzer des Kontos, das verknüpft wird, muss eine IBMid haben.
  * Jedes Benutzerkonto, das mit einem {{site.data.keyword.Bluemix_notm}}-Konto verknüpft wird, muss zu einer eindeutigen IBMid mit einer eindeutigen E-Mail-Adresse gehören. Auch wenn eine einzelne IBMid mehreren SoftLayer-Konten zugeordnet sein kann, müssen Sie die Masterbenutzer für jedes Konto in eine jeweils eindeutige IBMid ändern. Wenden Sie sich an den [IBM SoftLayer-Support ![Symbol für externen Link](../icons/launch-glyph.svg)](https://knowledgelayer.softlayer.com/topic/support){: new_window}, um den Masterbenutzer für ein SoftLayer-Konto zu ändern.
  * Wenn Sie einem verknüpften Konto neue Benutzer hinzufügen, müssen Sie sie sowohl dem SoftLayer-Konto als auch dem {{site.data.keyword.Bluemix_notm}}-Konto hinzufügen, damit sie Zugriff auf alle Funktionen in der einheitlichen Konsole erhalten. 
  
Führen Sie die folgenden Schritte aus, um jedes Konto mit einem {{site.data.keyword.Bluemix_notm}}-Konto zu verknüpfen:
1. Um eine Verknüpfung mit einem vorhandenen {{site.data.keyword.Bluemix_notm}}-Konto zu erstellen oder um ein neues zu erstellen, melden Sie sich als Masterbenutzer bei Ihrem SoftLayer-Konto an und klicken Sie auf den {{site.data.keyword.Bluemix_notm}}-Link. 

   Die IBMid, die der Masterbenutzer des SoftLayer-Kontos ist, muss der Eigner des {{site.data.keyword.Bluemix_notm}}-Kontos sein, zu dem die Verknüpfung hergestellt wird.  
   
2. Befolgen Sie die Eingabeaufforderungen im Assistenten und fügen Sie die Benutzer im SoftLayer-Konto dem {{site.data.keyword.Bluemix_notm}}-Konto hinzu.
3. Nachdem Sie das Konto verknüpft haben, informieren Sie die Endbenutzer der einzelnen Konten darüber, dass sie zur IBMid migrieren müssen. Dabei sollte das im vorherigen Abschnitt beschriebene Verfahren verwendet werden.

**Empfehlung**: Migrieren Sie nur Endbenutzerkonten zur IBMid. Migrieren Sie keine Brandkonten. Dies sind übergeordnete Konten für Endbenutzerkonten und enthalten keine Ressourcen. Brandkontenbenutzer, die zur IBMid migrieren, können sich anschließend nicht mehr bei beim BAP (Brand Agent Portal) anmelden.  
  
