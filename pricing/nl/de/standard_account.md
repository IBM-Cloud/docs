---



copyright:

  years: 2016, 2017
lastupdated: "2017-05-02"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# IBM {{site.data.keyword.Bluemix_notm}}-Standardkonto (Betaversion) 
{: #betaintro}

Mit der Betaversion des {{site.data.keyword.Bluemix}}-Standardkontos wird ein neues kostenfreies Konto eingeführt, das eine neue Möglichkeit bietet, in der öffentlichen Cloud von {{site.data.keyword.Bluemix_notm}} zu arbeiten. Für das Standardkonto gilt kein Ablaufdatum, im Gegensatz zum {{site.data.keyword.Bluemix_notm}}-Testkonto mit einer Gültigkeit von 30 Tagen. Sie können die Arbeit mit den {{site.data.keyword.Bluemix_notm}}-Anwendungen fortsetzen, ohne sich um Zeitbegrenzungen zu kümmern. 
{:shortdesc}

Die Teilnahme bei der Betaversion des Standardkontos ist nur mit einer Einladung möglich. Nachdem Sie die Einladung akzeptiert und ein Standardkonto erstellt haben, können Sie Freunde und Kollegen einladen, an der Betaversion teilzunehmen.  

## {{site.data.keyword.Bluemix_notm}}-Standardkonto - Einführung
{: #standardaccount}

Sicher interessiert es Sie, welche Unterschiede zwischen dem Standardkonto und dem Testkonto bestehen. Die folgende Tabelle enthält eine Zusammenfassung der wichtigen Details zum {{site.data.keyword.Bluemix_notm}}-Standardkonto. 

|Neuerungen bei einem Standardkonto |    
|-----------------|
| Für das Konto existiert kein Ablaufdatum. |
| Cloud Foundry-Anwendungen können auf bis zu 256 MB an freiem, sofort verfügbarem Laufzeitspeicher zugreifen. |
| Sie können auf kostenfreie Lite-Pläne für Cloudant NoSQL DB und Internet of Things Platform zugreifen; weitere Services sind demnächst verfügbar. |
| Ihre Anwendungen werden in den Ruhemodus versetzt, falls über einen Zeitraum von 10 Tagen keine Entwicklungsaktivität stattfindet. |
| Ihre Serviceinstanzen werden nach einem Inaktivitätszeitraum von 30 Tagen gelöscht. |
{:caption="Tabelle 1. Neuerungen in einem Standardkonto" caption-side="top"}

|Was bleibt nach dem Konvertieren eines Testkontos unverändert? | 
|-----------------|
|Das Konto ist kostenfrei - Sie benötigen keine Kreditkarte. |
|Alle Lite-Instanzen von Cloudant NoSQL DB und Internet of Things Platform. Eine Lite-Instanz für jeden dieser Services kann an das neue Konto übertragen werden. |
|Die Organisation, Bereiche und zugehörige Zugriffseinstellungen für Teammitglieder bleiben unverändert. Eine Organisation kann an das neue Konto übertragen werden. |
|Die {{site.data.keyword.Bluemix_notm}} Support-Stufe bleibt unverändert. |
{:caption="Tabelle 2. Was bleibt unverändert?" caption-side="top"}

**Hinweis**: Wenn Ihr Testkonto nicht konvertiert werden kann, erhalten Sie eine Nachricht mit einer Erläuterung zur Ursache. Möglicherweise enthält das bestehende Testkonto mehr als eine Organisation oder Apps, die nicht übertragen werden können. Sie können die entsprechende Maßnahme ausführen und dann die Konvertierung des Kontos erneut versuchen.

Wenn Sie bei einem Standardkonto angemeldet sind, können Sie Teammitglieder dazu einladen, in Ihrer Organisation und Ihren Bereichen mitzuarbeiten, Nutzungsdaten anzuzeigen, Bereiche zu erstellen, das Kontoprofil zu aktualisieren und die Organisation zu verwalten. Weitere Informationen
finden Sie in [Konto verwalten](/docs/admin/adminpublic.html#account). 

## Lite-Pläne
{: #liteplans}
   
Lite-Pläne, die auch in einem nutzungsabhängigen Konto verfügbar sind, sind mit kostenfreien Kontingenten strukturiert. Sie können an Ihren Projekten arbeiten, ohne sich darüber Gedanken zu machen, versehentlich Kosten zu generieren. Das Kontingent kann über einen bestimmten Zeitraum hinweg gültig sein, z . B. für einen Monat, oder auf einer Einzelnuztungsbasis. Beispiele für Kontingente im Rahmen eines Lite-Plans:

<ul>
<li>Maximale Anzahl registrierter Geräte.</li>
<li>Maximale Anzahl von Anwendungsbindungen.</li>
<li>Grenzwert für den verschlüsselten Datenspeicher, z. B. 1 GB.</li>
<li>Bereitgestellte Durchsatzkapazität.</li>
</ul> 

In einem Standardkonto können Sie alle Angebote des {{site.data.keyword.Bluemix_notm}}-Katalogs nutzen, für die ein Lite-Plan vorgesehen ist. Lite-Pläne sind einfach zu finden. Beim Öffnen des Katalogs werden standardmäßig alle Services mit einem Lite-Plan angezeigt und mit einem Lite-Tag ![Lite-Tag](../icons/Lite.svg) gekennzeichnet. Wählen Sie einen Service aus, um die Kontingentdetails für den zugehörigen Lite-Plan anzuzeigen.

## Was ist mit einem Standardkonto verfügbar?
{: #whatsavailable}

In einem Standardkonto können Cloud Foundry-Anwendungen auf maximal 256 MB sofort verfügbaren Laufzeitspeicher zugreifen. Wenn das zugeordnete Kontingent überschritten wird, können Sie einige Ihrer Apps stoppen, um Laufzeitspeicher freizugeben. 

Währen der Betaphase des Standardkontos wird für die folgenden Services ein Lite-Plan angeboten:

<ul>
<li>Cloudant NoSQL DB</li>
<li>Internet of Things Platform</li>
</ul>

Zu dieser Liste werden weitere Services hinzugefügt, bleiben Sie also dran!

Wenn die Grenzwerte des Kontingents erreicht sind, wird die Anwendung gestoppt oder der Service wird inaktiviert. Wenn im Lite-Plan angegeben ist, dass das Kontingent auf monatlicher Basis bereitgestellt wird, wird die Ressourcennutzung am ersten Tag jedes Monats zurückgesetzt und Sie können die Arbeit mit dem Service fortsetzen. Wenn ein Kontingentgrenzwert erreicht oder fast erreicht ist, erhalten Sie eine Benachrichtigungs-E-Mail. 

Sie können 1 Instanz pro Lite-Plan bereitstellen. 

**Hinweis**: Diese Einschränkungen gelten nur für das Standardkonto. Sie können jederzeit ein Upgrade auf ein nutzungsabhängiges Konto oder ein abonnementbasiertes Abrechnungskonto durchführen. Kosten fallen nur für die Nutzung an, die über die kostenfreien Kontingente hinausgeht. Weitere Informationen zu nutzungsabhängigen Konten und Abonnementkonten finden Sie unter [Kontotypen](/docs/pricing/index.html#pay-accounts).

## Entwicklungsaktivität
{: #devactivity}

Als Unterstützung für Standardkontobenutzer bei der bestmöglichen Verwaltung ihrer Ressourcen stehen einige Optimierungsfeatures zur Verfügung, die auf der Entwicklungsaktivität und Nutzung basieren:

 * Ihre Apps werden in den Ruhemodus versetzt, falls über einen Zeitraum von 10 Tagen keine Entwicklungsaktivität stattfindet. Dies ist nützlich, wenn Sie an einer neuen App arbeiten möchten, da Sie auf diese Weise den Grenzwert von 256 MB für das Speicherkontingent nicht so schnell erreichen. Wenn Sie die Apps erneut aktivieren möchten, beginnen Sie in der Cloud Foundry-Befehlszeile oder der {{site.data.keyword.Bluemix_notm}}-Konsole erneut mit der Bearbeitung der Apps. 
 
 In der folgenden Liste sind alle Befehle aufgeführt, mit denen die App aktiviert wird:
  * cf push
  * cf restate
  * cf restart
  * cf ssh
  * cf scale
  * cf stop
  * cf start
  * cf create-route
  * cf map-route
  * cf unmap-route
  * cf delete-route
  * cf enable-ssh
  * cf disable-ssh

 **Hinweis**: Wenn für die App der SSH-Modus bereits aktiviert ist, kann sie mit den Befehlen `cf enable-ssh` und `cf disable-sh` nicht aktiviert werden. 

 * Ihre Lite-Plan-Services werden gelöscht, wenn über einen Zeitraum von 30 Tagen keine Aktivität dafür stattfindet. Auf diese Weise müssen Sie keine inaktiven Instanzen löschen, wenn Sie eine neue Instanz erstellen möchten. Zum gegenwärtigen Zeitpunkt verwendet nur der Internet of Things Platform-Service dieses Feature. 
 
 Sie können die Lite-Instanz für Internet of Things Platform im aktiven Modus behalten, indem Sie sich beim Dashboard der Internet of Things Platform-Serviceinstanz anmelden.
 
## An der Betaversion des Standardkontos teilnehmen
{: #betainvitation}

Wenn Sie für die Teilnahme an der Betaversion ausgewählt werden, wird eine Einladung an die E-Mail-Adresse gesendet, die Ihrem {{site.data.keyword.Bluemix_notm}}-Testkonto zugeordnet ist. Wenn Sie die Einladung erhalten, führen Sie die in der E-Mail enthaltenen Anweisungen zur Registrierung beim Standardkonto aus. 

Möchten Sie am Angebot der Betaversion für das Standardkonto teilnehmen? Fragen Sie auch Ihre Freunde und Kollegen. Falls diese eine Einladung zur Teilnahme an der Betaversion erhalten und ein Standardkonto erstellt haben, können sie auch Ihnen eine Einladung senden. 
