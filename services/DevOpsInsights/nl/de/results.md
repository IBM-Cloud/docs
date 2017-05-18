---

copyright:
  years: 2016, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Ergebnisse anzeigen

## Deployment Risk-Bewertungen

Nach der Pipeline-Ausführung beginnt {{site.data.keyword.DRA_short}} für die Erstellung einer Baseline mit der Erfassung und Analyse der Testergebnisse aus der Pipeline. Es werden Daten aus allen nachfolgenden Ausführungen erfasst und mit den vorherigen Ergebnissen verglichen. In Entscheidungsgates werden diese Daten verwendet, um zu bestimmen, wann eine Bereitstellung gestoppt werden soll. 

Sie können sich Ihre Bereitstellung und Gatebewertungsdaten im Deployment Risk-Dashboard ansehen. Öffnen Sie zum Aufrufen des Dashboards {{site.data.keyword.DRA_short}} und klicken Sie im seitlichen Menü auf **Deployment Risk**. 

Wenn Sie eine {{site.data.keyword.contdelivery_short}}-Pipeline verwenden, können Sie einzelne Berichte zur Gateausführung über die Pipeline selbst anzeigen. Führen Sie die folgenden Schritte aus, um den Entscheidungsbericht für ein Gate aus der Pipeline anzuzeigen:

1. Klicken Sie bei der Stufe mit dem zu überprüfenden Gate auf die Option zum Anzeigen von Protokollen und Verlauf.

2. Klicken Sie im Job, der das Gate enthält, auf den Namen des Gates. 

3. Suchen Sie in der Protokollansicht nach der Nachricht `Check {{site.data.keyword.DRA_short}} report here` und klicken Sie auf den Link, um den Bericht zu öffnen. 

## Developer Insights- und Team Dynamics-Berichte

Nach einem anfänglichen Zeitraum des Data-Minings können Sie Dashboards über Ihr Team und Ihren Code anzeigen. Klicken Sie im Navigationsmenü des Service auf **Developer Insights** oder **Team Dynamics** und wählen Sie anschließend eine Datenkategorie zum Anzeigen dieser Informationen aus. 
