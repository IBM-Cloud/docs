---



copyright:

  years: 2015, 2017
lastupdated: "2017-04-12"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Eigene Kosten schätzen
{: #cost}

Es gibt unterschiedliche Methoden zur Ermittlung der Kosten für die Nutzung von {{site.data.keyword.Bluemix_notm}}, um Ihre App zu erstellen und zu hosten.

* Von den Kostenschätzern auf der {{site.data.keyword.pricing_sheet}} von {{site.data.keyword.Bluemix_notm}} wird eine grobe Einschätzung der Kosten auf Grundlage der Größe Ihrer App bereitgestellt.
* Mit dem Kostenrechner auf der Seite für die Preisstruktur von {{site.data.keyword.Bluemix_notm}} werden auf der Grundlage Ihrer Eingabe zu Laufzeit und Servicenutzung genaue App-Preise ermittelt.
* Sie können Ihre Kosten auch manuell berechnen.

## Kostenrechner verwenden
{: #calculator}

Sie können den Preis für Ihre App mithilfe der von {{site.data.keyword.Bluemix_notm}} bereitgestellten Kostenrechner rasch ermitteln.

1. Wechseln Sie zur {{site.data.keyword.pricing_sheet}} von {{site.data.keyword.Bluemix_notm}}.
2. Verwenden Sie eines der Infrastrukturwidgets oder klicken Sie auf **Preisrechner**.

Zur Verwendung der Berechnungsfunktion geben Sie Ihre projizierte monatliche Nutzung der aufgelisteten Ressourcen ein, z. B. die Anzahl der Instanzen oder Push-Benachrichtigungen. Klicken Sie in das Feld **Monatliche Nutzung**, um Hinweise zu den Einheiten zu erhalten, die in dem Feld erwartet werden. Die Berechnungsfunktion zeigt die Kosten für Ihre Eingabe sofort an. Sie können die Berechnungsfunktion auch anpassen, um jährliche Kosten anstelle von monatlichen Kosten anzuzeigen.

## Kosten manuell schätzen
{: #manual}

Sie können zum Beispiel Ihre {{site.data.keyword.Bluemix_notm}}-Kosten selbst schätzen, um besser zu verstehen, wie sich {{site.data.keyword.Bluemix_notm}}-Kosten errechnen. Sie können den Gesamtpreis für die Nutzung von {{site.data.keyword.Bluemix_notm}} für das Erstellen und Hosting Ihrer App berechnen, indem Sie die Preise der Laufzeit und der von der Laufzeit verwendeten Services betrachten. Die Preise der Laufzeiten und Services ändern sich manchmal, sodass Sie jeweils die neuesten Informationen auf der {{site.data.keyword.Bluemix_notm}}-Preisliste für die Berechnung des Gesamtpreises verwenden müssen.

## Beispiel: Preis für eine Beispielanwendung ermitteln
{: #sample}

Nehmen Sie an, Sie haben eine Node.js-Web-App mit Skalierbarkeitsfunktionalität und die App nutzt verschiedene Services, die von {{site.data.keyword.Bluemix_notm}} bereitgestellt werden. Dieses Beispiel zeigt, wie die tatsächlichen Kosten Ihrer App berechnet werden. Die Web-App nutzt die folgenden {{site.data.keyword.Bluemix_notm}}-Services und -Elemente:

* Vier Node.js-Laufzeitinstanzen mit jeweils 256 MB
* Zwei {{site.data.keyword.autoscaling}}-Richtlinien (Prozessor und Speicher)
* 2 GB {{site.data.keyword.datacshort}} pro Monat
* 150 GB NoSQL-Datenbank pro Monat, 100.000 komplexe API-Aufrufe und 500.000 einfache API-Aufrufe
* 20 GB Datenvolumen für ein- und ausgehenden Netzverkehr

## Preise für Bluemix-Ressourcen
{: #sample_resources}

Nehmen Sie an, um das Beispiel einfach zu halten, dass die Preise in der folgenden Tabelle innerhalb eines Zeitrahmens oder zwischen zwei Perioden zum Beispiel eines Monats nicht schwanken. Alle Preisangaben in diesem Beispiel erfolgen in US-Währung.

|Service |	Features |	Preis |
|--------|-----------|--------|
|SDK for Node.js |	375 GB-Stunden pro Monat kostenlos (für alle Laufzeiten gemeinsam) |	$0,07 USD/GB-Stunde|
|Auto-Scaling |	Kostenloser Serviceplan für den Auto-Scaling-Service |	Kostenlos |
|Datencache - Starter |	1 GB Cachebereich und ein Replikat |	$55,00 USD/Instanz |
|Datencache - Standard |	5 GB Cachebereich und ein Replikat |	$155,00 USD/Instanz |
|Datencache - Premium |	25 GB Cachebereich und ein Replikat |	$505,00 USD/Instanz|
|IBM Cloudant® NoSQL DB for {{site.data.keyword.Bluemix_notm}} |	2 GB Datenspeicher kostenlos<br/>50.000 einfache API-Aufrufe pro Monat kostenlos<br/>10.000 komplexe API-Aufrufe pro Monat kostenlos | $1,00 USD/GB<br/>$0,03 USD/1000 einfache API-Aufrufe<br/>$0,15 USD/1000 komplexe API-Aufrufe |
{:caption="Tabelle 1. Preisliste" caption-side="top"}

## Preis der App berechnen

Der Preis der App kann auf die folgende Weise berechnet werden:

<dl>
<dt>Vier Node.js-Laufzeitinstanzen mit jeweils 256 MB</dt>
<dd>Bluemix rechnet für eine Laufzeit nach GB-Stunden ab. Die Anzahl der genutzten GB pro Monat beträgt <code>4 x 256 = 1024 MB oder 1 GB pro Monat</code>. Nehmen Sie an, dass <code>ein Monat 24 x 30 = 720 Stunden</code> hat, sodass für die Anwendung <code>1 x 720 = 720 GB-Stunden</code> berechnet werden.
<p>
375 GB-Stunden gehören zu den kostenlosen Leistungen eines Monats, die für alle {{site.data.keyword.Bluemix_notm}}-Laufzeiten genutzt werden können. Daher betragen die Gesamtkosten für die Laufzeit <code>$0,07 x (720-375) = $24,15</code>.</p></dd>

<dt>Zwei Auto-Scaling-Richtlinien (Prozessor und Speicher)</dt>
<dd>Die Auto-Scaling-Richtlinien sind gebührenfrei.</dd>

<dt>2 GB Datencache pro Monat</dt>
<dd>Der 50-MB-Plan, der vom Auto-Scaling-Service bereitgestellt wird, ist gebührenfrei. Ihr gebührenfreier Plan würde jedoch nicht Ihre projektierte Nutzung von 2 GB pro Monat abdecken. Die drei gebührenpflichtigen Pläne für Datencache kosten einen festen Betrag für eine bestimmte Speichergröße unabhängig davon, wie viel Speicher Sie tatsächlich nutzen. Daher ist es sinnvoll, den Minimalplan zu wählen, der Ihre projektierte Nutzung abdeckt. Dies ist der Standardplan von 5 GB. Die Gesamtkosten betragen $155 pro Monat.</dd>

<dt>150 GB NoSQL-Datenbank pro Monat</dt>
<dd>Die Gebühren für den IBM Cloudant NoSQL DB for {{site.data.keyword.Bluemix_notm}}-Service basieren auf der Speicherung von Daten und der Möglichkeit, auf diese Daten mit verschiedenen API-Methoden zuzugreifen. Die Befehle <strong>PUT</strong> und <strong>POST</strong> werden als komplexe API-Aufrufe betrachtet, während Befehle <strong>GET</strong> als einfache API-Aufrufe betrachtet werden.
<p>
Addieren Sie die Anzahl GB und ziehen Sie 2 GB für kostenlos nutzbaren Speicher ab. 148 GB werden pro Monat in Rechnung gestellt. Subtrahieren Sie die kostenlos nutzbaren 50.000 einfachen API-Aufrufe und die 10.000 komplexen API-Aufrufe. Der Gesamtspeicherpreis setzt sich dann wie folgt zusammen:</p>
<pre class="codeblock">
<codeblock>
    148 x 1 = $148
    (450.000 / 1000) x 0,03 = $13,5
    (90.000 / 1000) x 0,15 = $13,5
</codeblock>
</pre>
<p>
Der Gesamtpreis beträgt 148 + 13,5 + 13,5 = $175.</p></dd>

<dt>20 GB Datenvolumen für ein- und ausgehenden Netzverkehr</dt>
<dd>Eingehender und ausgehender Netzdatenverkehr ist gebührenfrei.</dd>

</dl>

Wenn alle Positionen addiert werden, beträgt der Gesamtpreis der Anwendung $354.15.

## Unterstützte Währungen

Obwohl in den Preisbeispielen US-Dollar (USD) verwendet werden, werden in {{site.data.keyword.Bluemix_notm}} auch andere Währungen unterstützt. In der folgenden Tabelle werden die unterstützten Währungen aufgelistet.

|ISO 4217-Code| Währung|
|-------------|---------|
|AUD |	  Australischer Dollar|
|BRL |	  Brasilianischer Real|
|CAD |	  Kanadischer Dollar|
|CHF |	  Schweizer Franken|
|DKK |	  Dänische Krone|
|EUR |	  Euro|
|GBP |	  Britisches Pfund|
|INR |	  Indische Rupie|
|JPY |	  Japanischer Yen|
|KRW |	  Südkoreanischer Won|
|NOK |	  Norwegische Krone|
|NZD |	  Neuseeländischer Dollar|
|SEK |	  Schwedische Krone|
|USD |    US-Dollar|
|ZAR |	  Südafrikanischer Rand|
{:caption="Tabelle 2. Unterstützte Währungen" caption-side="top"}

**Hinweis:** Wenn Sie Ihre {{site.data.keyword.Bluemix_notm}}- und SoftLayer-Konten verknüpft haben, ist die einzige Rechnung, die Sie erhalten, nur in USD ausgestellt.
