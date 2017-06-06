---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-20"

---

{:new_wind{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:tip: .tip}

# Klassifikationsmerkmale mithilfe des Toolkits verwalten
{: #managing-toolkit}

Sie können Ihre Trainingsdaten und Klassifikationsmerkmale mithilfe der Webanwendung {{site.data.keyword.nlclassifierfull}} Toolkit verwalten. Das Toolkit bietet Ihnen eine einheitliche Sicht aller Klassifikationsmerkmale, die in derselben {{site.data.keyword.Bluemix_notm}}-Serviceinstanz ausgeführt werden.
{: shortdesc}

Dies ist eine Betaversion des Toolkits. Nach einem neuen Release oder nachdem das Toolkit den Betastatus verlassen hat, wird die Betaversion dieses Toolkits möglicherweise nicht mehr unterstützt. Verwenden Sie das Toolkit nicht für einen Einsatz in der Produktion. 

Die Webschnittstelle des Toolkits vereinfacht den Ablauf für das Trainieren und Testen eines Klassifikationsmerkmals. Ihre Fachleute können sich mithilfe des Toolkits auf die Qualität Ihrer Trainingsdaten konzentrieren. 

## Zugriff erhalten 
{: #getting-access}

Auf der Seite des {{site.data.keyword.Bluemix_notm}}-Service-Dashboards für Ihre Instanz von {{site.data.keyword.nlclassifiershort}} finden Sie einen Link zum Toolkit. 

### Toolkitzugriff für Sie selbst

Damit Sie zu dem Link zum Toolkit gelangen, führen Sie folgende Schritte aus, mit denen Sie Ihr {{site.data.keyword.Bluemix_notm}}-Dashboard **Service** aufrufen: 

1. Öffnen Sie die Kachel des Service '{{site.data.keyword.nlclassifiershort}}', indem Sie sich bei Ihrem [{{site.data.keyword.Bluemix_notm}}-Dashboard ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](https://console.{DomainName}/dashboard/services){: new_window} anmelden. 

	-  Klicken Sie im Bereich **Services** auf die Kachel des Service '{{site.data.keyword.nlclassifiershort}}', um das Dashboard der Instanz zu öffnen. (Wenn Sie keine Kachel für den Service haben, [erstellen Sie eine Instanz ![Symbol 'Externer Link'](../../icons/launch-glyph.svg)](https://console.{DomainName}/catalog/services/natural-language-classifier/){: new_window} des Service '{{site.data.keyword.nlclassifiershort}}'.) 
1. Klicken Sie im Dashboard des Service auf **Auf Beta-Toolkit zugreifen**. 

	Setzen Sie ein Lesezeichen für die URL, um später ohne großen Aufwand auf das Toolkit zugreifen zu können.
	{: tip}

### Toolkitzugriff für Andere

Sie können Anderen die Verwendung des Toolkits ermöglichen, indem Sie sie in {{site.data.keyword.Bluemix_notm}} hinzufügen. 

1.  Klicken Sie in {{site.data.keyword.Bluemix_notm}} auf **Konto > Teammitglieder einladen**. 
1.  Wählen Sie die Organisation aus, die Ihren Klassifikationsservice enthält, und klicken Sie auf **Weiter**. 
1.  Wählen Sie den Bereich aus, der Ihren Klassifikationsservice enthält. 
1.  Wählen Sie die Bereichsrolle **Entwickler** aus. Details zu Rollen finden Sie in [Teammitglieder und Rollen verwalten](/docs/admin/users_roles.html). 
1.  Geben Sie die E-Mail-Adresse des Benutzers ein und klicken Sie auf **Senden**. 
1.  Senden Sie in einer separaten E-Mail die URL Ihres Toolkits (für die Sie zuvor ein Lesezeichen gesetzt haben) an die Benutzer. 

## Beispiele für die Verwendung
{: #example-uses}

In diesen Beispielen führen Sie Folgendes aus: Sie erstellen und ändern Trainingsdaten, Sie testen ein Klassifikationsmerkmal interaktiv oder ausgehend von einer Gruppe von Testdaten, und Sie aktualisieren Trainingsdaten auf der Basis der Ergebnisse. 

### Trainingsdaten im Toolkit erstellen

Erlernen Sie den Umgang mit dem {{site.data.keyword.nlclassifiershort}}-Toolkit, indem Sie eine kleine Gruppe von Trainingsdaten mithilfe des Toolkits erstellen. 

Vor dem Erstellen eines Klassifikationsmerkmals müssen Sie Trainingsdaten bereitstellen. Sie können die Daten erstellen, indem Sie Text und Klassen eingeben oder Sie können Ihre Trainingsdaten aus einer CSV-Datei hochladen, die dem [Dateiformat](/docs/services/natural-language-classifier/using-your-data.html) entspricht. 
1. Fügen Sie auf der Seite **Trainingsdaten** des Toolkits einen Text hinzu. Wenn Ihnen kein Text einfällt, fügen Sie 'Where is the nearest ATM?' (Wo ist der nächste Geldautomat?) hinzu. . 
1. Weisen Sie dem Text eine Klasse zu, indem Sie sie eingeben. Für das Beispiel mit dem Geldautomaten geben Sie 'location' ein. 
1. Fahren Sie fort, zu Ihren Trainingsdaten Texte und Klassen hinzuzufügen. Sie haben folgende Möglichkeiten, um den Texten Klassen zuzuweisen: 
	-   Wählen Sie eine Klasse durch Anklicken aus; klicken Sie anschließend auf **Text hinzufügen**. Oder wählen Sie einen Text aus und klicken Sie anschließend auf **Klassen zuweisen**. 
	-   Wählen Sie eine Klasse aus und ziehen Sie dann einen Text zu dieser Klasse. Oder wählen Sie einen Text aus und ziehen Sie dann eine Klasse zum Text. 

	Sie können gleichzeitig mehrere Klassen oder Texte bearbeiten, indem Sie die Steuerungstaste gedrückt halten und auf den Text oder die Klasse klicken (drücken Sie auf einem MAC-Computer auf die Befehlstaste). Machen Sie einige Versuche.
1. Nachdem Sie eine Weile mit Ihren Trainingsdaten gearbeitet haben, klicken Sie auf **Trainingsdaten herunterladen**, um die Daten als Sicherung zu speichern. 

	Sie können diese Datei auch in das Toolkit hochladen, um mit den Trainingsdaten später erneut zu arbeiten.
	{: tip}
1. Wenn Sie mindestens fünf Texten Klassen zugewiesen haben, können Sie anhand dieser Trainingsdaten ein Klassifikationsmerkmal erstellen. Klicken Sie auf **Klassifikationsmerkmal erstellen**. {{site.data.keyword.watson}} beginnt mit dem Training des Klassifikationsmerkmals. 

### Klassifikationsmerkmal testen und Trainingsdaten aktualisieren

Nachdem ein Klassifikationsmerkmal trainiert wurde und zur Verfügung steht, können Sie überprüfen, wie gut es Text klassifiziert, den es zuvor nicht gesehen hat. Sie können eine Reihe von Texten testen und die Trainingsdaten verbessern, indem Sie die falschen Antworten oder die Antworten mit einer niedrigen Konfidenz hinzufügen. 

1.  Klicken Sie auf der Seite **Klassifikationsmerkmale** auf **Testen und Leistung verbessern** für das Klassifikationsmerkmal, das Sie testen möchten. 
1.  Geben Sie auf der Seite **Leistung verbessern** einen Text ein, der in den Trainingsdaten nicht vorhanden ist, und klicken Sie auf **Klassifizieren**. {{site.data.keyword.watson}} gibt relevante Klassen und die zugehörigen Konfidenzstufen zurück. 
1.  Fügen Sie weitere Texte hinzu, um die Leistung zu testen. 
1.  Überprüfen Sie die Antworten. Markieren oder genehmigen Sie die Ergebnisse, die Sie Ihren Trainingsdaten hinzufügen möchten: 
	- Wenn die Klassifizierung falsch ist, markieren Sie das Ergebnis. 
	- Wenn die Antwort richtig ist, aber die Konfidenz niedrig ist, fügen Sie sie durch Klicken auf **Genehmigen** zu Ihren Trainingsdaten hinzu. 
1.  Klicken Sie auf **Zu Trainingsdaten hinzufügen**, um die genehmigten und markierten Antworten Ihren Trainingsdaten hinzuzufügen. 
1.  Überprüfen Sie auf der Seite **Trainingsdaten** die Klassen, die den von Ihnen markierten Texten zugewiesen sind, und aktualisieren Sie sie. 
1.  Erstellen Sie ein weiteres Klassifikationsmerkmal, um Ihr Klassifikationsmerkmal mit diesen neuen Trainingsdaten zu aktualisieren. Klicken Sie auf **Klassifikationsmerkmal erstellen**. Nachdem das Klassifikationsmerkmal trainiert wurde, testen Sie es, um die Art der Verbesserung zu ermitteln. 

### Daten zum Testen des Klassifikationsmerkmals hochladen 

Für Schnelltests ist es effektiv, Texte nacheinander einzugeben. Wenn Sie jedoch eine *Testgruppe* haben, können Sie die Gruppe in das Toolkit hochladen, um mehrere Klassifizierungen gleichzeitig durchzuführen. Eine Testgruppe ist eine Gruppe von Beispieltexten, die sich nicht in Ihren Trainingsdaten befinden. Sie verwenden die Gruppe, um die Leistung des Klassifikationsmerkmals zu überprüfen. 

1.  Erstellen Sie eine Datei für die Testgruppe: 
	- Die Datei kann dasselbe Format wie die Trainingsdaten aufweisen (d. h., sie kann die richtigen Klassen enthalten) oder sie kann nur Texte enthalten, und zwar pro Zeile einen Text. Stellen Sie sicher, dass die Texte (und Klassen) die Voraussetzungen an das [Dateiformat](/docs/services/natural-language-classifier/using-your-data.html) erfüllen. 
    -   Speichern Sie die Datei mit der Erweiterung `.csv`. 
1.  Klicken Sie auf der Seite **Klassifikationsmerkmale** auf **Testen und Leistung verbessern** für das Klassifikationsmerkmal, das Sie testen möchten. 
1.  Klicken Sie auf der Seite **Leistung verbessern** auf **Testdaten verwenden**. {{site.data.keyword.watson}} lädt die Daten hoch, klassifiziert die einzelnen Texte und gibt eine Antwort zurück. 
1.  Vergleichen Sie die Antworten mit der richtigen Klassifikation und achten Sie auch auf niedrige Konfidenz. 
1.  Verbessern Sie die Trainingsdaten, indem Sie weitere Beispiele hinzufügen. Fügen Sie keine Beispiele hinzu, die in Ihrer Testgruppe vorhanden sind, wenn Sie die Testgruppe weiterhin zum Bewerten der Leistung des Klassifikationsmerkmals verwenden wollen. 
