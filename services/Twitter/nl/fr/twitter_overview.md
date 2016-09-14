---

copyright:
  années : 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# A propos de {{site.data.keyword.twittershort}}
{: #about_twitter}

*Dernière mise à jour : 13 mai 2016*
{: .last-updated}

Utilisez {{site.data.keyword.twitterfull}} pour incorporer un contenu Twitter depuis les flux [Decahose](http://support.gnip.com/apis/firehose/overview.html){: new_window} ou [PowerTrack](http://support.gnip.com/apis/powertrack/overview.html){: new_window} de  Twitter dans vos applications {{site.data.keyword.Bluemix}}.
{:shortdesc}

Le magasin de contenu est actualisé et indexé en temps réel, ce qui rend les recherches dynamiques et rapides. Le service apporte à Tweets divers enrichissements comme la possibilité d'exprimer un sentiment particulier ou d'autres idées de ce type, pour plusieurs langues différentes, qui reposent sur des algorithmes de traitement du langage naturel approfondi provenant d'[IBM Social Media Analytics](http://www.ibm.com/software/products/en/social-media-analytics/){: new_window}. Le traitement en temps réel des flux de données Twitter est entièrement pris en charge et peut être configuré via un ensemble riche de paramètres de requête et de mots clés. {{site.data.keyword.twittershort}}
inclut des API RESTful qui vous permettent de personnaliser vos recherches et renvoie des tweets et des enrichissements au format JSON. Les
tweets renvoyés sont au format [flux d'activités Gnip](http://support.gnip.com/sources/twitter/data_format.html){: new_window} pour les données Twitter.

Le service {{site.data.keyword.twittershort}} analyse les flux Twitter Decahose et PowerTrack en temps réel pour fournir les enrichissements suivants à l'auteur de chaque tweet :
* Sexe
* Résidence (pays, état et ville)

Les enrichissements suivants sont également disponibles pour le contenu des tweets :

* Expression d'un sentiment (positif, négatif, ambivalent ou neutre, pour les tweets en anglais, allemand, français et espagnol)
* Phrases de sentiment positives ou négatives contenues dans un tweet (pour les tweets en anglais, allemand, français et espagnol)

Pour valider les résultats de recherche d'{{site.data.keyword.twittershort}}, le service fournit une méthode d'API REST
qui confirme l'accessibilité d'un tweet particulier sur Twitter. 

## Commentaires en retour et support 
{: #feedback_support}

L'équipe {{site.data.keyword.twitterfull}} souhaite recueillir vos commentaires.

Si vous rencontrez des problèmes avec ce service, visitez le forum [developerWorks Answers](https://developer.ibm.com/answers/topics/insights-twitter/?smartspace=bluemix){: new.window}. Consultez les réponses aux questions déjà posées ou ajoutez une question.
Incluez les étiquettes **insights-twitter** et **bluemix** pour améliorer le temps de réponse.

Si vous avez des questions pour lesquelles aucune réponse n'est fournie dans developerWorks Answers, postez votre question sur
[stackoverflow](http://stackoverflow.com/search?q=twitter+bluemix){: new.window} et étiquetez vos questions avec **twitter** et **bluemix**.

Vous pouvez afficher le statut de la plateforme [Bluemix Platform](https://developer.ibm.com/bluemix/support/#status){: new.window}
ou [ouvrir un ticket de demande de service](https://cloudoe.support.ibmcloud.com/ics/support/default.asp?deptid=31036&offering=ibmbluemix){: new.window}. Pour plus d'informations, voir la [rubrique de traitement des incidents](https://console.{DomainName}/docs/troubleshoot/troubleshoot.html){: new_window}.
