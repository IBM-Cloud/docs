---

copyright:
  years: 2015, 2016

---


{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}


# Allgemeine Serviceprobleme
{: #general}

*Letzte Aktualisierung: 9. Dezember 2015*

Ein {{site.data.keyword.Bluemix}}-Serviceproblem liegt zum Beispiel vor, wenn für ein Gateway ein Zeitlimitfehler auftritt, sobald Sie eine Serviceinstanz löschen. In vielen Fällen können Sie diese Probleme jedoch durch Ausführen weniger einfacher Schritte beheben.
{:shortdesc}

## Fehlernachricht wegen Gatewayzeitlimitüberschreitung beim Löschen einer Serviceinstanz
{: #ts_service_broker}

Es kann vorkommen, dass eine Fehlernachricht angezeigt wird, wenn Sie versuchen, eine Serviceinstanz zu löschen, die bereits vom Cloud-Controller gelöscht wurde.
{:shortdesc}


Wenn Sie versuchen, eine Serviceinstanz zu löschen, wird die Service-Broker-Fehlernachricht ```Gateway timeout``` (Zeitlimitüberschreitung für Gateway) angezeigt.
{: tsSymptoms}


Dieses Problem tritt auf, wenn die Serviceinstanz bereits vom Cloud-Controller gelöscht wurde.
{: tsCauses}


Erstellen Sie zum Beheben des Problems eine Serviceinstanz mit demselben Namen und binden Sie sie an Ihre Anwendungen. Danach können Sie die Serviceinstanz und die Anwendungen löschen, von denen der Service verwendet wird.   
{: tsResolve}


