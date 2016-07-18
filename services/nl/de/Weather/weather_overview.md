---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Informationen zu {{site.data.keyword.weather_short}}
{: #about_weather}

*Letzte Aktualisierung: 01. Juli 2016*
{: .last-updated}

Verwenden Sie {{site.data.keyword.weatherfull}},
um Wetterdaten von "The Weather Company" (TWC) in Ihre {{site.data.keyword.Bluemix}}-Anwendungen einzubinden.
{:shortdesc}

Sie können Wetterbeobachtungen und -vorhersagen zu Ihrer {{site.data.keyword.Bluemix_notm}}-Anwendung hinzufügen und die Wetterdaten für ein durch Geoortungsdaten angegebenes Gebiet mit den [REST-APIs](https://twcservice.{APPDomain}/rest-api/){:new_window} anzeigen.
"The Weather Company" ist der Anbieter mit den umfassendsten Langzeitwetterdaten und Vorhersagen. Es werden Daten zu allen Wetterphänomenen erfasst, darunter Niederschlag, Luftdruck, Wind und Gewitter.

Sie können die REST-APIs zum Abrufen der folgenden Informationen verwenden:

* Eine stündliche Wettervorhersage für die nächsten 48 Stunden, beginnend mit dem aktuellen Zeitpunkt, für angegebene Geoortungsdaten.
* Eine tägliche Vorhersage ab dem aktuellen Tag für die nächsten 3, 5, 7 oder 10 Tage, einschließlich Vorhersage-Abschnitten für Tag und Nacht, für angegebene Geoortungsdaten. Diese Vorhersage umfasst eine
beschreibende Textzeichenfolge mit bis zu 256 Zeichen und die entsprechenden Maßeinheiten
für den angeforderten Standort und in der angeforderten Sprache.
* Eine tägliche Vorhersage ab dem aktuellen Tag für die nächsten 3, 5, 7 oder 10 Tage, aufgegliedert in Vormittag, Nachmittag, Abend und Nacht.
* Die aktuellen Wetterbeobachtungsdaten für angegebene Geoortungsdaten. Zu diesen Wetterdaten
zählen Temperatur, Niederschlag, Windrichtung und -geschwindigkeit, Feuchtigkeit, Luftdruck,
Kondensationspunkt, Sichtweite und UV-Strahlung.
* Die Wetterbeobachtungsdaten für angegebene Geoortungsdaten für die letzten 24 Stunden. Diese Daten stammen von Beobachtungsstationen.
* Amtlich ausgegebene Wetterwarnungen, darunter Wetterbeobachtungen, Warnungen, Aussagen und Empfehlungen, die vom National Weather Service (USA), Environment Canada und MeteoAlarm (Europa) ausgegeben werden.
* Almanach-Services mit historischen täglichen oder monatlichen Wetterdaten von Beobachtungsstationen des National Weather Service aus einem Zeitraum von 10 bis 30 Jahren oder mehr.
* Standort-Zuordnungsservices, die die Suche nach Standortnamen oder Geodaten (Längen- und Breitengrade) ermöglichen, um einen Satz von Standorten abzurufen, die mit Ihrer Suche übereinstimmen.

Sie können auch eine [Gruppe von Symbolen herunterladen](https://twcdocs.mybluemix.net/download/weatherinsightsicons.zip){:new_window}, die Sie in Ihrer App verwenden können.

## Preismodell
{: #pricing_models}

Das Preismodell basiert auf der Anzahl der Aufrufe an die REST-APIs pro Minute. Die Rechnungsstellung an den Kunden erfolgt monatlich. Die Free- und Base-Pläne ermöglichen maximal 10 API-Aufrufe pro Minute. Die Standard- und Premium-Pläne ermöglichen jeweils 150 bzw. 375 API-Aufrufe pro Minute. Für jeden Plan gibt es eine maximale Anzahl zulässiger API-Aufrufe.

Sie können die Wetterdaten in Ihren Anwendungen testen,
ohne dass Einschränkungen hinsichtlich Geografie, Vorhersagetyp oder Zeitreihenbeobachtungen bestehen.
Es besteht lediglich eine Einschränkung hinsichtlich der Anzahl der Aufrufe. Die Pläne Free, Base, Standard und Premium können ohne Vertrag erworben werden. Der Free-Plan lässt 10.000 Aufrufe von Ihrer App zu. Die anderen Pläne lassen pro Monat jeweils 150.000, 2 Millionen oder 5 Millionen API-Aufrufe zu.

Es ist auch möglich, mehrere entgeltliche Pläne für jede Serviceinstanz zu erwerben, die während des Abrechnungszeitraums bereitgestellt wird. Wenn Ihre App mehr als 10.000 Aufrufe verwendet, benötigen Sie einen Vertrag mit IBM, damit die gewünschten Serviceleistungen weiterhin erbracht werden.

Wenn Ihre App den Grenzwert der API-Aufrufe pro Minute erreicht, die im Rahmen des ausgewählten Plans zulässig sind, ist der darauf folgende API-Aufruf erst dann wieder erfolgreich, wenn weitere API-Aufrufe von Ihrer App aus zulässig sind.

Beispiel: Im Rahmen des Standard-Plans *kann* Ihre App 500 API-Aufrufe pro Minute durchführen, selbst wenn der Grenzwert des Plans (150 Aufrufe pro Minute) überschritten wird, der nächste API-Aufruf wird jedoch erst 5 Minuten später zugelassen. Aus diesem Grund stellt ein Benutzer möglicherweise eine Verzögerung bei der Aktualisierung
der Wetterdaten in der App fest.
Sie müssen sicherstellen, dass die App so entwickelt wird,
dass sie diese Grenzwerte berücksichtigt und keine großen Blöcke mit API-Aufrufen anfordert. Stattdessen können Sie die Verwendung von API-Aufrufen Ihrer App überwachen.
Sie können prüfen, ob die App den Grenzwert des jeweiligen Plans erreicht,
indem Sie die Anzahl der Elemente, die durch den API-Aufruf zurückgegeben werden, überprüfen.

Wenn Ihre App den Grenzwert der API-Aufrufe pro Monat erreicht, die im Rahmen des ausgewählten Plans zulässig sind, werden die darauf folgenden API-Aufrufe mit einem Überschreitungssatz von 1,70 Dollar pro 10.000 API-Aufrufe berechnet.

## Feedback und Support
{: #feedback_support}

Wenn Sie technische Fragen zum Erstellen einer App mit {{site.data.keyword.weather_short}} haben, posten Sie Ihre Frage bei [Stack Overflow](https://stackoverflow.com/questions/tagged/ibm-bluemix+weather){:new_window} und markieren Sie Ihre Frage mit **ibm-bluemix** und **weather**.

Wenn Sie Probleme mit diesem Service haben sollten, verwenden Sie das Forum [IBM developerWorks Answers forum](https://developer.ibm.com/answers/topics/weather/?smartspace=bluemix){:new_window}.
Schließen Sie die Tags **bluemix** und **weather** in Ihre Beiträge ein, damit IBM Sie besser unterstützen kann.

Wenn Sie Fragen zum Migrieren Ihrer App von Insights for Weather auf {{site.data.keyword.weather_short}} haben, kontaktieren Sie uns unter [IBM developerWorks](http://www.ibm.com/developerworks){:new_window}.

Informationen zur Fehlerbehebung bei Bluemix finden Sie im Thema zur [Fehlerbehebung](https://console.{DomainName}/docs/troubleshoot/troubleshoot.html){: new_window}.
Details zur Suche nach Informationen und für das Stellen von Fragen in Foren sowie zur Kontaktaufnahme mit dem Support finden Sie im Thema zum [Abrufen der Kundenunterstützung](https://console.{DomainName}/docs/support/index.html#getting-customer-support){: new_window}.
