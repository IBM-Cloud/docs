---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Analyse des Streckenverlaufsmusters verwalten
{: #tp_iotdriverinsights_admin}

Letzte Aktualisierung: 22. Juli 2016
{: .last-updated}

Verwenden Sie zur Verwaltung des Service zur Analyse des Streckenverlaufsmusters die Administrationskonsole im {{site.data.keyword.Bluemix_notm}}-Dashboard. Über die Administrationskonsole können Sie Parameter für die Analyse des Streckenverlaufsmusters konfigurieren und die im Service gespeicherten Daten verwalten. Außerdem können Sie die Tenantinformationen anzeigen und das Tenantkennwort zurücksetzen.

{:shortdesc}

## Administrationskonsole starten
{: #start-admin-console}

Gehen Sie wie folgt vor, um auf die Administrationskonsole für den Service zur Analyse des Streckenverlaufsmusters von {{site.data.keyword.iotdriverinsights_full}} zuzugreifen: 

1. Klicken Sie im {{site.data.keyword.Bluemix_notm}}-Dashboard auf die Kachel für den {{site.data.keyword.iotdriverinsights_short}}-Service. 
2. Wählen Sie die Ansicht **Verwalten** Ihrer Serviceinstanz aus. Notieren Sie die Berechtigungsnachweise aus Benutzername und Kennwort, die Sie zu einen späteren Zeitpunkt benötigen. Für den Zugriff auf die Administrationskonsole benötigen Sie Ihre IBM ID, die unter Umständen nicht mit den Berechtigungsnachweisen für {{site.data.keyword.Bluemix_notm}} identisch ist. 
3. Klicken Sie auf **Starten** und geben Sie bei der entsprechenden Eingabeaufforderung die Berechtigungsnachweise für Ihre IBM ID ein. 
4. Klicken Sie auf **Anmelden**. Das Fenster **Administrationskonsole** wird geöffnet. 


## Tenantinformationen verwalten
{: #viewtenantinfo}

Klicken Sie zum Anzeigen der Tenantinformationen auf **Tenantinformationen**. 

### Tenantkennwort zurücksetzen
{: #resettenantpassword}

Gehen Sie wie folgt vor, um das Tenantkennwort zurückzusetzen: 

1. Klicken Sie im Fenster **Tenantinformationen** auf **Zurücksetzen**.
2. Klicken Sie im Bestätigungsdialogfenster auf **OK**. Ein neues Kennwort wird generiert und in der Ansicht **Tenantinformationen** angezeigt.
**Wichtig:** Stellen Sie sicher, dass Sie das Kennwort in allen Anwendungen aktualisieren, die auf die {{site.data.keyword.iotdriverinsights_short}}-API zugreifen. 

## Serviceparameter konfigurieren
{: #configureparameters}

Serviceparameter steuern, wie die Fahrtdaten analysiert werden. Gehen Sie wie folgt vor, um die Parameter des Service für die Analyse des Streckenverlaufsmusters zu ändern: 

1. Öffnen Sie die Ansicht **Parameter**. 
2. Klicken Sie auf die Registerkarte **Parameter für Streckenverlaufsmuster** und aktualisieren Sie die [Parameter für die Analyse des Streckenverlaufsmusters](#tp_parameters), sodass sie Ihren Anforderungen entsprechen. 
3. Klicken Sie auf **Speichern**.
4. Klicken Sie auf **OK**. 

Die aktualisierten Parameterwerte werden auf den nächsten Job angewendet, der übergeben wird. 

### Schwellenwertparameter für Relevanz

In der folgenden Tabelle werden die Schwellenwertparameter für die Relevanz beschrieben, die Sie auf der Registerkarte **Parameter für Streckenverlaufsmuster** konfigurieren können. 

|Parametername|Beschreibung|Standardwert|
|:--------|:--------|:-------|
|Minimale Relevanz der Anzahl Fahrten für S/Z|Die minimale absolute Relevanz der Anzahl Fahrten, die für ein S/Z-Muster (Start/Ziel) erforderlich sind.|4 (muss größer als Null sein)|
|Minimale Relevanz der Anzahl Fahrten für Route|Die minimale absolute Relevanz der Anzahl Fahrten, die für ein Routenmuster erforderlich sind.|2 (muss größer als Null sein)|

## Ergebnisdaten verwalten
{: #managedata}

Die vom Service zur Analyse des Streckenverlaufsmusters generierten Ergebnisdaten bleiben im System gespeichert, bis sie gelöscht werden. 

Gehen Sie wie folgt vor, um die Ergebnisdaten zu löschen: 

1. Klicken Sie auf **Data Management** > **Ergebnis des Streckenverlaufsmusters**. Die Ergebnisdaten werden angezeigt. 
2. Wählen Sie einen Datensatz aus und klicken Sie dann auf **Löschen**.
