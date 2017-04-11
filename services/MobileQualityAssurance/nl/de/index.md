---

copyright:
  years: 2017
lastupdated: "2017-02-28"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note:.deprecated}

# Einführung in {{site.data.keyword.mqa}} (veraltet)
{: #gettingstartedtemplate}

**Der Service {{site.data.keyword.mqafull}} wird nicht weiter unterstützt.** Informationen zu Status und Datumsangaben finden Sie unter [Retirement of Bluemix Mobile Quality Assurance blog entry ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/blogs/bluemix/?p=72728){: new_window}.
{:deprecated}

Mit {{site.data.keyword.mqafull}} können Teams die Erfahrung von Testern und die zeitnahe Benutzererfahrung für eine unterbrechungsfreie Erstellung und Bereitstellung qualitativ hochwertiger mobiler Apps erfassen.
{: shortdesc}

Führen Sie für einen schnelleren Start mit dem Service {{site.data.keyword.mqa}} die folgenden Schritte aus:

1. Nach dem Erstellen einer Instanz <!--[create an instance](https://console.{DomainName}/docs/services/reqnsi.html#req_instance)--> des Service {{site.data.keyword.mqa}} können Sie durch Klicken auf Ihre Kachel im Abschnitt **Services** des {{site.data.keyword.Bluemix}}-Dashboards auf die {{site.data.keyword.mqa}}-Konsole zugreifen.

	Der Service {{site.data.keyword.mqa}} wird gestartet.

2. Fügen Sie der {{site.data.keyword.mqa}}-Instanz durch Auswahl der Option zum Hinzufügen einer MQA-App und durch Angabe eines Namens für die App eine mobile App hinzu.

3. Laden Sie die {{site.data.keyword.mqa}}-[Client-SDKs ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://www.ibm.com/support/docview.wss?uid=swg27044490){: new_window} herunter und führen Sie die Instrumentierung Ihrer App durch, indem Sie mit einer der folgenden Prozeduren fortfahren:

	* [MQA mit einer Android-App instrumentieren](mqa_inst_app_android.html)
	* [MQA mit einer iOS-App instrumentieren](mqa_inst_app_ios.html)
	* [MQA mit einer Cordova-App instrumentieren](mqa_inst_app_cord.html)

	Ein einfaches SDK dient zum Instrumentieren sowohl von Vorproduktions- als auch von Produktions-Apps. Mit dem Parameter `MODE:` können Sie *QA* für den Vorproduktionsmodus bzw. *MARKET* für den Produktionsmodus angeben. Geben Sie den Vorproduktionsmodus an, damit interne Tester ausführliche Informationen zu Programmfehlern und -abstürzen bereitstellen können, zu denen es in Verbindung mit Ihrer App kommt. Geben Sie den Produktionsmodus an, damit Benutzer ausführliche Informationen zu Ihrer App angeben können. Befindet sich Ihre App im Produktionsmodus, vereinfacht {{site.data.keyword.mqa}} den Abruf von Feedback von Benutzern direkt innerhalb der App.

4. Nach der Instrumentierung Ihrer App können Sie detaillierte Informationen zur Qualität anzeigen, und zwar durch Auswahl einer der folgenden Optionen in der Schnittstelle Ihrer Instanz des Service {{site.data.keyword.mqa}}:

	<dl>
		<dt><strong>Sitzungen</strong></dt>
		<dd>Anzeigen der Informationen zu Programmabstürzen, Programmfehlern, Feedback und dem Status des Geräts während der Sitzung. Weitere Informationen finden Sie im Abschnitt [Sitzungsdetails anzeigen ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/t_ViewingSessionDetails.html){: new_window} des IBM Knowledge Center.</dd>
		<dt>![](/images/cap_crashicon.jpg) <strong>Programmabstürze</strong></dt>
		<dd>Anzeigen der Informationen zu den Ursachen von Programmabstürzen. Weitere Informationen finden Sie im Abschnitt [Berichte zu Programmabstürzen ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/c_CrashReports.html){: new_window} des IBM Knowledge Center.</dd>
		<dt>![](/images/cap_bugicon.jpg) <strong>Programmfehler</strong></dt>
		<dd>Anzeigen der Informationen, die von Benutzern dokumentiert werden, z. B. Programmfehlerberichte, Screenshots und Gerätedetails. Weitere Informationen finden Sie im Abschnitt [Berichte zu Programmfehlern ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/c_BugReports.html){: new_window} des IBM Knowledge Center.</dd>
		<dt>![](/images/cap_feedbackicon.jpg) <strong>Feedback</strong></dt>
		<dd>Anzeigen der Antworten zum Benutzerfeedback, um zu sehen, wer wann das Feedback verfasst hat. Weitere Informationen finden Sie im Abschnitt [Benutzerfeedback ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/c_UserFeedback.html){: new_window} des IBM Knowledge Center.</dd>
		<dt><strong>Stimmungsscore (sofern konfiguriert)</strong></dt>
		<dd>Anzeigen des Benutzerstimmungsscores über einen bestimmten Zeitraum hinweg und für bestimmte Versionen zur Überwachung, Bewertung und Verbesserung der App-Qualität. Weitere Informationen finden Sie im Abschnitt [Benutzerstimmung ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/UserSentiment.html){: new_window} des IBM Knowledge Center.</dd>
		<dt><strong>Registrierte Geräte</strong></dt>
		<dd>Anzeigen der Liste von Geräten, die für eine Testsitzung verwendet werden, sowie Anzeigen der Informationen zu diesen Geräten. Weitere Informationen finden Sie im Abschnitt [Geräteinformationen anzeigen ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/t_ManagingDevices.html){: new_window} des IBM Knowledge Center.</dd>
	</dl>

	Zu diesen Metriken gehören die folgenden Daten:

	* Vorproduktionsdaten für Abstürze, Programmfehler, Feedback und Sitzungen.
	* Produktionsdaten für Abstürze, Feedback, Stimmung und Sitzungen.

	![Screenshot der Schnittstelle, in dem Sie die Qualitätsmetriken für eine App sehen können.](images/quality_metrics_saas4.gif)

	Durch das Anzeigen dieser Informationen für Ihre Apps können Sie feststellen, ob es für bestimmte Probleme einer weiteren Untersuchung bedarf. Wenn beispielsweise die Programmabsturzrate für eine App ihren Höchststand erreicht, können Sie auf die Programmabsturzrate klicken, um weitere ausführliche Informationen zu den Programmabsturzberichten für diese App anzuzeigen.

5. Um den Gesamt-Stimmungsscore für die App anzuzeigen, muss die Stimmungsanalyse konfiguriert werden:

	1. Klicken Sie im Abschnitt *Stimmungsanalyse* auf den Link, um die Stimmungsanalyse für die ausgewählte App zu konfigurieren.

	2. [Konfigurieren Sie die Stimmungsanalyse ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/tEnablingUserSentiment.html){: new_window} auf der Seite mit den Anwendungsdetails und speichern Sie Ihre Änderungen.


# Zugehörige Links
{: #rellinks notoc}

## Lerntexte und Beispiele
{: #samples notoc}

* [Video: Einführung in Mobile Quality Assurance in Bluemix ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.youtube.com/watch?v=zHRfGatcKPM){: new_window}  
* [Video: Stimmungsanalyse in Mobile Quality Assurance ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.youtube.com/watch?v=uhkqb8BIn6k){: new_window}
* [developerWorks: IBM Mobile Quality Assurance zur eigenen mobilen Qualität hinzufügen ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://www.ibm.com/developerworks/library/mo-mqa/index.html){: new_window}
* [developerWorks: Funktionierende mobile Apps erstellen: Fünf Expertentipps ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://www.ibm.com/developerworks/library/mo-mqa-tips/index.html){: new_window}
* [developerWorks: Beinahe perfekte mobile App erstellen ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://www.ibm.com/developerworks/library/mo-build-imperfect-mobile-app/){: new_window}
* [developerWorks: DevOps für mobile Apps - Anforderungen und Best Practices ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://www.ibm.com/developerworks/library/mo-bestdevops-mobileapps/index.html){: new_window}
* [Beispiel: bluelist-mqa ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://hub.jazz.net/project/mobilecloud/bluelist-mqa/overview){: new_window}
