---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-01"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}



<!-- {{site.data.keyword.iotinsurance_full}}  {{site.data.keyword.iotinsurance_short}}  -->

# Daten sichern
Sie können Ihre {{site.data.keyword.iotinsurance_full}}-Daten durch Replizieren der {{site.data.keyword.cloudantfull}}-Datenbank sichern.
{:shortdesc}

In der folgenden Tabelle sehen Sie die {{site.data.keyword.iotinsurance_short}}-Datenbanken, die in {{site.data.keyword.iotinsurance_full}} gespeichert werden.

*Tabelle 1: {{site.data.keyword.iotinsurance_short}}-Datenbanken*

Datenbanknamen| Häufigkeit der Änderung| Grund für Änderung | Sicherung erforderlich | Kommentare
------------- | -------------| -------------| -------------| -------------
favorites|Administration|Neue Administratoraktion|JA|-
Devices|Administration|Neue Geräte oder Benutzer hinzugefügt oder entfernt|JA| Der Transformator generiert im Hauptspeicher dynamisch eine Tabelle und füllt sie mit Daten aus dem Geräteprovider. Bei direkt verbundenen Gateways werden in dieser Tabelle die Geräte gespeichert.
hazardevents|Beliebig|Neues Shield-Ereignis festgestellt|JA|-
Jscode|Administration|Neuer JS-Code für Shields bereitgestellt|JA*| Der Administrator kann die Sicherung optional überspringen und eine neue Version des JS-Codes bereitstellen.
Promotions|Administration|Neue Hochstufung hinzugefügt|JA|-
shieldassociations|Administration|Neuer Benutzer oder neues Shield hinzugefügt|JA|-
Shields|Administration|Neues Shield hinzugefügt|JA|-
Users|Administration|Neuer Benutzer hinzugefügt|JA|-
aggregation|-|-|NEIN|Kann erneut erstellt werden.
aggregationschedule|-|-| NEIN|Kann erneut erstellt werden.

Führen Sie die folgenden Schritte aus, um die {{site.data.keyword.iotinsurance_short}}-Daten zu sichern:

