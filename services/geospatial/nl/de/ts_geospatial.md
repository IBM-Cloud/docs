---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-09"

---

<!-- Attribute definitions --> 
{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

#{{site.data.keyword.geospatialshort_Geospatial}} Fehlerbehebung 
{: #ts_geospatial}


In diesem Abschnitt finden Sie die Antworten auf einige häufig gestellte Fragen zur Verwendung von {{site.data.keyword.geospatialshort_Geospatial}} unter {{site.data.keyword.Bluemix_short}}.
{:shortdesc}

##Nach dem Stoppen der Anwendung werden Regionen weiterhin überwacht
{: #stop-monitoring}


Das Stoppen der Anwendung hat nicht automatisch ein Stoppen von {{site.data.keyword.geospatialshort_Geospatial}} zur Folge.
{:shortdesc}


Sie haben die Anwendung gestoppt, die {{site.data.keyword.geospatialshort_Geospatial}} verwendet, im Dashboard für
die Serviceadministration wird jedoch angezeigt, dass die in der App angegebenen Regionen weiterhin vom Service überwacht werden.
{: tsSymptoms}


Wenn Sie die Anwendung stoppen, wird die {{site.data.keyword.geospatialshort_Geospatial}}-Serviceinstanz weiterhin ausgeführt. Der Service überwacht weiterhin die Regionen, bis Sie den Service stoppen; dies ist davon unabhängig, ob
Ihre App aktiv ist. 
{: tsCauses}


Stoppen Sie {{site.data.keyword.geospatialshort_Geospatial}} im Dashboard für die Serviceadministration. Alternativ können Sie die Anwendung so ändern, dass der Service mithilfe der REST-API gestoppt wird und anschließend die Änderungen per Push-Operation wieder an {{site.data.keyword.Bluemix_short}} übertragen werden.
{: tsResolve}

##Service überwacht nicht in Anwendung angegebene Regionen
{: #unspecified-region}



Wenn Sie mehrere Anwendungen an dieselbe Serviceinstanz gebunden haben, können diese Regionen von einer anderen Anwendung hinzugefügt worden sein.
{:shortdesc}



Wenn Sie die {{site.data.keyword.geospatialshort_Geospatial}}-Instanz im Dashboard für Serviceadministration anzeigen, wird angegeben, dass von ihr mehr Regionen überwacht werden, als Sie in einer der Anwendungen festgelegt haben.
{: tsSymptoms}

Eine einzelne Instanz von {{site.data.keyword.geospatialshort_Geospatial}} überwacht die Regionen aller Anwendungen, die an sie gebunden sind. Dies bedeutet, dass beim Anzeigen der Instanz im Dashboard für Serviceadministration die Informationen zu den Regionen angezeigt werden, die von allen Anwendungen angegeben werden.
{: tsCauses}

Gehen Sie wie folgt vor, um das Überwachen bestimmter Regionen durch {{site.data.keyword.geospatialshort_Geospatial}} zu stoppen:

1. Stoppen Sie den Service.
2. Entfernen Sie die jeweiligen Regionen aus der Anwendung bzw. den Anwendungen.
3. Übertragen Sie die Anwendung bzw. Anwendungen mit einer Push-Operation wieder an {{site.data.keyword.Bluemix_short}}.
{: tsResolve}


##Fehlerbehebung im Dashboard für Serviceadministration
{: #dashboard}

Wenn Sie Fehler für eine Anwendung beheben, möchten Sie wahrscheinlich das Dashboard für Serviceadministration aufrufen, um dort den Status der Serviceinstanz zu überprüfen. Wenn dort keine Daten verarbeitet werden, kann das Problem unter Umständen durch das Stoppen und erneute Starten des Service behoben werden.
{:shortdesc}

Der Status Ihrer {{site.data.keyword.geospatialshort_Geospatial}}-Serviceinstanz wird getrennt vom Status Ihrer Anwendung angezeigt, aber mehrere Anwendungen können an dieselbe Serviceinstanz gebunden sein. 

Vom Dashboard für Serviceadministration werden Informationen zum Status von {{site.data.keyword.geospatialshort_Geospatial}} bereitgestellt, nicht zu den Anwendungen, die an den Service gebunden sind. Dass die Statusangaben der Serviceinstanz von den Angaben der Anwendung bzw. der Anwendungen getrennt angezeigt werden, bedeutet, dass die {{site.data.keyword.geospatialshort_Geospatial}}-Serviceinstanz bei einem Stoppen der Anwendung weiterhin aktiv ist. Der Service überwacht somit weiterhin die von Ihnen ausgewählten Regionen, bis Sie diese entfernen; dies ist unabhängig davon, ob die Anwendung aktiv ist oder nicht.
