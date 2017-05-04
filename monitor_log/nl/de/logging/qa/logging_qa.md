---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-07"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Häufige Fragen und Antworten
{: #logging_qa}

In diesem Abschnitt finden Sie die Antworten auf häufige Fragen zu Protokollfunktionen von {{site.data.keyword.Bluemix}}.
{:shortdesc}

* [Was kann ich tun, wenn keine Daten auf der Seite 'Discover' in Kibana angezeigt werden?](logging_qa.html#logging_qa_no_data_discover_kibana)

* [Was kann ich tun, wenn eine Authentifizierungsausnahmebedingung auftritt?](logging_qa.html#logging_qa_no_data_dashboard_kibana)





## Was kann ich tun, wenn keine Daten auf der Seite 'Discover' in Kibana angezeigt werden?
{: #logging_qa_no_data_discover_kibana}

Es sind verschiedene Szenarios möglich, in denen in Kibana keine Daten angezeigt werden können: 

1. Wenn Sie Kibana starten, werden möglicherweise keine Daten auf der Seite 'Discover' angezeigt. Sie empfangen die folgende Nachricht: **No results found.** (Keine Ergebnisse gefunden).  
2. Sie arbeiten auf der Seite 'Discover' in Kibana. Nach kurzer Zeit empfangen Sie jedoch die folgende Nachricht, wenn Sie versuchen, eine Task in Kibana auszuführen: **No results found.** (Keine Ergebnisse gefunden). 

Führen Sie die folgenden Schritte aus, um dieses Problem zu beheben: 

1. Überprüfen Sie das Zeitauswahlfeld (*Time Picker*), das auf der Seite 'Discover' eingestellt ist, und vergrößern Sie den Zeitraum.  

    **Hinweis:**: In {{site.data.keyword.Bluemix_notm}} ist das Zeitauswahlfeld (*Time Picker*) standardmäßig auf das Anzeigen von Daten der letzten 15 Minuten eingestellt. 

    Weitere Informationen zur Einstellung des Zeitauswahlfelds (*Time Picker*) finden Sie unter [Zeitfilter festlegen](../kibana4/logging_kibana_set_time_filter.html#set_time_filter). 
       
2. Klicken Sie auf das Lupensymbol, das sich in der Suchleiste der Seite *Discover* befindet. Die Seitendaten werden auf der Grundlage der Standardsuchabfrage aktualisiert.

    Alternativ können Sie einen Zeitraum zur automatischen Aktualisierung (*Auto refresh*) festlegen. 

    **Hinweis:** In {{site.data.keyword.Bluemix_notm}} ist der Zeitraum für automatisches Aktualisieren (*Auto refresh*) standardmäßig inaktiviert (**OFF**). 
    
    Weitere Informationen zur Aktivierung des Zeitraums finden Sie unter [Datenanzeige automatisch aktualisieren](../kibana4/logging_kibana_analize_logs_interactively.html#kibana_discover_view_refresh_interval).



## Was kann ich tun, wenn eine Authentifizierungsausnahmebedingung auftritt?
{: #logging_qa_no_data_dashboard_kibana}

Wenn keine Daten in Ihren Visualisierungen auf einer Dashboardseite angezeigt werden und die Fehlernachricht **Error: Authorization Exception.** (Fehler: Berechtigungsausnahmebedingung.) ausgegeben wird, überprüfen Sie Ihre Berechtigungen zum Anzeigen von Daten in jeder einzelnen Visualisierung. 

Berücksichtigen die folgenden Informationen:
Sie können eine oder mehrere Visualisierungen auf einer Seite 'Dashboard' konfigurieren. Wenn die Seite 'Dashboard' eine Anforderung sendet, um die Daten zusammenzustellen, die in diesen Visualisierungen angezeigt werden, wird nur eine Anforderung für alle Visualisierungen ausgegeben. Wenn Sie keine Berechtigung zum Anzeigen von Daten in mindestens einer der Visualisierungen haben, schlägt die gesamte Anforderung fehl. 

Führen Sie die folgenden Schritte aus, um dieses Problem zu beheben: 

1. Ermitteln Sie die Visualisierungen, für die Sie keine Berechtigungen haben. 

    1. Klicken Sie auf das *Stiftsymbol* der Visualisierung auf der Seite *Dashboard*. Die Visualisierung wird auf der Seite *Visualize* geöffnet. Alternativ können Sie auf der Seite *Visualize* eine Visualisierung laden.  
    2. Überprüfen Sie, ob die Daten angezeigt werden. 
    
    Wiederholen Sie diese Schritte für jede Visualisierung. 

2. Fordern Sie Zugriff zum Anzeigen von Daten in diesen Visualisierungen von Ihrem Cloudadministrator an. 

3. Erstellen Sie eine neue Seite 'Dashboard', die die Visualisierungen ausschließt, für die Sie keine Berechtigungen haben, während Ihnen der Zugriff zum Anzeigen der Daten in den Visualisierungen erteilt wird, die das Problem verursachen.  

    Wenn Sie das Dashboard mit anderen gemeinsam nutzen, löschen Sie keine Visualisierungen, da dies sich auch auf andere Teammitglieder auswirkt, die das betreffende Dashboard verwenden. 


