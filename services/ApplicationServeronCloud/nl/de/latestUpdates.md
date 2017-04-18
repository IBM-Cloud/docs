---

Copyright:
  Jahre: 2015, 2016
Letzte Aktualisierung: 08.11.2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Letzte Aktualisierungen
{: #latest_updates}

Eine Liste der neuesten Aktualisierungen für den Service.

## 8. November 2016: WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} aktualisiert

* Möglichkeit für Kunden hinzugefügt, eine [öffentliche IP-Adresse](networkEnvironment.html#networkEnvironment) für die WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}-VM anzufordern.
* Es wurden [verschiedene Sicherheitslücken](http://www-01.ibm.com/support/docview.wss?uid=swg21993842){: new_window} adressiert, die sich auf WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} auswirken; dazu gehören die folgenden:
  * Eine Sicherheitslücke in IBM WebSphere Application Server, die es Remote-Angreifern ermöglicht, beliebigen Java-Code mit einem serialisierten Objekt aus nicht vertrauenswürdigen Quellen auszuführen.
  * Eine Denial-of-Service-Sicherheitslücke, verursacht durch einen Lesevorgang außerhalb des gültigen Bereichs in der Funktion 'TS_OBJ_print_bio'. Ein Remote-Angreifer könnte diese Sicherheitslücke nutzen und den Absturz der Anwendung durch eine speziellentwickelte Zeitmarkendatei verursachen.
  * Eine potenzielle Sicherheitslücke in OpenSSL, die einem Remote-Angreifer das Abrufen schutzwürdiger Informationen ermöglicht, verursacht durch einen Triple-DES-Fehler in der im SSL/TLS-Protokoll verwendeten 64-Bit-Blockverschlüsselung. Durch die Erfassung großer verschlüsselter Datenmengen zwischen dem SSL/TLS-Server und dem Client könnte ein Remote-Angreifer mit der Möglichkeit zur Durchführung einer Man-in-the-Middle-Attacke diese Sicherheitslücke nutzen, um die unverschlüsselten Daten und damitschutzwürdige Informationen abzurufen. Diese Sicherheitslücke wird auch 'SWEET32 Birthday-Attacke' genannt.
  * Denial-of-Service-Sicherheitslücke bei OpenSSL. Durch die wiederholte Anforderung von Neuvereinbarungen könnte ein authentifizierter Remote-Angreifer eine übermäßig große OCSP Status Request Extension senden, um alle verfügbaren Speicherressourcen zu belegen.
  * Denial-of-Service-Sicherheitslücke bei OpenSSL, verursacht durch einen Ganzzahlüberlauf in der Funktion 'MDC2_Update'. Ein Remote-Angreifer könnte diese Sicherheitslücke unter Verwendung unbekannter Angriffsvektoren nutzen, um einen Schreibvorgang außerhalb des gültigen Bereichs auszulösen und dadurch den Absturz der Anwendung zu verursachen.
  * Eine potenzielle Sicherheitslücke in OpenSSL, die einem Remote-Angreifer das Abrufen schutzwürdiger Informationen ermöglicht, verursacht durch einen Fehler in der DSA-Implementierung, der bei bestimmten Operationen die Verfolgung eines nicht konstanten Zeitcodepfads ermöglicht. Ein Remote-Angreifer könnte diese Sicherheitslücke nutzen und den privaten DSA-Schlüssel mittels einer Cache-Timing-Attacke abrufen.
  * Denial-of-Service-Sicherheitslücke bei OpenSSL, verursacht durch fehlende Überprüfung der Nachrichtenlänge beim Parsing von Zertifikaten. Ein authentifizierter Remote-Angreifer könnte diese Sicherheitslücke nutzen, um einen Lesevorgang außerhalb des gültigen Bereichs auszulösen und eine Serviceverweigerung zu verursachen.

## 19. September 2016: WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} aktualisiert

* Upgrade der WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}-Binärdateien, damit für neue Instanzen von WebSphere Application Server Liberty (Core- und ND-Pläne) Fixpack 16.0.0.3 installiert wird. 
* Es wurden [verschiedene Sicherheitslücken](http://www-01.ibm.com/support/docview.wss?uid=swg21990236){: new_window} adressiert, die sich auf WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} auswirken; dazu gehören die folgenden:
  * Eine Sicherheitslücke in IBM WebSphere Application Server Liberty, die es einem Remote-Angreifern ermöglicht, Phishing-Attacken durchzuführen.
  * Eine Sicherheitslücke in IBM WebSphere Application Server Liberty bezüglich Cross-Site Scripting in OIDC-Clients (OpenID Connect).
  * Eine potenzielle Sicherheitslücke in IBM WebSphere Application Server Liberty, die Remote-Angreifern das Abrufen schutzwürdiger Informationen ermöglicht, verursacht durch die falsche Handhabung von Ausnahmebedingungen bei Nichtvorhandensein einer Standardfehlerseite.
  * Eine Denial-of-Service-Sicherheitslücke in Apache Tomcat, verursacht durch einen Fehler in der Komponente 'Apache Commons FileUpload'.
  * Eine Sicherheitslücke in IBM WebSphere Application Server und IBM WebSphere Application Server Liberty, die Remote-Angreifern das Abrufen schutzwürdiger Informationen ermöglicht, verursacht durch die falsche Handhabung von Antworten unter bestimmten Bedingungen.
  * Eine nicht spezifizierte Sicherheitslücke in Verbindung mit der Netzkomponente, die keine Auswirkungen auf die Vertraulichkeit, geringe Auswirkungen auf die Integrität und keine Auswirkungen auf die Verfügbarkeit hat.

## 17. August 2016: WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} aktualisiert

* Die Binärdateien von WebSphere Application Server for Bluemix wurden von Version 8.5.5.9 auf Version 8.5.5.10 aktualisiert
* Es wurden [verschiedene Sicherheitslücken](http://www-01.ibm.com/support/docview.wss?uid=swg21988710){: new_window} adressiert, die sich auf WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} auswirken; dazu gehören die folgenden:
  * Apache Struts-Sicherheitslücken, die sich auf WebSphere Application Server und auf die WebSphere Application Server Hypervisor Edition-Administrationskonsole auswirken.
  * Eine potenzielle DoS-Sicherheitslücke mit IBM WebSphere Application Server bei der Verwendung von SIP-Services.
  * Verschiedene Sicherheitslücken, die sich auf den von WebSphere Application Server verwendeten IBM HTTP Server auswirken können.
  * Eine Sicherheitslücke, die das Weiterleiten von HTTP-Datenverkehr mit CGI-Anwendungen ermöglicht und sich auf IBM HTTP Server (IHS) auswirken kann. Diese Sicherheitslücke wird auch "HTTPOXY" genannt.
  * Eine Sicherheitslücke bei der Informationsweitergabe in IBM WebSphere Application Server.
  * Eine potenzielle Sicherheitslücke zur Umgehung von Sicherheitsbeschränkungen in IBM WebSphere Application Server, die nur in Umgebungen mit aktivierter angepasster Web-Container-Eigenschaft 'HttpSessionIdReuse' auftritt.


## 24. Juni 2016: WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} aktualisiert

* Möglichkeit für Kunden hinzugefügt, bei der Erstellung einer neuen Instanz von *klassischem ND* oder *klassischem WebSphere* zwischen V8.5 und V9.0 zu wählen.
* Upgrade der WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}-Binärdateien, damit für neue Instanzen von WebSphere Application Server Liberty (Core- und ND-Pläne) Fixpack 16.0.0.2 installiert wird. 16.0.0.2 ist das an 8.5.5.9 anschließende Fixpack. Ab 16.0.0.2 werden alle berechtigten optionalen Liberty-Features, die für diese Pläne unterstützt werden, standardmäßig installiert.
* Es wurden [schwerwiegende Sicherheitslücken](http://www-01.ibm.com/support/docview.wss?uid=swg21984977){: new_window} adressiert, die sich auf WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} auswirken; dazu gehören die folgenden:
  * Eine XXE-Sicherheitslücke (XML External Entity Injection) in den Apache Standard Taglibs, die sich auf IBM WebSphere Application Server auswirkt.
  * Ein Potenzial für die Weaker-than-expected-Sicherheit bei der Verwendung des API-Erkennungsfeatures und der Swagger-Dokumente von WebSphere Application Server Liberty Profile.
  * Eine potenzielle Sicherheitslücke bei der Weitergabe von Informationen im Admin Center für IBM WebSphere Application Server Liberty.
  * Eine potenzielle Sicherheitslücke für das Splitting von HTTP-Antworten in IBM WebSphere Application Server.
  * OpenSSL-Sicherheitslücken, die am 03. Mai 2016 vom OpenSSL-Projekt offengelegt wurden.

## 13. Juni 2016: WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} aktualisiert

* Clients können nun mithilfe einer Anwendung oder eines Scripts, die bzw. das REST-konforme APIs von WebSphere Application Server for Bluemix nutzt, VM-Instanzen erstellen, bereitstellen, verwalten und löschen.
* Eine Funktion wurde hinzugefügt, die es einem Client ermöglicht, über eine feste Anzahl von Instanzen im Status GESTOPPT mit maximal 10 IP-Adressen oder 64 GB Speicherplatz zu verfügen. Für Clients werden nun Gebühren für die Summe von Instanzen im Status GESTOPPT mit einer reduzierten Rate von 5 % berechnet.

## 26. April 2016: WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} aktualisiert

* Es wurden [potenzielle Sicherheitslücken](http://www-01.ibm.com/support/docview.wss?uid=swg21982128){: new_window} in WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} bei aktiviertem FIPS 140-2 sowie eine Reihe von Sicherheitslücken in Samba - einschließlich Badlock - behoben.
* Verschiedene Funktionen für die Servicewartung wurden integriert.

## 15. April 2016: WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} aktualisiert

* Die Binärdateien von WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} wurden von Version 8.5.5.8 auf Version 8.5.5.9 aktualisiert.
* Es wurde eine Sicherheitslücke des Typs [Cross-Site Scripting](http://www-01.ibm.com/support/docview.wss?uid=swg21981221){: new_window} in Liberty for Java for IBM {{site.data.keyword.Bluemix_notm}} behoben, die sich auf Nutzer auswirkt, die den OIDC-Client (OpenID Connect) verwenden.
* Verschiedene Funktionen für die Servicewartung wurden integriert.

## 19. Februar 2016: WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} aktualisiert
* Es wurde eine Option für Kunden mit speicherintensiven Anwendungen hinzugefügt, um ihrer Umgebung durch größere virtuelle Maschinen zur richtigen Größe zu verhelfen. Kunden können die jeweilige Ressourcengröße einer angegebenen WebSphere Application Server-Komponente ode eines einzelnen Systems bis zu 32 GB RAM VM auswählen.
* Die Binärdateien von WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} wurden von Version 8.5.5.7 auf Version 8.5.5.8 aktualisiert.
* Es wurden mehrere Sicherheitslücken in der IBM SDK Java Technology Edition behoben, die sich auf WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} auswirken und die allgemein als [SLOTH](http://www-01.ibm.com/support/docview.wss?uid=swg21977244){: new_window} bezeichnet werden.
* Es wurde eine Sicherheitslücke des Typs [Cross-Site Scripting](http://www-01.ibm.com/support/docview.wss?uid=swg21976337){: new_window} behoben, die sich auf Nutzer der OAuth-Providerausgabe auswirkt.
* Verschiedene Funktionen für die Servicewartung wurden integriert.

## 11. Dezember 2015: WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} aktualisiert
* Der offizielle Produktname wurde von IBM Application Server on Cloud for {{site.data.keyword.Bluemix_notm}} in IBM WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} geändert.
* Dem WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} Network Deployment-Plan wurden neue Funktionen hinzugefügt. Der Plan besteht aus einer WebSphere Application Server Network Deployment-Zellenumgebung mit mindestens zwei virtuellen Maschinen. Mit diesen neuen Funktionen können Benutzer eine Clusterumgebung für hohe Verfügbarkeit, Funktionsübernahme und Skalierbarkeit konfigurieren.
* Dem WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} Liberty Core-Plan wurden neue Funktionen hinzugefügt. Der Plan umfasst die Verwendung eines Liberty-Verbunds. Dabei handelt es sich um eine Verwaltungsdomäne für eine Gruppe von Liberty-Profilen (Servern), die aus mindestens zwei virtuellen Maschinen besteht.
* Die Binärdateien von WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} wurden von Version 8.5.5.6 auf Version 8.5.5.7 aktualisiert.
* Eine [Apache Commons Collections-Sicherheitslücke](https://www.us-cert.gov/ncas/current-activity/2015/11/13/Apache-Commons-Collections-Java-Library-Vulnerability){: new_window} für die Verarbeitung der Java-Objekt-Deserialisierung wurde behoben.
* Eine Sicherheitslücke, über die ein [HTTP Response Splitting-Angriff](http://www-01.ibm.com/support/docview.wss?uid=swg21972254){: new_window} möglich war, wurde behoben.
* Verschiedene Funktionen für die Servicewartung wurden integriert.

## 15. Oktober 2015: Application Server on Cloud aktualisiert
* Die beiden folgenden neuen Pläne wurden hinzugefügt:
  * [Klassische WebSphere Application Server Version 9 Beta](https://www-01.ibm.com/marketing/iwm/iwmdocs/web/cc/earlyprograms/websphere.shtml){: new_window}
  * WebSphere Application Server ND
* Verschiedene Maßnahmen zur Servicewartung
