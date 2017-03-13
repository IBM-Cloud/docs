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

# Initiation à {{site.data.keyword.mqa}} (obsolète)
{: #gettingstartedtemplate}

**Le service {{site.data.keyword.mqafull}} est obsolète.** Pour plus d'informations sur le statut et les dates, voir l'[article de blogue Retirement of Bluemix Mobile Quality Assurance ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/blogs/bluemix/?p=72728){: new_window}.
{:deprecated}

{{site.data.keyword.mqafull}} permet aux équipes de capturer l'acquis des testeurs et des utilisateurs
réels afin de constamment créer et distribuer des applications mobiles de grande qualité.
{: shortdesc}

Pour être rapidement opérationnel avec le service {{site.data.keyword.mqa}}, procédez comme suit :

1. Après avoir créé une instance
<!--[create an instance](https://console.{DomainName}/docs/services/reqnsi.html#req_instance)-->du service
{{site.data.keyword.mqa}}, vous pouvez accéder à la console de {{site.data.keyword.mqa}}
en cliquant sur votre vignette dans la section **Services** du tableau de bord {{site.data.keyword.Bluemix}}.

	Le service {{site.data.keyword.mqa}} se lance.

2. Ajoutez une application mobile à l'instance {{site.data.keyword.mqa}} en sélectionnant **Add MQA App** et en indiquant le nom de l'application.

3. Téléchargez les [logiciels SDK client ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://www.ibm.com/support/docview.wss?uid=swg27044490){: new_window} de {{site.data.keyword.mqa}} et continuez à instrumenter votre application en procédant de l'une des manières suivantes :

	* [Instrumentation de MQA avec une application Android](mqa_inst_app_android.html)
	* [Instrumentation de MQA avec une application iOS](mqa_inst_app_ios.html)
	* [Instrumentation de MQA avec une application Cordova](mqa_inst_app_cord.html)

	Un seul logiciel SDK est utilisé pour instrumenter les applications de préproduction et les applications de production. Vous pouvez utiliser le paramètre `MODE:` afin de spécifier *QA* pour le mode préproduction ou *MARKET* pour le mode production. Spécifiez le mode préproduction pour que les testeurs internes puissent fournir des informations détaillées sur les bogues et les pannes qui surviennent dans votre application. Indiquez le mode production pour que les utilisateurs puissent fournir des informations détaillées sur votre application. Si votre application est en production, {{site.data.keyword.mqa}} facilite l'obtention des feedbacks de la part des utilisateurs depuis l'application.

4. Après avoir instrumenté votre application, vous pouvez afficher des informations plus détaillées sur la qualité de votre application en sélectionnant l'une des options suivantes dans l'interface de votre instance de service {{site.data.keyword.mqa}} :

	<dl>
		<dt><strong>Sessions</strong></dt>
		<dd>Consultez des informations sur les pannes, les bogues, le feedback et l'état du périphérique au cours de la session.  Pour plus d'informations, voir [Viewing session details ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/t_ViewingSessionDetails.html){: new_window} dans l'IBM Knowledge Center.</dd>
		<dt>![](/images/cap_crashicon.jpg) <strong>Crashes</strong></dt>
		<dd>Consultez des informations sur l'origine des pannes. Pour plus d'informations, voir [Crash reports ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/c_CrashReports.html){: new_window} dans l'IBM Knowledge Center.</dd>
		<dt>![](/images/cap_bugicon.jpg) <strong>Bugs</strong></dt>
		<dd>Consultez des informations mises à disposition par les utilisateurs, telles que des rapports de bogue, des captures d'écran et des détails sur les périphériques. Pour plus d'informations, voir [Bug reports ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/c_BugReports.html){: new_window} dans l'IBM Knowledge Center.</dd>
		<dt>![](/images/cap_feedbackicon.jpg) <strong>Feedback</strong></dt>
		<dd>Consultez les feedbacks des utilisateurs pour connaître l'auteur et la date d'un feedback. Pour plus d'informations, voir [User feedback ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/c_UserFeedback.html){: new_window} dans l'IBM Knowledge Center.</dd>
		<dt><strong>Sentiment score (si configuré)</strong></dt>
		<dd>Consultez le score de sentiment des utilisateurs au fil du temps et des versions afin de surveiller, de mesurer et d'améliorer la qualité des applications. Pour plus d'informations, voir [User sentiment ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/UserSentiment.html){: new_window} dans l'IBM Knowledge Center.</dd>
		<dt><strong>Registered devices</strong></dt>
		<dd>Consultez la liste des périphériques qui sont utilisés au cours d'une session de test ainsi que des informations sur ces périphériques. Pour plus d'informations, voir [Viewing device information ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/t_ManagingDevices.html){: new_window} dans l'IBM Knowledge Center.</dd>
	</dl>

	Ces mesures incluent les données suivantes :

	* Données de préproduction pour les pannes, les bogues, le feedback et les sessions.
	* Données de production pour les pannes, le feedback, le sentiment et les sessions.

	![Capture d'écran de l'interface dans laquelle vous pouvez afficher les métriques de qualité associées à une application](images/quality_metrics_saas4.gif)

	En affichant ces informations pour vos applications, vous pouvez déterminer s'il est nécessaire d'examiner les problèmes plus en détail. Par
exemple, si le taux de panne d'une application augmente considérablement, vous pouvez cliquer sur le taux de panne afin d'afficher des informations plus
détaillées dans des rapports de panne pour cette application.

5. Pour afficher le score de sentiment général pour l'application, vous devez configurer l'analyse des sentiments :

	1. Dans la section *Sentiment Score*, cliquez sur le lien de configuration de l'analyse des sentiments pour l'application
sélectionnée.

	2. Dans la page Application Details, [configurez l'analyse des sentiments ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/tEnablingUserSentiment.html){: new_window} et sauvegardez vos modifications.


# Liens connexes
{: #rellinks notoc}

## Tutoriels et exemples
{: #samples notoc}

* [Vidéo : Getting Started with Mobile Quality Assurance in Bluemix ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.youtube.com/watch?v=zHRfGatcKPM){: new_window}  
* [Vidéo : Sentiment Analysis in Mobile Quality Assurance ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.youtube.com/watch?v=uhkqb8BIn6k){: new_window}
* [developerWorks : Add IBM Mobile Quality Assurance to your mobile quality regimen ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://www.ibm.com/developerworks/library/mo-mqa/index.html){: new_window}
* [developerWorks : Build mobile apps that work: Five tips from an expert panel ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://www.ibm.com/developerworks/library/mo-mqa-tips/index.html){: new_window}
* [developerWorks : Build a mobile app that isn't perfect ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://www.ibm.com/developerworks/library/mo-build-imperfect-mobile-app/){: new_window}
* [developerWorks : DevOps for mobile apps challenges and best practices ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://www.ibm.com/developerworks/library/mo-bestdevops-mobileapps/index.html){: new_window}
* [Sample: bluelist-mqa ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://hub.jazz.net/project/mobilecloud/bluelist-mqa/overview){: new_window}
