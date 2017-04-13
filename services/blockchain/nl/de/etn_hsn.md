---

copyright:
  years: 2016, 2017
lastupdated: "2016-10-13"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Unternehmensnetz mit hohem Sicherheitsniveau
{: #etn_overview}


Das Unternehmensnetz mit hohem Sicherheitsniveau von IBM Blockchain wird in einer isolierten und hoch sicheren Umgebung ausgeführt und unterscheidet sich so von anderen in einer Cloud gehosteten Angeboten. Das Betriebssystem, die Struktur und alle Knoten befinden sich in einem IBM Secure Service Container; dies garantiert das Sicherheitsniveau und die Unüberwindbarkeit, die Unternehmenskunden inzwischen von der z Systems-Technologie erwarten.  Von IBM Secure Service Container wird auch die Leistungsoptimierung für die Peer-to-Peer-Kommunikation, Verfügbarkeit, Skalierbarkeit, Hardwareverschlüsselung, manipulationssichere Verschlüsselungsschlüssel und sicher verschlüsselte virtuelle Maschinen bereitgestellt.  
{:shortdesc}

Die Umgebung (LinuxONE on z) besteht aus einem Netzwerk mit vier Peers, in dem PBFT mit den Mitgliedschaftsservices implementiert ist und ein Anwendungscontainer ausgeführt wird.  Vom Anwendungscontainer werden die Blockchain-Software, der Chaincode und die im System aktiven Daten geschützt. Die Blockchain-Software im sicheren Bootbereich kann signiert, zertifiziert und verschlüsselt werden; sobald sie im Anwendungscontainer installiert ist, kann sie nicht manipuliert werden.  Rootbenutzer der Plattform und Systemadministratoren können nicht auf sicheren Containerinhalt zugreifen und diesen auch nicht anzeigen.  LinuxONE on z bietet FIPS-Konformität, hohen EAL-Schutz (EAL - Evaluation Assurance Level), eine sehr gut überprüfbare Betriebsumgebung und eine Optimierung der Verschlüsselung.

Weitere Details zu den Sicherheitsfunktionen finden Sie im Abschnitt [IBM Secure Service Container](etn_ssc.html).
