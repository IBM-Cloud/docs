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

# Zugriffsebenen für Anwendungsrollen

Die folgende Tabelle zeigt die Zugriffsebenen der einzelnen Anwendungsrollen.

Die Tabellen zeigen Zugriffsebenen für:
- [Geräteoperationen](#app-device-ops)
- [Protokolloperationen](#app-log-ops)
- [Cacheoperationen](#app-cache-ops)
<!-- [Historian Operations](#app-historian) -->
- [Organisationsoperationen](#app-org-ops)
- [Zugriffssteuerungsoperationen](#app-access-ops)
- [Analyseoperationen](#app-analytics-ops)
- [Operationen von Drittanbietern](#app-third-party)  
<!-- - [Risk Management Operations](#app-risk-mgt) -->

## Anwendungsrollen
{: #app-roles}

### Geräteoperationen {: #app-device-ops}

Geräteoperationen ||| Anwendungsrollen||||
:--------: | -------------|-------------|---------------|-----|---
           | **Standardanwendung** | **Operationsanwendung** | **Vertrauenswürdige Backend-Anwendung** | **Datenprozessoranwendung** | **Visualisierungsanwendung** | **Geräteanwendung**
Geräte erstellen, aktualisieren oder löschen|X|X|X|-|-|-
Geräte anzeigen|X|X|X|X|X|-
Gerät aktivieren|X|X|X|-|-|-
Ereignis publizieren|X|-|X|-|-|X
Ereignis subskribieren|X|X|X|X|X|X
Befehl publizieren|X|X|X|X|-|-
Befehl subskribieren|X|-|X|-|-|X
Gerätemanagementaktion initiieren|X|X|-|-|-|-
Gerätemanagementaktionen anzeigen|X|X|-|-|-|X
Gerätemanagementaktionen löschen|X|X|-|-|-|-
DM-Aktionsbundles verwalten|X|X|-|-|-|-
Gerätetypen erstellen, aktualisieren oder löschen|X|X|X|-|-|-
Gerätetypen anzeigen|X|X|X|X|-|-
Diagnoseprotokolle verwalten|X|X|-|-|-|X
Diagnoseprotokolle anzeigen|X|X|X|-|-|-

### Protokolloperationen {: #app-log-ops}

Protokolloperationen ||| Anwendungsrollen||||
:--------: | -------------|-------------|---------------|-----|---
           | **Standardanwendung** | **Operationsanwendung** | **Vertrauenswürdige Backend-Anwendung** | **Datenprozessoranwendung** | **Visualisierungsanwendung** | **Geräteanwendung**
Serverprotokolle anzeigen|X|X|X|-|-|-

### Cacheoperationen {: #app-cache-ops}

Cacheoperationen ||| Anwendungsrollen||||
:--------: | -------------|-------------|---------------|-----|---
           | **Standardanwendung** | **Operationsanwendung** | **Vertrauenswürdige Backend-Anwendung** | **Datenprozessoranwendung** | **Visualisierungsanwendung** | **Geräteanwendung**
Livedaten anzeigen (Ereigniscache)|X|X|X|X|X|X
Livedaten verwalten (Ereigniscache)|X|X|X|X|X|X

### Organisationsoperationen {: #app-org-ops}

Organisationsoperationen ||| Anwendungsrollen||||
:--------: | -------------|-------------|---------------|-----|---
           | **Standardanwendung** | **Operationsanwendung** | **Vertrauenswürdige Backend-Anwendung** | **Datenprozessoranwendung** | **Visualisierungsanwendung** | **Geräteanwendung**
Speicherparameter konfigurieren|-|-|-|-|-|-
Authentifizierungsprovider konfigurieren|-|-|-|-|-|-
Mailkonfiguration erstellen, anzeigen, aktualisieren oder löschen|-|-|-|-|-|-
Verfügbare Mail-Provider anzeigen|X|X|-|-|-|-
Mailvorlagen erstellen, anzeigen, aktualisieren oder löschen|X|X|-|-|-|-
Benutzer erstellen, aktualisieren oder löschen|-|X|-|-|-|-
Benutzer anzeigen|X|X|-|-|-|-
Benutzereinladungen erstellen, aktualisieren oder löschen|-|X|-|-|-|-
Benutzereinladungen anzeigen|X|X|-|-|-|-
Einladung abschließen|X|X|-|-|-|-
API-Schlüssel erstellen, aktualisieren oder löschen|-|X|-|-|-|-
API-Schlüssel anzeigen|X|X|-|-|-|-
ORG-Nutzungsinformationen anzeigen|X|X|-|-|-|-

### Zugriffssteuerungsoperationen {: #app-access-ops}

Zugriffssteuerungsoperationen ||| Anwendungsrollen||||
:--------: | -------------|-------------|---------------|-----|---
           | **Standardanwendung** | **Operationsanwendung** | **Vertrauenswürdige Backend-Anwendung** | **Datenprozessoranwendung** | **Visualisierungsanwendung** | **Geräteanwendung**
Benutzereigenschaften einschließlich Zugriffsrechte anzeigen|X|X|-|-|-|-
Eigene Eigenschaften des Benutzers einschließlich Zugriffsrechte anzeigen|-|-|-|-|-|-
Benutzer einschließlich Zugriffsrechte verwalten|-|X|-|-|-|-
Eigenschaften des API-Schlüssel einschließlich Zugriffsrechte anzeigen|X|X|-|-|-|-
Eigene Eigenschaften des API-Schlüssels einschließlich Zugriffsrechte anzeigen|X|X|X|X|X|X
API-Schlüssel einschließlich Zugriffsrechte erstellen, aktualisieren, löschen|-|X|-|-|-|-
Geräteeigenschaften einschließlich Zugriffsrechte anzeigen|X|X|X|X|X|-
Eigene Eigenschaften des Geräts einschließlich Zugriffsrechte anzeigen|-|-|-|-|-|-
Geräte einschließlich Zugriffsrechte erstellen, aktualisiere, löschen|X|X|X|-|-|-
Rollen anzeigen|X|X|-|-|-|-
Angepasste Rollen erstellen, aktualisieren, löschen|-|X|-|-|-|-
Operationen anzeigen*|X|X|-|-|-|-

### Analyseoperationen {: #app-analytics-ops}

Analyseoperationen ||| Anwendungsrollen||||
:--------: | -------------|-------------|---------------|-----|---
           | **Standardanwendung** | **Operationsanwendung** | **Vertrauenswürdige Backend-Anwendung** | **Datenprozessoranwendung** | **Visualisierungsanwendung** | **Geräteanwendung**
Analyseregeln anzeigen|X|X|-|X|X|-
Analyseregeln verwalten|X|X|-|X|-|-
Analyseaktionen anzeigen|X|X|-|X|X|-
Analyseaktionen verwalten|X|X|-|X|X|-
Analysealerts anzeigen|X|X|-|X|X|X
Nachrichtenschemas der Analyse anzeigen|X|X|-|X|X|-
Nachrichtenschemas der Analyse verwalten|X|X|-|X|-|-

### Serviceoperationen von Drittanbietern {: #app-third-party}

Serviceoperationen von Drittanbietern ||| Anwendungsrollen||||
:--------: | -------------|-------------|---------------|-----|---
           | **Standardanwendung** | **Operationsanwendung** | **Vertrauenswürdige Backend-Anwendung** | **Datenprozessoranwendung** | **Visualisierungsanwendung** | **Geräteanwendung**
Stapelbenachrichtigungen von einer externen Plattform verarbeiten|X|X|-|-|-|-
Stapelbenachrichtigungen verarbeiten und an eine externe Plattform senden|X|X|-|-|-|-
Ereignis für ein Gerät publizieren|X|X|-|-|-|-
Ereignisse eines Geräts subskribieren|X|X|-|-|-|-
Callback-URL für die externe Plattform festlegen|X|X|-|-|X|-
Subskriptionsebene der externen Plattform festlegen|X|X|-|-|X|-
Allgemeinzustand vom Connector abrufen|X|X|X|-|X|-
Prüfen, ob ein externes System aktiv ist, und Berechtigungsnachweise validieren|X|X|X|-|X|-
