---



copyright:

  years: 2015，2017

lastupdated: "2016-03-15"


---

{:shortdesc: .shortdesc}

# VCAP-Services


Die Umgebungsvariable VCAP_SERVICES ist ein JSON-Objekt, das Informationen enthält,
die Sie für die Interaktion mit einer Serviceinstanz in {{site.data.keyword.Bluemix_notm}} verwenden können.
{:shortdesc}


## Wert der Umgebungsvariable VCAP_SERVICES abrufen
{:retrieving}

Die Umgebungsvariable VCAP_SERVICES ist ein JSON-Objekt, das Informationen enthält,
die Sie für die Interaktion mit einer Serviceinstanz in {{site.data.keyword.Bluemix_notm}} verwenden können. Die Informationen umfassen den Namen der Serviceinstanz, den Berechtigungsnachweis und die URL für die Verbindung zu der Serviceinstanz. Mit diesen Werten wird die Umgebungsvariable VCAP_SERVICES gefüllt, wenn Ihre Anwendung an eine Serviceinstanz in {{site.data.keyword.Bluemix_notm}} gebunden wird.

Der Wert der Umgebungsvariable VCAP_SERVICES steht nur zur Verfügung, wenn Sie eine Serviceinstanz an Ihre Anwendung binden. Sie können die Anwendungsumgebungsvariablen mit dem folgenden Befehl anzeigen:
```
cf env APP_NAME
```