## {{site.data.keyword.cloudant}}-Replikatinstanz erstellen
{: #createinstance}
Erstellen Sie unter Verwendung der [Anweisungen zur {{site.data.keyword.cloudant}}-Replikation ![Symbol für externen Link](../../icons/launch-glyph.svg)](https://docs.cloudant.com/replication.html) eine {{site.data.keyword.cloudant}}-Replikatsinstanz. Erstellen Sie zu Zwecken der Disaster-Recovery das Replikat an einer Position, die sich von der Position des ursprünglichen {{site.data.keyword.iotinsurance_short}}-Service unterscheidet. Wenn Ihre ursprüngliche Instanz in Dallas ansässig ist, kann sich das Replikat in London befinden.

## Berechtigungsnachweise und URLs suchen
{: #locate_credentials}
Suchen Sie die Berechtigungsnachweise und die URLs für Ihre ursprüngliche {{site.data.keyword.cloudant}}-Instanz und Ihre replizierte Instanz.
1. Öffnen Sie den Service '{{site.data.keyword.cloudant}}'.
2. Klicken Sie auf die Registerkarte **Serviceberechtigungsnachweise**, die sich unter dem Namen des Service befindet.
3. Klicken Sie auf **Berechtigungsnachweise anzeigen**.
4. Notieren Sie sich den Benutzernamen, das Kennwort und die URL.

## Neue Replikationstasks erstellen
{: #create_replication}
Erstellen Sie für jede Datenbank, die gesichert werden muss, eine Replikationstask. Die Datenbanken, für die eine Sicherung erforderlich ist, sind in Tabelle 1 des vorherigen Abschnitts aufgeführt.

1. Öffnen Sie Ihre {{site.data.keyword.Bluemix_notm}}-Konsole.

2. Öffnen Sie den ursprünglichen {{site.data.keyword.cloudant}}-Service.

3. Klicken Sie auf **Starten**, um das {{site.data.keyword.cloudant}}-Dashboard zu öffnen.

4. Wählen Sie im Menü **Replikation** aus.

5. Geben Sie im Abschnitt 'Quellendatenbank' die URL der ursprünglichen Datenbank ein. Jede Datenbank-URL hat das Format https://<CloudantbaseURL>/<Datenbankname>.  So lautet die URL der Datenbank 'hazardevents' beispielsweise https://<CloudantbaseURL>/hazardevents.

6. Geben Sie im Abschnitt 'Zieldatenbank' die URL der neuen Datenbank ein.

7. **Wichtig:** Wählen Sie nicht die Option aus, mit der diese Replikation fortlaufend durchgeführt wird.  Eine fortlaufende Replikation wirkt sich deutlich auf die Leistung aus.

8. Klicken Sie auf die Option zum Replizieren der Daten.  

9. (Optional) Da die vorherigen Daten durch nachfolgende Replikationstasks überschrieben werden, sollten Sie die Daten in eine CSV-Datei exportieren.  Anweisungen finden Sie unter [Export Cloudant JSON as CSV, RSS, or iCal ![Symbol für externen Link](../../icons/launch-glyph.svg)](https://developer.ibm.com/clouddataservices/2015/09/22/export-cloudant-json-as-csv-rss-or-ical/){: new_window}.

10. Wiederholen Sie diese Schritte für jede Datenbank.

## Sicherung ausführen
{: #run_backup}
Nach der Erstellung der Replikationstasks können Sie Sicherungen jederzeit wiederholen.
1. Öffnen Sie Ihre {{site.data.keyword.Bluemix_notm}}-Konsole.
2. Öffnen Sie Ihren ursprünglichen {{site.data.keyword.cloudant}}-Service.
3. Klicken Sie auf **Starten**, um das {{site.data.keyword.cloudant}}-Dashboard zu öffnen.
4. Klicken Sie im Menü auf **Replikation** und wählen Sie anschließend **Alle Replikationen** aus.
5. Wählen Sie alle Datenbanken aus und führen Sie die einzelnen Replikationen erneut aus. Sie können den Status der Jobs, die in Bearbeitung sind, überprüfen, indem Sie auf **Aktive Replikationen** klicken.
6. Wenn alle Replikationen ausgeführt sind, können Sie die Daten in eine CSV-Flatfile exportieren.

## Daten wiederherstellen
{: #restore_data}
Sie können die Daten aus einer replizierten Datenbank oder durch Laden einer gespeicherten CSV-Datei wiederherstellen.
1. Öffnen Sie Ihre {{site.data.keyword.Bluemix_notm}}-Konsole.
2. Stoppen Sie den Service '{{site.data.keyword.iotinsurance_short}}'.
3. Stellen Sie die Daten auf eine der folgenden Weisen wieder her:
  - Laden Sie die Daten aus einer CSV-Sicherungsdatei direkt in die primäre Cloudant-Instanz.
  - Erstellen Sie eine Replikationstask, die die replizierte Datenbank als Quelle und die ursprüngliche Datenbank als Ziel hat. Durch diese Task werden die replizierten Daten in die ursprüngliche Datenbank verschoben.
4. Führen Sie die folgenden Scripts aus, um Entwurfsdokumente erneut zu erstellen und referenzielle Integrität wiederherzustellen.  Die Scripts befinden sich auf der [GitHub-Site mit den {{site.data.keyword.iotinsurance_short}}-API-Beispielen ![Symbol für externen Link](../../icons/launch-glyph.svg)](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/){: new_window}.
  - iot4i-api/wearable-framework/auto-create/create.sh - Durch dieses Script werden die Entwurfsdokumente in {{site.data.keyword.cloudant}} neu erstellt.
  - iot4i-api/wearable-framework/health/check-relations - Durch dieses Script wird die referenzielle Integrität neu erstellt. So korrigiert das Script beispielsweise einen Fall, in dem ein Shield zwar gelöscht, die Zuordnung zu einem Benutzer aber noch vorhanden ist.
