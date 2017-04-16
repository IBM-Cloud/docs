---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Benutzerbasierte Benachrichtigungen aktivieren
{: #user_based_notifications}
Letzte Aktualisierung: 16. Januar 2017
{: .last-updated}

Auf Benutzer-ID basierte Push-Benachrichtigungen zielen mit angepassten Nachrichten auf Benutzer mobiler Apps ab. Bei benutzerbasierten Benachrichtigungen können Sie auswählen, dass bestimmte Personen auf Grundlage Ihrer Vorgaben benachrichtigt werden.

## Gerät mit Benutzer-ID registrieren
Um Push-Benachrichtigungen zu aktivieren, die auf einer Benutzer-ID basieren, müssen Sie sicherstellen, dass Sie das Gerät mit einer Benutzer-ID registrieren.     

Die Benutzer-ID kann eine beliebige Zeichenfolge sein, die die Anwendung gegenüber der API für die Geräteregistrierung bereitstellt. Normalerweise führt eine mobile Anwendung zuerst einen Authentifizierungszyklus aus, in dessen Verlauf der Benutzer mobiler Apps bei einem Authentifizierungsservice wie [{{site.data.keyword.amafull}} ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.ng.bluemix.net/docs/services/mobileaccess/index.html){: new_window} authentifiziert wird. Nach der erfolgreichen Authentifizierung wird die ID des authentifizierten Benutzers dann an die API für Push-Geräteregistrierungen übergeben. 

## Benutzeranmeldung/-abmeldung synchronisieren 

Sie können festlegen, dass Benachrichtigungen nur gesendet werden, wenn der Benutzer angemeldet ist. 

Beispiel: Ein Gerät wird von mehreren Familienmitgliedern oder Teammitgliedern an der Arbeit gemeinsam genutzt und es müssen bestimmte Benutzer angesprochen werden. In einem derartigen Anwendungsfall würde eine entsprechende Benutzeranmelde- und -abmeldesequenz zum Einsatz kommen. Dieser Authentifizierungsmechanismus ermöglicht es der Anwendung, die Identität des aktuellen Benutzer der Anwendung zu ermitteln. So wird sichergestellt, dass Benachrichtigungen, die einen bestimmten Benutzer zum Ziel haben, auch stets nur von diesem Benutzer empfangen werden. Rufen Sie nach einer erfolgreichen Anmeldung die API für die Geräteregistrierung auf, indem Sie die Benutzer-ID des angemeldeten Benutzers übergeben. Ebenso müssen Sie vor dem Abmelden die API für die Rücknahme der Registrierung aufrufen. Durch die Reihenfolgeplanung für diese Push-APIs in Verbindung mit der An- und Abmeldung wird sichergestellt, dass Benachrichtigungen für einen bestimmten Benutzer wirklich nur an diesen Benutzer gesendet werden.
