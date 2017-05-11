---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-11"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# App-Details
{: #manageapps}

Das Dashboard 'Apps' in der {{site.data.keyword.Bluemix}}-Konsole stellt Übersichtsinformationen zu den von Ihnen erstellten Anwendungen bereit. Diese Übersichtsinformationen umfassen den Namen, das Symbol, die URL, die Laufzeit und den Ausführungsstatus sowie die Serviceinstanzen, die an die App gebunden sind.
{:shortdesc}

Im Dashboard 'Apps' können Sie den Status jeder Anwendung anzeigen. 

**Gestoppt oder Unbekannt (grau)**

  Ihre App wurde gestoppt oder der Status ist unbekannt. Das graue Symbol gibt an, dass die App gestoppt wurde oder dass der Status unbekannt ist. 

**Aktiv (grün)**

  Ihre App ist aktiv. Das grüne Symbol gibt an, dass die App gestartet wurde und alle Instanzen aktiv sind. 

*Anzahl* **aktiv (gelb)**

  Die App ist zwar gestartet, doch es sind nicht alle Instanzen aktiv. Das gelbe Symbol gibt an, dass weniger als 100 % der Instanzen aktiv sind. Die Anzahl der aktiven Instanzen und die Anzahl der fehlgeschlagenen Instanzen wird angezeigt. 

**Nicht aktiv (rot)**

  Ihre App ist nicht aktiv. Das rote Symbol gibt an, dass die App zwar gestartet wurde, aber keine Instanz aktiv ist. 

Zum Anzeigen weiterer Informationen zu einer App klicken Sie auf den Namen, um die Seite 'Übersicht' der App zu öffnen. 

Nachdem eine App bereitgestellt wurde, können Sie sie starten, stoppen oder erneut starten oder (im Falle von Webanwendungen) die Anzahl der Instanzen sowie die von der App verwendete Speichermenge ändern. Gegenwärtig führt {{site.data.keyword.Bluemix_notm}} für Webanwendungen keine automatische Skalierung der Apps auf Basis der jeweiligen Auslastung durch, weshalb Sie sich um diesen Aspekt selbst kümmern müssen. 

Nach einer Aktualisierung können Apps erneut bereitgestellt werden. Der Mechanismus zum Aktualisieren der App ist mit dem identisch, der für die ursprüngliche Bereitstellung verwendet wurde. {{site.data.keyword.Bluemix_notm}} stoppt alle aktiven Instanzen und ersetzt sie automatisch durch neue Instanzen.
