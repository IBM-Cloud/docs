---

copyright:
  years: 2015, 2016

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

#Anwendungen verwalten
{: #manageapps}

*Letzte Aktualisierung: 17. März 2015*

Mithilfe des Dashboards in der {{site.data.keyword.Bluemix}}-Benutzerschnittstelle können Sie Ihre Anwendungen und Services anzeigen und verwalten sowie die Ressourcennutzung anhand der Messanzeigen für Kontingente überwachen.
{:shortdesc}

Der Anwendungsabschnitt im Dashboard enthält Übersichtsinformationen zu den von Ihnen erstellten Anwendungen. Diese
Übersichtsinformationen umfassen den Namen, das Symbol, die URL, die Laufzeit und den Ausführungsstatus der entsprechenden Anwendung sowie die an sie gebundenen
Serviceinstanzen. Der Ausführungsstatus der einzelnen Anwendungen wird durch unterschiedliche Farben angezeigt.

**Gestoppt oder Unbekannt (grau)**

  Ihre App wurde gestoppt oder der Status ist unbekannt. Das graue Symbol gibt an, dass die Anwendung gestoppt wurde oder
dass der Status unbekannt ist.

**Aktiv (grün)**

  Ihre App ist aktiv. Das grüne Symbol gibt an, dass die Anwendung gestartet wurde und alle Instanzen aktiv sind.

*Anzahl* **aktiv (gelb)**

  Die App ist zwar gestartet, doch es sind nicht alle Instanzen aktiv. Das gelbe Symbol gibt an, dass weniger als 100 % der Instanzen
aktiv sind. Die Anzahl der aktiven Instanzen und die Anzahl der fehlgeschlagenen Instanzen
wird angezeigt.

**Nicht aktiv (rot)**

  Ihre App ist nicht aktiv. Das rote Symbol gibt an, dass die Anwendung zwar gestartet wurde, aber keine Instanz aktiv ist.

Im {{site.data.keyword.Bluemix_notm}}-Katalog
können Sie die verfügbaren Services und Starter anzeigen. Sie können einen Starter auswählen, um eine Anwendung zu erstellen, einen Service zu binden und die Anwendung zu verwalten. Nachdem ein
Service an eine Anwendung gebunden wurde, können Sie die vorhandenen Serviceinstanzen verwalten, die an die aktuelle Anwendung gebunden sind, und Serviceinstanzen
für die Anwendung erstellen. Sie können auch die Bindung einer Serviceinstanz an eine Anwendung aufheben bzw. eine Serviceinstanz aus einer Anwendung löschen oder einen anderen Serviceplan auswählen.

Um weitere
Informationen zu einer Anwendung anzuzeigen, klicken Sie auf die entsprechende Kachel, um die Übersichtsseite der App zu öffnen.

**Hinweis:** Es können jeweils immer nur die Ressourcen einer einzelnen Organisation angezeigt
werden. Wenn Sie Mitglied mehrerer Organisationen sind, können Sie zwischen Organisationen umschalten,
indem Sie in der Kopfzeile des Dashboards neben der angezeigten Organisation auf
das Symbol **Organisation ändern** klicken.

Nachdem eine Anwendung bereitgestellt wurde, können Sie die Anwendung starten, stoppen oder erneut starten oder (im Falle von Webanwendungen) die Anzahl der Instanzen sowie die von der Anwendung verwendete Speichermenge ändern. Gegenwärtig führt {{site.data.keyword.Bluemix_notm}} für Webanwendungen keine automatische Skalierung der Anwendungen auf Basis der jeweiligen Auslastung durch, weshalb Sie sich um diesen Aspekt selbst kümmern müssen.

Nach einer Aktualisierung können Anwendungen
erneut bereitgestellt werden. Der Mechanismus zum Aktualisieren der Anwendung ist mit dem identisch, der für die ursprüngliche Bereitstellung verwendet wurde. {{site.data.keyword.Bluemix_notm}} stoppt alle aktiven Instanzen und ersetzt sie automatisch durch neue Instanzen.
