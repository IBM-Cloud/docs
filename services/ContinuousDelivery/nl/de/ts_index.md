---

copyright:
  years: 2015, 2017
lastupdated: "2017-2-9"

---
<!-- Common attributes used in the template are defined as follows: -->
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Fehlerbehebung für {{site.data.keyword.contdelivery_short}}
{: #ts_cd}

Hier erhalten Sie Antworten auf allgemeine Fragen zur Fehlerbehebung im Zusammenhang mit der Verwendung von {{site.data.keyword.contdelivery_full}}.
{:shortdesc}


## Autorisierung mit GitHub nicht möglich
{: #cannot_authorize_github}

Sie sind nicht mit GitHub autorisiert.
{:shortdesc}

Wenn Sie {{site.data.keyword.Bluemix_notm}} nicht für den Zugriff auf Ihr GitHub-Konto autorisiert haben, kann eines der folgenden Probleme auftrete:
{: tsSymptoms}

 * Bei dem Versuch, die GitHub-Toolintegration zu Ihrer Toolchain hinzuzufügen, wird die Toolintegration nicht hinzugefügt.
 * Die Pipeline wird nicht automatisch ausgeführt (ausgelöst), wenn Sie Änderungen per Push-Operation an Ihr GitHub- oder GitHub Enterprise-Repository übertragen.

{{site.data.keyword.Bluemix_notm}} ist nicht für den Zugriff auf GitHub autorisiert.  
{: tsCauses}
 
Wenn Sie die GitHub-Toolintegration konfigurieren, während Sie die Toolchain erstellen, gehen Sie dabei anhand der folgenden Schritte vor:
{: tsResolve}
 
  1. Klicken Sie im Abschnitt mit den konfigurierbaren Integrationen auf **GitHub**. 
  1. Wenn Sie die Toolchain unter {{site.data.keyword.Bluemix_notm}} Public erstellen und {{site.data.keyword.Bluemix_notm}} nicht für den Zugriff auf GitHub autorisiert haben, klicken Sie auf **Autorisieren**, um zur GitHub-Website zu wechseln. 
  1. Wenn keine aktive GitHub-Sitzung existiert, werden Sie aufgefordert, sich anzumelden. Klicken Sie auf **Anwendung autorisieren**, um {{site.data.keyword.Bluemix_notm}} den Zugriff auf Ihr GitHub-Konto zu erlauben. Falls eine aktive GitHub-Sitzung existiert, Sie Ihr Kennwort aber bereits vor einiger Zeit eingegeben haben, werden Sie möglicherweise aufgefordert, Ihr GitHub-Kennwort durch erneute Eingabe zu bestätigen.
  
Wenn Sie bereits über eine Toolchain verfügen, aktualisieren Sie die Konfiguration der GitHub-Toolintegration wie folgt:

 1. Klicken Sie im DevOps-Dashboard auf der Seite **Toolchains** auf die Toolchain, um die zugehörige Übersichtsseite zu öffnen. Alternativ können Sie auf der Übersichtsseite der App auf der Karte für Continuous Delivery auf **Toolchain anzeigen** und dann auf **Übersicht** klicken.
 1. Klicken Sie auf der Karte für GitHub auf das Menü und klicken Sie dann auf **Konfigurieren**.
 1. Aktualisieren Sie die Konfigurationseinstellungen so, dass {{site.data.keyword.Bluemix_notm}} die Autorisierung für den Zugriff auf GitHub erhält. Klicken Sie auf **Autorisieren**, um zur GitHub-Website zu wechseln. Wenn keine aktive GitHub-Sitzung existiert, werden Sie aufgefordert, sich anzumelden. Klicken Sie auf **Anwendung autorisieren**, um {{site.data.keyword.Bluemix_notm}} den Zugriff auf Ihr GitHub-Konto zu erlauben. Falls eine aktive GitHub-Sitzung existiert, Sie Ihr Kennwort aber bereits vor einiger Zeit eingegeben haben, werden Sie möglicherweise aufgefordert, Ihr GitHub-Kennwort durch erneute Eingabe zu bestätigen.
 1. Wenn Sie die Aktualisierung der Einstellungen abgeschlossen haben, klicken Sie auf **Integration speichern**.


## Toolintegration ist nicht konfiguriert
{: #tool_integration_error}

Nachdem Sie die Toolintegration für Ihre Toolchain konfiguriert haben, wird der Fehler `Einrichtung fehlgeschlagen` auf der Karte des Tools angezeigt.
{:shortdesc}

Nachdem Sie eine Toolintegration konfiguriert haben, zeigen Sie auf der Übersichtsseite der Toolchain die Karte für das Tool an und stellen fest, dass die Einrichtung fehlgeschlagen ist.
{: tsSymptoms}

 ![Fehler 'Einrichtung fehlgeschlagen'](images/tool_setup_failed.png)
 
Wenn Sie eine Toolintegration hinzufügen, kommuniziert die Toolchain mit dem Tool, das durch die Toolintegration dargestellt wird, um alle notwendigen Ressourcen bereitzustellen und diese der Toolchain zuzuordnen. Wenn während der Einrichtung ein Fehler auftritt oder die Kommunikation zwischen der Toolchain und dem Tool nicht ordnungsgemäß abgeschlossen wird, so wird die Toolintegration in einen Fehlerstatus versetzt.
{: tsCauses}

Konfigurieren Sie die Toolintegration erneut:
{: tsResolve}

1. Bewegen Sie auf der Karte des Tools den Mauszeiger über die Nachricht `Einrichtung fehlgeschlagen` und klicken Sie auf **Neu konfigurieren**.

 ![Schaltfläche 'Neu konfigurieren'](images/tool_reconfigure.png)
 
1. Stellen Sie sicher, dass Sie gültige Konfigurationsparameter verwenden. Wenn der Fehler durch eine ungültige Konfiguration verursacht wurde, wird eine Fehlermeldung angezeigt, wie zum Beispiel `Die Integration konnte nicht eingerichtet werden. Überprüfen Sie die Einstellungen und wiederholen Sie die Operation. Ursache: Ungültiger api_key:fakeKey`. Aktualisieren Sie die Einstellungen für die Toolintegration und klicken Sie auf **Integration speichern**.
1. Wenn der Fehler durch einen Kommunikationsfehler verursacht wurde, klicken Sie auf **Integration speichern**, um einen erneuten Versuch zu starten.
