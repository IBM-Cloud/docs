---

Copyright :
  Années : 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Journalisation et traçage
{: #logging_tracing}

*Dernière mise à jour : 23 mars 2016*

## Fichiers journaux
{: #log_files}

Les journaux Liberty standard, tels que le fichier messages.log ou le répertoire ffdc, sont disponibles dans IBM Bluemix, dans le répertoire logs de chaque instance d'application. Vous pouvez accéder à ces journaux à partir de la console IBM Bluemix ou à l'aide des commandes cf logs et cf files.
Par exemple, pour afficher le fichier messages.log, exécutez la commande suivante :
```
    $ cf files <yourappname> logs/messages.log
```
{: codeblock}

Vous
pouvez définir le niveau de journalisation et d'autres options de trace dans
le fichier de configuration de Liberty. Pour plus d'informations, voir
[Profil
Liberty : trace et journalisation](http://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/rwlp_logging.html?cp=SSAW57_8.5.5%2F3-17-0-0). Vous pouvez également ajuster le traçage sur une instance d'application en cours d'exécution à l'aide de la console IBM Bluemix.

## Utilisation des fonctions de trace et de vidage
{: #using_trace_and_dump}

L'interface utilisateur d'IBM Bluemix dispose de fonctions de trace et de vidage.
* Utilisez la fonction Trace pour examiner et mettre à jour la spécification
traceSpecification de journalisation Liberty sur les instances d'application en cours d'exécution.
* Utilisez la fonction Vidage pour créer et manipuler les clichés d'unité d'exécution et de pile sur les instances d'application en cours d'exécution.

Pour
ce faire, sélectionnez une application Liberty dans l'interface utilisateur. Depuis Contexte d'exécution dans le panneau de navigation sur la gauche, vous pouvez ouvrir la page des détails de l'instance. Sélectionnez une ou plusieurs instances. Sous le menu Actions, vous pouvez sélectionner TRACE ou DUMP.

# rellinks
## general
* [Environnement d'exécution Liberty](index.html)
* [Présentation de Liberty Profile](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
