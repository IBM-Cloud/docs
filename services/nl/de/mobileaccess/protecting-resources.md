---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}

# Cloudressourcen mit {{site.data.keyword.amashort}} schützen
{: #protecting-resources}
Mit dem {{site.data.keyword.amashort}}-Service können Sie Ihre Node.js- und Java-basierten Back-End-Anwendungen, die in {{site.data.keyword.Bluemix_notm}} ausgeführt werden, mit mobilgerätefähiger OAuth-Sicherheit und Überwachungsfunktionen schützen.
{:shortdesc}
## Berechtigungsfilter
{: #auth-filter}
Das {{site.data.keyword.amashort}}-Server-SDK verfügt über Berechtigungsfilter, mit deren Hilfe Sie Ihre Back-End-Anwendungen schützen können.  Der Berechtigungsfilter fängt eingehende Anforderungen ab und prüft, ob ein Berechtigungsheader vorhanden ist. Wenn der Berechtigungsheader nicht vorhanden oder ungültig ist, gibt der Filter eine Antwort mit dem Code HTTP 401 zurück. Das {{site.data.keyword.amashort}}-Client-SDK weiß, wie eine Antwort mit dem Code HTTP 401 abzufangen ist, die vom {{site.data.keyword.amashort}}-Server-SDK zurückgegeben wird, und löst den Authentifizierungsablauf aus.
## Berechtigungsheader
{: #auth-header}
Der Berechtigungsheader in der eingehenden Anforderung besteht aus drei Teilen: Träger (Bearer), Zugriffstoken und ID-Token, die durch Leerzeichen voneinander getrennt sind. Das `Zugriffstoken` ist eine verbindliche Komponente, während das `ID-Token` optional ist.

Der eingehende Berechtigungsheader wird von dem entsprechenden Berechtigungsfilter verarbeitet. Der Filter validiert die Signaturen des Zugriffstokens und des ID-Tokens, das Ablaufdatum und die strukturelle Integrität. Wenn die Validierung erfolgreich war, wird dem Anforderungsobjekt ein Sicherheitskontextobjekt hinzugefügt. Sie können eine Referenz auf den Sicherheitskontext mithilfe einer entsprechenden API abrufen.

Der Sicherheitskontext enthält die Informationen zu Subjekt, Benutzer, Gerät und Anwendung, die mit der folgenden Struktur gespeichert werden:
```JSON
{
    "imf.sub":"myclientid",
    "imf.user": {
        "id":"user-name",
        "authBy":"myrealm",
        "displayName":"display-name"
    },
    "imf.device": {
        "id":"device-id",
        "platform":"iOSnative",
        "model":"device-model",
        "osVersion":"device-os"
    },
    "imf.application": {
        "id":"ios.bundle.id",
        "version":"1.0"
    }
}
```
* `imf.sub`: Gibt das Subjekt (Betreff) des ID-Tokens oder die eindeutige ID des Clients an, falls kein ID-Token vorhanden ist.
* `imf.user`: Gibt die Benutzeridentität an, die aus dem ID-Token extrahiert wurde. Falls kein ID-Token vorhanden ist, enthält dieses Feld ein leeres Objekt.
* `imf.device`: Gibt die Geräteidentität an, die aus dem ID-Token extrahiert wurde. Falls kein ID-Token vorhanden ist, enthält dieses Feld ein leeres Objekt.
* `imf.application`: Gibt die Anwendungsidentität an, die aus dem ID-Token extrahiert wurde. Falls kein ID-Token vorhanden ist, enthält dieses Feld ein leeres Objekt.

## Nächste Schritte
{: #next-steps}
* [Node.js-Ressourcen schützen](protecting-resources-nodejs.html)
* [Liberty for Java&trade;-Ressourcen schützen](protecting-resources-java.html)
* [Lokale Entwicklung](protecting-resources-local.html)
