---

copyright:
  years: 2015, 2017
  
lastupdated: "2017-03-02"

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 



# Fehlerbehebung für den Zugriff auf {{site.data.keyword.Bluemix_notm}} 
{: #accessing}


Allgemeine Probleme beim Zugriff auf {{site.data.keyword.Bluemix}} können sein, dass es Schwierigkeiten bei der Anmeldung bei {{site.data.keyword.Bluemix_notm}} gibt oder sich ein Konto dauerhaft im Wartestatus befindet. In vielen Fällen können Sie diese Probleme durch Ausführen weniger einfacher Schritte beheben.
{:shortdesc}

## Anmeldung bei {{site.data.keyword.Bluemix_notm}} nicht möglich: Falsches Kennwort
{: #ts_logintobm}

Sie müssen über ein gültiges Kennwort verfügen, das Ihrer IBMid zugeordnet ist, um sich bei der {{site.data.keyword.Bluemix_notm}}-Konsole anzumelden.

Sie müssen über ein gültiges Kennwort verfügen, das Ihrer IBMid oder SoftLayer-ID zugeordnet ist, um sich über das [Kundenportal](https://control.softlayer.com) anzumelden.

Wenn Sie versuchen, sich bei {{site.data.keyword.Bluemix_notm}} anzumelden, wird die folgende Fehlernachricht angezeigt:
{: tsSymptoms} 

`Das eingegebene Kennwort ist nicht korrekt.` 

Die IBMid und das Kennwort für die Anmeldung bei {{site.data.keyword.Bluemix_notm}} sind ungültig.
{: tsCauses} 
 
Verwenden Sie eine der folgenden Lösungen:
{: tsResolve}
 * Geben Sie das richtige Kennwort ein. Um zu prüfen, ob Ihre IBMid und das Kennwort gültig sind, können Sie auf die Seite 'Mein IBM Profil' wechseln. Klicken Sie dort auf **Anmelden** und geben Sie Ihre IBMid und das Kennwort auf der Anmeldeseite ein. 
 * Falls Sie Ihr Kennwort vergessen haben, klicken Sie auf **Kennwort vergessen**, um Ihr Kennwort zurückzusetzen. Rufen Sie anschließend erneut die [Bluemix-Konsole](https://console.{DomainName}) oder das [Kundenportal](https://control.softlayer.com) auf und melden Sie sich erneut an.
 * Wenn Sie Ihre IBMid vergessen haben oder weiterhin Probleme mit dem Kennwort vorliegen, suchen Sie auf der Site 'Worldwide IBM Registration Helpdesk' nach Hilfe. 
 * Um eine gültige IBMid und ein gültiges Kennwort anzufordern, rufen Sie die Seite 'Mein IBM Profil' auf und klicken Sie dann auf **Registrieren**.
  
**Hinweis:** Falls Sie sich auf der Seite für die Anmeldung bei IBM befinden und der Anmeldeprozess aus irgendeinem Grund unterbrochen wird (beispielsweise beim Zurücksetzen Ihres Kennworts), rufen Sie erneut die [Bluemix-Konsole](https://console.{DomainName}) oder das [Kundenportal](https://control.softlayer.com) auf und beginnen Sie den Anmeldeprozess erneut. 
 

## Anmeldung bei {{site.data.keyword.Bluemix_notm}} nicht möglich: Falsche Anmeldeberechtigungsnachweise
{: #ts_login_invalid_credentials}

Wenn Sie sich mit Ihrer IBMid anmelden, wird die folgende Nachricht angezeigt:
{: tsSymptoms}

`Es wurden falsche Anmeldeberechtigungsnachweise angegeben. Falls Ihrem Konto eine IBM ID zugeordnet ist, melden Sie sich bitte hier an.` 

* Sie haben zur Verwendung einer IBMid gewechselt, aber versucht, sich über das [Kundenportal](https://control.softlayer.com) mit Ihrem vorherigen SoftLayer-Benutzernamen und -Kennwort anzumelden.
{: tsCauses}

* Sie haben versucht, sich über das [Kundenportal](https://control.softlayer.com) anzumelden, aber Ihre IBMid und das zugehörige Kennwort in den Feldern für den Benutzernamen und das Kennwort eingegeben. 

Klicken Sie in der Nachricht auf den Link **hier** oder wechseln Sie zum Abschnitt für die Kontoanmeldung mit IBMid und klicken Sie auf **Mit IBM ID anmelden**.
{: tsResolve}

Verwenden Sie nicht die Felder **Benutzername** und **Kennwort**, die Sie für Ihre vorherige SoftLayer-ID verwendet haben.


## Anmeldung bei {{site.data.keyword.Bluemix_notm}} nicht möglich: Nicht erkannte IBMid oder E-Mail-Adresse
{: #ts_softlayer_username}

Wenn Sie sich bei der {{site.data.keyword.Bluemix_notm}}-Konsole anmelden, wird die folgende Nachricht angezeigt:
{: tsSymptoms} 

`Diese IBMid oder E-Mail wurde nicht erkannt.`

Sie haben versucht, sich bei der {{site.data.keyword.Bluemix_notm}}-Konsole anzumelden, jedoch keine gültige IBMid verwendet. Beispielsweise haben Sie keine vollständig qualifizierte E-Mail-Adresse für die IBMid eingegeben oder versucht, einen SoftLayer-Benutzernamen mit dem zugehörigen Kennwort zu verwenden.
{: tsCauses}
 
Sie müssen über eine gültige IBMid und ein Kennwort verfügen, um sich bei {{site.data.keyword.Bluemix_notm}} anmelden zu können.

 * Stellen Sie sicher, dass Sie eine vollständig qualifizierte E-Mail-Adresse für die IBMid eingeben.
 {: tsResolve}
 * Falls Sie einen SoftLayer-.Benutzer mit einer SoftLayer-ID verwenden, müssen Sie für jedes Konto, auf das Sie zugreifen können, im Kundenportal zur Authentifizierung mit IBMid wechseln, bevor Sie sich mit der Authentifizierung über IBMid amelden können. Weitere Informationen finden Sie unter [Zur IBMid wechseln](/docs/admin/softlayerlink.html#ibmid_switch).


## Anmeldung bei {{site.data.keyword.Bluemix_notm}} nicht möglich: IBMid ist keinem IBM Cloud-Konto zugeordnet
{: #ts_login_noswitch}

Wenn Sie sich mit Ihrer IBMid anmelden, wird die folgende Nachricht angezeigt:
{: tsSymptoms}

`Sie sind auf diese Seite gelangt, weil Ihre Authentifizierung erfolgreich war; allerdings ist diese IBMid keinem IBM Cloud-Konto zugeordnet. Wenn Sie dies für einen Fehler halten, wenden Sie sich an Ihren Kontoeigner oder Masterbenutzer.`

Sie haben sich über das [Kundenportal](https://control.softlayer.com) mit einer gültigen IBM ID angemeldet, aber in SoftLayer zur Authentifizierung mit IBM ID gewechselt.
{: tsCauses} 
 
Führen Sie die folgenen Prüfungen durch:
{: tsResolve}
 * Lassen Sie von Ihrem Masterbenutzer oder Kontoadministrator überprüfen, ob Sie zur Authentifizierung mit IBMid wechseln können. 
 * Stellen Sie sicher, dass Sie den Schritt für den Wechsel zur IBMid in Ihrem SoftLayer-Konto ausgeführt haben. Weitere Informationen finden Sie unter [Zur IBMid wechseln](/docs/admin/softlayerlink.html#ibmid_switch).
 * Stellen Sie sicher, dass Sie die Aktionen ausgeführt haben, die in der E-Mail für die **Zuordnung des SoftLayer-Benutzers zu einer IBMid** beschrieben sind. Prüfen Sie, ob die E-Mail in Ihrem Posteingang oder im Spamordner vorhanden ist. Um die E-Mail erneut abzurufen, weil sie beispielsweise abgelaufen ist, wechseln Sie im Steuerungsportal auf die Seite für die Bearbeitung des Benutzerprofils und klicken Sie auf **E-Mail erneut senden**. Setzen Sie sich alternativ mit dem [{{site.data.keyword.Bluemix_notm}}-Support ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](http://ibm.biz/bluemixsupport.com){: new_window} in Verbindung.

**Hinweis:** Falls Sie Ihre IBMid direkt über IBMid erstellt haben, empfangen Sie zwei E-Mails, die Sie verarbeiten müssen. Eine E-Mail stammt von der IBMid-Registrierung, die andere von Softlayer. Stellen Sie sicher, dass Sie die Aktionen ausführen, die in beiden E-Mails aufgeführt sind. 

Je nachdem, wie Ihr Konto eingerichtet wurde, können einige dieser Anmeldeoptionen auf Sie zutreffen: 
 * SoftLayer-Benutzer mit SoftLayer-IDs müssen sich über das [Kundenportal](https://control.softlayer.com) anmelden.
 * SoftLayer-Benutzer mit einer IBMid und mit oder ohne verknüpftes Bluemix-Konto können sich über das [Kundenportal](https://control.softlayer.com) anmelden, um das SoftLayer-Kundenportal zu öffnen, ober über die [Bluemix-Konsole](https://console.{DomainName}), um das Infrastruktur-Dashboard zu öffnen. 


## Anmeldung bei {{site.data.keyword.Bluemix_notm}} nicht möglich: IBMid ist keinem {{site.data.keyword.Bluemix_notm}}-Konto zugeordnet
{: #ts_unabletologin}

Wenn Sie sich bei {{site.data.keyword.Bluemix_notm}} anmelden, wird die folgende Nachricht angezeigt:
{: tsSymptoms} 
 
`Sie sind auf diese Seite gelangt, weil Ihre Authentifizierung erfolgreich war; allerdings ist diese IBMid keinem {{site.data.keyword.Bluemix_notm}}-Konto zugeordnet.`

Sie haben sich über die [Bluemix-Konsole](https://console.{DomainName}) mit einer gültigen IBM ID angemeldet, aber es wurde noch kein {{site.data.keyword.Bluemix_notm}}-Konto erstellt.
{: tsCauses} 

Führen Sie den Anmeldeprozess durch, um ein {{site.data.keyword.Bluemix_notm}}-Konto zu erstellen.
{: tsResolve}

Je nachdem, wie Ihr Konto eingerichtet wurde, können einige dieser Anmeldeoptionen auf Sie zutreffen: 
 * Bluemix-Benutzer ohne verknüpftes SoftLayer-Konto müssen sich über die Bluemix-Konsole anmelden.
 * Bluemix-Benutzer mit verknüpftem SoftLayer-Konto können sich über die [Bluemix-Konsole](https://console.{DomainName}) oder das [Kundenportal](https://control.softlayer.com) anmelden.
 

## Anmeldung bei {{site.data.keyword.Bluemix_notm}} nicht möglich: Konsole wird nicht geöffnet
{: #ts_login_stalls}

Wenn Sie sich mit Ihrer IBMid anmelden, wird eine Nachricht über die erfolgreiche Anmeldung ausgegeben, aber die [Bluemix-Konsole](https://console.{DomainName}) oder das [Kundenportal](https://control.softlayer.com) nicht erneut angezeigt.
{: tsSymptoms}

Verwenden Sie eine der folgenden Lösungen:
{: tsResolve}
 * Schließen Sie Ihren Browser, löschen Sie Cookies sowie den Inhalt des Cache und versuchen Sie erneut, sich anzumelden. 
 * Stellen Sie sicher, dass Sie zur Anmeldung die [Bluemix-Konsole](https://console.{DomainName}) oder das [Kundenportal](https://control.softlayer.com) und nicht direkt den Service für die Authentifizierung mit IBMid verwenden. 
 
 
## Anmeldung bei {{site.data.keyword.Bluemix_notm}} nicht möglich: Anmeldung mit IBMid wird nicht vollständig ausgeführt
{: #ts_login_ibmid}

Wenn Sie sich bei {{site.data.keyword.Bluemix_notm}} anmelden, wird die Authentifizierung mit der IBMid nicht vollständig abgeschlossen.
{: tsSymptoms}

Möglicherweise besteht ein Problem beim Service für die Authentifizierung mit IBMid.
{: tsCauses}

Überprüfen Sie den Status des Service auf der Seite [IBM BlueID ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://new.wind.ibmcloud.com/webapp/#/status/a1a0c5d743d94a6a9597087541564d8e){: new_window} und wiederholen Sie anschließend den Versuch.
{: tsResolve}


## Anmeldung bei {{site.data.keyword.Bluemix_notm}} nicht möglich: Konto ist im Wartestatus
{: #ts_accntpding}

Falls sich Ihr Konto im Wartestatus befindet, können Sie sich nicht bei {{site.data.keyword.Bluemix_notm}} anmelden.
 
Wenn Sie sich für ein {{site.data.keyword.Bluemix_notm}}-Testkonto registriert haben, kann es vorkommen, dass Sie sich nicht an {{site.data.keyword.Bluemix_notm}} anmelden können. Die folgende Nachricht wird angezeigt:
{: tsSymptoms}

<code>Ihr Konto befindet sich im Zustand 'Anstehend'. Es kann bis zu 24 Stunden dauern, bis Sie eine Bestätigungs-E-Mail für Ihr Konto erhalten. Überprüfen Sie außerdem Ihren Spamordner. Wenn Sie trotzdem keine E-Mail-Bestätigung erhalten haben, wenden Sie sich an <a href="http://ibm.biz/bluemixsupport.com" target="_blank">Bluemix-Support</a>.</code>

Wenn Sie sich für ein {{site.data.keyword.Bluemix_notm}}-Testkonto registriert haben, erhalten Sie eine Bestätigungs-E-Mail. Sie müssen auf den Link in dieser Bestätigungs-E-Mail klicken, um den Registrierungsprozess abzuschließen.
{: tsCauses} 

Die Bestätigungs-E-Mail wird an die E-Mail-Adresse gesendet, die Sie angegeben haben. Überprüfen Sie Ihren Posteingang und Ihren Spamordner. Falls Sie die Bestätigungs-E-Mail nicht erhalten haben, setzen Sie sich mit dem [{{site.data.keyword.Bluemix_notm}}-Support ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](http://ibm.biz/bluemixsupport.com){: new_window} in Verbindung.  
{: tsResolve}


## Es sind nicht gespeicherte Änderungen vorhanden
{: #ts_unsaved_changes}

Wenn Sie zur Detailseite der App navigieren, können Sie möglicherweise keine Aktionen ausführen und werden aufgefordert, Änderungen zu speichern, bevor Sie fortfahren. 

Wenn Sie versuchen, Ihre App oder Services auf der Detailseite der App zu prüfen, empfangen Sie immer wieder die folgende Fehlernachricht:
{: tsSymptoms} 

`Es gibt nicht gespeicherte Änderungen auf Seite 'Name der App'. Speichern oder verwerfen Sie die Änderungen.`

Wenn Sie Ihre Maus über das Feld **INSTANCES** (Instanzen) oder **MEMORY QUOTA** (Speicherkontingent) im Teilfenster für die Laufzeit bewegen, ändern sich die Werte. Dieses Verhalten ist wie vorgesehen. Allerdings werden Sie von der Fehlernachricht aufgefordert, die Speicher- oder Instanzeinstellungen zu speichern, bevor Sie von der Seite wegnavigieren. 
{: tsCauses}

Schließen Sie das Nachrichtenfenster und klicken Sie auf die Schaltfläche **ZURÜCKSETZEN** in Ihrem Laufzeitfenster. 
{: tsResolve} 
  
    
## Automatische Funktionsübernahme zwischen {{site.data.keyword.Bluemix_notm}}-Regionen nicht verfügbar
{: #ts_failover}

Die automatische Funktionsübernahme zwischen {{site.data.keyword.Bluemix_notm}}-Regionen
kann nicht verwendet werden. Sie können allerdings einen DNS-Anbieter nutzen, der eine Funktionsübernahme zwischen mehreren
IP-Adressen als Ausweichlösung unterstützt.

Wenn eine {{site.data.keyword.Bluemix_notm}}-Region nicht mehr verfügbar ist, sind auch die Apps, die in dieser Region ausgeführt werden, nicht mehr verfügbar, selbst dann nicht, wenn dieselben Apps in einer anderen {{site.data.keyword.Bluemix_notm}}-Region ausgeführt werden.
{: tsSymptoms}
 
{{site.data.keyword.Bluemix_notm}}
bietet noch keine automatische Funktionsübernahme zwischen zwei Regionen an.
{: tsCauses}
 
Sie können einen
DNS-Anbieter nutzen, der eine intelligente Funktionsübernahme zwischen mehreren ID-Adressen
unterstützt, und Ihre DNS-Einstellungen zur Aktivierung der automatischen Funktionsübernahme
zwischen {{site.data.keyword.Bluemix_notm}}-Regionen manuell konfigurieren. DNS-Anbieter mit dieser Funktion sind z. B. NSONE, Akamai, Dyn.
{: tsResolve}

Wenn Sie Ihre DNS-Einstellungen konfigurieren, müssen Sie die öffentlichen IP-Adressen der {{site.data.keyword.Bluemix_notm}}-Regionen angeben, in denen Ihre Apps ausgeführt werden. Verwenden Sie zum Abrufen der öffentlichen IP-Adresse
einer {{site.data.keyword.Bluemix_notm}}-Region
den Befehl `nslookup`. Sie können in einem Befehlszeilenfenster beispielsweise
den folgenden Befehl eingeben:
```
nslookup stage1.mybluemix.net
```

## Hinzufügen von Benutzern zu Organisation nicht möglich
{: #ts_adduser}

Zur Arbeit für eine Organisation können mehrere Benutzer eingeladen werden. Sie können nur Benutzer in Ihre Organisation einladen, wenn Sie der Kontoeigner sind oder wenn Sie sowohl Manager als auch Mitglied der Organisation sind.
 
Sie können den Link **Neuen Benutzer einladen** im Abschnitt **Organisation verwalten** nicht anzeigen.
{: tsSymptoms}

Nur die folgenden {{site.data.keyword.Bluemix_notm}}-Benutzer können Benutzer zu einer Organisation einladen:
{: tsCauses}
  * Der Kontoeigner der Organisation
  * Organisationsmanager, die auch Mitglieder, aber nicht Collaborator der Organisation sind
  
In {{site.data.keyword.Bluemix_notm}} können Sie entweder ein Mitglied oder ein Collaborator einer Organisation sein:

<dl><dt>Collaborator</dt>
<dd>Sie sind Collaborator einer Organisation, wenn Sie bereits über ein {{site.data.keyword.Bluemix_notm}}-Konto verfügen und Sie von einer anderen Person zur Organisation eingeladen werden.</dd>
<dt>Mitglied</dt>
<dd>Sie sind ein Mitglied einer Organisation, wenn Sie nicht über ein {{site.data.keyword.Bluemix_notm}}-Konto verfügen, Sie aber von einer Person zur Organisation eingeladen werden und Sie sich im Rahmen der Einladung bei {{site.data.keyword.Bluemix_notm}} registrieren.</dd>
</dl>

Sie können nicht Benutzer zu Ihrer Organisation einladen, wenn Sie ein Collaborator der Organisation sind; dies ist auch dann nicht möglich, wenn Sie ein Organisationsmanager sind.

**Hinweis:** Alle Organisationsmanager, einschließlich der Manager, die auch Collaborator einer Organisation sind, können Benutzer hinzufügen, ändern und entfernen, die bereits in der Organisation sind.

Wenn Sie nicht Benutzer zu Ihrer Organisation einladen können und zum Einladen eine andere Rolle benötigen, kontaktieren Sie Ihren Organisationsmanager, damit er Ihre Rolle ändert. Führen Sie die folgenden Schritte aus, um festzustellen, wer Ihr Organisationsmanager ist:
{: tsResolve}

  1. Rufen Sie das {{site.data.keyword.Bluemix_notm}}-Dashboard auf. Klicken Sie in der Menüleiste auf das Menüelement **Konto** und anschließend auf **Organisationen verwalten**.
  2. Wechseln Sie zu Ihrer Organisation und zeigen Sie die Informationen zum Organisationsmanager in der Registerkarte **Benutzer** an.  
  
Wenn Sie nicht in der Lage sind, Benutzer einzuladen, weil Sie ein Mitarbeiter und kein Mitglied sind, müssen Sie Ihr vorheriges {{site.data.keyword.Bluemix_notm}}-Konto löschen und anschließend eingeladen werden, als Mitglied der Organisation am Konto teilzunehmen. Um Ihr vorheriges Konto zu löschen und dem Konto als Mitglied beizutreten, führen Sie die folgenden Schritte durch: 

  1. Wenden Sie sich an den [{{site.data.keyword.Bluemix_notm}}-Support ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](http://ibm.biz/bluemixsupport){: new_window}, um ein Support-Ticket zu öffnen und die Löschung Ihres Kontos anzufordern. Wenn Sie Daten besitzen, die zu Ihrem alten Konto gehören, und die Sie speichern und in das neue Konto verschieben möchten, beziehen Sie diese Informationen in Ihre E-Mail ein. 
  2. Nachdem Ihr Konto gelöscht ist, lassen Sie sich von dem Benutzer mit der Organisationsmanager-Rolle als Organisationsmanager in die Organisation einladen. Anschließend melden Sie sich über die Einladung bei {{site.data.keyword.Bluemix_notm}} an. 

## Registrierung von Benutzern im Stapelbetrieb wird nicht unterstützt
{: #ts_batchregistration}

Wenn Sie Benutzer für {{site.data.keyword.Bluemix_notm}} registrieren, müssen Sie für jeden Benutzer eine individuelle Registrierung vornehmen.

{{site.data.keyword.Bluemix_notm}} bietet keine Funktionalität, um mehrere Benutzer gleichzeitig zu registrieren.
{: tsSymptoms}
 
{{site.data.keyword.Bluemix_notm}} unterstützt nicht die Registrierung von Benutzern im Stapelbetrieb. Zum Registrieren von Benutzern für {{site.data.keyword.Bluemix_notm}}, müssen Sie für jeden einzelnen Benutzer eine individuelle Registrierung vornehmen.
{: tsCauses}
 
Zum Registrieren mehrerer Benutzer für {{site.data.keyword.Bluemix_notm}} führen Sie für jeden einzelnen Benutzer folgende Schritte aus:
{: tsResolve}

  1. Klicken Sie in der {{site.data.keyword.Bluemix_notm}}-Konsole auf **Registrieren**.
  2. Führen Sie die Schritte aus, indem Sie dem Assistenten folgen.
    

## Laden einer {{site.data.keyword.Bluemix_notm}}-Seite nicht möglich
{: #ts_err}

Wenn Sie die {{site.data.keyword.Bluemix_notm}}-Konsole verwenden, kann es vorkommen, dass Sie eine {{site.data.keyword.Bluemix_notm}}-Seite nicht laden können. Stattdessen können die Fehlernachrichten BXNUI0001E oder BXNUI0016E angezeigt werden.
 
Während der Verwendung der {{site.data.keyword.Bluemix_notm}}-Konsole kann eine der folgenden Fehlernachrichten angezeigt werden:
{: tsSymptoms}

`BXNUI0001E: Die Seite wurde nicht geladen, weil von Bluemix nicht erkannt wurde, ob eine Sitzung vorhanden ist.`

`BXNUI0016E: Die Apps und Services wurden nicht abgerufen, da eine Bluemix-Seite nicht geladen wurde.`

Führen Sie nach Bedarf eine oder mehrere der folgenden Aktionen aus:
{: tsResolve}

  * Aktualisieren Sie den Browser oder starten Sie ihn erneut. 
  * Melden Sie sich bei {{site.data.keyword.Bluemix_notm}} ab und anschließend wieder an. 
  * Verwenden Sie den persönlichen Browsingmodus des Browsers. 
  * Löschen Sie Cookies und den Inhalt des Browser-Cache.
  * Verwenden Sie einen anderen Browser. Informationen zu den Versionen der Browser, die von {{site.data.keyword.Bluemix_notm}} unterstützt werden, finden Sie in den [Voraussetzungen für Bluemix](/docs/overview/whatisbluemix.html#prereqs).
  * Wenn Sie die cf-Befehlszeilenschnittstelle installiert haben, geben Sie den Befehl `cf apps` ein, um anzuzeigen, ob die App aktiv ist.
