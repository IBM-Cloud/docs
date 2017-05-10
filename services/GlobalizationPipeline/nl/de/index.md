---

copyright:
  years: 2015, 2017
lastupdated: "2016-09-09"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Einführung in {{site.data.keyword.GlobalizationPipeline_short}}
{: #globalizationpipeline}

{{site.data.keyword.GlobalizationPipeline_full}} ist ein Service, der automatische Übersetzungs- und Bearbeitungsfunktionen für die schnelle Übersetzung von mobilen oder Webbenutzerschnittstellen bietet. Mit dem zugehörigen Dashboard, der RESTful-API und der Integration in die Bereitstellungspipeline Ihrer App können Sie die Freigabe für globale Kunden erteilen, ohne einen erneuten Build für Ihre App zu erstellen oder diese erneut zu implementieren.
{:shortdesc}

Sie können den Service {{site.data.keyword.GlobalizationPipeline_short}} mit einer beliebigen App in {{site.data.keyword.Bluemix}} oder in nicht gebundener Form als eigenen Service verwenden. Sie können Übersetzungen schnell und ohne großen Aufwand erstellen, verwalten und überarbeiten, ohne Ihre DevOps-Umgebung verlassen zu müssen.

Von der {{site.data.keyword.GlobalizationPipeline_short}}-Schnittstelle können Sie in kurzer Zeit Ihre {{site.data.keyword.Bluemix_notm}}-Apps übersetzen. Informationen zur Übersetzung Ihrer Apps mithilfe der RESTful-API finden Sie unter [API-Referenz](https://gp-rest.ng.bluemix.net/translate/swagger/index.html){: new_window}. 


## Bundle erstellen
{: #globalizationpipeline_creatingbundles}

Mit dem Service {{site.data.keyword.GlobalizationPipeline_short}} können Sie Bundle erstellen, die die Ressourcendateien der Apps einbeziehen, die übersetzt werden. Die Ressourcendateien können entweder Java-Eigenschaften, AMD I18N oder JSON-Dateien sein und müssen den Inhalt in Form von Schlüssel/Wertpaaren enthalten, die die Zeichenfolgen der Benutzerschnittstelle Ihrer App darstellen.  Weitere Details und Beispiele unterstützter Dateitypen finden Sie unter [Mit Bundles arbeiten](./bundles.html){: new_window}.

Führen Sie die folgenden Schritte aus, um ein Bundle zu erstellen:

<ol>
<li>Klicken Sie auf der Registerkarte <strong>Übersicht</strong> auf <strong>Neues Bundle</strong>.</li>

<li>Geben Sie Informationen zu Ihrem Bundle an:</li>
<table>
<thead>
<tr>
<th>Feld</th>
<th>Erforderlich</th>
<th>Beschreibung</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>Bundle-ID</strong></td>
<td>Ja</td>
<td>Ein eindeutiger Name, der das Bundle angibt.</td>
</tr>
<tr>
<td><strong>Ausgangssprache</strong></td>
<td>Ja</td>
<td>Die Landessprache der Quellendatei.</td>
</tr>
<tr>
<td><strong>Ressourcendatei</strong></td>
<td>Nein</td>
<td>Eine zu übersetzende <a href=https://new-console.ng.bluemix.net/docs/services/GlobalizationPipeline/bundles.html>Ressourcendatei</a>. Die maximale Dateigröße ist auf 2MB begrenzt. Angegebene Ressourcendateien werden hochgeladen.</td>
</tr>
<tr>
<td><strong>Dateiformat</strong></td>
<td>Nein</td>
<td>Der Dateityp, der hochgeladen wird.</td>
</tr>
<tr>
<td><strong>Zielsprache</strong></td>
<td>Nein</td>
<td>Die Sprachen, für die Sie Übersetzungen wünschen.</td>
</tr>
</tbody>
</table>

<p><strong>Hinweis:</strong> Um den Sprachservice zu ändern, der die automatische Übersetzung für Ihre Bundle anbietet, klicken Sie auf die Registerkarte <a href=https://new-console.ng.bluemix.net/docs/services/GlobalizationPipeline/managing_translations.html#globalizationpipeline_service_to_service>MT-Konfiguration</a>, um andere unterstützte Engines für automatische Übersetzungen anzuzeigen.</p>

<li>Klicken Sie auf <strong>Speichern</strong>.</li></ol>


Nach der Erstellung des Bundles wird die hochgeladene Ressourcendatei in alle angegebenen Zielsprachen übersetzt. Das neue Bundle wird zur Registerkarte 'Bundles' hinzugefügt. Auf dieser Registerkarte können Sie folgende Aktionen ausführen:

* Sprachen hinzufügen und entfernen
* Generierte Übersetzungen bearbeiten
* Die Quellendatei aktualisieren, die im Bundle verwendet wird, und die Übersetzungen neu erstellen.

## Übersetzte Bundles importieren
{: #globalizationpipeline_importtranslatedbundlesintoservice}

Alternativ können Sie, falls Sie über bereits übersetzte Ressourcendateien verfügen, diese in ein neues Bundle importieren. Weitere Informationen finden Sie unter [Java Client Tools für {{site.data.keyword.GlobalizationPipeline_short}}](https://github.com/IBM-Bluemix/gp-java-tools).

**Hinweis:**  Wenn die ursprüngliche Quellendatei aktualisiert wird, werden die Schlüssel und Werte, die in der Datei definiert sind, mit der aktuellsten Version der Quellendatei synchronisiert, so dass nur die geänderten Schlüssel und Werte übersetzt werden.

## Datennutzung von {{site.data.keyword.GlobalizationPipeline_short}} schätzen
{: #globalizationpipeline_documentpricing}

{{site.data.keyword.GlobalizationPipeline_short}} speichert Ihre Übersetzungen in einer Back-End-Datenbank. Um die Größe des Datenarchivs zu schätzen, können Sie die Formel zur Schätzung des Datenspeichers verwenden:

`<erwartete Speichergröße für Ressourcendaten in MB> ˜= 0,0005 * <Anzahl der Schlüssel/Wertpaaree in der Quellenressourcee> * <Anzahl der Sprachen einschließlich der Ausgangssprache >`

Nach der Formel ist die Größe eines typischen Bundles `(Länge des Schlüssels + Länge des Wertes in UTF-8 = ˜40 Byte `.

Wenn Sie zum Beispiel über 100 Schlüssel/Wertpaare verfügen und diese in 9 Sprachen übersetzen, beträgt die geschätzte Speichergröße 0,0005 100 (9+1) = 0,5 MB. Die tatsächliche Größe kann sich abhängig von der tatsächlichen Größe der Schlüssel/Wertpaare und der Metadaten, die mit der Übersetzung gespeichert werden, davon unterscheiden.

Verwenden Sie den Bluemix [Preisrechner](https://console.ng.bluemix.net/?direct=classic/#/pricing/cloudOEPaneId=pricing&paneId=pricingSheet&orgGuid=127a45f4-4461-4d5b-a26b-6dc2fdd1a3a2&spaceGuid=208fb1ff-413b-4fd9-9615-e8226062d0f3), um Ihre monatlichen Kosten zu ermitteln.


# Zugehörige Links
{: #rellinks}
## Lernprogramme und Beispiele
{: #samples}

* [Beispiel Node.js ](https://github.com/IBM-Bluemix/gp-nodejs-sample){: new_window}
* [Beispiel Ruby ](https://github.com/IBM-Bluemix/gp-ruby-sample){: new_window}

## SDK
{: #sdk}

* [Java-Client](https://github.com/IBM-Bluemix/gp-java-client){: new_window}
* [Java-Tools](https://github.com/IBM-Bluemix/gp-java-tools){: new_window}
* [JavaScript-Client](https://github.com/IBM-Bluemix/gp-js-client){: new_window}
* [AngularJS-Client](https://github.com/IBM-Bluemix/gp-angular-client){: new_window}
* [Ruby-Client](https://github.com/IBM-Bluemix/gp-ruby-client){: new_window}
* [Python-Client](https://github.com/IBM-Bluemix/gp-python-client){: new_window}

## API-Referenz
{: #api}

* [IBM Globalization Pipeline - RESTful-API](https://gp-rest.ng.bluemix.net/translate/swagger/index.html){: new_window}

## Zugehörige Links
{: #general}

* [Globalization Pipeline in Delivery Pipeline integrieren](https://hub.jazz.net/docs/deploy_ext/#globalize){: new_window}
* [IBM Bluemix - Preisliste](https://www.ng.bluemix.net/#/pricing){: new_window}
* [IBM Bluemix - Voraussetzungen](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}
