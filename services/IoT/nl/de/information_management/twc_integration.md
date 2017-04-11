---

copyright:
years: 2016, 2017
lastupdated: "2017-03-13"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Daten von The Weather Company mit Ihren Geräten verwenden
{: #weathercompany}

Mit der Integration 'The Weather Company' können Sie Ihre vorhandenen {{site.data.keyword.iot_short_notm}}-Geräte mit Wetterdaten kombinieren. {:shortdesc}

Wetterdaten von The Weather Company werden in der Ansicht 'Gerätedetails' angezeigt, wenn mithilfe der API die Anforderung 'Position aktualisieren' vorgenommen wurde oder wenn das Gerät seine Position bereits mithilfe einer Gerätemanagementnachricht festgelegt hat.

**Wichtig:** Nur verwaltete Geräte können ihre eigene Position festlegen. Für alle nicht verwalteten Geräte muss die Position manuell mithilfe der API festgelegt werden. Weitere Informationen zum Festlegen einer Geräteposition finden Sie in [Anforderung 'Position aktualisieren'](../../devices/device_mgmt/index.html#update-location).

### REST-APIs für The Weather Company
Informationen für den Zugriff auf die REST-API für The Weather Company finden Sie im Abschnitt
'Device Location Weather' in der Dokumentation für die [{{site.data.keyword.iot_short_notm}}-HTTP-REST-API ![Symbol für externen Link](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Device_Location_Weather){: new_window}.

### Wetterdaten anzeigen

Gehen Sie wie folgt vor, um die für eine Geräteposition abgerufenen Wetterdaten anzuzeigen. 
1. Klicken Sie auf das Gerät im Teilfenster **Geräte**.
2. Blättern Sie in der detaillierten Ansicht für Geräte zum Abschnitt **Erweiterungen**.  
Folgende Wetterdaten werden aufgelistet:
 - Aktuelles Wetter.
 - Aktuelle Temperatur.
 - Vorhergesagte minimale und maximale Temperatur.
 - Relative Feuchtigkeit.
 - Druck.
 - Sichtweite.
 - Windgeschwindigkeit.
 - Windrichtung.
 - Breitengrad.
 - Längengrad.

<!-- Weather data from The Weather Company extension can be retrieved by using the API. For information on the Weather Company API, see [The Weather Company API documentation ![External link icon](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/swagger/ext-twc.html){: new_window}. -->
