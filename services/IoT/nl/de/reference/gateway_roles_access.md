---

copyright:
  years: 2016, 2017
lastupdated: "2016-10-16"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Zugriffsebenen für Gateway-Rollen

Die folgende Tabelle zeigt die Zugriffsebenen der einzelnen Gateway-Rollen.

Die Tabellen zeigen Zugriffsebenen für:
- [Geräteoperationen](#gateway-device-ops)
- [Protokolloperationen](#gateway-log-ops)
- [Cacheoperationen](#gateway-cache-ops)
<!-- [Historian Operations](#gateway-historian) -->
- [Organisationsoperationen](#gateway-org-ops)
- [Zugriffssteuerungsoperationen](#gateway-access-ops)
- [Analyseoperationen](#gateway-analytics-ops)
- [Operationen von Drittanbietern](#gateway-third-party)  
<!-- - [Risk Management Operations](#gateway-risk-mgt) -->

## Gateway-Rollen
{: #gateway-roles}

### Geräteoperationen {: #gateway-device-ops}

Geräteoperationen || Gateway-Rollen|
:--------: | ---------------------|------------------------
           | **Standardgateway** | **Privilegiertes Gateway**
Geräte erstellen, aktualisieren oder löschen|-|X
Geräte anzeigen|X|X
Gerät aktivieren|-|X
Ereignis publizieren|X|X
Ereignis subskribieren|-|-
Befehl publizieren|-|-
Befehl subskribieren|X|X
Gerätemanagementaktion initiieren|X|X
Gerätemanagementaktionen anzeigen|X|X
Gerätemanagementaktionen löschen|-|-
DM-Aktionsbundles verwalten|-|X
Gerätetypen erstellen, aktualisieren oder löschen|-|-
Gerätetypen anzeigen|X|X
Diagnoseprotokolle verwalten|-|-
Diagnoseprotokolle anzeigen|-|-

### Protokolloperationen {: #gateway-log-ops}

Protokolloperationen || Gateway-Rollen|
:--------: | ---------------------|------------------------
           | **Standardgateway** | **Priviligiertes Gateway**
Serverprotokolle anzeigen|-|-

### Cacheoperationen {: #gateway-cache-ops}

Cacheoperationen || Gateway-Rollen|
:--------: | ---------------------|------------------------
           | **Standardgateway** | **Priviligiertes Gateway**
Livedaten anzeigen (Ereigniscache)|-|-
Livedaten verwalten (Ereigniscache)|-|-


### Organisationsoperationen {: #gateway-org-ops}

Organisationsoperationen || Gateway-Rollen|
:--------: | ---------------------|------------------------
           | **Standardgateway** | **Privilegiertes Gateway**
Speicherparameter konfigurieren|-|-
Authentifizierungsprovider konfigurieren|-|-
Mailkonfiguration erstellen, anzeigen, aktualisieren oder löschen|-|-
Verfügbare Mail-Provider anzeigen|-|-
Mailvorlagen erstellen, anzeigen, aktualisieren oder löschen|-|-
Benutzer erstellen, aktualisieren oder löschen|-|-
Benutzer anzeigen|-|-
Benutzereinladungen erstellen, aktualisieren, löschen|-|-
Benutzereinladungen anzeigen|-|-
Einladung abschließen|-|-
API-Schlüssel erstellen, aktualisieren oder löschen|-|-
API-Schlüssel anzeigen|-|-
ORG-Nutzungsinformationen anzeigen|-|-

### Zugriffssteuerungsoperationen {: #gateway-access-ops}

Zugriffssteuerungsoperationen || Gateway-Rollen|
:--------: | ---------------------|------------------------
           | **Standardgateway** | **Privilegiertes Gateway**
Benutzereigenschaften (einschl. Zugriffsrechte) anzeigen|-|-
Eigene Eigenschaften des Benutzers anzeigen (einschl. Zugriffsrechte)|-|-
Benutzer verwalten (einschl. Zugriffsrechte)|-|-
Eigenschaften des API-Schlüssels anzeigen (einschl. Zugriffsrechte)|-|-
Eigenschaften des API-Schlüssels anzeigen (einschl. Zugriffsrechte)|-|-
API-Schlüssel erstellen, aktualisieren oder löschen (einschl. Zugriffsrechte)|-|-
Geräteeigenschaften anzeigen (einschl. Zugriffsrechte)|X|X
Eigene Eigenschaften des Geräts anzeigen (einschl. Zugriffsrechte)|X|X
Gerät erstellen, aktualisieren, löschen (einschl. Zugriffsrechte)|-|X
Rollen anzeigen|-|-
Angepasste Rollen erstellen, aktualisieren, löschen|-|-
Operationen anzeigen|-|-

### Analyseoperationen {: #gateway-analytics-ops}

Analyseoperationen || Gateway-Rollen|
:--------: | ---------------------|------------------------|
           | **Standardgateway** | **Privilegiertes Gateway** |
Analyseregeln anzeigen|-|-
Analyseregeln verwalten|-|-
Analyseaktionen anzeigen|-|-
Analyseaktionen verwalten|-|-
Analysealerts anzeigen|-|-
Nachrichtenschemas der Analyse anzeigen|-|-
Nachrichtenschemas der Analyse verwalten|-|-

### Serviceoperationen von Drittanbietern {: #gateway-third-party}

Serviceoperationen von Drittanbietern || Gateway-Rollen|
:--------: | ---------------------|------------------------
           | **Standardgateway** | **Privilegiertes Gateway**
Stapelbenachrichtigungen von einer externen Plattform verarbeiten|-|-
Stapelbenachrichtigungen verarbeiten und an eine externe Plattform senden|-|-
Ereignis für ein Gerät publizieren|-|-
Ereignisse eines Geräts subskribieren|-|-
Callback-URL für die externe Plattform festlegen|-|-
Subskriptionsebene der externen Plattform festlegen|-|-
Allgemeinzustand vom Connector abrufen|-|-
Prüfen, ob ein externes System aktiv ist, und Berechtigungsnachweise validieren|-|-
