---

 

copyright:

  years: 2015, 2016

 

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

#Organisation et filtrage des éléments de travail {: #tp-organize}  

*Dernière mise à jour : 29 avril 2016*
{: .last-updated}

Le service {{site.data.keyword.trackplan}} inclut plusieurs options pour trier et organiser vos éléments de travail.
{: shortdesc}

##Filtrage des éléments de travail {: #tp-filteringwis}

Vous pouvez filtrer les éléments de travail en fonction de mots ou de valeurs pour des attributs spécifiques. 

Le filtrage est pris en charge dans les vues ci-après :   
- Mon travail
- Eléments auxquels je suis abonné
- Travail entrant
- Journal des éléments en attente
- Planification de sprint
- Travail de l'équipe
- Tout le travail

Si vous entrez un mot, les récapitulatifs des éléments de travail qui contiennent ce mot sont présentés. Vous pouvez aussi filtrer des éléments de travail en fonction de valeurs pour des attributs spécifiques. Pour plus de détails, voir le tableau suivant. 

| Attribut |Exemple | 
|-------|-------|
|*Type  | `*Defect` |
|#Tag  | `#conference`| 
|@:Owner  | `@:jasmith`|
|$Priority|`$High`|
|!Severity|`!Major`|       
   

Vous pouvez créer des requêtes qui utilisent un attribut d'élément de travail en entrant le nom de cet attribut. Ainsi, si vous entrez `Créé par`, les options de la requête et la syntaxe s'affichent. Vous pouvez utiliser des opérateurs, comme "and", "or" et "not" dans vos critères de filtrage. Il vous est aussi possible d'inclure des opérations complexes qui imbriquent des opérateurs multiples en utilisant des parenthèses. Pour voir des exemples, cliquez sur l'icône **Aide**.
![icône d'aide pour le filtrage](images/filter_helpicon.png)

Quand vous cliquez sur la zone **Filtrer les éléments de travail par mot clé**, les opérateurs et les filtres que vous pouvez utiliser pour créer les requêtes s'affichent.

![Filtrage avec choix en saisie semi-automatique](images/filterMenu2.png)

##Sauvegarde des vues personnalisées {: #tp-customviews}
Vous pouvez créer des vues personnalisées en appliquant des filtres. Vous partagez ensuite ces vues avec votre équipe.    

1. Dans la zone **Filtrer les éléments de travail par mot clé**, entrez le type d'attribut au format court et une valeur pour cet attribut, `$high`, par exemple. Certains attributs sont automatiquement répertoriés quand vous entrez le format court, *Type, $Priority, and !Severity, par exemple.
![Filtrage avec types d'attribut et attributs](images/filterAttributes.png)
2. Cliquez sur **Sauvegarder**.
3. Donnez un nom à la vue.  
4. Si vous voulez que la vue personnalisée inclut le sprint que vous affichez, sélectionnez la case à cocher pour inclure le sprint. Dans l'exemple suivant, le sprint du journal des éléments en attente sera inclus dans la vue relative au journal des éléments en attente de priorité élevée.
![Boîte de dialogue de sauvegarde de vue personnalisée avec sprint inclus](images/filterIncludeSprints.png)
5. Cliquez sur **Sauvegarder**. 
6. Si vous voulez partager vos vues sauvegardées avec votre équipe, dans la section Vues personnalisées, cliquez sur l'icône de partage en regard de la vue suivante puis cliquez sur **OK**.
![Partage de vue personnalisée - flèche](images/filterShare.png)

Les vues personnalisées ne retournent des résultats que pour le sprint et le statut que vous affichez. Si vous voulez que la vue retourne des résultats pour d'autres sprints ou statuts, cliquez sur la vue et procédez aux changements nécessaires.

##Affichage et organisation de vos éléments de travail {: #tp-organizingwis}

- Pour afficher les éléments de travail que vous possédez, consultez la vue Mon travail. 
- Si vous utilisez souvent des éléments de travail spécifiques, vous pouvez les marquer comme favoris en cliquant sur l'icône réservée à cet effet <img class="inline"  src="./images/star.gif" alt="icône des favoris">. Vous pouvez alors voir tous vos éléments de travail favoris dans la vue Mes éléments marqués d'un astérisque. Quand vous cliquez sur l'icône de favori associé à un élément de travail, vous êtes seul à savoir que vous avez l'avez marqué en tant que favori.  
- Pour afficher tous les éléments de travail auxquels vous êtes abonné, ouvrez la vue Eléments auxquels je suis abonné.
- Pour afficher vos éléments de travail triés par dates de modification, consultez la vue Mon travail récent.
- Pour afficher l'activité relative à vos éléments de travail, ouvrez la vue Mes activités. La section Mes événements répertorie les éléments de travail dans lesquels vous êtes mentionné. La section Mes abonnements dresse la liste de tous les changements qui se sont produits dans les éléments de travail auxquels vous êtes abonné.

##Tri des éléments de travail {: #tp-triaging}

Quand un élément de travail est créé mais qu'il n'est pas affecté à un sprint, il s'affiche dans la vue Travail entrant.
Dès qu'un sprint est attribué à cet élément de travail, ce dernier est retiré de la vue Travail entrant.

Dans la vue Travail entrant, vous pouvez procéder à un triage des éléments de travail de diverses façons : 
- Pour rejeter l'élément de travail, cliquez sur l'icône **Jeter cet élément** <img class="inline"  src="./images/trash.gif" alt="icône Jeter cet élément">. L'élément de travail est résolu et son statut passe à Non valide.
- Pour accepter l'élément de travail et l'affecter au journal des éléments en attente, cliquez sur l'icône **Placer dans le journal des éléments en attente** <img  class="inline" src="./images/triage.gif" alt="icône Placer dans le journal des éléments en attente">. Vous pouvez ensuite évaluer l'élément de travail par rapport aux autres éléments de travail qui se trouvent dans la vue Planification de sprint et affecter cet élément de travail à un sprint.
- Pour affecter l'élément de travail à un sprint, ouvrez-le et sélectionnez une valeur dans la liste **Planifié pour**.

![Triage des éléments de travail dans la vue Travail entrant](images/incoming_work_attributes.png)  

Pour plus d'informations sur la gestion des éléments de travail, [voir Gestion d'un projet avec le planificateur rapide](http://www.ibm.com/support/knowledgecenter/SSYMRC_6.0.1/com.ibm.team.concert.tutorial.doc/topics/tut_quick_planner_lesson.html).
