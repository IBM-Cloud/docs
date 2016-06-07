---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Informationen zu Insights for Weather
{: #about_weather}

*Letzte Aktualisierung: 19. Mai 2016*

Verwenden Sie {{site.data.keyword.weatherfull}},
um Wetterdaten von "The Weather Company" (TWC) in Ihre {{site.data.keyword.Bluemix}}-Anwendungen einzubinden.
{:shortdesc}

Sie können Wetterbeobachtungen und -vorhersagen zu Ihrer {{site.data.keyword.Bluemix_notm}}-Anwendung hinzufügen und die Wetterdaten
für ein durch Geoortungsdaten angegebenes Gebiet mit den [REST-APIs von Insights](https://twcservice.{APPDomain}/rest-api/){:new_window} anzeigen.
"The Weather Company" ist der Anbieter mit den umfassendsten Langzeitwetterdaten und Vorhersagen. Es werden Daten zu allen Wetterphänomenen erfasst, darunter Niederschlag, Luftdruck, Wind und Gewitter.

Sie können die REST-APIs zum Abrufen der folgenden Informationen verwenden:

* Eine stündliche Wettervorhersage für die nächsten 24 Stunden, beginnend mit
dem aktuellen Zeitpunkt, für angegebene Geoortungsdaten.
* Eine tägliche Vorhersage für die nächsten 10 Tage, einschließlich Vorhersagen
für Tag und Nacht, für angegebene Geoortungsdaten. Diese Vorhersage umfasst eine
beschreibende Textzeichenfolge mit bis zu 256 Zeichen und die entsprechenden Maßeinheiten
für den angeforderten Standort und in der angeforderten Sprache.
* Die aktuellen Wetterbeobachtungsdaten für angegebene Geoortungsdaten. Zu diesen Wetterdaten
zählen Temperatur, Niederschlag, Windrichtung und -geschwindigkeit, Feuchtigkeit, Luftdruck,
Kondensationspunkt, Sichtweite und UV-Strahlung.
* Die Wetterbeobachtungsdaten für angegebene Geoortungsdaten für einen bestimmten Zeitraum. Diese Daten stammen von Beobachtungsstationen. Diese API gibt Wetterbeobachtungen
für aktuelle Bedingungen sowie zurückliegende Beobachtungen für einen Zeitraum von bis zu 24 Stunden zurück.

Weitere Informationen zu Wetterbezeichnungen und Wettersymbolen von "The Weather Company"
finden Sie in [Icon Code, Phrases and Images](https://docs.google.com/document/d/1MZwWYqki8Ee-V7c7InBuA5CDVkjb3XJgpc39hI9FsI0/edit?pli=1){:new_window}.
Sie können auch eine [Reihe von Symbolen herunterladen](https://twcdocs.mybluemix.net/download/weatherinsightsicons.zip){:new_window}, um Sie in Ihrer App zu verwenden.

## Preismodell
{: #pricing_models}

Das Preismodell basiert auf der Anzahl der täglichen Aufrufe der Insights for Weather-APIs, die dem Kunden monatlich
in Rechnung gestellt werden. Sie können die Wetterdaten in Ihren Anwendungen testen,
ohne dass Einschränkungen hinsichtlich Geografie, Vorhersagetyp oder Zeitreihenbeobachtungen bestehen.
Es besteht lediglich eine Einschränkung hinsichtlich der Anzahl der Aufrufe. Der Plan für kostenfreie Aufrufe, der Basisplan und der Premium-Plan können
ohne Vertrag erworben werden. Diese Pläne ermöglichen der App
500, 5.000 bzw. 50.000 API-Aufrufe pro Tag.

Es ist auch möglich, mehrere Premium-Pläne für jede Serviceinstanz zu erwerben,
die während des Abrechnungszeitraums bereitgestellt wird. Wenn Ihre App mehr als 50.000 Aufrufe pro Tag oder über 1.000 Aufrufe pro Minute verwendet,
benötigen Sie einen Vertrag mit IBM, damit die gewünschten Serviceleistungen weiterhin erbracht werden.

Wenn die App den Grenzwert der API-Aufrufe erreicht, die im Rahmen des ausgewählten Plans zulässig sind,
ist der darauf folgende API-Aufruf erst wieder erfolgreich, wenn die nächsten API-Aufrufe zulässig sind.

Beispiel: Im Rahmen des Basisplans kann die App 500 API-Aufrufe pro Minute durchführen,
auch wenn der Grenzwert des Plans überschritten wird, der nächsten API-Aufruf wird jedoch
erst 5 Minuten später zugelassen. Aus diesem Grund stellt ein Benutzer möglicherweise eine Verzögerung bei der Aktualisierung
der Wetterdaten in der App fest. Sie müssen sicherstellen, dass die App so entwickelt wird,
dass sie diese Grenzwerte berücksichtigt und keine großen Blöcke mit API-Aufrufen anfordert. Stattdessen können Sie die Verwendung von API-Aufrufen Ihrer App überwachen. Sie können prüfen, ob die App den Grenzwert des jeweiligen Plans erreicht,
indem Sie die Anzahl der Elemente, die durch den API-Aufruf zurückgegeben werden, überprüfen.

## Feedback und Support
{: #feedback_support}

Wenn Sie technische Fragen zum Erstellen einer App mit "Insights for Weather" haben, posten Sie Ihre Frage bei [Stack Overflow](http://stackoverflow.com/search?q=weather+bluemix){:new_window}
und versehen Sie Ihre Frage mit den Tags **bluemix** und **weather**.

Wenn Sie Probleme mit diesem Service haben sollten, verwenden Sie das Forum [IBM developerWorks Answers forum](https://developer.ibm.com/answers/topics/insights-weather/?smartspace=bluemix){:new_window}.
Schließen Sie die Tags **insights-weather** und **bluemix** in Ihre Beiträge ein, um IBM eine bessere Unterstützung für Sie zu ermöglichen.

Informationen zur Fehlerbehebung bei Bluemix finden Sie im Thema zur [Fehlerbehebung](https://console.{DomainName}/docs/troubleshoot/troubleshoot.html){: new_window}.
Details zur Suche nach Informationen und für das Stellen Fragen in Foren sowie zur Kontaktaufnahme mit dem Support finden Sie im Thema zum [Abrufen der Kundenunterstützung](https://console.{DomainName}/docs/support/index.html#getting-customer-support){: new_window}.
