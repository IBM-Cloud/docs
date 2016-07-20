---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Informationen zu {{site.data.keyword.twittershort}}
{: #about_twitter}

*Letzte Aktualisierung: 13. Mai 2016*
{: .last-updated}

Mithilfe von {{site.data.keyword.twitterfull}} können Sie Twitter-Inhalte aus den Twitter [Decahose](http://support.gnip.com/apis/firehose/overview.html){: new_window}- oder [PowerTrack](http://support.gnip.com/apis/powertrack/overview.html){: new_window}-Streams in Ihre {{site.data.keyword.Bluemix}}-Anwendungen integrieren.
{:shortdesc}

Der Content Store wird in Echtzeit aktualisiert und indexiert, wodurch schnelle und dynamische Suchvorgänge möglich sind. Durch den Service werden Tweets mit Stimmungen und anderen Informationen für mehrere Sprachen versehen, und zwar auf der Grundlage von Algorithmen für eine tiefgreifende Verarbeitung natürlicher Sprache aus [IBM Social Media Analytics](http://www.ibm.com/software/products/en/social-media-analytics/){: new_window}. Die Echtzeitverarbeitung von Twitter-Streams	wird vollständig unterstützt und sie kann über eine umfangreiche Menge an Abfrageparametern und Schlüsselwörtern konfiguriert werden. {{site.data.keyword.twittershort}} umfasst	REST-konforme APIs, mit deren Hilfe Sie Ihre Suchvorgänge anpassen können; außerdem werden Tweets und zusätzliche Informationen mit Insights for Twitter im JSON-Format zurückgegeben. Bei zurückgegebenen Tweets wird das [Gnip Activity Stream](http://support.gnip.com/sources/twitter/data_format.html){: new_window}-Format für Twitter-Daten beachtet.

Mit dem {{site.data.keyword.twittershort}}-Service werden der Twitter Decahose-Stream und der Twitter PowerTrack-Stream in Echtzeit analysiert, um so die folgenden zusätzlichen Informationen für den Verfasser eines jeden Tweets bereitzustellen:
* Geschlecht
* Hauptwohnsitz (Land, Bundesland/Kanton und Stadt)

Für den Tweet-Inhalt stehen auch die folgenden zusätzlichen Informationen zur Verfügung:

* Stimmung (positive, negative, ambivalente oder neutrale Stimmung für Tweets in Englisch, Deutsch, Französisch und Spanisch)
* Positive/negative Stimmungsausdrücke in einem Tweet (für Tweets in Englisch, Deutsch, Französisch und Spanisch)

Zur Auswertung der {{site.data.keyword.twittershort}}-Suchergebnisse stellt der Service eine REST-API-Methode bereit, durch die bestätigt wird, dass ein bestimmter Tweet noch immer in Twitter zugänglich ist. 

## Feedback und Support 
{: #feedback_support}

Das {{site.data.keyword.twitterfull}}-Team wünscht Ihr
  Feedback.

Bei Problemen mit diesem Service können Sie das
IBM [developerWorks Answers](https://developer.ibm.com/answers/topics/insights-twitter/?smartspace=bluemix){: new.window}-Forum nutzen. Sie können nach Antworten auf bereits eingereichte Fragen suchen oder selbst eine Frage stellen.
Nehmen Sie die Tags **insights-twitter** und **bluemix** mit auf, um die Antwortzeit zu verbessern.

Wenn Sie Fragen haben, auf die in developerWorks Answers keine Antworten enthalten sind, können Sie Ihre Frage an
[Stack Overflow](http://stackoverflow.com/search?q=twitter+bluemix){: new.window} richten und mit den Tags **twitter** und **bluemix** versehen.

Sie können außerdem den Status der [Bluemix-Plattform](https://developer.ibm.com/bluemix/support/#status){: new.window}
anzeigen oder ein [Support-Ticket öffnen](https://cloudoe.support.ibmcloud.com/ics/support/default.asp?deptid=31036&offering=ibmbluemix){: new.window}. Weitere Informationen finden Sie im Abschnitt zur [Fehlerbehebung](https://console.{DomainName}/docs/troubleshoot/troubleshoot.html){: new_window}.
