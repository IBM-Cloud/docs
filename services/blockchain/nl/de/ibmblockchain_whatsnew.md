---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-16"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Neuerungen
{: #whatsnew}

Der **HSBN vNext Beta**-Plan basiert auf einer stabilen Festschreibung der Open-Source-Codebasis von [Hyperledger Fabric v1.0](https://www.hyperledger.org/){:new_window}. Hyperledger Fabric v1.0 implementiert eine modulare Architektur, die eine ausfallsichere, sichere und anpassbare Plattform für das Erstellen von Blockchain-Netzen für Unternehmen bereitstellt.  
{: shortdesc}

Der **HSBN vNext Beta**-Service ist mehr als eine einfache Sandboxumgebung, indem er ein verteiltes Blockchain-Netz mit Ressourcengruppen bereitstellt, die sich über verschiedene Bluemix-Organisationen erstrecken. Weitere Informationen zur Netzarchitektur finden Sie im Abschnitt [Übersicht](v10_netoverview.html).

## Neue Architektur in Version 1.0
{:why}

Die Hyperledger Fabric-Architektur zeigt sich in Version 1.0 deutlich verbessert und unterstützt nun auf Unternehmen abgestimmte Netze, deren Fokus auf Sicherheit, Skalierbarkeit, Vertraulichkeit und Leistung liegt. Peers sind in zwei verschiedene Laufzeiten aufgeteilt - **zulassend** und **festschreibend** - und die Zuständigkeit für die Anordnung von Transaktionen wird in eine separate Komponente verlegt. Möglichen Bedenken bezüglich des Datenschutzes und der Vertraulichkeit wird durch Kanäle entgegengewirkt, mit denen eine Trennung von Daten ermöglicht wird. Konten existieren auf Pro-Konto-Basis; Netze können daher so angepasst werden, dass sie verschiedene Kombinationen bilateraler, multilateraler oder sogar öffentlicher Transaktionen unterstützen.

Nähere Informationen zur Netztopologie und Interaktion finden Sie in der detaillierten Veröffentlichung zur [Hyperledger-Architektur](http://hyperledgerdocs.readthedocs.io/en/latest/arch-deep-dive.html){: new_window}.

## Zusätzliche Änderungen

Der HSBN vNext Beta-Plan umfasst zudem die folgenden Änderungen:
* Über das [neue Dashboard](v10_dashboard.html) können Subskribenten ein Blockchain-Netz erstellen, Mitglieder einladen, einem anderen Netz beitreten und Ressourcen und Assets verwalten.
* Mit der [neuen Marbles-Chaincode-Beispielanwendung für v1.0](https://github.com/hyperledger/fabric/blob/master/examples/chaincode/go/marbles02/marbles_chaincode.go){: new_window} können Tests mit der aktuellen Codebasis durchgeführt werden.
* Der neue [Transaktionsablauf](http://hyperledger-fabric.readthedocs.io/en/latest/txflow.html) in Hyperledger Fabric v1.0 sorgt für Datenkonsistenz und -integrität durch die Implementierung von Prüfpunkten im gesamten Transaktionsprozess.
