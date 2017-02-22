---

copyright:
  years: 2015, 2017
  
lastupdated: "2017-01-11"

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 



# Fehlerbehebung für den Zugriff auf {{site.data.keyword.Bluemix_notm}} 
{: #accessing}


Ein allgemeines Problem in Bezug auf den Zugriff auf {{site.data.keyword.Bluemix}} kann sein, dass sich ein Benutzer nicht an {{site.data.keyword.Bluemix_notm}} anmelden kann oder dass sich ein Konto dauerhaft im Wartestatus befindet. In vielen Fällen können Sie diese Probleme jedoch durch Ausführen weniger einfacher Schritte beheben. 
{:shortdesc}

## Anmelden an {{site.data.keyword.Bluemix_notm}} nicht möglich
{: #ts_unabletologin}

Sie müssen über ein gültiges {{site.data.keyword.Bluemix_notm}}-Konto verfügen, um sich anmelden zu können.


Wenn Sie versuchen, sich bei {{site.data.keyword.Bluemix_notm}} anzumelden, wird eine der folgenden Fehlermeldungen angezeigt: 
{: tsSymptoms} 

 * Vom Kundenportal
  
   `Sie sind auf diese Seite gelangt, weil Ihre Authentifizierung erfolgreich war; allerdings ist diese IBMid keinem IBM Cloud-Konto zugeordnet. Wenn Sie dies für einen Fehler halten, wenden Sie sich an Ihren Kontoeigner oder Masterbenutzer.`

 * Von der {{site.data.keyword.Bluemix_notm}}-Konsole
  
  `Sie sind auf diese Seite gelangt, weil Ihre Authentifizierung erfolgreich war; allerdings ist diese IBMid keinem {{site.data.keyword.Bluemix_notm}}-Konto zugeordnet.`


Einer der wahrscheinlichsten Gründe für diese Fehlernachricht ist, dass Sie noch kein {{site.data.keyword.Bluemix_notm}}-Konto eingerichtet haben oder dass Sie zur IBMid-Authentifizierung wechseln müssen. 
{: tsCauses} 
 

Folgen Sie dem Anmeldeprozess, um ein {{site.data.keyword.Bluemix_notm}}-Konto zu erstellen oder sich an Ihren Masterbenutzer oder Kontoadministrator zu wenden, um zur IBMid zu wechseln. 
{: tsResolve}

Je nachdem, wie Ihr Konto eingerichtet wurde, können einige dieser Anmeldeoptionen auf Sie zutreffen: 
 * SoftLayer-Benutzer mit SoftLayer-IDs müssen sich über das [Kundenportal ![Symbol für externen Link](../icons/launch-glyph.svg)](https://control.softlayer.com){: new_window} anmelden.
 * SoftLayer-Benutzer mit einer IBMid und mit oder ohne verknüpftes Bluemix-Konto können sich über das [Kundenportal ![Symbol für externen Link](../icons/launch-glyph.svg)](https://control.softlayer.com){: new_window} anmelden und dort das SoftLayer-Kundenportal öffnen oder sie können sich über die [Bluemix-Konsole ![Symbol für externen Link](../icons/launch-glyph.svg)](https://console.{DomainName}){: new_window} anmelden und dort das Infrastruktur-Dashboard öffnen. 
 * Bluemix-Benutzer ohne verknüpftes SoftLayer-Konto müssen sich über die Bluemix-Konsole anmelden.
 * Bluemix-Benutzer mit verknüpftem SoftLayer-Konto können sich über die [Bluemix-Konsole ![Symbol für externen Link](../icons/launch-glyph.svg)](https://console.{DomainName}){: new_window} oder das [Kundenportal ![Symbol für externen Link](../icons/launch-glyph.svg)](https://control.softlayer.com){: new_window} anmelden.
 

## Das Kennwort ist ungültig.
{: #ts_logintobm}

Sie müssen über eine gültige IBMid verfügen, um sich bei der {{site.data.keyword.Bluemix_notm}}-Konsole anzumelden.

Wenn Sie versuchen, sich bei {{site.data.keyword.Bluemix_notm}} anzumelden, wird die folgende Fehlernachricht angezeigt: 
{: tsSymptoms} 

`The password that you entered is not correct.` (Das eingegebene Kennwort ist nicht korrekt.)

Die IBMid und das Kennwort für die Anmeldung bei {{site.data.keyword.Bluemix_notm}} sind ungültig.
{: tsCauses} 
 
Um eine gültige IBMid und ein gültiges Kennwort zu erhalten, rufen Sie die Seite 'My IBM Profile' auf und führen anschließend einen der folgenden Schritte aus:
{: tsResolve}
  * Wenn Sie sich bereits für eine IBMid registriert haben und überprüfen möchten, ob die ID und das Kennwort gültig sind, klicken Sie auf **Anmelden** und geben Sie Ihre IBMid und Ihr Kennwort auf der Anmeldeseite ein. Wenn Sie das Kennwort vergessen haben, klicken Sie auf der Anmeldeseite auf **Kennwort vergessen**, um das Kennwort zurückzusetzen. Wenn Sie Ihre IBMid vergessen haben oder weiterhin Probleme mit dem Kennwort haben, suchen Sie auf der Site 'Worldwide IBM Registration Helpdesk' nach Hilfe. 
  * Wenn Sie über keine IBMid verfügen, klicken Sie auf **Registrieren**, um sich für eine IBMid und ein Kennwort zu registrieren. 



## Anmeldung mit Softlayer-Benutzernamen nicht möglich
{: #ts_softlayer_username}

Sie müssen über eine gültige IBMid und ein Kennwort verfügen, um sich an {{site.data.keyword.Bluemix_notm}} anmelden zu können.


Wenn Sie versuchen, sich mit Ihrem Softlayer-Benutzernamen bei der {{site.data.keyword.Bluemix_notm}}-Konsole anzumelden, erhalten Sie folgende Nachricht: 
{: tsSymptoms} 

`Diese IBMid oder E-Mail wurde nicht erkannt.`

Sie müssen über eine IBMid verfügen, um sich anmelden und das Infrastruktur-Dashboard in der Bluemix-Konsole verwenden zu können.
{: tsCauses} 
 
Wenn Sie SoftLayer-Benutzer sind und eine SoftLayer-ID verwenden, müssen Sie in jedem Konto, auf das Sie Zugriff haben, zur IBMid-Authentifizierung im Kundenportal wechseln, bevor Sie sich mithilfe der IBMid-Authentifizierung anmelden können. 

Wenden Sie sich an Ihren Masterbenutzer oder Kontoadministrator, um zur IBMid zu wechseln. 
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



## Konto ist im Wartestatus
{: #ts_accntpding}

Wenn sich Ihr Konto im Wartestatus befindet, können Sie sich nicht an {{site.data.keyword.Bluemix_notm}} anmelden.

 
Wenn Sie sich für ein {{site.data.keyword.Bluemix_notm}}-Testkonto registriert haben, kann es vorkommen, dass Sie sich nicht an {{site.data.keyword.Bluemix_notm}} anmelden können. Stattdessen wird die folgende Nachricht angezeigt:
{: tsSymptoms}

<code>Your account is pending. (Ihr Konto befindet sich im Zustand 'Anstehend'.) Please wait up to 24 hours for email confirmation and also check your spam folder. (Warten Sie bitte maximal 24 Stunden auf die E-Mail-Bestätigung und überprüfen Sie auch Ihren Spamordner.) If you still have not received your email confirmation, contact Bluemix Support. (Wenn Sie trotzdem keine E-Mail-Bestätigung erhalten haben, wenden Sie sich für weitere Hilfe an den <a href="http://ibm.biz/bluemixsupport.com" target="_blank">Bluemix-Support <img src="../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>). </code>


Wenn Sie sich für ein {{site.data.keyword.Bluemix_notm}}-Testkonto registriert haben, erhalten Sie eine Bestätigungs-E-Mail. Sie müssen auf den Link in dieser Bestätigungs-E-Mail klicken, um den Registrierungsprozess abzuschließen.
{: tsCauses} 

Die Bestätigungs-E-Mail wird an die E-Mail-Adresse gesendet, die Sie angegeben haben. Überprüfen Sie Ihren Posteingang und Ihren Ordner für Junk-Mail. Wenn Sie die Bestätigungs-E-Mail nicht empfangen haben, wenden Sie sich an den [{{site.data.keyword.Bluemix_notm}}-Support ![Symbol für externen Link](../icons/launch-glyph.svg)](http://ibm.biz/bluemixsupport.com){: new_window}.  
{: tsResolve}



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

  1. Rufen Sie das {{site.data.keyword.Bluemix_notm}}-Dashboard auf. Klicken Sie in der Menüleiste auf das Menüelement **Support** und anschließend auf **Organisationen verwalten**.
  2. Wechseln Sie zu Ihrer Organisation und zeigen Sie die Informationen zum Organisationsmanager in der Registerkarte **Benutzer** an.  
  
Wenn Sie nicht die Möglichkeit haben, Benutzer einzuladen, weil Sie ein Mitarbeiter und kein Mitglied sind, müssen Sie Ihr vorheriges {{site.data.keyword.Bluemix_notm}}-Konto löschen und anschließend eingeladen werden, als Mitglied der Organisation am Konto teilzunehmen. Um Ihr vorheriges Konto zu löschen und dem Konto als Mitglied beizutreten, führen Sie die folgenden Schritte durch: 

  1. Wenden Sie sich an den [{{site.data.keyword.Bluemix_notm}}-Support ![Symbol für externen Link](../icons/launch-glyph.svg)](http://ibm.biz/bluemixsupport){: new_window}, um ein Support-Ticket zu öffnen und die Löschung Ihres Kontos anzufordern. Wenn Sie Daten besitzen, die zu Ihrem alten Konto gehören, und die Sie speichern und in das neue Konto verschieben möchten, beziehen Sie diese Informationen in Ihre E-Mail ein. 
  2. Nachdem Ihr Konto gelöscht ist, lassen Sie sich von dem Benutzer mit der Organisationsmanager-Rolle als Organisationsmanager in die Organisation einladen. Anschließend melden Sie sich über die Einladung bei {{site.data.keyword.Bluemix_notm}} an. 




## Registrierung von Benutzern im Stapelbetrieb wird nicht unterstützt
{: #ts_batchregistration}

Wenn Sie Benutzer für {{site.data.keyword.Bluemix_notm}} registrieren, müssen Sie für jeden Benutzer eine individuelle Registrierung vornehmen.
 

{{site.data.keyword.Bluemix_notm}} bietet keine Funktionalität, um mehrere Benutzer gleichzeitig zu registrieren.
{: tsSymptoms}
 

{{site.data.keyword.Bluemix_notm}} unterstützt nicht die Registrierung von Benutzern im Stapelbetrieb. Zum Registrieren von Benutzern für {{site.data.keyword.Bluemix_notm}}, müssen Sie für jeden einzelnen Benutzer eine individuelle Registrierung vornehmen.
{: tsCauses}
 

Zum Registrieren mehrerer Benutzer für {{site.data.keyword.Bluemix_notm}} sind für jeden einzelnen Benutzer folgende Schritte auszuführen:
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

 
Sie können nach Bedarf mindestens eine der folgenden Aktionen ausführen:
{: tsResolve}

  * Den Browser aktualisieren oder erneut starten.
  * Von {{site.data.keyword.Bluemix_notm}} abmelden und anschließend wieder anmelden.
  * Den persönlichen Browsingmodus des Browsers verwenden. 
  * Die Cookies und den Cache des Browsers löschen.
  * Einen anderen Browser verwenden. Informationen zu den Versionen der Browser, die von {{site.data.keyword.Bluemix_notm}} unterstützt werden, finden Sie in den [Voraussetzungen für {{site.data.keyword.Bluemix_notm}} ![Symbol für externen Link](../icons/launch-glyph.svg)](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}.
  * Wenn Sie die cf-Befehlszeilenschnittstelle installiert haben, geben Sie den Befehl `cf apps` ein, um anzuzeigen, ob die Anwendung aktiv ist.
  
  
  
  
  

