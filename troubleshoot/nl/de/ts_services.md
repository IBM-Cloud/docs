---

copyright:
  years: 2015, 2016
  
lastupdated: "2016-08-12"

---



{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}


# Fehlerbehebung für Services
{: #services}


Ein {{site.data.keyword.Bluemix}}-Serviceproblem liegt zum Beispiel vor, wenn für ein Gateway ein Zeitlimitfehler auftritt, sobald Sie eine Serviceinstanz löschen. Sie können solche Probleme durch Ausführen weniger einfacher Schritte beheben.
{:shortdesc}

## Service-Broker-Fehler beim Löschen einer Serviceinstanz
{: #ts_service_broker}

Es kann vorkommen, dass eine Fehlernachricht angezeigt wird, wenn Sie versuchen, eine Serviceinstanz zu löschen, die bereits vom Cloud-Controller gelöscht wurde.
{:shortdesc}

Wenn Sie versuchen, eine Serviceinstanz zu löschen, wird die folgende Service-Broker-Fehlernachricht über eine Gateway-Zeitlimitüberschreitung angezeigt:
{: tsSymptoms}
`Gateway timeout`

Dieses Problem tritt auf, wenn die Serviceinstanz bereits vom Cloud-Controller gelöscht wurde.
{: tsCauses}

Erstellen Sie eine Serviceinstanz mit demselben Namen und binden Sie sie an Ihre Anwendungen. Anschließend können Sie die Serviceinstanz und die Anwendungen löschen, die den Service verwenden.   
{: tsResolve}
