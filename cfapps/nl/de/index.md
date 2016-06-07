---

 

copyright:

  years: 2015，20166

 

---

{:shortdesc: .shortdesc} 
{:new_window: target="_blank"}

# Cloud Foundry-Apps erstellen
*Letzte Aktualisierung: 18. April 2016*

In {{site.data.keyword.Bluemix}} können Sie Ihre Anwendung in der
{{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle erstellen. Nachdem die Anwendung erstellt wurde, können Sie wählen, ob Sie weiterhin die Benutzerschnittstelle, die Befehlszeilenschnittstelle 'cf' oder {{site.data.keyword.jazzhub_title}} verwenden möchten, um Ihre Anwendung zu entwickeln, zu verfolgen, zu planen und bereitzustellen.
{:shortdesc}

Wenn Sie eine Anwendung in {{site.data.keyword.Bluemix_notm}} erstellen, beginnen Sie mit einem
Starter. Bei einem *Starter* handelt es sich um eine Vorlage, die vordefinierte Services sowie Anwendungscode enthält, der mit einem bestimmten Buildpack konfiguriert ist. Es gibt zwei Arten von Startern: Boilerplates und Laufzeiten. 

Eine *Boilerplate* ist ein Container für eine Anwendung und die zugehörige Laufzeitumgebung sowie vordefinierte Services für eine bestimmte Domäne. Beispiel: Die Boilerplate 'Mobile Cloud'
enthält eine Node.js-Laufzeit sowie die Services 'Mobile Data', 'Mobile Application Security' und 'Push'. Darüber hinaus sind auch ein SDK und Beispielanwendungen enthalten, um in die Entwicklung von mobilen Anwendungen, die auf diese Services zugreifen, einsteigen
zu können.

Mit *Laufzeit* wird die Ressourcengruppe bezeichnet, die für die Ausführung einer Anwendung verwendet
wird. {{site.data.keyword.Bluemix_notm}} stellt Laufzeitumgebungen als Container für verschiedene Anwendungstypen bereit. Die
Laufzeitumgebungen werden als Buildpacks in {{site.data.keyword.Bluemix_notm}} integriert,
automatisch für die Verwendung konfiguriert und müssen nur sehr wenig oder auch gar nicht gewartet werden.

Gehen Sie wie folgt vor, um mit der Erstellung Ihrer Anwendung zu beginnen:
  1. Wechseln Sie zum Dashboard in der {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle.
  2. Klicken Sie auf **Anwendung erstellen**.
  3. Klicken Sie auf **Web** und befolgen Sie die Anweisungen, um einen Starter auszuwählen, einen Namen anzugeben und zu entscheiden, welchen Code Sie verwenden möchten.
  4. Nachdem Sie die Anweisungen abgeschlossen haben, klicken Sie auf **App-Übersicht anzeigen**. Die Übersichtsseite der App wird im Dashboard angezeigt.
  5. Sie können Ihrer App einen Service hinzufügen, indem Sie in der Anwendungsübersicht in der Bluemix-Benutzerschnittstelle auf **Service oder API hinzufügen** klicken. Durchsuchen Sie den Katalog und wählen Sie Services aus oder blättern Sie zum Ende des Katalogs und klicken Sie auf **{{site.data.keyword.Bluemix_notm}} Experimental Services**, um die experimentellen Services zu durchsuchen. Sie haben auch die Möglichkeit, die Befehlszeilenschnittstelle 'cf' zu verwenden. Weitere Informationen finden Sie unter 'Optionen für das Arbeiten mit Anwendungen'.
  6. Klicken Sie in der Anwendungsübersicht auf 'Git hinzufügen', um Ihre Anwendungsquelle in einem Git-Repository zu speichern und ein von Git gehostetes Projekt zu erstellen. Sie können die Anwendung auch über
{{site.data.keyword.jazzhub_title}}
bereitstellen.

**Hinweis:** Wenn ein an eine App gebundener Service abstürzt, wird die App
möglicherweise gestoppt oder weist Fehler auf. {{site.data.keyword.Bluemix_notm}} startet die App nicht automatisch erneut, um eine Recovery für diese Probleme durchzuführen. Ziehen Sie in Betracht, die App so zu codieren, dass sie eine Recovery für Ausfallzeiten, Ausnahmen und Verbindungsfehler durchführt. Weitere Informationen finden Sie im Abschnitt, in dem beschrieben wird, dass Apps nicht automatisch neu gestartet werden.

## Optionen für das Arbeiten mit Anwendungen

Nach dem Erstellen Ihrer Anwendung steht Ihnen eine Reihe von Optionen zur Verfügung, um Ihrer Anwendung weitere Services hinzuzufügen und um Ihre Anwendung
zu erstellen und bereitzustellen:

<dl><dt>Befehlszeilenschnittstelle 'cf'</dt>
<dd>Über die Befehlszeilenschnittstelle 'cf' können Sie Ihre Anwendung aktualisieren, eine Serviceinstanz erstellen oder den Service an
Ihre Anwendung binden. Sie können auch die Befehlszeilenschnittstelle 'cloud-cli' verwenden, um Serviceangebote zu
erstellen, zu aktualisieren und zu löschen.</dd>
<dt>{{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle</dt>
<dd>Mit der {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle können Sie Ihre Anwendung erstellen und dabei
auswählen, welche Services und Laufzeiten kombiniert werden sollen, um Ihre geschäftsbezogenen Probleme zu lösen.</dd>
<dt>{{site.data.keyword.jazzhub_title}}</dt>
<dd>Verwenden Sie {{site.data.keyword.jazzhub_title}}, um eine Anwendung in der Cloud zu erstellen und in {{site.data.keyword.Bluemix_notm}} bereitzustellen. Die von {{site.data.keyword.jazzhub_title}} zur Verfügung gestellten Services umfassen 'Track & Plan' und 'Delivery Pipeline', die im {{site.data.keyword.Bluemix_notm}}-Katalog unter 'DevOps' aufgeführt sind, sowie 'Web-IDE' und 'Git Hosting'.</dd>
</dl>

## Tipps

Nutzen Sie bei der Entwicklung Ihrer Webanwendungen die folgenden Tipps:

<dl><dt>Persistenz</dt>
<dd>Geben Sie für Ihre Anwendungen keinen lokalen Speicher an. Jede Instanz Ihrer Anwendung kann jederzeit
erneut gestartet oder auf eine andere virtuelle Maschine verschoben werden. Dies gilt auch dann, wenn nur eine einzige Instanz aktiv ist. Dies geschieht
üblicherweise, um einen Lastausgleich zu erreichen. Wenn die Anwendung verschoben oder gelöscht wird, gehen sämtliche Daten im
lokalen Speicher verloren. Verwenden Sie zwecks Persistenz einen der Datenspeicherservices von Bluemix.</dd>
<dt>Ressourcengrenzen</dt>
<dd>Berücksichtigen Sie die Grenzwerte im Hinblick auf die Ressourcenmengen, die bei einem Testkonto verwendet
werden können. Es gelten folgende Grenzwerte:
<table style="width:100%">
  <th>Ressourcentyp</th>	<th>Mengenbegrenzung</th>
<tr><td>Anzahl der in allen Anwendungen verwendeten Services</td> <td>10</td>
<tr><td>Menge des in allen Anwendungen belegten Hauptspeichers</td> <td>	2 GB</td>
<tr><td>Anzahl der Routen</td> <td>500</td>
</table>
</dd></dl>

*Tabelle 1. {{site.data.keyword.Bluemix_notm}}-Ressourcengrenzwerte für ein Testkonto*
