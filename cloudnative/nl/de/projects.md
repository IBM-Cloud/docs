---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Projekte
{: #projects}

Die {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}} kombiniert die App-Benutzerschnittstelle, die Daten und Services zu einem vollständigen Projekt (*project*). Indem Sie ein Projekt erstellen, werden alle erforderlichen Teile Ihrer App und die hinzugefügten Funktionen auf dem {{site.data.keyword.Bluemix_notm}}-Server beibehalten. Sie können den App-Code und die erforderlichen Berechtigungsnachweise und Initialisierungsoperatoren herunterladen, wenn die Services im Projekt konfiguriert sind. Durch Auswahl von **Projekte** können Sie alle Projekte anzeigen.   

Sie können zusätzliche Informationen zu einem einzelnen Projekt anzeigen; hierfür müssen Sie es auf der Seite **Projekte** auswählen. Dadurch wird die Seite **Projektübersicht** angezeigt; dort sind die Services aufgeführt, die konfiguriert und für das Projekt verfügbar sind. Services sind separate Funktionen, die Ihre App durch Hinzufügen einer Funktion erweitern. Da sie einzeln hinzugefügt werden, können Sie sich auf die Services beschränken, die Sie benötigen, wie zum Beispiel Push-, Authentication-, Data- und Storage-Services oder andere Services. Wenn Sie auf der Seite **Projektübersicht** einen Service zu Ihrem Projekt hinzufügen und die Anweisungen zum Konfigurieren des Service befolgen, wird der Service automatisch Ihrer App zugeordnet. Weitere Informationen zur Seite 'Projektübersicht' finden Sie im Abschnitt [Seite 'Projektübersicht'](project_overview_page.html).

Zum Erstellen eines Projekts müssen Sie ein [Muster](patterns.html) und danach einen [Starter](starters.html) auswählen. 


## Seite 'Projektübersicht'
{: #project_overview}

Sie können ein einzelnes Projekt in der {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}} anzeigen und verwenden, indem Sie das Projekt auf der Seite **Projekte** auswählen. Durch diese Aktion wird die Seite 'Projektübersicht' geöffnet.
{: shortdesc}

Auf der Seite **Projektübersicht** wird eine Kachel für jede Funktion angezeigt, die für das ausgewählte Projekt konfiguriert oder zum Konfigurieren verfügbar ist. In der Kachel werden der Funktionstyp und die Schaltfläche *Aktionen* mit drei vertikal ausgerichteten Punkten angezeigt. Zu den verfügbaren bzw. konfigurierten Funktionen können beispielsweise {{site.data.keyword.mobilepushshort}}, Analytics oder Data und Storage gehören. Welche Funktionen kompatibel sind, hängt vom Typ des Projekts und von den Funktionen ab, die in der jeweiligen Region verfügbar sind (d. h. nicht alle Funktionen können allen Projekten zugeordnet werden). 

Wenn ein Funktionstyp noch nicht dem Projekt zugeordnet ist, wird auf der Kachel die Schaltfläche **Erstellen** angezeigt. Die verfügbaren Optionen der Schaltfläche für Aktionen ermöglichen das Erstellen einer Serviceinstanz oder das Hinzufügen einer vorhandenen Serviceinstanz, falls die betreffende Funktion noch nicht zugeordnet ist. Nach dem Auswählen der Option **Vorhandene hinzufügen** wird eine Liste der Serviceinstanzen des betreffenden Typs im Bereich angezeigt. 

Wenn die Funktion bereits diesem Projekt zugeordnet ist, wird der Name der zugehörigen Serviceinstanz auf der Kachel nach dem Funktionstyp angezeigt. Dies vereinfacht das Auffinden der zugehörigen Serviceinstanz für dieses Projekt in der {{site.data.keyword.dev_console}}. Über die Aktionsschaltfläche stehen die Aktionen **Anzeigen** und **Entfernen** zur Verfügung, wenn die Funktion bereits dem Projekt zugeordnet ist. Beim Entfernen einer Serviceinstanz wird lediglich die Zuordnung zu diesem Projekt aufgehoben. Die Serviceinstanz in der {{site.data.keyword.dev_console}} wird nicht gelöscht. Klicken Sie zum Löschen einer Serviceinstanz auf die Seite **Web and Mobile > Services**, um die Serviceinstanzen anzuzeigen und zu löschen. 

Wählen Sie **Code abrufen** in der Kachel **Code** aus, um den Code für Ihr Projekt herunterzuladen. Weitere Informationen zum Herunterladen von Code finden Sie unter [Code abrufen](get_code.html).


## Projekt zur Verwendung eines neuen Starters aktualisieren
{: #update-starter}

1. Klicken Sie auf der Seite **Projekte** oder **Projektübersicht** auf das Symbol **Überlaufmenü** und wählen Sie **Starter aktualisieren** aus. 

2. Wählen Sie einen neuen Starter aus und klicken Sie auf **Aktualisieren**. 

3. Klicken Sie auf der Seite **Projektübersicht** auf **Code abrufen**, um Ihre Sprache auszuwählen. 

   Alternativ können Sie auf die Seite **Code** klicken.


## Projekt zum Generieren einer neuen Sprache aktualisieren
{: #update-language}

1. Klicken Sie auf der Seite **Projekte** oder **Projektübersicht** auf das Symbol **Überlaufmenü** und wählen Sie **Starter aktualisieren** aus. 

2. Wählen Sie eine neue Sprache aus und klicken Sie auf **Aktualisieren**. 

3. Klicken Sie auf der Seite **Projektübersicht** auf **Code abrufen**, um Ihre Sprache auszuwählen. 
