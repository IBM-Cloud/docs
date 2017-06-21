---

copyright:
  years: 2017
lastupdated: "2017-05-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Informationen
{: #about}

{{site.data.keyword.bplong}} kann verwendet werden, um Infrastruktur-Bausteine zu erstellen. Sie können {{site.data.keyword.IBM_notm}} Cloud-Services zusammenstellen, um eine Infrastruktur zu erstellen, die bereitgestellt und wiederverwendet werden kann.{:shortdesc}

{{site.data.keyword.bpshort}} verwendet Terraform, um die Infrastrukturverwaltung zu vereinfachen. Wenn Sie z. B. möchten, dass mehrere Kopien Ihres Service, der einen Cluster von App-Servern, eine Lastausgleichsfunktion und einen Datenbankserver verwendet, den Betrieb aufnehmen, müssen Sie möglicherweise ein Bash-Script schreiben, um Befehle ausführen und diese Komponenten in Betrieb zu nehmen. Es ist jedoch einfacher, schneller und geordneter, eine Konfiguration mit einer Ausführungskomponente zu haben, die die Konfiguration in echte Ressourcen umwandelt. Mit Terraform können mehrere Ressourcen zur gleichen Zeit den Betrieb aufnehmen, als kollektive Gruppe, innerhalb derer Abhängigkeiten zugeordnet sind. 

## Gründe für die Verwendung von {{site.data.keyword.bpshort}}
{: #reasons}

Möglicherweise möchten Sie eine codifizierte Infrastruktur in den folgenden Szenarios verwenden:
{:shortdesc}

| Szenario     | Gründe    |
| :------------- | :------------- |
| Sie möchten Ihre Infrastruktur neu erstellen und wiederverwenden.  | Sie können {{site.data.keyword.bpshort}} für die Infrastrukturverwaltung verwenden. Mit {{site.data.keyword.bpshort}} können Sie Ihre Ressourcen programmgesteuert bereitstellen, ändern und vernichten. Wenn Sie Ressourcen codifizieren und konfigurieren, können Sie eine Bibliothek von Ressourcen aufbauen, die immer wieder verwendet werden kann, um dieselben Ergebnisse zu verknüpfen.|
| Sie wünschen Transparenz hinsichtlich der Einrichtung Ihrer Umgebung.  | {{site.data.keyword.bpshort}} arbeitet mit den Konfigurationen in der Quellcodeverwaltung, die Zusammenarbeit und Überprüfung ermöglicht und Ihnen ein Prüfprotokoll bietet, um zu sehen, wie und wann Änderungen vorgenommen wurden. Sie können Ihre Änderungen auch anzeigen, wenn Sie ein Rollback auf eine vorherige Konfiguration durchführen müssen. |
| Sie möchten die Ausführung von Umgebungsänderungen vereinfachen.  | {{site.data.keyword.bpshort}} befolgt das deklarative Modell, das eine Single Source of Truth bereitstellt. Wenn Sie eine Änderung an Ihrer Umgebung planen, geben Sie das gewünschte Ergebnis an. |
| Sie verwenden bereits ein Configuration Management (CM-) Tool, aber Sie wünschen eine stärker automatisierte Methode zur Einrichtung Ihrer Umgebungen. | {{site.data.keyword.bpshort}} kann mit CM-Tools zusammenarbeiten. Umgebungen, die mit {{site.data.keyword.bpshort}} bereitgestellt werden, sind allgemeine Abstraktionen, die Infrastrukturressourcen erstellen können. Anschließend können Sie CM-Tools verwenden, um Software auf den Ressourcen, die von {{site.data.keyword.bpshort}} bereitgestellt werden, zu installieren und zu konfigurieren.  
  
## Funktionsweise
{: #how}

Sie können Ressourcen für Ihre Umgebungen bereitstellen, indem Sie {{site.data.keyword.bpshort}} verwenden.
{:shortdesc}

{{site.data.keyword.bpshort}} verwendet Terraform als zugrunde liegendes Tool, um Infrastruktur als Code zu aktivieren, sodass Sie {{site.data.keyword.IBM}} Cloud-Ressourcen als Code definieren können. Cloudressourcen können verschiedene Komponenten Ihrer Infrastruktur sein, wie z. B. Bare-Metal-Server, virtuelle Server, Lastausgleichsfunktionen oder Software-definierte Netzkomponenten. 

### Konfigurationen zum Definieren zum Ressourcen
{: #how-define}

Eine Konfiguration oder Terraform-Konfiguration ist eine Datei, die definiert, welche Ressourcen Ihre Infrastruktur bilden. Konfigurationen sind implementierbare Architekturen, die auf eine oder mehrere Umgebungen angewendet werden können. Das folgende Diagramm zeigt, woraus sich eine Konfiguration zusammensetzt und wie die Teile zusammen eine bereitstellbare Umgebung in {{site.data.keyword.bpshort}} erstellen.


![{{site.data.keyword.bpshort}}-Architekturdiagramm](/images/anatomy_of_a_schematic.png)

Abbildung 1. {{site.data.keyword.bpshort}}-Architekturdiagramm

### Quellcodeverwaltung zur Ermöglichung der Zusammenarbeit
{: #how-collaborate}

Konfigurationen sind in GitHub gespeichert, sodass Teams den Code überprüfen und zusammenarbeiten können. Mit GitHub verfügen Sie über ein integriertes Auditprotokoll und können einen vollständigen Festschreibungsverlauf der Änderungen anzeigen, die an Ihren Konfigurationen vorgenommen werden. Sie können Nutzungsinformationen in Readme-Dateien speichern, um die Konfiguration gemeinsam nutzbar und für mehrere Teams verwendbar zu machen.

### {{site.data.keyword.bpshort}}-Umgebungen zur Bereitstellung von Ressourcen
{: #how-provision}

Sie können {{site.data.keyword.bpshort}} verwenden, um Ihren Code in GitHub durchsuchen und Ressourcen in einer Umgebung bereitstellen zu können. Umgebungen können allgemeine Konfigurationen gemeinsam nutzen. Sie können beispielsweise eine temporäre QA-Umgebung, die wie eine Produktionsumgebung aussieht, in Betrieb nehmen und sie zerstören, wenn die Tests beendet sind. Sie können eine Bibliothek der allgemeinen Umgebungskonfigurationen erstellen, die mit Tags versehen und von allen Benutzern in Ihrem {{site.data.keyword.Bluemix_notm}} -Konto durchsucht werden können.
