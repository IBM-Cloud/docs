---

copyright:
  years: 2015, 2016

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 

# Fehlerbehebung für den Zugriff auf {{site.data.keyword.Bluemix_notm}} 
{: #accessing}

*Letzte Aktualisierung: 16. Mai 2016*

Ein allgemeines Problem in Bezug auf den Zugriff auf {{site.data.keyword.Bluemix}} kann sein, dass sich ein Benutzer nicht an {{site.data.keyword.Bluemix_notm}} anmelden kann oder dass sich ein Konto dauerhaft im Wartestatus befindet. In vielen Fällen können Sie diese Probleme jedoch durch Ausführen weniger einfacher Schritte beheben. 
{:shortdesc}

## Anmelden an {{site.data.keyword.Bluemix_notm}} nicht möglich
{: #ts_logintobm}

Sie müssen über eine gültige IBM ID und ein Kennwort verfügen, um sich an {{site.data.keyword.Bluemix_notm}} anmelden zu können.


Wenn Sie versuchen, sich an {{site.data.keyword.Bluemix_notm}} anzumelden, wird die folgende Fehlernachricht angezeigt: 
{: tsSymptoms} 

`The IBM id and/or password entered below is incorrect. Please try again.` (Die unten eingegebene IBM ID und/oder das Kennwort ist falsch.)


Die IBM ID und das Kennwort für die Anmeldung an {{site.data.keyword.Bluemix_notm}} sind nicht gültig.
{: tsCauses} 
 

Wenn Sie eine gültige IBM ID und ein gültiges Kennwort erhalten möchten, rufen Sie die Seite 'My IBM Profile' auf und führen anschließend einen der folgenden Schritte aus:
{: tsResolve}
  * Wenn Sie bereits eine IBM ID registriert haben und überprüfen möchten, ob die ID und das Kennwort gültig sind, klicken Sie auf **Anmelden** und geben die IBM ID und das Kennwort auf der Anmeldeseite an. Wenn Sie das Kennwort vergessen haben, klicken Sie auf der rechten Seite der Anmeldeseite auf **Kennwort vergessen**, um das Kennwort zurückzusetzen. Wenn Sie Ihre IBM ID vergessen haben oder weiterhin Probleme mit dem Kennwort haben, suchen Sie auf der Site 'Worldwide IBM Registration Helpdesk' nach Hilfe. 
  * Wenn Sie nicht über eine IBM ID verfügen, klicken Sie auf **Registrieren**, um eine IBM ID und ein Kennwort zu erhalten. 
  
**Hinweis:** Die IBM ID kann für IBM Mitarbeiter von der Anmelde-ID für das Intranet abweichen. 





## Es sind nicht gespeicherte Änderungen vorhanden
{: #ts_unsaved_changes}


Wenn Sie zur Detailseite der App navigieren, können Sie möglicherweise keine Aktionen ausführen und werden aufgefordert, Änderungen zu speichern, bevor Sie fortfahren. 


Wenn Sie versuchen, Ihre App oder Services auf der Detailsseite der App zu prüfen, empfangen Sie immer wieder die folgende Fehlernachricht:
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
 

Wenn eine {{site.data.keyword.Bluemix_notm}}-Region nicht mehr verfügbar ist, sind auch die Anwendungen, die in dieser Region ausgeführt werden, nicht mehr verfügbar, selbst dann nicht, wenn dieselben Anwendungen in einer anderen {{site.data.keyword.Bluemix_notm}}-Region ausgeführt werden.
{: tsSymptoms}

 
{{site.data.keyword.Bluemix_notm}}
bietet noch keine automatische Funktionsübernahme zwischen zwei Regionen an.
{: tsCauses}

 
Sie können einen
DNS-Anbieter nutzen, der eine intelligente Funktionsübernahme zwischen mehreren ID-Adressen
unterstützt, und Ihre DNS-Einstellungen zur Aktivierung der automatischen Funktionsübernahme
zwischen {{site.data.keyword.Bluemix_notm}}-Regionen manuell konfigurieren. DNS-Anbieter mit dieser Funktion sind z. B. NSONE, Akamai, Dyn.
{: tsResolve}

Wenn Sie Ihre DNS-Einstellungen konfigurieren, müssen Sie die öffentlichen IP-Adressen der {{site.data.keyword.Bluemix_notm}}-Regionen angeben, in denen Ihre Anwendungen ausgeführt werden. Verwenden Sie zum Abrufen der öffentlichen IP-Adresse
einer {{site.data.keyword.Bluemix_notm}}-Region
den Befehl `nslookup`. Sie können in einem Befehlszeilenfenster beispielsweise
den folgenden Befehl eingeben:
```
nslookup mybluemix.net
```



## Konto ist im Wartestatus
{: #ts_accntpding}

Wenn sich Ihr Konto im Wartestatus befindet, können Sie sich nicht an {{site.data.keyword.Bluemix_notm}} anmelden.

 
Wenn Sie sich für ein {{site.data.keyword.Bluemix_notm}}-Testkonto registriert haben, kann es vorkommen, dass Sie sich nicht an {{site.data.keyword.Bluemix_notm}} anmelden können. Stattdessen wird die folgende Nachricht angezeigt:
{: tsSymptoms}

<code>Your account is pending. (Ihr Konto befindet sich im Zustand 'Anstehend'.) Please wait up to 24 hours for email confirmation and also check your spam folder. (Warten Sie bitte maximal 24 Stunden auf die E-Mail-Bestätigung und überprüfen Sie auch Ihren Spamordner.) Wenn Sie trotzdem keine E-Mail-Bestätigung erhalten haben, wenden Sie sich für weitere Hilfe an den <a href="http://ibm.biz/bluemixsupport.com" target="_blank">Bluemix-Support</a>.</code>


Wenn Sie sich für ein {{site.data.keyword.Bluemix_notm}}-Testkonto registriert haben, erhalten Sie eine Bestätigungs-E-Mail. Sie müssen auf den Link in dieser Bestätigungs-E-Mail klicken, um den Registrierungsprozess abzuschließen.
{: tsCauses} 

Die Bestätigungs-E-Mail wird an die E-Mail-Adresse gesendet, die Sie angegeben haben. Überprüfen Sie Ihren Posteingang und Ihren Ordner für Junk-Mail. Wenn Sie die Bestätigungs-E-Mail nicht empfangen haben, wenden Sie sich an den [{{site.data.keyword.Bluemix_notm}}-Support](http://ibm.biz/bluemixsupport.com){: new_window}.  
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

  1. Rufen Sie das {{site.data.keyword.Bluemix_notm}}-Dashboard auf, klicken Sie auf das Symbol **Konto und Unterstützung** ![Konto und Unterstützung](images/account_support.svg) in der oberen Menüleiste und wählen Sie **Organisationen verwalten** aus.
  2. Wechseln Sie zu Ihrer Organisation und zeigen Sie die Informationen zum Organisationsmanager in der Registerkarte **Benutzer** an.  
  
Wenn Sie nicht die Möglichkeit haben, Benutzer einzuladen, weil Sie ein Mitarbeiter und kein Mitglied sind, müssen Sie Ihr vorheriges {{site.data.keyword.Bluemix_notm}}-Konto löschen und anschließend eingeladen werden, als Mitglied der Organisation am Konto teilzunehmen. Um Ihr vorheriges Konto zu löschen und dem Konto als Mitglied beizutreten, führen Sie die folgenden Schritte durch: 

  1. Wenden Sie sich an den [{{site.data.keyword.Bluemix_notm}} Support](http://ibm.biz/bluemixsupport){: new_window}, um ein Support-Ticket zu öffnen und die Löschung Ihres Kontos anzufordern. Wenn Sie Daten besitzen, die zu Ihrem alten Konto gehören, und die Sie speichern und in das neue Konto verschieben möchten, beziehen Sie diese Informationen in Ihre E-Mail ein. 
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

  1. Klicken Sie in der rechten oberen Ecke der Benutzerschnittstelle von {{site.data.keyword.Bluemix_notm}} auf **REGISTRIEREN**.
  2. Führen Sie die Schritte aus, indem Sie dem Assistenten folgen.

    

## Laden einer {{site.data.keyword.Bluemix_notm}}-Seite nicht möglich
{: #ts_err}

Wenn Sie die {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle verwenden, kann es vorkommen, dass Sie eine {{site.data.keyword.Bluemix_notm}}-Seite nicht laden können. Stattdessen können die Fehlernachrichten BXNUI0001E oder BXNUI0016E angezeigt werden.
 

Während der Verwendung der {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle kann eine der folgenden Fehlernachrichten angezeigt werden:
{: tsSymptoms}

`BXNUI0001E: Die Seite wurde nicht geladen, weil von Bluemix nicht erkannt wurde, ob eine Sitzung vorhanden ist.`


`BXNUI0016E: Die Apps und Services wurden nicht abgerufen, da eine Bluemix-Seite nicht geladen wurde.`

 

Sie können nach Bedarf mindestens eine der folgenden Aktionen ausführen:
{: tsResolve}

  * Den Browser aktualisieren oder erneut starten.
  * Von {{site.data.keyword.Bluemix_notm}} abmelden und anschließend wieder anmelden.
  * Den persönlichen Browsingmodus des Browsers verwenden. 
  * Die Cookies und den Cache des Browsers löschen.
  * Einen anderen Browser verwenden. Informationen zu den Versionen der Browser, die von {{site.data.keyword.Bluemix_notm}} unterstützt werden, finden Sie unter [{{site.data.keyword.Bluemix_notm}} Voraussetzungen](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}.
  * Wenn Sie die cf-Befehlszeilenschnittstelle installiert haben, geben Sie den Befehl `cf apps` ein, um anzuzeigen, ob die Anwendung aktiv ist.
  
  
  
  
  
## Obere {{site.data.keyword.Bluemix_notm}}-Menüleiste wird
nicht mehr angezeigt
{: #ts_topmenubar}

Möglicherweise wird die obere {{site.data.keyword.Bluemix_notm}}-Menüleiste
beim Ändern der Größe des Browserfensters oder bei der Verwendung eines Mobilgeräts nicht angezeigt.


Wenn Sie Ihr Browserfenster verkleinern oder ein
Mobilgerät verwenden, ist die obere {{site.data.keyword.Bluemix_notm}}-Menüleiste
nicht mehr zu sehen. Wenn die obere Menüleiste nicht mehr zu sehen ist, wird in der linken oberen Ecke
das Seitenleistenmenü als gestapelte Linie dargestellt. 
{: tsSymptoms}

 

Die Benutzerschnittstelle von {{site.data.keyword.Bluemix_notm}}
weist ein responsives Design auf. Wenn sich die angezeigte Umgebung verändert,
kann sich auch das Layout der Benutzerschnittstelle von {{site.data.keyword.Bluemix_notm}}
ändern. 
{: tsCauses}
 

Verwenden Sie stattdessen
das Seitenleistenmenü in der linken oberen Ecke.
{: tsResolve}








# Fehlerbehebung für die Verwaltung von Anwendungen
{: #managingapps}

Allgemeine Probleme im Zusammenhang mit der Verwaltung von Anwendungen können sein, dass Anwendungen nicht aktualisiert werden können
oder Doppelbytezeichen nicht angezeigt werden. In vielen Fällen können Sie diese Probleme jedoch durch Ausführen weniger einfacher Schritte beheben.
{:shortdesc}





## Apps können nicht in den Debugmodus versetzt werden
{: #ts_debug}

Möglicherweise können Sie den Debugmodus nicht aktivieren, wenn die JVM-Version 8 oder eine frühere Version verwendet wird (JVM = Java Virtual Machine). 


Wenn Sie die Option zum Aktivieren des Anwendungsdebuggings**** auswählen, versuchen die Tools, die Anwendung in den Debugmodus zu versetzen. Daraufhin startet die Eclipse-Workbench eine Debugsitzung. Wenn die Tools den Debugmodus erfolgreich aktivieren können, wird als Status für die Webanwendung `Updating mode` (Aktualisierungsmodus), `Developing` (Entwicklung) und `Debugging` (Fehlerbehebung) angezeigt. 
{: tsSymptoms}

Wenn die Tools den Debugmodus jedoch nicht aktivieren können, wird als Status für die Webanwendung lediglich `Updating mode` (Aktualisierungsmodus) und `Developing` (Entwicklung) ohne die Angabe `Debugging` (Fehlerbehebung) angezeigt. Außerdem zeigen die Tools möglicherweise die folgende Fehlernachricht in der Konsolenansicht an:

```
bluemixMgmgClient - ???? [pool-1-thread-1] .... ERROR --- ClientProxyImpl: Cannot create the websocket connections for MyWebProj
com.ibm.ws.cloudoe.management.client.exception.ApplicationManagementException: javax.websocket.DeploymentException: The HTTP request to initiate the  WebSocket connection failed
at com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl.onNewClientSocket(ClientProxyImpl.java:161)
at com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl$RunServerTask.run(ClientProxyImpl.java:267)
at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:522)
at java.util.concurrent.FutureTask.run(FutureTask.java:277)
at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1153)
at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:628)
at java.lang.Thread.run(Thread.java:785)
Caused by: javax.websocket.DeploymentException: The HTTP request to initiate the WebSocket connection failed
at  org.apache.tomcat.websocket.WsWebSocketContainer.connectToServer(WsWebSocketContainer.java:315)
at  com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl.onNewClientSocket(ClientProxyImpl.java:158)
... 6 more
Caused by: java.util.concurrent.TimeoutException
at org.apache.tomcat.websocket.AsyncChannelWrapperSecure$WrapperFuture.get(AsyncChannelWrapperSecure.java:505)
at org.apache.tomcat.websocket.WsWebSocketContainer.processResponse(WsWebSocketContainer.java:542)
at org.apache.tomcat.websocket.WsWebSocketContainer.connectToServer(WsWebSocketContainer.java:296)
... 7 more
[2016-01-15 13:33:51.075] bluemixMgmgClient - ????  [pool-1-thread-1] .... ERROR --- ClientProxyImpl: Cannot create the  websocket connections for MyWebProj
com.ibm.ws.cloudoe.management.client.exception.ApplicationManagementException: javax.websocket.DeploymentException: The HTTP request to initiate the  WebSocket connection failed
at com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl.onNewClientSocket(ClientProxyImpl.java:161)
at com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl$RunServerTask.run(ClientProxyImpl.java:267)
at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:522)
at java.util.concurrent.FutureTask.run(FutureTask.java:277)
at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1153)
at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:628)
at java.lang.Thread.run(Thread.java:785)
Caused by: javax.websocket.DeploymentException: The HTTP request to initiate the WebSocket connection failed
at org.apache.tomcat.websocket.WsWebSocketContainer.connectToServer(WsWebSocketContainer.java:315)
at com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl.onNewClientSocket(ClientProxyImpl.java:158)
... 6 more
Caused by: java.util.concurrent.TimeoutException
at org.apache.tomcat.websocket.AsyncChannelWrapperSecure$WrapperFuture.get(AsyncChannelWrapperSecure.java:505)
at org.apache.tomcat.websocket.WsWebSocketContainer.processResponse(WsWebSocketContainer.java:542)
at org.apache.tomcat.websocket.WsWebSocketContainer.connectToServer(WsWebSocketContainer.java:296)
... 7 more
```
 

Die folgende JVM-Versionen (JVM = Java Virtual Machine) können keine Debugsitzung erstellen: IBM JVM 7, IBM JVM 8 sowie frühere Versionen als Oracle JVM 8.
{: tsCauses}

Wenn Ihre Workbench eine dieser JVM-Versionen verwendet, treten möglicherweise Probleme beim Erstellen einer Debugsitzung auf. Ihre Workbench verwendet in der Regel dieselbe JVM-Version, die auf Ihrem lokalen Computer als System-JVM installiert ist. Ihre System-JVM ist nicht identisch mit der JVM Ihrer aktiven Bluemix-Java-Anwendung. Die Bluemix-Java-Anwendung wird fast immer unter IBM JVM und in manchen Fällen unter OpenJDK JVM ausgeführt.
  

Führen Sie die folgenden Schritte aus, um zu überprüfen, welche Java-Version von IBM Eclipse Tools for Bluemix verwendet wird:
{: tsResolve}

  1. Wählen Sie in IBM Eclipse Tools for Bluemix select **Hilfe** > **Informationen zu Eclipse** > **Installationsdetails** > **Konfiguration** aus.
  2. Suchen Sie in der Liste die Eigenschaft `eclipse.vm`. Die folgende Zeile enthält ein Beispiel für die Eigenschaft `eclipse.vm`:
	
	```
	eclipse.vm=C:\Programme\IBM\ibm-java-sdk-80-win-x86_64\bin\..\jre\bin\j9vm\jvm.dll
	```

  3. Geben Sie in der Befehlszeile `java -version` im Verzeichnis `bin` Ihrer Java-Installation ein. Die Informationen zu Ihrer IBM JVM-Version werden angezeigt.

Wenn Ihre Workbench IBM JVM 7 oder 8 verwendet bzw. eine frühere Version als Oracle JVM 8, führen Sie die folgenden Schritte aus, um zu Oracle JVM 8 zu wechseln:

  1. Laden Sie Oracle JVM 8 herunter und installieren Sie es (Details hierzu finden Sie in [Java SE Downloads](http://www.oracle.com/technetwork/java/javase/downloads/index.html){: new_window}).
  2. Starten Sie Eclipse erneut.
  3. Überprüfen Sie, ob die Eigenschaft `eclipse.vm` auf Ihre neue Oracle JVM 8-Installation verweist.







## Angeforderte Aktionen konnten nicht ausgeführt werden
{: #ts_authority}

Möglicherweise können Sie die Aktionen ohne entsprechende Zugriffsberechtigung nicht ausführen.

 

Wenn Sie versuchen, Aktionen für eine Serviceinstanz oder eine App-Instanz auszuführen, können Sie die angeforderten Aktionen nicht abschließen und es wird eine der folgenden Fehlernachrichten angezeigt: 
{: tsSymptoms}

`BXNUI0514E: Sie sind kein Entwickler für die Bereiche in der Organisation <Organisationsname>.`


`Serverfehler, Statuscode: 403, Fehlercode: 10003, Nachricht: Sie sind nicht berechtigt, die angeforderte Aktion auszuführen.`

 

Sie verfügen nicht über die erforderliche Berechtigungsebene zum Ausführen der Aktionen. 
{: tsCauses}

  

Verwenden Sie zum Abrufen der erforderlichen Berechtigungsebene eine der folgenden Methoden: 
{: tsResolve}
 * Wählen Sie eine andere Organisation und einen anderen Bereich aus, für die bzw. den Sie die Rolle des Entwicklers ausfüllen. 
 * Bitten Sie den Manager der Organisation, Ihre Rolle in die eines Entwicklers zu ändern oder einen Bereich zu erstellen und Ihnen dann eine Entwicklerrolle zuzuweisen. Details finden Sie unter [Organisationen verwalten](../admin/orgs_spaces.html).
 

 


## Auf {{site.data.keyword.Bluemix_notm}}-Services kann aufgrund von Berechtigungsfehlern nicht zugegriffen werden
{: #ts_vcap}

Berechtigungsfehler können auftreten, wenn Ihre App auf einen {{site.data.keyword.Bluemix_notm}}-Service zugreift und die Serviceberechtigungen in Ihrer App fest codiert sind. 

Nachdem Sie Ihre App für die Kommunikation mit einem {{site.data.keyword.Bluemix_notm}}-Service konfiguriert haben, stellen Sie sie in {{site.data.keyword.Bluemix_notm}} bereit. Sie können die App jedoch nicht für den Zugriff auf den {{site.data.keyword.Bluemix_notm}}-Service verwenden und empfangen einen Berechtigungsfehler.
{: tsSymptoms}

Die fest codierten Berechtigungsnachweise in der App sind möglicherweise nicht korrekt. Jedes Mal, wenn der Service erneut erstellt wird, ändern sich die Berechtigungsnachweise für den Zugriff darauf.
{: tsCauses}


Statt die Berechtigungsnachweise in Ihrer App fest zu codieren, verwenden Sie Verbindungsparameter aus der Umgebungsvariablen VCAP_SERVICES. Die Methoden für die Verwendung von Verbindungsparametern aus der Umgebungsvariablen VCAP_SERVICES variieren abhängig von den Programmsprachen. Für Node.js-Apps können Sie beispielsweise den folgenden Befehl verwenden: 
{: tsResolve}

```
process.env.VCAP_SERVICES
```
Weitere Informationen zu den Befehlen, die Sie in anderen Programmsprachen verwenden können, finden Sie unter [Java](http://docs.run.pivotal.io/buildpacks/java/java-tips.html#env-var){: new_window} und [Ruby](http://docs.run.pivotal.io/buildpacks/ruby/ruby-tips.html#env-var){: new_window}. 
 

 
 




## Bereitstellung von Apps mit IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} nicht möglich
{: #ts_bm_tools_facet}

Wird eine nicht unterstützte Facette auf Ihr Eclipse-Projekt angewendet,
können Sie Ihre Apps möglicherweise
nicht mithilfe von IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} in {{site.data.keyword.Bluemix_notm}}
bereitstellen. 

 

Mit
der Cloud Foundry-Befehlszeilenschnittstelle können Sie Ihre App erfolgreich in {{site.data.keyword.Bluemix_notm}}
bereitstellen. Allerdings ist es nicht möglich, die App mit IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} in {{site.data.keyword.Bluemix_notm}} bereitzustellen, und es wird die folgende Fehlernachricht angezeigt: `Project facet <facet_name> is not supported. (Projektfacette 'facettenname' wird nicht unterstützt.)` Beispiel: `Project facet Cloud Foundry Standalone Application version 1.0 is not supported. (Projektfacette Cloud Foundry Standalone Application Version 1 wird nicht unterstützt.)`
{: tsSymptoms}

 

IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}
ordnet Projekte zu {{site.data.keyword.Bluemix_notm}}-Laufzeiten zu, und zwar mittels Projektfacetten. Facetten definieren
die Voraussetzungen für Java EE-Projekte in Eclipse und werden im Rahmen der Laufzeitkonfiguration
genutzt, sodass unterschiedliche Laufzeiten unterschiedlichen Projekten zugeordnet werden. Wird die auf das Projekt angewendete Facette nicht von
IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} unterstützt,
können Sie Ihre App möglicherweise nicht mit IBM Eclipse
Tools for {{site.data.keyword.Bluemix_notm}} bereitstellen.
{: tsCauses}


Sie müssen die Facette aus dem Eclipse-Projekt entfernen,
damit Sie Ihre App mit IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} bereitstellen können.
{: tsResolve} 

Um die
Facette zu entfernen, klicken Sie für das Projekt in IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}
auf **Projekt>Eigenschaften>Projektfacetten**. Nehmen Sie anschließend die Markierung des Kontrollkästchens für die nicht unterstützte Facette zurück. 



## Fehler des Typs '502 Bad Gateway' empfangen
{: #ts_502_error}

Wenn Sie bei der Interaktion mit Apps
unter {{site.data.keyword.Bluemix_notm}} Fehler vom Typ '502 Bad Gateway' erhalten,
überprüfen Sie die {{site.data.keyword.Bluemix_notm}}-Seite 'Status'
und führen Sie anschließend die entsprechenden Aktionen durch.

 

Sie erhalten Fehlernachrichten, die mit '502 Bad Gateway' beginnen. So wird beispielsweise die Fehlernachricht `502 Bad Gateway:
Registered endpoint failed to handle the request (502 Bad Gateway: Verarbeitung der Anfrage durch registrierten Endpunkt fehlgeschlagen)` angezeigt.
{: tsSymptoms}

 

Zu einem
Fehler des Typs 'Bad Gateway' kommt es in der Regel, wenn Sie eine Website besuchen, bei der zum Speichern und
Vermitteln der Daten aus dem Hauptserver, der die Site hostet, einen Proxy-Server verwendet wird. Der Hauptserver und der Proxy-Server
stellen möglicherweise keine ordnungsgemäße Verbindung her; aus diesem Grund wird der HTTP-Statuscode 502 in Ihrem Browserfenster
angezeigt. Dieser Statuscode weist darauf hin, dass der Hauptserver der Site die HTTP-Implementierung, die vom Proxy-Server erwartet
wird, nicht erhalten hat.
{: tsCauses}

Andere, weniger häufige Ursachen eines Fehlers vom Typ 'Bad Gateway'
sind Ausfälle des Internet-Service-Providers, falsche Firewallkonfigurationen und
Fehler des Browser-Cache. 

 

Wenn Sie vermuten, dass
ein {{site.data.keyword.Bluemix_notm}}-Service
inaktiv ist, überprüfen Sie zunächst die
[{{site.data.keyword.Bluemix_notm}}-Seite 'Status'](https://developer.ibm.com/bluemix/support/#status){: new_window}. Sie können, wenn Sie möchten, den Service in einer anderen {{site.data.keyword.Bluemix_notm}}-Region
als Ausweichlösung verwenden. Ausführliche Informationen finden Sie in [Services
in einer anderen Region verwenden](../services/reqnsi.html#cross_region_service){: new_window}. Wenn der Status des Service normal ist,
führen Sie die folgenden Schritte aus, um das Problem zu lösen: 
{: tsResolve}

  * Wiederholen Sie die Aktion.
    * Laden Sie die Seite erneut durch Drücken der Taste F5 auf Ihrer Tastatur oder durch
Klicken auf die Schaltfläche für die Aktualisierung. Wenn dieser Schritt nicht funktioniert, leeren Sie den Cache und die Cookies des Browsers
und laden Sie die Seite anschließend erneut.
	* Verwenden Sie einen anderen Browser.
	* Führen Sie für Ihren Router, Ihr Modem und Ihren Computer einen Warmstart durch. Durch einen Warmstart dieser Einheiten
können verschiedene Fehler bereinigt werden, die zu dem Fehler 502 führen. 
  * Warten Sie und wiederholen Sie den Vorgang zu einem späteren Zeitpunkt. Bei einigen Instanzen kann es in Verbindung mit
Ihrem Internet-Service-Provider oder den {{site.data.keyword.Bluemix_notm}}-Services zu vorübergehenden Problemen kommen. Warten Sie, bis die vorübergehenden Probleme gelöst wurden.
  * Wenn das Problem dennoch bestehen bleibt, wenden Sie sich an den {{site.data.keyword.Bluemix_notm}}-Support. Weitere Informationen finden Sie unter [Kontaktaufnahme mit dem {{site.data.keyword.Bluemix_notm}}-Support](../support/index.html#contacting-bluemix-support){: new_window}. 




## Überschrittenes Plattenkontingent
{: #ts_disk_quota}

Wenn der Plattenspeicher immer weniger wird, können Sie das Plattenkontingent manuell
so ändern, dass Sie mehr Plattenspeicher zur Verfügung haben.

  

Wenn der Plattenspeicher immer weniger wird, wird möglicherweise eine
Nachricht angezeigt, die besagt, dass das Plattenkontingent überschritten wurde. Zur Lösung des Problems
haben Sie möglicherweise versucht, für Ihre App-Instanz ein Scale-up durchzuführen, um
mehr Plattenspeicher zu erhalten. Sie haben beispielsweise versucht, ein Scale-up von 256 MB auf 1256 MB durchzuführen,
und zwar durch Ändern des Speicherkontingents auf der Seite mit den App-Details. Da jedoch das Plattenkontingent
dasselbe geblieben ist, haben Sie nicht mehr Plattenspeicher bekommen. 
{: tsSymptoms}


Das Standardplattenkontingent, das für eine App zugeordnet wird, beträgt
1 GB. Wenn Sie mehr Plattenspeicher benötigen, müssen Sie das Plattenkontingent manuell angeben. 
{: tsCauses}

 
Verwenden Sie eine der folgenden Methoden, um Ihr Plattenkontingent anzugeben. Sie können ein maximales Plattenkontingent von 2 GB angeben. Falls 2 GB dennoch nicht genug sein sollten, setzen Sie versuchsweise einen externen Service ein, z. B. [Object Store](../services/ObjectStorage/index.html){: new_window}.
{: tsResolve}

  * Fügen Sie in der Datei 'manifest.yml' den folgenden Teil hinzu:
    ```
	disk_quota: <disk_quota>
	```
  * Verwenden Sie die Option **-k** in Kombination mit dem Befehl `cf push`,
wenn Sie Ihre App mit Push-Operation an {{site.data.keyword.Bluemix_notm}} übertragen:
    ```
	cf push appname -p app_path -k <disk_quota>
	```

	
	
## Git-Repository kann nicht hinzugefügt werden
{: #ts_cannot_addgit}

Nach der Erstellung einer App im Dashboard haben Sie auf 'Git hinzufügen' geklickt, um ein Git-Repository zu erstellen; Sie können allerdings nicht fortfahren.



Wenn Sie auf
**Git hinzufügen** klicken, wird ein Fenster geöffnet
und es kommt zu einem dieser Fehler:
{: tsSymptoms} 

  * Das Fenster bleibt mit einer leeren Anzeige hängen.
  * In einer Nachricht werden Sie darauf hingewiesen, dass es ein Problem mit Cookies von Drittanbietern gibt.



Möglicherweise ist Ihr Browser so konfiguriert,
dass kein Cookie definiert werden kann. Dieses Cookie muss über die IBM® Bluemix DevOps Services-Site in der Internetdomäne hub.jazz.net festgelegt werden, und zwar im Kontext der {{site.data.keyword.Bluemix_notm}}-Konsole.
{: tsCauses}  

 

Zur Lösung dieses Problems stehen Ihnen die folgenden Möglichkeiten zur Verfügung:
{: tsResolve}

  * Befolgen Sie die Anweisungen in dem Fenster, das in der
{{site.data.keyword.Bluemix_notm}}-Konsole geöffnet wird. Klicken Sie auf die Schaltfläche. Vorübergehend wird ein weiteres Browserfenster geöffnet. In diesem Fenster legt DevOps Services das Authentifizierungscookie fest.
  * Rufen Sie auf einer weiteren Browserregisterkarte https://hub.jazz.net auf und melden Sie sich an. Kehren Sie zur {{site.data.keyword.Bluemix_notm}}-Konsole
zurück und aktualisieren Sie die Seite. Klicken Sie erneut auf **Git hinzufügen**.
  * Ändern Sie Ihre Browsereinstellungen so, dass Cookies von Drittanbietern möglich sind, und klicken Sie erneut auf 'Git hinzufügen'. Details zur Konfiguration dieser Einstellungen
finden Sie in der Dokumentation Ihres Browsers:
    * [Mozilla Firefox](https://support.mozilla.org/en-US/kb/enable-and-disable-cookies-website-preferences#w_how-do-i-change-cookie-settings){: new_window}
	* [Google
Chrome](https://support.google.com/chrome/answer/95647){: new_window}
	* [Apple Safari](https://support.apple.com/kb/PH17191){: new_window}
	* [Microsoft Internet Explorer](http://windows.microsoft.com/en-us/internet-explorer/delete-manage-cookies#ie=ie-11){: new_window} Falls durch diese Ausweichlösungen das Problem nicht behoben wird, senden Sie eine E-Mail an idslogin@jazz.net.



## Android-Apps empfangen keine Push-Benachrichtigungen
{: #ts_push}

In bestimmten Regionen, in denen nicht auf Google zugegriffen werden kann,
empfangen Android-Apps keine Benachrichtigungen, die Sie über den IBM Push-Service senden. In diesem Fall können Sie als Ausweichlösung Services von Drittanbietern verwenden.

 

Sie binden einen Push-Service für Ihre Bluemix-App und senden eine Nachricht an die registrierten Geräte. Jedoch können Apps, die auf der Android-Plattform entwickelt wurden,
Ihre Benachrichtigungen in bestimmten Regionen nicht empfangen. 
{: tsSymptoms}

 
Der IBM Push-Service nutzt den GCM-Service (Google Cloud Messaging),
um Benachrichtigungen an mobile Apps zu versenden, die auf der Android-Plattform entwickelt wurden. Zur Aktivierung der Android-Apps für den Empfang von Benachrichtigungen
muss der GCM-Service (Google Cloud Messaging) für die mobilen Apps zugänglich sein. In Regionen, in denen der GCM-Service nicht von den Android-Apps erreicht werden kann,
können die Android-Apps keine Push-Benachrichtigungen empfangen.
{: tsCauses}

 
Verwenden Sie Services von Drittanbietern,
die nicht vom GCM-Service als Ausweichlösung abhängig sind, z. B. [Pushy](https://pushy.me){: new_window},
[igetui](http://www.getui.com/){: new_window} und [jpush](https://www.jpush.cn/){: new_window}.
{: tsResolve}



## Für Organisation geltender Grenzwert für Services wurde überschritten
{: #ts_servicelimit}

Wenn Sie Benutzer eines Testkontos sind, können Sie möglicherweise eine Anwendung in {{site.data.keyword.Bluemix_notm}} nicht erstellen, wenn Sie den für Ihre Organisation geltenden Grenzwert für Services überschritten haben.
 

Bei dem Versuch, in {{site.data.keyword.Bluemix_notm}} eine Anwendung zu erstellen, wird die folgende Fehlernachricht angezeigt: 
{: tsSymptoms}

`BXNUI2032E: Die Ressource <service_instances> wurde nicht erstellt. Während der Kontaktaufnahme mit Cloud Foundry zum Erstellen der Ressource ist ein Fehler aufgetreten. Cloud Foundry-Nachricht: "You have exceeded your organization's services limit." ("Sie haben den für Ihre Organisation geltenden Grenzwert für Services überschritten.")`



Dieser Fehler tritt auf, wenn Sie den Grenzwert für die Anzahl der Serviceinstanzen, die für Ihr Konto bestehen können, überschritten haben. Die maximale Anzahl von Serviceinstanzen für ein Testkonto beträgt 10.
{: tsCauses} 

 

Löschen Sie alle nicht benötigten Serviceinstanzen oder entfernen Sie den Grenzwert für die Anzahl der Serviceinstanzen, die für Sie bestehen können.
{: tsResolve}
 
  * Zum Löschen einer Serviceinstanz können Sie die {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle oder die Befehlszeilenschnittstelle verwenden.
    Führen Sie folgende Schritte aus, wenn Sie die {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle zum Löschen einer Serviceinstanz verwenden:
	  1. Klicken Sie im {{site.data.keyword.Bluemix_notm}}-Dashboard im linken Teilfenster auf die Option **SERVICES**. Die Kacheln für die Services werden angezeigt. 
	  2. Klicken Sie auf der Servicekachel, die Sie löschen wollen, auf das Symbol **Menü**.
	  3. Klicken Sie auf **Service löschen**. Nach dem Löschen der Serviceinstanz werden Sie aufgefordert, die Anwendung erneut bereitzustellen, an die die Serviceinstanz gebunden war. 
    Führen Sie folgende Schritte aus, wenn Sie die Befehlszeilenschnittstelle zum Löschen einer Serviceinstanz verwenden:
	  1. Heben Sie die Bindung zwischen der Serviceinstanz und der Anwendung auf, indem Sie Folgendes eingeben: `cf unbind-service <appname> <service_instance_name>`.
	  2. Löschen Sie die Serviceinstanz durch Eingeben von `cf delete-service <service_instance_name>`.
	  3. Nach dem Löschen der Serviceinstanz möchten Sie möglicherweise Ihre Anwendung, an die die Serviceinstanz gebunden war, erneut bereitstellen, indem Sie `cf restage <appname>` eingeben.
  * Zum Löschen des Grenzwerts für die Anzahl Serviceinstanzen, die für Sie bestehen können, wandeln Sie Ihr Testkonto in ein Zahlungskonto um. Informationen dazu, wie Ihr Testkonto in ein Zahlungskonto umgewandelt wird, finden Sie unter [Vorgehensweise zum Ändern des Plans](../pricing/index.html#changing){: new_window}.

  
  
## Ausführbare Dateien können in {{site.data.keyword.Bluemix_notm}} nicht ausgeführt werden
{: #ts_executable}

Möglicherweise können Sie ausführbare Dateien in {{site.data.keyword.Bluemix_notm}} nicht ausführen, wenn diese ausführbaren Dateien in einer anderen Umgebung entwickelt und der Build für sie dort erstellt wurde. 

 

Sie können ausführbare Dateien nicht in {{site.data.keyword.Bluemix_notm}} ausführen, wenn diese ausführbaren Dateien in einer anderen Umgebung entwickelt und der Build für sie dort erstellt wurde.
{: tsSymptoms}

 

Wenn es sich bei dem Inhalt, den Sie per Push-Operation an {{site.data.keyword.Bluemix_notm}} übertragen wollen, bereits um eine ausführbare Datei handelt, wurde der Build für den Inhalt zuvor erstellt und ein erneuter Build in {{site.data.keyword.Bluemix_notm}} ist nicht erforderlich. In diesem Fall ist kein Buildpack erforderlich, damit die ausführbare Datei in {{site.data.keyword.Bluemix_notm}} ausgeführt werden kann. Sie müssen jedoch für {{site.data.keyword.Bluemix_notm}} explizit angeben, dass ein Buildpack nicht erforderlich ist.
{: tsCauses}

 

Wenn Sie die ausführbare Datei per Push-Operation an {{site.data.keyword.Bluemix_notm}} übertragen, müssen Sie durch einen 'Null-Buildpack' angeben, dass kein Buildpack erforderlich ist. Geben Sie einen Null-Buildpack an, indem Sie die Option **-b** mit dem Befehl `cf push` verwenden:
{: tsResolve}

```
cf push appname -p <app_path> -c <start_command> -b <null-buildpack>
```
Beispiel:
```
cf push appname -p <app_path> -c ./RunMeNow -b https://github.com/ryandotsmith/null-buildpack
```


## Für Organisation geltende Speicherbegrenzung wurde überschritten
{: #ts_outofmemory}

Wenn Sie Benutzer eines Testkontos sind, können Sie möglicherweise eine Anwendung nicht in {{site.data.keyword.Bluemix_notm}} bereitstellen, wenn Sie die für Ihre Organisation geltende Speicherbegrenzung überschritten haben. Sie können entweder den von Ihren Apps verwendeten Speicherplatz verringern oder das Speicherkontingent Ihres Konto erhöhen. 



Wenn Sie eine Anwendung unter {{site.data.keyword.Bluemix_notm}} bereitstellen, wird die folgende Fehlernachricht angezeigt:
{: tsSymptoms} 

`FAILED Server error, status code: 400, error code: 100005, message: You have exceeded your organization's memory limit.` (FEHLGESCHLAGEN Serverfehler, Statuscode: 400, Fehlercode: 100005, Nachricht: Sie haben die für Ihre Organisation geltende Speicherbegrenzung überschritten.)

 

Dieser Fehler tritt auf, wenn die für Ihre Organisation verbleibende Speichermenge niedriger ist, als die Speichermenge, die für die bereitzustellende Anwendung erforderlich ist. Das Kontingent der maximalen Hauptspeicherkapazität für ein Testkonto beträgt 2 Gigabyte.
{: tsCauses}



Sie können entweder das Speicherkontingent für Ihr Konto erhöhen oder den von Ihren Anwendungen verwendeten Speicherplatz verringern.
{: tsResolve} 

  * Zum Erhöhen des Speicherkontingents für Ihr Konto wandeln Sie Ihr Testkonto in ein Zahlungskonto um. Informationen dazu, wie Ihr Testkonto in ein Zahlungskonto umgewandelt wird, finden Sie in [Zahlungskonten](../pricing/index.html#pay-accounts){: new_window}. 
  * Zum Verringern des von Ihren Anwendungen verwendeten Speicherplatzes verwenden Sie entweder die {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle oder die cf-Befehlszeilenschnittstelle.
    Wenn Sie die {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle verwenden, führen Sie die folgenden Schritte durch:
	  1. Wählen Sie im {{site.data.keyword.Bluemix_notm}}-Dashboard Ihre Anwendung aus. Die Seite mit den Anwendungsdetails wird geöffnet.
	  2. Im Teilfenster für die Laufzeit können Sie die maximale Hauptspeicherkapazität für Ihre Anwendung, die Anzahl der Anwendungsinstanzen oder beides reduzieren. 
	Führen Sie bei Verwendung der cf-Befehlszeilenschnittstelle folgende Schritte aus:
	  1. Überprüfen Sie, wie viel Speicherplatz für Ihre Anwendungen verwendet wird:
	  ```
	  cf apps
	  ```
	     Mit dem Befehl 'cf apps' werden alle Anwendungen aufgelistet, die Sie in Ihrem aktuellen Bereich bereitgestellt haben. Der Status der einzelnen Anwendungen wird auch angezeigt.
      2. Zum Verringern der von Ihrer Anwendung verwendeten Speichermenge verringern Sie die Anzahl der Anwendungsinstanzen, die maximale Hauptspeicherkapazität oder beides:
	  ```
	  cf push <appname> -p <app_path> -i <instance_number> -m <memory_limit>
      ```
	  3. Starten Sie Ihre Anwendung erneut, damit die Änderungen wirksam werden.



	  
## Apps werden nicht automatisch erneut gestartet
{: #ts_apps_not_auto_restarted}


Eine Anwendung wird nicht automatisch erneut gestartet, wenn ein Service, den Sie an die Anwendung binden, nicht mehr ausgeführt wird.	  
	  
 

Bei Absturz eines Service, den Sie an die Anwendung binden, können in der Anwendung Probleme wie beispielsweise Ausfallzeiten, Ausnahmebedingungen und Verbindungsfehler auftreten. {{site.data.keyword.Bluemix_notm}} startet die App nicht automatisch erneut, um eine entsprechende Recovery für diese Probleme durchzuführen.
{: tsSymptoms}



Dieses Verhalten gehört zum Design von Cloud Foundry.
{: tsCauses} 

 

Sie können die Anwendung manuell starten, indem Sie den folgenden Befehl in die Befehlszeilenschnittstelle eingeben:
{: tsResolve}

```
cf push <appname> -p <app_path>
```
Darüber hinaus können Sie die Anwendung so codieren, dass Probleme wie Ausfallzeiten, Ausnahmebedingungen und Verbindungsfehler erkannt werden und eine Recovery durchgeführt wird. 

	  

## Verlust benutzerdefinierter Variablen bei Push-Operation für Anwendung
{: #ts_varsnotretained}

Wenn Sie eine Anwendung mit einer Push-Operation aus IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} an {{site.data.keyword.Bluemix_notm}} übertragen, werden die angegebenen Variablen zurückgesetzt, sofern die Variablen nicht in der Manifestdatei gespeichert werden.



Die angegebenen Variablen gehen verloren, nachdem Sie eine Anwendung mit einer Push-Operation von IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} an {{site.data.keyword.Bluemix_notm}} übertragen haben.
{: tsSymptoms} 


Die angegebenen Variablen werden nur gespeichert, wenn Sie sie in der Manifestdatei speichern.
{: tsCauses} 

 

Wenn Sie eine Anwendung aus IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} mit einer Push-Operation an {{site.data.keyword.Bluemix_notm}} übertragen, wählen Sie das Kontrollkästchen **In Manifestdatei speichern** auf der Seite 'Anwendungsdetails' im Assistenten 'Anwendung' aus. Danach werden die Variablen, die Sie im Assistenten angeben, in der Manifestdatei für die Anwendung gespeichert. Beim nächsten Öffnen des Assistenten werden die Variablen automatisch angezeigt.
{: tsResolve}



## Symbole für {{site.data.keyword.Bluemix_notm}} Live Sync werden nicht angezeigt
{: #ts_llz_lkb_3r}

Sie haben in IBM Bluemix DevOps Services eine App erstellt, aber die Symbole für IBM Bluemix Live Sync werden in der Web-IDE nicht angezeigt.

 

Wenn Sie eine Node.js-App in der Web-IDE von DevOps Services bearbeiten, werden die Symbole für {{site.data.keyword.Bluemix_notm}} Live Edit, für den schnellen Neustart und für das Debugging nicht angezeigt.
{: tsSymptoms}

 

Die Symbole stehen unter folgenden Umständen nicht zur Verfügung:
{: tsCauses}

  * Die Datei `manifest.yml` ist nicht auf der höchsten Ebene Ihres Projekts gespeichert.
  * Ihre App ist in einem Unterverzeichnis und nicht auf der höchsten Ebene Ihres Projekts gespeichert; der Pfad zum Unterverzeichnis jedoch wird in der Datei `manifest.yml` nicht angegeben.
  * Die App enthält nicht die Datei `package.json`.


Verwenden Sie eine der folgenden Methoden, um das Problem zu lösen: 
{: tsResolve} 

  * Ist die Datei `manifest.yml` nicht auf der höchsten Ebene Ihres Projekts gespeichert, speichern Sie sie dort.
  * Ist Ihre App in einem Unterverzeichnis gespeichert, geben Sie den Pfad zum Unterverzeichnis in der Datei `manifest.yml` an.
  ```
   path: path_to_application
   ```
  * Erstellen Sie die Datei `package.json` im selben Verzeichnis wie Ihre App.

  
  
  

  
  

  
  
## Suchen von Organisationen in {{site.data.keyword.Bluemix_notm}} nicht möglich
{: #ts_orgs}

Es kann vorkommen, dass Sie Ihre Organisation in {{site.data.keyword.Bluemix_notm}} nicht suchen können, wenn Sie in einer {{site.data.keyword.Bluemix_notm}}-Region arbeiten.
  
 

Sie können sich zwar erfolgreich an der {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle anmelden, jedoch nicht Anwendungen mithilfe der cf-Befehlszeilenschnittstelle oder des Eclipse-Plug-ins per Push-Operation übertragen.
{: tsSymptoms}

Wenn Sie versuchen, mithilfe der Befehlszeilenschnittstelle 'cf' eine Anwendung per Push-Operation an
{{site.data.keyword.Bluemix_notm}} zu übertragen,
wird eine der folgenden Fehlernachrichten mit angegebenem Organisationsnamen angezeigt: 

`Error finding org` (Fehler bei der Suche nach der Organisation)

`Organization not found` (Organisation nicht gefunden)


Wenn Sie versuchen, mithilfe des Eclipse-Plug-ins von Cloud Foundry eine Anwendung per Push-Operation an {{site.data.keyword.Bluemix_notm}} zu übertragen, wird die folgende Fehlernachricht angezeigt:

`Cloudspace not found` (Cloudbereich nicht gefunden)



Dieses Problem tritt auf, weil der API-Endpunkt der Region, mit der Sie arbeiten möchten, nicht angegeben ist, und sich die gesuchte Organisation eventuell in einer anderen Region befindet.
{: tsCauses} 

   
  
Wenn Sie eine Anwendung mithilfe der cf-Befehlszeilenschnittstelle per Push-Operation an {{site.data.keyword.Bluemix_notm}} übertragen, geben Sie den Befehl 'cf api' ein und geben Sie den API-Endpunkt der Region an. Geben Sie beispielsweise den folgenden Befehl ein, um eine Verbindung zu der {{site.data.keyword.Bluemix_notm}}-Region 'Europe United Kingdom' herzustellen:
{: tsResolve}

```
cf api https://api.eu-gb.bluemix.net
```
Wenn Sie eine Anwendung mithilfe von Eclipse Tools mit einer Push-Operation an {{site.data.keyword.Bluemix_notm}} übertragen, müssen Sie zuerst einen {{site.data.keyword.Bluemix_notm}}-Server erstellen und den API-Endpunkt der {{site.data.keyword.Bluemix_notm}}-Region angeben, in der die Organisation erstellt wurde. Weitere Informationen zur Verwendung
der Eclipse-Tools finden Sie im Thema zur [Bereitstellung von Apps mit IBM Eclipse Tools for Bluemix](../manageapps/eclipsetools/eclipsetools.html){: new_window}.  
  
  


## Erstellung einer Anwendungsroute nicht möglich
{: #ts_hostistaken}

Wenn Sie eine Anwendung unter {{site.data.keyword.Bluemix_notm}} implementieren, kann die Route einer Anwendung nicht erstellt werden, wenn der angegebene Hostname bereits verwendet wird.



Wenn Sie eine Anwendung unter {{site.data.keyword.Bluemix_notm}} bereitstellen, wird die folgende Fehlernachricht angezeigt: 
{: tsSymptoms} 

`Creating route hostname.domainname ... FAILED Server error, status code: 400, error code: 210003, message: The host is taken: hostname` (Erstellen von Route 'hostname.domänenname' ... FEHLGESCHLAGEN Serverfehler, Statuscode: 400, Fehlercode: 210003, Nachricht: Der Hostname ist vergeben: 'hostname')



Dieses Problem tritt auf, wenn der angegebene Hostname bereits verwendet wird.
{: tsCauses} 


  
Der angegebene Hostname muss innerhalb der verwendeten Domäne eindeutig sein. Verwenden Sie zum Angeben eines anderen Hostnamens eine der folgenden Methoden:
{: tsResolve} 

  * Wenn Sie zum Implementieren der Anwendung die Datei `manifest.yml` verwenden, geben Sie den Hostnamen in der Option host an.	 
    ```
    host: <hostname>	
	```
  * Wenn Sie die Anwendung über die Eingabeaufforderung bereitstellen, verwenden Sie den Befehl `cf push` mit der Option **-n**. 
    ```
    cf push <appname> -p <app_path> -n <hostname>
    ```


## Push-Operation für WAR-Anwendung mit Befehl 'cf push' nicht möglich
{: #ts_cf_war}

Es kann vorkommen, dass Sie mit dem Befehl 'cf push' nicht eine archivierte Webanwendung unter {{site.data.keyword.Bluemix_notm}} implementieren können, wenn die Position der Anwendung nicht ordnungsgemäß angegeben ist.
	


Wenn Sie eine WAR-Anwendung in {{site.data.keyword.Bluemix_notm}} mit dem Befehl `cf push` hochladen, wird die Fehlernachricht `Staging error: cannot get instances since staging failed.` (Staging-Fehler: Instanzen können nicht abgerufen werden, weil Staging fehlgeschlagen ist) angezeigt.
{: tsSymptoms} 

 

Dieses Problem kann auftreten, wenn die WAR-Datei nicht angegeben ist oder wenn der Pfad zur WAR Datei nicht angegeben ist. 
{: tsCauses}

 	
	
Verwenden Sie die Option **-p** zum Angeben einer WAR-Datei oder fügen Sie den Pfad zur WAR-Datei hinzu. Beispiel:
{: tsResolve}

```
cf push MyUniqueAppName01 -p app.war
```

```
cf push MyUniqueAppName02 -p "./app.war"
```
Weitere Informationen zum Befehl `cf push` erhalten Sie, wenn Sie `cf push -h` eingeben. 	





## Anzeigen von Doppelbytezeichen bei Push-Operation für Anwendungen von Liberty zu {{site.data.keyword.Bluemix_notm}} nicht ordnungsgemäß
{: #ts_doublebytes}

Es kann vorkommen, dass Doppelbytezeichen nicht ordnungsgemäß angezeigt werden, wenn die Unicode-Unterstützung für das Servlet oder die JSP-Dateien nicht ordnungsgemäß konfiguriert wurde.

 

Wenn eine Liberty-Anwendung per Push-Operation an {{site.data.keyword.Bluemix_notm}} übertragen wird, werden Doppelbytezeichen, die in der Anwendung angegeben sind, nicht ordnungsgemäß angezeigt.
{: tsSymptoms}

 

Das Problem kann auftreten, wenn die Unicode-Unterstützung für das Servlet oder die JSP-Dateien nicht ordnungsgemäß konfiguriert ist.
{: tsCauses}


Sie können den folgenden Code im Servlet oder der JSP-Datei verwenden:
{: tsResolve} 

  * In der Servletquellendatei: 
    ```
	response.setContentType("text/html; charset=UTF-8");
	```
  * In der JSP-Datei: 
    ```
	<meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
	```
	
	
	

## Bereitstellung von Node.js-Apps nicht möglich
{: #ts_nodejs_deploy}

Bei der Aktualisierung einer Node.js-App oder bei der Bereitstellung einer Node.js-App in {{site.data.keyword.Bluemix_notm}} kann es zu Problemen kommen.



Bei der Aktualisierung einer Node.js-App oder bei der Bereitstellung einer Node.js-App in {{site.data.keyword.Bluemix_notm}} wird möglicherweise eine der folgenden Fehlernachrichten angezeigt:
{: tsSymptoms} 

`An app was not successfully detected by any available buildpack.` (Eine App wurde von keinem verfügbaren Buildpack erfolgreich erkannt.)


`Instance (index 0) failed to start accepting connections.` (Bestätigen der Verbindungen durch Instanz (Index 0) fehlgeschlagen.)


`Cannot get instances since staging failed.` (Abrufen der Instanzen seit fehlgeschlagenem Staging nicht möglich.)


 

´Das Problem kann die folgenden
Ursachen haben:
{: tsCauses}
 
  * Der Startbefehl ist nicht angegeben.
  * Dateien, die für die Bereitstellung einer Node.js-App erforderlich sind, fehlen in der App
oder befinden sich in einem anderen Ordner und nicht im Stammverzeichnis.
  


	
Führen Sie die folgenden Aktionen
in Abhängigkeit von der Ursache durch, die zu dem Problem geführt hat:
{: tsResolve} 

  * Geben Sie unter Verwendung einer der folgenden Methoden den Startbefehl an: 
      * Mithilfe der Befehlszeilenschnittstelle 'cf'. Beispiel: 
        ```
		cf push MyUniqueNodejs01 -p app_path -c "node app.js"
		```
	  * Mithilfe der Datei [package.json](https://docs.npmjs.com/json){: new_window}. Beispiel:
	    ```
		{
      ...
  	   "scripts": {
	 		 "start": "node app.js"
 	   }
	}
	    ```
	  * Mithilfe der Datei `manifest.yml`. Beispiel: 
	    ```
		applications:
  name: MyUniqueNodejs01
  ...
  command: node app.js
  ...
        ```

  * Stellen Sie sicher, dass in Ihrer Node.js-App eine Datei des Typs `package.json`
existiert, damit das Node.js-Buildpack für die Erkennung der App aktiviert werden kann. Außerdem müssen Sie diese Datei
in das Stammverzeichnis Ihrer App stellen.	
    Im folgenden Beispiel wird eine einfache `package.json`-Datei dargestellt:  
	```
	{
        "name": "MyUniqueNodejs01",
        "version": "0.0.1",
        "description": "A sample package.json file",
        "dependencies": {
                "express": "3.4.x",
                "jade": "1.1.x"
        },
        "engines": {
                "node": "0.10.x"
        },
        "scripts": {
                  "start": "node app.js"
        }
 }
    ```
	
Weitere Tipps
zu Node.js-Apps finden Sie unter [Tips for Node.js Applications](http://docs.cloudfoundry.org/buildpacks/node/node-tips.html){: new_window}.	




## Konfigurationsfehler in Datei `server.xml` nach Import einer {{site.data.keyword.Bluemix_notm}} Liberty-Anwendung von Bluemix DevOps Services in Eclipse
{: #ts_eclipse}

Wenn in der Datei `server.xml` nach dem Import einer {{site.data.keyword.Bluemix_notm}} Liberty-Anwendung aus IBM Bluemix DevOps Services in Eclipse Konfigurationsfehler angezeigt werden, kann es erforderlich sein, die Datei `server.xml` aus dem Projekt zu entfernen. 

 

Nach dem Import einer {{site.data.keyword.Bluemix_notm}} Liberty-Anwendung aus {{site.data.keyword.Bluemix_notm}} DevOps Services in Eclipse werden in der Eclipse-Ansicht 'Fehler' Konfigurationsfehler in der Datei `server.xml` angezeigt. 
{: tsSymptoms}

 

Das Liberty-Buildpack verwendet die Datei `server.xml` zum Konfigurieren der Anwendung und generiert die Datei `runtime-vars.xml`, wenn die Liberty-Anwendung per Push-Operation an {{site.data.keyword.Bluemix_notm}} übertragen wird. Wenn Sie die Anwendung in Eclipse importieren, ist die Datei `runtime-vars.xml` in der lokalen Umgebung nicht vorhanden.
{: tsCauses}

 

Sie können dieses Problem durch Entfernen der Datei server.xml aus dem Projekt beheben. Vom Buildpack wird die Datei `server.xml` dynamisch erstellt, wenn Sie die Anwendung mit einer Push-Operation als WAR-Anwendung übertragen. Weitere Informationen finden Sie unter [Liberty for Java](../runtimes/liberty/index.html){: new_window}.
{: tsResolve}
	
	
## Staging für Anwendung mit angepasstem Buildpack nicht möglich
{: #ts_bp_compilation}

Es kann vorkommen, dass eine Anwendung unter {{site.data.keyword.Bluemix_notm}} nicht unter Verwendung eines angepassten Buildpacks implementiert werden kann, wenn die Scripts im Buildpack nicht ausführbar sind.



Wenn Sie eine App unter {{site.data.keyword.Bluemix_notm}} unter Verwendung eines angepassten Buildpacks implementieren, kann es vorkommen, dass die Fehlernachricht `The application failed to stage, so there are no instances to display.` (Anzeigen der Instanzen nicht möglich, da Staging der Anwendung fehlgeschlagen ist) angezeigt wird.
{: tsSymptoms} 


Dieses Problem kann auftreten, wenn Scripts, wie zum Beispiel die Scripts zum Identifizieren, Kompilieren und Freigeben, nicht ausgeführt werden können.
{: tsCauses}

 

Mit dem Befehl [git update](http://git-scm.com/docs/git-update-index){: new_window} können Sie die Berechtigung für jedes einzelne Script in 'ausführbar' ändern. Sie können zum Beispiel `git update --chmod=+x script.sh` eingeben.
{: tsResolve}
	
	
	
## Eine App kann nicht von DevOps Services für {{site.data.keyword.Bluemix_notm}} bereitgestellt werden
{: #ts_devops_to_bm}

Es kann vorkommen, dass Apps von Bluemix DevOps Services nicht mit einer Push-Operation zu {{site.data.keyword.Bluemix_notm}} übertragen werden können, wenn die Datei `manifest.yml` nicht in der App vorhanden ist.

 

Wenn Sie eine App von DevOps Services in {{site.data.keyword.Bluemix_notm}} implementieren, kann die Fehlernachricht `Unable to detect a supported application type` (Ermittlung eines unterstützten Anwendungstyps fehlgeschlagen) angezeigt werden.
{: tsSymptoms}

 

Dieses Problem kann auftreten, weil für DevOps Services die Datei `manifest.yml` zum Implementieren einer App in {{site.data.keyword.Bluemix_notm}} erforderlich ist.
{: tsCauses}

 

Zum Beheben dieses Problems müssen Sie die Datei `manifest.yml` erstellen. Weitere Informationen zum Erstellen der Datei `manifest.yml` finden Sie im
[Abschnitt zum Anwendungsmanifest](../manageapps/depapps.html#appmanifest){: new_window}.
{: tsResolve}	
	




## Push-Operation für Meteor-Anwendungen nicht möglich
{: #ts_meteor}

Es kann vorkommen, dass eine Meteor-Anwendung nicht per Push-Operation an {{site.data.keyword.Bluemix_notm}} übertragen werden kann, wenn der Buildpack nicht ordnungsgemäß angegeben ist.

 

Wenn Sie eine Meteor-App unter {{site.data.keyword.Bluemix_notm}}implementieren, kann die Fehlernachricht `The application failed to stage, so there are no instances to display.` (Anzeigen der Instanzen nicht möglich, da Staging der Anwendung fehlgeschlagen ist) angezeigt werden.
{: tsSymptoms}


Dieses Problem tritt auf, weil für Meteor-Apps kein integriertes Buildpack bereitgestellt wird. Sie müssen ein angepasstes Buildpack verwenden.
{: tsCauses} 


 

Verwenden Sie eine der folgenden Methoden, um ein angepasstes Buildpack für Meteor-Apps zu verwenden:
{: tsResolve}

  * Wenn Sie zum Implementieren der App die Datei `manifest.yml` verwenden, geben Sie die URL oder den Namen des angepassten Buildpacks mithilfe der Option 'buildpack' an. Beispiel:
  ```
  buildpack: https://github.com/Sing-Li/bluemix-bp-meteor 
  ```
  * Wenn Sie die Anwendung in einer Eingabeaufforderung bereitstellen, verwenden Sie den Befehl `cf push` und geben Sie das angepasste Buildpack mit der Option **-b** an. Beispiel:
    ```
	cf push appname -p app_path -b https://github.com/Sing-Li/bluemix-bp-meteor 
	```
	
  

    
## Schaltfläche für die Bereitstellung in {{site.data.keyword.Bluemix_notm}} führt nicht zum Bereitstellen einer App
{: #deploytobluemixbuttondoesntdeployanapp}

Wenn Sie auf die Schaltfläche für die Bereitstellung in {{site.data.keyword.Bluemix_notm}} klicken und feststellen, dass entweder das Git-Repository nicht geklont oder die App nicht bereitgestellt wurde, können Sie für folgende Probleme versuchen, die Fehlerbehebungsmethoden anzuwenden.
  * [Bluemix DevOps Services-Projekt kann nicht erstellt werden](#project-cannot-be-created)
  * [Git-Repository wurde nicht gefunden und kann in DevOps Services nicht geklont werden](#repo-not-found)
  * [Git-Repository ist in DevOps Services geklont, aber die App wurde in {{site.data.keyword.Bluemix_notm}} nicht bereitgestellt.](#repo-cloned-app-not-deployed) Weitere Informationen zum Erstellen der Schaltfläche finden Sie in 'Schaltfläche für die Bereitstellung in {{site.data.keyword.Bluemix_notm}} erstellen'.

### Bluemix DevOps Services-Projekt kann nicht erstellt werden
{: #project-cannot-be-created}

Wenn Sie feststellen, dass Ihr DevOps Services-Projekt nicht erstellt werden kann, ist möglicherweise Ihr IBM {{site.data.keyword.Bluemix_notm}}-Konto abgelaufen.



Sie klicken auf die Schaltfläche **In Bluemix bereitstellen**, aber der Schritt zum Erstellen eines Projekts wird nicht erfolgreich abgeschlossen.
{: tsSymptoms} 


Möglicherweise ist Ihr {{site.data.keyword.Bluemix_notm}}-Konto abgelaufen.
{: tsCauses} 

Verwenden Sie eine der folgenden Methoden, um das Problem zu lösen:
{: tsResolve}

  * Melden Sie sich bei {{site.data.keyword.Bluemix_notm}} an und aktualisieren Sie Ihre Kontoinformationen.
  * Klicken Sie erneut auf die Schaltfläche **In Bluemix bereitstellen**.


### Git-Repository wurde nicht gefunden und kann in DevOps Services nicht geklont werden
{: #repo-not-found}

Wenn Sie feststellen, dass das Git-Repository nicht geklont wurde, besteht möglicherweise ein Problem mit dem Repository oder mit dem Schaltflächen-Snippet.



Sie klicken auf die Schaltfläche **In Bluemix bereitstellen**, aber das Git-Repository wird nicht gefunden und kann in DevOps Services nicht geklont werden. Der Schritt zum Klonen eines Repositorys wird nicht erfolgreich abgeschlossen. Die App kann daher nicht in {{site.data.keyword.Bluemix_notm}} bereitgestellt werden. 
{: tsSymptoms} 

Dieses Problem kann aufgrund folgender Ursachen auftreten:
{: tsCauses} 

  * Das Git-Repository ist möglicherweise nicht vorhanden oder der Zugriff ist nicht möglich.
  * Möglicherweise besteht ein Problem im HTML- oder Markdown-Code für das Schaltflächen-Snippet.
  * Möglicherweise besteht das Problem, weil Sonderzeichen, Abfrageparameter oder Fragmente in der URL den ordnungsgemäßen Zugriff auf das Git-Repository verhindern.

Verwenden Sie eine der folgenden Methoden, um das Problem zu lösen:
{: tsResolve}

  * Überprüfen Sie, dass das Git-Repository vorhanden ist, dass der öffentliche Zugriff möglich ist und dass die URL richtig ist.
  * Überprüfen Sie, dass das Snippet keine Fehler im HTML- oder Markdown-Code enthält.
  * Wenn Sonderzeichen, Abfrageparameter oder Fragmente ein Problem mit der URL des Git-Repositorys verursachen, codieren Sie die URL im Schaltflächen-Snippet.
  

  
  
### Git-Repository wird in DevOps Services geklont, aber die App wurde in {{site.data.keyword.Bluemix_notm}} nicht bereitgestellt
{: #repo-cloned-app-not-deployed}

Wenn Sie feststellen, dass die App nicht bereitgestellt wurde, bestehen möglicherweise Probleme mit dem Code im Repository.
     


Sie klicken auf die Schaltfläche **In Bluemix bereitstellen** und das Git-Repository wird in DevOps Services geklont, die App wird jedoch nicht in {{site.data.keyword.Bluemix_notm}} bereitgestellt. Der Schritt für die Bereitstellung in Bluemix wird nicht erfolgreich abgeschlossen.
{: tsSymptoms} 

Dieses Problem kann aufgrund folgender Ursachen auftreten:
{: tsCauses}  

  * Möglicherweise ist in Ihrem {{site.data.keyword.Bluemix_notm}}-Bereich nicht ausreichend Speicherplatz zum Bereitstellen einer App vorhanden. 
  * Möglicherweise wurde ein erforderlicher Service nicht in der Datei `manifest.yml` deklariert.
  * Möglicherweise ist ein erforderlicher Service in der Datei `manifest.yml` deklariert, aber der Service befindet sich bereits im Zielbereich.
  * Möglicherweise besteht ein Problem mit dem Code im Repository.
Zum Diagnostizieren des Problems überprüfen Sie den Build und stellen Sie Protokolle aus der Bereitstellung (Implementierung) bereit:
  1. Wenn der Schritt für die Bereitstellung in Bluemix nicht erfolgreich ausgeführt wird, klicken Sie auf den Link im vorherigen Schritt zum Konfigurieren einer Pipeline, um 'Delivery Pipeline' zu öffnen.
  2. Ermitteln Sie die fehlgeschlagene Build- oder Bereitstellungsphase.
  3. Klicken Sie in der fehlgeschlagenen Phase auf die Option **Protokolle und Verlauf anzeigen**.
  4. Suchen Sie nach der Fehlernachricht.
   
Verwenden Sie eine der folgenden Methoden, um das Problem zu lösen:
{: tsResolve}

  * Wenn in der Fehlernachricht angegeben wird, dass im {{site.data.keyword.Bluemix_notm}}-Bereich nicht genügend Speicherplatz für die Bereitstellung der App vorhanden ist, wählen Sie als Ziel einen anderen Bereich aus.
  * Wenn in der Fehlernachricht angegeben wird, dass ein erforderlicher Service nicht in der Datei `manifest.yml` deklariert wurde, benachrichtigen Sie den Repository-Eigner darüber, dass der erforderliche Service hinzugefügt werden muss.
  * Wenn in der Fehlernachricht angegeben wird, dass ein erforderlicher Service im Zielbereich bereits vorhanden ist, wählen Sie aus, dass ein anderer Bereich verwendet werden soll.
  * Wenn in der Fehlernachricht angegeben wird, dass mit dem Build ein Problem besteht, beheben Sie alle Fehler im Code, die verhindern, dass für die App ein Build erfolgen kann. Zum Überprüfen, dass der Code keine Probleme enthält, erstellen Sie den Code mithilfe von Git-Befehlen:
    1. Klonen Sie das Git-Repository:
    ```
    git clone <URL des Git-Repositorys>
    ```
	2. Öffnen Sie das Verzeichnis der App:
	```
	cd <appname>
	```
	3. Erstellen Sie die App:
	```
	<appname> create
	```
	4. Stellen Sie Add-ons bereit, falls erforderlich.
	5. Fügen Sie erforderliche Konfigurationsvariablen hinzu.
	6. Führen Sie die Push-Operation für den Code durch:
	```
	git push <appname> master
	```
	7. Überprüfen Sie, dass der Build für die App ordnungsgemäß ausgeführt wird.
	8. Führen Sie, falls erforderlich, den nach der Bereitstellung auszuführenden Befehl (post deployment) aus:
	```
	<appname> run
	```
	9. Öffnen Sie die App und prüfen Sie, ob sie ordnungsgemäß ausgeführt wird:
	```
	<appname> open
	```
	



# Fehlerbehebung für die Verwaltung von Konten
{: #managingaccounts}

Es können Probleme bei der Verwaltung Ihres Kontos auftreten; so kann es zum Beispiel vorkommen, dass unterschiedliche Anwendungen gemeinsam denselben Domänennamen nutzen oder Administratoren nicht alle Organisationen anzeigen können. In vielen Fällen können Sie diese Probleme jedoch durch Ausführen weniger einfacher Schritte beheben.
{:shortdesc}


## Konto ist inaktiv
{: #ts_accnt_inactive}

Wenn Ihr Konto inaktiv ist, können Sie keine Anwendung in {{site.data.keyword.Bluemix_notm}} erstellen. Wenden Sie sich zur Lösung dieses Problems an das Support-Team.



Bei dem Versuch, in {{site.data.keyword.Bluemix_notm}} eine Anwendung zu erstellen, wird die folgende Fehlernachricht angezeigt:
{: tsSymptoms} 

`BXNUI0096E: Die App wurde nicht erstellt. Ihr Konto ist inaktiv, da es storniert oder ausgesetzt wurde.`


Der Status Ihres {{site.data.keyword.Bluemix_notm}}-Kontos verändert sich in 'Inaktiv', wenn es storniert oder ausgesetzt wurde.
{: tsCauses}

 

Wenden Sie sich an den [{{site.data.keyword.Bluemix_notm}}-Support](http://ibm.biz/bluemixsupport.com){: new_window}, um Ihr Konto zu reaktivieren. In der E-Mail müssen die folgenden Angaben enthalten sein:
{: tsResolve}

  * Die IBM ID, mit der Sie sich bei {{site.data.keyword.Bluemix_notm}} anmelden.
  * Der Name der Organisation für Ihre Anwendung. Mithilfe dieser Informationen kann das Support-Team feststellen, ob Ihnen die richtigen Rollen bzw. die richtige Zugehörigkeit innerhalb Ihrer Organisation zugewiesen wurden.



## Der momentanen Organisation ist kein Bereich zugeordnet
{: #ts_no_space}

Wenn Ihrer momentanen Organisation kein Bereich zugeordnet ist,
können Sie keine Anwendung erstellen.



Bei dem Versuch, in {{site.data.keyword.Bluemix_notm}} eine Anwendung zu erstellen, wird die folgende Fehlernachricht angezeigt:
{: tsSymptoms} 


`BXNUI0097E: Bevor Sie eine App hinzufügen können, muss Ihrer Organisation und Ihrer Region mindestens ein Bereich zugeordnet sein. Klicken Sie auf dem Dashboard auf die Option **Bereich erstellen**. Wiederholen Sie den Vorgang, wenn der Bereich erstellt worden ist. `



Anwendungen in {{site.data.keyword.Bluemix_notm}} müssen in Ihrer Organisation innerhalb eines Bereichs erstellt werden.
{: tsCauses} 

 

Wenden Sie eine der folgenden Methoden an,
um einen Bereich zu erstellen: 
{: tsResolve}
 
  * Wählen Sie auf dem Dashboard von {{site.data.keyword.Bluemix_notm}} die Organisation aus, in der Sie den Bereich erstellen möchten;
klicken Sie anschließend auf **Bereich erstellen**.
  * Geben Sie in die Befehlszeilenschnittstelle ```cf create-space <space_name> -o <organization_name>``` ein.
  
  
  
  
## Identische Domänennamen für unterschiedliche Anwendungen
{: #ts_domain_diff}

Es kann vorkommen, dass in {{site.data.keyword.Bluemix_notm}} von mehreren Anwendungen dieselbe URL gemeinsam genutzt wird.

 

Dieses Problem kann auftreten, wenn Sie unterschiedlichen Anwendungen in einem Bereich dieselbe URL-Route zuweisen.
{: tsCauses}

Beispiel: Sie übertragen die Anwendung 'myApp1' per Push-Operation an {{site.data.keyword.Bluemix_notm}} und legen als Domäne "mynewapp.mybluemix.net" fest. Anschließend übertragen Sie eine weitere Anwendung mit dem Namen 'myApp2' per Push-Operation in denselben Bereich und legen für eine der URL-Routen den Namen "mynewapp.mybluemix.net" fest. Die Route ist jetzt beiden Anwendungen zugeordnet.

 

Hierbei handelt es sich um ein unterstütztes Verhalten von {{site.data.keyword.Bluemix_notm}}; Sie können dieses Verfahren verwenden, um beim Upgrade einer Anwendung Ausfallzeiten vollständig zu vermeiden. Weitere Informationen finden Sie im Abschnitt zu Blue-Green-Bereitstellungen.
{: tsResolve}
  
	
	





## Kreditkarte kann nicht hinzugefügt werden
{: #ts_addcc}

Sie können Ihre Kreditkarteninformationen nicht übergeben, um Ihr Testkonto in ein Konto für nutzungsabhängige Zahlung umzuwandeln.

 

Die Schaltfläche 'Übergeben' auf der Seite 'Kreditkarte' hinzufügen ist inaktiviert.
{: tsSymptoms}

 

Dieses Problem tritt auf, wenn Sie auf der Seite 'Kreditkarte hinzufügen' nicht die korrekten Informationen eingegeben haben.
{: tsCauses}

 

Zur Lösung des Problems führen Sie die folgenden Schritte durch:
{: tsResolve}

  1. Füllen Sie auf der Seite 'Kreditkarte hinzufügen' alle erforderlichen Felder in den Abschnitten für die Kontaktinformationen, die Kontaktadresse und die Rechnungsadresse aus.
  2. Wählen Sie das Kontrollkästchen unter **Ich habe die allgemeinen Geschäftsbedingungen von IBM gelesen und stimme ihnen zu** aus und klicken Sie auf **Übergeben**. Der Abschnitt **Wählen Sie eine Zahlungsmethode aus** wird angezeigt.
  3. Geben Sie Ihre Kreditkartennummer, das Ablaufdatum Ihrer Karte und den Sicherheitscode auf Ihrer Karte ein. Anschließend klicken Sie auf **Übergeben**.





# Fehlerbehebung für Laufzeiten
{: #runtimes}

Es können Probleme bei der Verwendung von IBM® Bluemix™-Laufzeiten auftreten. In vielen Fällen können Sie diese Probleme jedoch durch Ausführen weniger einfacher Schritte beheben.
{:shortdesc}


## Bei einer Push-Operation für eine App wird ein veraltetes Buildpack aus dem Cache geladen
{: #ts_loading_bp}


Bei einer Push-Operation für eine App können möglicherweise nicht die neuesten Buildpack-Komponenten verwendet werden. Sie können Buildpacks mit integrierten Mechanismen verwenden, die das Laden veralteter Komponenten verhindern,
oder Sie können den Inhalt des Cacheverzeichnisses der App löschen, bevor Sie eine Push-Operation oder
erneutes Staging für die App durchführen. 

 

Wenn Sie eine Push-Operation oder
erneutes Staging für eine App durchführen, nachdem das Buildpack aktualisiert wurde, werden die neuesten
Buildpack-Komponenten nicht automatisch geladen. Dies führt dazu, dass die App die veralteten Buildpack-Komponenten verwendet. Aktualisierungen, die für das Buildpack angewendet wurden, seit die letzte Push-Operation
für die App ausgeführt wurde, werden nicht implementiert. 
{: tsSymptoms}



Einige Buildpacks
sind nicht so konfiguriert, dass sie alle aktualisierten Komponenten automatisch aus dem Internet herunterladen,
um sicherzustellen, dass stets die neueste Version verwendet wird.
{: tsCauses} 

 

Sie können Buildpacks verwenden,
die über integrierte Mechanismen verfügen, mit denen das Laden veralteter Komponenten vermieden wird. Zwei Beispiele für diese Buildpacks sind nachfolgend aufgeführt: 
{: tsResolve}

  * [Cloud Foundry Java-Buildpack](https://github.com/cloudfoundry/java-buildpack){: new_window}. Dieses Buildpack verfügt über einen integrierten Mechanismus, der sicherstellt,
dass die neueste Version des Buildpacks verwendet wird. Weitere Informationen zur Funktionsweise dieses Mechanismus finden Sie in [extending-caches.md](https://github.com/cloudfoundry/java-buildpack/blob/master/docs/extending-caches.md){: new_window}. 
  * [Cloud Foundry Node.js-Buildpack](https://github.com/cloudfoundry/nodejs-buildpack){: new_window}. Dieses Buildpack verfügt über eine ähnliche Funktionalität, die Umgebungsvariablen nutzt. Damit das Node.js-Buildpack jedes mal Knotenmodule aus dem Internet herunterladen kann,
geben Sie in der cf-Befehlszeilenschnittstelle den folgenden Befehl ein: 	
  ```
  set NODE_MODULES_CACHE=false
  ```
Wenn das verwendete Buildpack keinen Mechanismus zum automatischen Laden
der neuesten Komponenten bereitstellt, können Sie den Inhalt des Cacheverzeichnisses manuell löschen und
eine Push-Operation für Ihre App durchführen, indem Sie die folgenden Schritte ausführen:
  1. Checken Sie eine Verzweigung eines Null-Buildpacks aus, z. B. https://github.com/ryandotsmith/null-buildpack. Informationen zum Auschecken einer Verzweigung finden Sie in
[Git Basics - Getting a Git Repository](http://www.git-scm.com/book/en/v2/Git-Basics-Getting-a-Git-Repository){: new_window}.  
  2. Fügen Sie die folgende Zeile zur Datei `null-buildpack/bin/compile` hinzu
und schreiben Sie die Änderungen fest. Informationen zum Festschreiben von Änderungen finden Sie in [Git Basics - Recording Changes to the Repository](http://www.git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository){: new_window}.
  ```
  rm -rfv $2/*
  ```
  3. Führen Sie für Ihre App eine Push-Operation mit dem modifizierten Null-Buildpack durch,
um den Inhalt des Cache zu löschen. Verwenden Sie hierzu den folgenden Befehl: Nach der Ausführung dieses Schritts ist der gesamte Inhalt des Cacheverzeichnisses Ihrer App gelöscht.
  ```
  cf push appname -p app_path -b <modified_null_buildpack>
  ```
  4. Führen Sie für Ihre App eine Push-Operation mit dem neuesten Buildpack durch,
das Sie verwenden möchten. Geben Sie hierzu den folgenden Befehl ein: 
  ```
  cf push appname -p app_path -b <latest_buildpack>
  ```
  
	


## NOTICE-Nachrichten des PHP-Buildpacks
{: #ts_phplog}

Möglicherweise werden Nachrichten angezeigt, die einen Hinweis (NOTICE) aus den Protokollen enthalten. Sie können die Protokollierung dieser Nachrichten stoppen, indem Sie die Protokollstufe ändern.	
	
 

Wenn Sie eine Anwendung per Push-Operation an Bluemix übertragen, indem Sie ein PHP-Buildpack verwenden, werden möglicherweise Nachrichten angezeigt, die das Wort `NOTICE` (Hinweis) enthalten:
{: tsSymptoms}

```
• 2015-01-26T15:00:59.70+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: [pool www] 'user' directive is ignored when FPM is not running as root
• 2015-01-26T15:01:00.63+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: [pool www] 'user' directive is ignored when FPM is not running as root
• 2015-01-26T15:01:00.63+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: fpm is running, pid 93
• 2015-01-26T15:01:00.63+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: ready to handle connections
```



Im PHP-Buildpack wird der Parameter 'error_log' zum Definieren der Protokollstufe verwendet. Der Wert des Parameters `error_log` lautet standardmäßig **stderr notice**. Das folgende Beispiel zeigt die Standardkonfiguration für die Protokollstufe in der Datei `nginx-defaults.conf` des von Cloud Foundry bereitgestellten PHP-Buildpacks. Weitere Informationen finden Sie unter [cloudfoundry/php-buildpack](https://github.com/cloudfoundry/php-buildpack/blob/ff71ea41d00c1226d339e83cf2c7d6dda6c590ef/defaults/config/nginx/1.5.x/nginx-defaults.conf){: new_window}.
{: tsCauses} 

```
daemon off;
error_log stderr notice;
pid @{HOME}/nginx/logs/nginx.pid;
```

 	
	
Die `NOTICE`-Nachrichten haben lediglich Informationswert und geben nicht unbedingt an, dass ein Problem aufgetreten ist. Sie können die Protokollierung dieser Nachrichten stoppen, indem Sie in der Datei 'nginx-defaults.conf' Ihres Buildpacks die Protokollstufe von 'stderr notice' in 'stderr error' ändern. Beispiel: 	
{: tsResolve}

```
daemon off;
error_log stderr error;
pid @{HOME}/nginx/logs/nginx.pid;
```
Weitere Informationen dazu, wie die Standardkonfiguration für die Protokollierung geändert wird, finden Sie unter [error_log](http://nginx.org/en/docs/ngx_core_module.html#error_log){: new_window}.
	

## Importieren der Python-Bibliothek eines Drittanbieters in {{site.data.keyword.Bluemix_notm}} nicht möglich
{: #ts_importpylib}

Möglicherweise können Sie die Python-Bibliothek eines Drittanbieters nicht in {{site.data.keyword.Bluemix_notm}} importieren. Sie können das Problem lösen, indem Sie dem Stammverzeichnis Ihrer Python-Anwendung Konfigurationsdateien hinzufügen.


Beim Versuch, die Python-Bibliothek eines Drittanbieters (beispielsweise die Bibliothek `web.py`) zu importieren, schlägt der Befehl `cf push` fehl.
{: tsSymptoms}


 

Dieses Problem tritt auf, wenn für die Python-Anwendung Konfigurationsinformationen fehlen.
{: tsCauses}


 

Fügen Sie zum Lösen des Problems die Datei `requirements.txt` und die Datei `Procfile` im Stammverzeichnis Ihrer Python-Anwendung hinzu. Bei den folgenden Informationen wird vorausgesetzt, dass Sie die Bibliothek 'web.py' importieren:
{: tsResolve}

  1. Fügen Sie die Datei `requirements.txt` im Stammverzeichnis Ihrer Python-Anwendung hinzu.
     Die Datei `requirements.txt` gibt die für Ihre Python-Anwendung erforderlichen Bibliothekspakete sowie die Version der Pakete an. Das folgende Beispiel zeigt den Inhalt der Datei `requirements.txt`, wobei `web.py==0.37` angibt, dass es sich bei der Version der Bibliothek `web.py` um '0.37' handelt, und `wsgiref==0.1.2` angibt, dass es sich bei der für die Bibliothek 'web.py' erforderliche Version der Gateway-Schnittstelle des Web-Servers um '0.1.2' handelt.
	 ```
	 web.py==0.37
     wsgiref==0.1.2
	 ```
	Weitere Informationen zur Konfiguration der Datei `requirements.txt` finden Sie unter [Requirements files](https://pip.readthedocs.org/en/1.1/requirements.html). 
	 
  2. Fügen Sie im Stammverzeichnis Ihrer Python-Anwendung die Datei `Procfile` hinzu.
	Die Datei `Procfile` muss den Startbefehl für Ihre Python-Anwendung enthalten. Im folgenden Befehl ist *NameIhrerAnwendung* der Name Ihrer Python-Anwendung und *PORT* ist die Portnummer, die Ihre Python-Anwendung zum Empfangen von Anforderungen von Benutzern der Anwendung verwenden muss. *$PORT* ist optional. Wenn Sie im Startbefehl PORT nicht angeben, wird stattdessen die Portnummer unter der Umgebungsvariablen `VCAP_APP_PORT` verwendet, die sich innerhalb der Anwendung befindet. 
	```
	web: python <NameIhrerAnwendung>.py $PORT
	```
Sie können nun die Python-Bibliothek eines Drittanbieters in {{site.data.keyword.Bluemix_notm}} importieren.	



## Schaltfläche 'Aktionen' auf Seite 'Instanzdetails' ist inaktiviert
{: #ts_actionsbutton}



Die Schaltfläche 'Aktionen' auf der Seite 'Instanzdetails' ist inaktiviert.
{: tsSymptoms} 

 

Dieses Problem tritt aufgrund folgender Ursachen auf:
{: tsCauses}

  * Die Anwendung ist keine Java™-Webanwendung. Von Runtime Management Utilities (RMU) werden nur Webanwendungen unterstützt, die mit Liberty-Buildpacks bereitgestellt werden.
  * Die Anwendung wurde nicht mit dem integrierten Liberty-Buildpack bereitgestellt.
  * Die Anwendung wurde mit einer älteren Version eines Liberty-Buildpacks bereitgestellt.



Wenn das Problem durch eine ältere Version des Liberty-Buildpacks verursacht wird, stellen Sie die Anwendung erneut in {{site.data.keyword.Bluemix_notm}} bereit. Andernfalls können Sie dem Support-Team die folgenden Protokolldateien der Clientanwendung zur Verfügung stellen:
{: tsResolve} 

  * logs/messages.log
  * logs/stdout.log
  * logs/stderr.log
  

  
  
## Berechtigungsnachweise beim Öffnen des Trace- oder Speicherauszugsfensters erforderlich
{: #ts_username}


 

Zum Öffnen des Trace- und Speicherauszugsfenster sind ein Benutzername und ein Kennwort erforderlich.
{: tsSymptoms}

 

Dieses Problem tritt auf, weil das Zeitlimit für die Anmeldesitzung überschritten ist.
{: tsCauses}

 

Die Lösung besteht darin, den Benutzernamen und das Kennwort erneut einzugeben.
{: tsResolve}




## Fehler treten während Ausführung von Trace- oder Speicherauszugsoperationen auf
{: #ts_target}

 

Während Trace- oder Speicherauszugsoperationen ausgeführt werden, wird eine Fehlernachricht angezeigt. Die Nachricht gibt an, dass sich eine Zielinstanz für eine App nicht im Status 'Aktiv' befindet:	
{: tsSymptoms}

```
Instance 0: Trace specification is set successfully
Instance 2: Trace specification is set successfully
Instance 1: Target instance 1 for app abcd is not in the running state.
Instance 3: Trace specification is set successfully
Instance 4: Trace specification is set successfully
```



Dieses Problem tritt aufgrund folgender Ursachen auf:
{: tsCauses} 

  * Die Funktionen für die Trace- und Speicherauszugsverwaltung stehen nur für Anwendungsinstanzen zur Verfügung, die aktiv sind. Trace- bzw. Speicherauszugsoperationen können nicht für Anwendungen verwendet werden, die gestoppt wurden, derzeit gestartet werden oder ausgefallen sind.
  * Der Status der Anwendungsinstanz wird geändert, wenn der Trace- oder Speicherauszugsdialog geöffnet wird. 
  


Die Lösung für dieses Problem ist, das Fenster zu schließen und es anschließend wieder zu öffnen.
{: tsResolve} 



## Instanzen verfügen über unterschiedliche Konfigurationen für Tracespezifikation
{: #ts_different_config}

 

Für unterschiedliche Instanzen einer Anwendung können unterschiedliche Konfiguration für die Tracespezifikation angezeigt werden.
{: tsSymptoms}

 

Dieses Problem tritt aufgrund folgender Ursachen auf:
{: tsCauses}

  * Es kann vorkommen, dass die Konfiguration vorher für mindestens eine Instanz geändert wurde. Wenn Sie die Konfiguration für eine Tracespezifikation ändern, wird die Änderung nicht auf die anderen Instanzen derselben Anwendung angewendet. Beispiel: Von der Anwendung wird 'log4j' verwendet und Sie verfügen über 2 Instanzen für diese Anwendung. Sie können die Protokollebene für Instanz 0 von 'info' in 'debug' ändern, die Protokollebene für Instanz 1 bleibt jedoch 'info'. 
  * Für die Anwendung wird ein Scale-out durchgeführt und sie verfügt über neue Instanzen. Von Runtime Management Utilities (RMU) wird die Konfiguration der Tracespezifikation auf die neue Instanz angewendet, für die das Scale-out durchgeführt wird. Von der neuen Instanz wird die Standardkonfiguration verwendet. Beispiel: Von der Anwendung wird 'log4j' verwendet und sie verfügt über eine Instanz. Sie können die Protokollebene dieser Instanz 0 von 'info' in 'debug' ändern. Wenn Sie diese Änderung durchgeführt und für die Anwendung ein Scale-out in zwei Instanzen durchgeführt haben, lautet die Protokollebene der neuen Instanz 'info' und nicht 'debug'.
  


Hierbei handelt es sich um ein erwartetes Verhalten.
{: tsResolve} 





## Überschrittenes Datenträgerkontingent
{: #ts_diskquota}

Es kann vorkommen, dass im Anwendungsprotokoll angezeigt wird, dass das Datenträgerkontingent überschritten ist.

 

Die Fehlernachricht `Disk quota exceeded` (Datenträgerkontingent überschritten) wird im Protokoll der Anwendung angezeigt.
{: tsSymptoms}



Dieses Problem wird durch einen der folgenden Gründe verursacht: 
{: tsCauses} 

  * Die Speicherauszugsdateien werden mit aktiven Anwendungsinstanzen generiert und die Dateien belegen das zugeordnete Datenträgerkontingent. Das Datenträgerkontingent für eine Anwendungsinstanz beträgt standardmäßig 1 GB. Wenn Sie die Plattenbelegung überprüfen möchten, klicken Sie auf **Dashboard>Anwendung>Anwendungslaufzeit**. Im folgenden Beispiel werden die Laufzeitinformationen inklusive der Plattenbelegung für zwei Instanzen einer Anwendung aufgeführt:
    ```
    Instance	State	CPU	Memory Usage	Disk Usage

	0		Running	1.0%	344.8MB/512MB	236.8MB/1GB
	2		Running	2.3%	361.2MB/512MB	235.7MB/1GB
    ```
  * Das Datenträgerkontingent wird durch das aktuelle Organisationskontingent eingeschränkt.
  
  


Sie können dieses Problem auch auf eine der folgenden Methoden beheben:
{: tsResolve} 

  * Löschen der Speicherauszugsdateien, nachdem sie heruntergeladen wurden.
  * Erneute Bereitstellung der Anwendung mit einem größeren Datenträgerkontingent und dem folgenden Eintrag im Bereitstellungsmanifest:
    ```
	disk_quota: 2048
	```
	
	


