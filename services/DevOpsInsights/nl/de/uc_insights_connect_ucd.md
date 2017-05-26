---

copyright:
  years: 2017
lastupdated: "2017-03-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# IBM UrbanCode Deploy-Server mit Delivery Insights verbinden
{: #connect_ucd}

Um Daten von einem IBM UrbanCode Deploy-Server in Delivery Insights anzeigen zu können, müssen Sie ein Patch auf dem Server installieren und dann diesen Server mit DevOps Connect verbinden.
{:shortdesc}

## Vorbereitende Schritte

- Entsprechende Informationen finden Sie im Abschnitt mit den [Voraussetzungen](uc_insights_prereqs.html), einschließlich Informationen zum Einrichten einer Instanz von DevOps Connect. 
- Ihr IBM UrbanCode Deploy-Server muss Version 6.2 oder höher sein. 

## Vorgehensweise

1. Installieren Sie das Patch auf Ihrem IBM UrbanCode Deploy-Server. Alle Versionen von IBM UrbanCode Deploy benötigen ein Patch für die Kommunikation mit DevOps Connect.  
  1. Laden Sie das richtige Patch für Ihre Version von IBM UrbanCode Deploy herunter, indem Sie die folgende Seite aufrufen und das entsprechende Patch herunterladen:
  [http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/](http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/). 

  1. Extrahieren Sie die Datei. Sie enthält eine oder mehrere Patchdateien, die dem Server hinzugefügt werden müssen. 

  1. Stoppen Sie den Server. Informationen hierzu finden Sie in der Veröffentlichung zum [Starten und Stoppen des Servers](https://www.ibm.com/support/knowledgecenter/SS4GSP_6.2.3/com.ibm.udeploy.install.doc/topics/run_server.html). 

  1. Legen Sie die Dateien im Ordner <code><em>anwendungsdaten</em>/patches</code> ab, wobei <code><em>anwendungsdaten</em></code> der Ordner mit den Serveranwendungsdaten ist. Der Standardanwendungsdatenordner lautet unter Linux `/opt/ibm-ucd/server/appdata` und unter Windows `C:\Programme\ibm-ucd\server\appdata`. Auf Hochverfügbarkeitssystemen befindet sich der Anwendungsdatenorder immer auf einem gemeinsam genutzten Netzlaufwerk, auf das jeder Server Zugriff hat. 

  1. Optional: Während der Server gestoppt ist, können Sie den Datenimport von diesem Server verbessern, indem Sie für die Datenbank die folgenden SQL-Befehle ausführen:  
  ```
  create index rt_cpr_submitted_time on MyUCDDatabase.rt_app_process_request(submitted_time); 
  create index rt_cpr_submitted_time on MyUCDDatabase.rt_comp_process_request(component_id, submitted_time);
  ```
  Verwenden Sie den Namen Ihrer Datenbank für `MyUCDDatabase`.
  <!-- Ross says that this will not be necessary for versions 6.2.4.1 and later if he gets his code changes in. -->

  1. Starten Sie den Server.  

    **Hinweis:** Es kann möglicherweise länger als normal dauern, bis der IBM UrbanCode Deploy-Server gestartet wird. Falls der Server letztendlich nicht startet oder nicht ordnungsgemäß funktioniert, löschen Sie die Patchdateien und starten Sie den Server erneut. Die Patchdateien wirken sich nicht permanent auf den Server aus. 

1. Für einige Versionen von IBM UrbanCode Deploy ist ein zusätzlicher Patch für den Server erforderlich, damit eine Verbindung zu DevOps Connect hergestellt werden kann. Wenn Sie IBM UrbanCode Deploy Version 6.2 bis 6.2.1.2 verwenden, müssen Sie das folgende zusätzliche Patch auf dem Server installieren:
  1. Laden Sie das Patch herunter: [http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/ucd-6.2.1.1-WI149200-CLI-Updates-for-UCSync.jar](http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/ucd-6.2.1.1-WI149200-CLI-Updates-for-UCSync.jar).
  1. Stoppen Sie den Server. 
  1. Legen Sie die Patchdatei im Ordner <code><em>anwendungsdaten</em>/patches</code> ab. 
  1. Starten Sie den Server. 

1. Erstellen Sie eine Integration zwischen DevOps Connect und dem IBM UrbanCode Deploy-Server:  
  **Wichtig:** Bei der ersten Ausführung der Integration ruft DevOps Connect Daten für die letzten 90 Tage ab. Wenn Sie über eine große Menge an Bereitstellungsdaten verfügen, kann dieser Prozess sehr lange dauern. Informationen darüber, wie Sie Daten für weniger als 90 Tage abrufen, finden Sie in [Fehlerbehebung](uc_insights_connect_ucd.html#troubleshooting). 
  1. Erstellen Sie in IBM UrbanCode Deploy ein Authentifizierungstoken. Weitere Informationen finden Sie in der Veröffentlichung [Tokens](https://www.ibm.com/support/knowledgecenter/SS4GSP_6.2.3/com.ibm.udeploy.admin.doc/topics/security_token.html). 
  1. Klicken Sie in DevOps Connect auf **Integrationen** und dann auf **Neue hinzufügen**. 
  1. Geben Sie einen Namen und eine Beschreibung für die Integration an. Die Standardposition von DevOps Connect ist `https://hostname:8443/`, wobei `hostname` der Hostname des Systems ist, das DevOps Connect hostet. 
  1. Wählen Sie aus der Liste mit den Integrationstypen die Option **IBM UrbanCode Deploy for Cloud Reporting** aus. 
  1. Geben Sie im Feld für den Server-URI die öffentliche URL des IBM UrbanCode Deploy-Servers ein. Beispiel: `https://my_UCD.example.com:8447`. 
  1. Geben Sie im Feld für das Authentifizierungstoken das Authentifizierungstoken an, das von IBM UrbanCode Deploy generiert wurde. 
  1. Geben Sie im Feld für den Benutzer mit Administratorberechtigung eine durch Kommas getrennte Liste mit IBM IDs ein, die Zugriff auf die DevOps Connect-Schnittstelle erhalten sollen. 
  1. Optional: Klicken Sie auf **Integration ausführen**, um die Integration sofort auszuführen. Standardmäßig werden Integrationen jede Minute ausgeführt. 
  1. Klicken Sie auf **Speichern**.

  ![Integration in DevOps Connect einrichten](images/uc_insights_dc_integration.gif)

Nun sind Ihre Daten mit Delivery Insights synchronisiert. Basierend auf diesen Daten können Sie jetzt Berichte erstellen und anzeigen. 

## Fehlerbehebung
{: #troubleshooting}

Wenn viele Prozessanforderungen für Anwendungen und Komponenten in der IBM UrbanCode Deploy-Serverdatenbank gespeichert sind, können während des Abrufens Fehler auftreten. Dann wird eine Nachricht ähnlich der folgenden Nachricht im Ausgabeprotokoll des Servers aufgezeichnet:

`ORA-01652: unable to extend temp segment by 128 in tablespace TEMP`

Um dieses Verhalten zu umgehen, bearbeiten Sie die Datei `plugin.properties` für das Plug-in, um die Anzahl der Tage zu reduzieren, für die Daten abgerufen werden. Die Datei `plugin.properties` befindet sich im Verzeichnis `~/.ibm/cloud-sync/plugins/settings/reporting-ucd-plugin/` auf dem Computer, auf dem DevOps Connect installiert ist. Bearbeiten Sie die folgende Zeile, um das Nummernzeichen (#) zu entfernen und die Anzahl der Tage zu reduzieren:

`#numDaysToRetrieve=90`

Ändern Sie beispielsweise die Zeile in den folgenden Text, um nur Daten für die letzten 30 Tage abzurufen:

`numDaysToRetrieve=30`

Speichern Sie die Datei und führen Sie die Integration dann erneut aus. Überprüfen Sie die Serverprotokolle, um sicherzustellen, dass keine Fehler aufgetreten sind. 
