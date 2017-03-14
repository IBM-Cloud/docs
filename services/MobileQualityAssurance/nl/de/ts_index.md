---

copyright:
  years: 2012, 2017
  
lastupdated: "2017-01-25"  

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 



# Fehlerbehebung für {{site.data.keyword.mqa}} 
{: #tsmqa}
Hier finden Sie die Antworten auf einige häufig gestellte Fragen zur Verwendung von {{site.data.keyword.mqa}}.{:shortdesc}

## JavaScript-Hybrid-Build schlägt fehl
{: #ts_js_build_fail}

Der Build Ihrer JavaScript-Hybridanwendung {{site.data.keyword.mqa}} schlägt fehl, obwohl die JavaScript&tm; Hybrid SDK for IBM MobileFirst Platform Foundation-Komponente in die App integriert ist und der erforderliche Code hinzugefügt wurde.


Wenn Sie versuchen, den Build für Ihre {{site.data.keyword.mqa}}-Anwendung auszuführen, schlägt dieser fehl.
{: tsSymptoms notoc} 


1. Die Android- und iOS-plattformspezifischen Hybrid SDK-Komponenten sind in dem Projekt nicht installiert.
2. Die installierten Android- und iOS-plattformspezifischen Hybrid SDK-Komponenten sind mit der installierten JavaScript-SDK-Komponente nicht kompatibel.
3. Das native Android SDK und/oder das native iOS SDK sind zwar installiert, doch die Android- und iOS-plattformspezifischen Hybrid SDK-Komponenten sind nicht installiert.
{: tsCauses notoc} 
 

Einige Vorschläge für die Lösung dieses Problems umfassen die folgenden Schritte:
{: tsResolve notoc}
  1.  Stellen Sie sicher, dass Sie alle erforderlichen Android- und iOS-plattformspezifischen Hybrid SDK-Komponenten und alle erforderlichen nativen Android SDKs oder iOS SDKs für die Plattformen installiert haben, die Ihre App unterstützt. 
  2. Stellen Sie sicher, dass Ihre Android- und iOS-plattformspezifischen Hybrid SDK-Komponenten dieselbe übergeordnete Versionsnummer aufweisen wie die JavaScript-Komponente bzw. höher, bis zur nächsten übergeordneten Version. In der folgenden Tabelle sind Beispiele enthalten:
  
| JavaScript-Komponentenversion | Plattformspezifische Komponentenversion | Kompatibel? |
|---------: |------------: |------------: |
| 1.2.3 | 1.2.3 | Ja |
| 1.2.3 | 1.2.1 | Nein |
| 1.2.3 | 1.3.2 | Ja |
| 1.2.3 | 2.0.0 | Nein |

  3. Stellen Sie sicher, dass Sie die Android- und iOS-plattformspezifischen Hybrid SDK-Komponenten installiert haben. Das native Android SDK und das native iOS SDK sind erforderlich, wenn Ihre App auf einer dieser Plattformen ausgeführt wird; für die Hybridanwendungen müssen die Android- und iOS-plattformspezifischen Hybrid SDK-Komponenten ebenfalls für die jeweilige Plattform installiert sein.

  
## Öffnen der Stimmungsanalyse oder Verteilen von Test-Apps nicht möglich
{: #ts_sent_fail}

Sie können die Stimmungsanalyse nicht öffnen oder Ihre Test-App nicht verteilen.

Sie können die Stimmungsanalyse nicht öffnen oder Ihre Test-App nicht verteilen, weil Ihr Browser Popup-Fenster blockiert.
{: tsSymptoms notoc} 

Mobile Quality Assurance nutzt Popup-Fenster und Cookies für die Kommunikation mit dem Mobile Quality Assurance-Server.
{: tsCauses notoc}


Für die Einrichtung einer Kommunikation zwischen Mobile Quality Assurance und dem Mobile Quality Assurance-Server müssen Sie möglicherweise Ihre Browsereinstellungen so konfigurieren, dass Popup-Fenster und Cookies zulässig sind. Beispiel: Wenn Sie in der Benutzerschnittstelle auf eine Option klicken, z. B. Stimmungsscore, verhindert dies möglicherweise die Kommunikation zwischen Mobile Quality Assurance und dem Server. Die Stimmungsanalyse kann nicht angezeigt werden, wenn Popup-Fenster und Cookies blockiert sind. Weitere Informationen zur Konfiguration Ihrer Browsereinstellungen finden Sie in der Dokumentation Ihres jeweiligen Browsers.
{: tsResolve notoc}


## Abgelaufene Anwendung kann nicht ausgeführt werden
{: #ts_app_expired}

Sie können Ihre Mobile Quality Assurance-Anwendung nicht ausführen.

Wenn Sie versuchen, Ihre Mobile Quality Assurance-Anwendung auszuführen, wird die folgende Nachricht angezeigt: Your application has expired and cannot be run at this time.
{: tsSymptoms notoc} 

Ihre Anwendung ist auf der Mobile Quality Assurance-Seite mit den Builds als inaktiviert markiert.
{: tsCauses notoc}


Prüfen Sie die Mobile Quality Assurance-Seite mit den Builds, um sicherzustellen, dass keine Anwendung als inaktiviert markiert ist. In der Regel sind Anwendungen als inaktiviert markiert, um Tester darüber zu informieren (über die Anwendung selbst), keine bestimmte Version des Builds zu verwenden. Weitere Informationen zu den Einstellungen auf der Mobile Quality Assurance-Seite mit den Builds finden Sie im Thema zur Verwaltung von Builds im IBM Knowledge Center.
{: tsResolve notoc}

