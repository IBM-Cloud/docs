---

copyright:
  years: 2017
lastupdated: "2017-5-8"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Utilisation de Git dans Eclipse Orion Web IDE
{: #git_web_ide}

Si vous utilisez l'interface Eclipse Orion {{site.data.keyword.webide}}, vous n'avez pas besoin du terminal Git : vous pouvez exécuter un grand nombre de commandes Git
communes dans l'interface Web IDE.

Quel que soit l'endroit où vous codez, vous pouvez utiliser cette référence rapide pour réaliser les tâches communes.

## Création d'une branche locale
{: #create_branch}

### Eclipse Orion Web IDE
1. Cliquez sur la liste **Référence**.

1. Cliquez sur **Nouvelle branche**.

2. Entrez votre nom de branche puis cliquez sur **Soumettre**.

### Terminal Git
1. Entrez `git branch <nom de branche>` et appuyez sur Entrée.

## Utilisation d'une branche locale
{: #start_working_on_branch}

### Eclipse Orion Web IDE
1. Cliquez sur la liste **Référence** et développez **local**.

2. En regard de la branche à modifier, cliquez sur l'icône de réservation <img  class="inline" src="./images/checkout.png" alt="Icône de réservation">.

1. Vérifiez que la branche sélectionnée s'affiche dans la liste **Référence**.

### Terminal Git
1. Pour afficher vos branches locales, entrez `git branch -l` et appuyez sur Entrée.

2. Entrez `git checkout <nom de branche>` et appuyez sur Entrée.


## Mise à jour d'une branche locale pour inclure des modifications de la branche distante
{: #update_branch}

### Eclipse Orion Web IDE
1. Cliquez sur **Synchroniser**.

1. Si vous rencontrez des conflits, [résolvez-les](#resolve_a_rebase_conflict).

### Terminal Git
1. Entrez `git pull` et appuyez sur Entrée.

## Suppression d'une branche locale
{: #delete_branch}

### Eclipse Orion Web IDE
1. Vérifiez que la branche à supprimer n'est pas réservée. Si cette branche est réservée, [réservez une autre branche](#start_working_on_branch).

1. Cliquez sur la liste **Référence** et développez **local**.

2. En regard de la branche locale à supprimer, cliquez sur **Supprimer** <img class="inline"  src="./images/delete.png" alt="Icône de suppression">.

### Terminal Git
1. Entrez `git branch -d <nom de branche>` et appuyez sur Entrée.

##Insertion forcée des modifications locales dans une banche distante
{: #force_push}

Ecrasez le contenu d'une branche distante référencée avec le contenu de votre branche locale active.

**Important :** lorsque vous forcez l'insertion d'une branche locale dans une branche distante, il est possible que vous perdiez des validations sur la branche
distante.

### Eclipse Orion Web IDE

1. Dans la section Modification du répertoire de travail, dans la section Sortant, cliquez sur la flèche située en regard de **Insérer**.
2. Cliquez sur **Forcer l'insertion de branche**.
3. Confirmez l'avertissement.

### Terminal Git

1. Entrez `git push <origine> <branche distante> -f` et appuyez sur Entrée.

## Elimination des contenus retirés de l'index de la branche locale active
{: #discard_changes}

### Eclipse Orion Web IDE
1. Dans la section Modifications du répertoire de travail, cochez la case pour chaque fichier modifié contenant des modifications que vous souhaitez éliminer.
2. Cliquez sur l'icône de réservation <img class="inline"  src="./images/discard.png" alt="Réserver les fichiers sélectionnés en annulant tous les changements">.

### Terminal Git
1. Entrez `git checkout -- chemin/d'accès/au/fichier/nom_de_fichier` pour éliminer toutes les modifications apportées à un fichier.

## Validation des fichiers et envoi par commande push à la branche distante
{: #commit}

### Eclipse Orion Web IDE
1. Dans la section Modifications du répertoire de travail, cochez la case de chaque fichier à valider.

3. Dans la zone **Entrez le message de validation**, tapez un message décrivant vos modifications.

  **Astuce **: fournissez un message de validation détaillé. Votre message doit fournir suffisamment de détails pour que quelqu'un puisse comprendre pourquoi la
modification était nécessaire sans information additionnelle. Vous pouvez inclure un lien vers un élément dans le dispositif de suivi de votre équipe pour aider. La première ligne du message de
validation doit contenir moins de 50 caractères. Ajoutez une ligne vierge avant d'ajouter le reste du texte.

4. Cliquez sur **Valider**.

5. Cliquez sur **Insérer**.

### Terminal Git
1. Entrez `git status` et appuyez sur Entrée.

2. Examinez les modifications à valider. Si tous vos fichiers à valider figurent dans la liste, vous pouvez continuer. Pour valider des fichiers avec retrait du contenu de l'index,
ajoutez-leur d'abord le contenu de l'index.

3. Entrez `git commit` et appuyez sur Entrée.

4. Entrez le récapitulatif de la validation, ajoutez une ligne vierge, puis entrez une description de la validation.

  **Astuce **: le récapitulatif de la validation ne doit pas dépasser 50 caractères. La description de la validation doit fournir suffisamment de détails pour que
quelqu'un puisse comprendre pourquoi la modification était nécessaire sans information additionnelle. Vous pouvez inclure un lien vers un élément dans le dispositif de suivi de votre équipe
pour aider.

5. Sauvegardez le message de validation.

  **Remarque :** pour sauvegarder votre message de validation et fermer Vim, qui est peut-être votre éditeur de texte par défaut, appuyez sur Echap, entrez
`:wq` et appuyez sur Entrée.

4. Entrez `git push` et appuyez sur Entrée.

## Affichage de l'historique de validation
{: #view_commit_history}

### Eclipse Orion Web IDE
1. Dans la section Branche active, développez **Historique** pour afficher l'historique de validation de cette branche.

  L'historique de validation peut également être affiché en tant que graphique visuel connecté.

1. Cliquez sur l'icône **bouton à bascule de représentation graphique** <img  class="inline" src="./images/graphicalhistoryicon.png" alt="Icône d'historique graphique">.

  Une fois le bouton activé, l'historique de validation et toutes les modifications entrantes ou sortantes pour une branche active s'affichent en tant que graphique connecté. La
représentation visuelle montre toutes les validations et toutes les branches sur lesquelles elles ont été effectuées.

  <img class="screen-shot" src="./images/visualhistoryexample.png" alt="Historique visuel des validations">

### Terminal Git
1. Entrez `git log` et appuyez sur Entrée.

2. Parcourez les validations du valideur.
 * Pour afficher plus d'entrées, appuyez sur Page avant.
 * Pour afficher les entrées précédentes, appuyez sur Page arrière.

3. Pour arrêter l'affichage des entrées, appuyez sur Q.

## Comparaison des modifications introduites par une validation
{: #compare_changes}

### Eclipse Orion Web IDE
1. Affichez votre historique des validations et localisez la validation. Pour plus d'informations, voir [ Afficher l'historique de validation](#view_commit_history).

2. Affichez les détails de la validation en cliquant dessus.

3. En regard d'un fichier, cliquez sur **>** et examinez les modifications du fichier.

  **Remarque :** si une validation a introduit une modification dans une ligne, la ligne d'origine est ombrée en rose et la nouvelle ligne est ombrée en vert.
De même, les lignes ajoutées par une validation sont ombrées en vert et les lignes supprimées par une validation sont ombrées en rose. 

### Terminal Git
1. Entrez `git log -p` et appuyez sur Entrée.

  **Remarque :** pour afficher uniquement un certain nombre de validations, entrez `git log -p -<nombre_de_validations_à_afficher>`.

2. Parcourez les validations.
 * Pour afficher plus d'entrées, appuyez sur Page avant.
 * Pour afficher les entrées précédentes, appuyez sur Page arrière.

3. Passez en revue les modifications.

  **Remarque :** si une validation a introduit un changement dans une ligne, le texte de la ligne d'origine apparaît en rouge et est précédé d'un signe moins (-). Le texte de la nouvelle ligne est affiché en vert et est précédé d'un signe plus (+). De même, le texte des lignes ajoutées par une validation est affiché en vert et est précédé d'un signe plus (+). 
Le texte des lignes supprimées par une validation est affiché en rouge et est précédé d'un signe moins (-). 

1. Pour arrêter l'affichage des entrées, appuyez sur Q.

## Modification de la dernière validation
{: #modify_last_commit}

  **Remarque :** lorsque vous modifiez la dernière validation avant de l'insérer dans un référentiel distant, vous réécrivez l'historique des validations. Ceci peut
causer des erreurs de validation et d'autres problèmes aux autres contributeurs de votre projet. Assurez-vous de ce que vous faîtes avant de modifier une validation envoyée par commande push à un référentiel distant.

### Eclipse Orion Web IDE
1. Cochez les cases correspondant aux éléments à ajouter à la validation. 

1. Cochez la case **Modifier la validation précédente**.

2. Si nécessaire, entrez un nouveau message de validation.

3. Cliquez sur **Valider**.

### Terminal Git
1. Vérifiez votre statut. Si nécessaire, ajoutez ou supprimez le contenu de l'index des fichiers.

2. Entrez `git commit --amend` et appuyez sur Entrée.

3. Dans votre éditeur de texte, acceptez ou modifiez le message de validation.

  **Remarque :** pour sauvegarder votre message de validation et fermer Vim, qui est peut-être votre éditeur de texte par défaut, appuyez sur Echap, entrez
`:wq` et appuyez sur Entrée.

## Etiquetage d'une validation
{: #tag_commit}

### Eclipse Orion Web IDE
1. Affichez votre historique des validations et localisez la validation. Pour plus d'informations, voir [ Afficher l'historique de validation](#view_commit_history).

2. Affichez les détails de la validation en cliquant dessus.

2. Dans le panneau de validation, cliquez sur **Créer une étiquette pour la validation** <img class="inline"  src="./images/tag.png" alt="Créer une étiquette pour la validation">.

3. Dans la zone de nom, entrez le texte de votre étiquette. Cliquez sur **Soumettre**.

### Terminal Git
1. Affichez l'historique de validation et obtenez l'ID de la validation à étiqueter. Pour plus d'informations, voir [Afficher l'historique de validation](#view_commit_history).

2. Entrez `git tag -a <texte_étiquette> <ID_validation>` et appuyez sur Entrée.

## Modification du nom et de l'adresse e-mail du valideur
{: #change_the_committer_name_and_email_address}

### Eclipse Orion Web IDE
1. Cliquez sur l'icône de configuration <img class="inline" src="./images/configurations.png" alt="Icône de configuration">.

3. Modifiez l'adresse e-mail et le nom de l'utilisateur en mettant à jour les valeurs user.email et user.name. Cliquez sur **Soumettre** pour enregistrer les modifications.

### Terminal Git
Pour mettre à jour votre nom et votre adresse e-mail pour un référentiel spécifique :

1. Entrez `git config user.email "<votre@e-mail.com>"` et appuyez sur Entrée.

2. Entrez `git config user.name "<votre nom>"` et appuyez sur Entrée.

Pour mettre à jour votre nom et votre adresse e-mail pour tous les référentiels :

1. Entrez `git config --global user.email "<votre@e-mail.com>"` et appuyez sur Entrée.

2. Entrez `git config --global user.name "<votre nom>"` et appuyez sur Entrée.

##Annulation d'une validation
{: #revert}

Annuler les modifications introduites par une validation dans votre branche active. 

### Eclipse Orion Web IDE

1. Sous historique, sélectionnez une validation.

2. Sur le côté droit de la page, au-dessus du récapitulatif de validation, cliquez sur l'icône Rétablir <img class="inline" src="./images/revert.png" alt="Icône Rétablir">.

### Terminal Git

1. Entrez `git revert <ID validation>` et appuyez sur Entrée.

## Fusion des modifications
{: #merge_changes}

Si vous avez besoin de distribuer des modifications d'une branche source à une branche de destination, vous devez d'abord les faire fusionner. Généralement, la branche source
est la branche dans laquelle vous avez effectué des changements et la branche de destination est votre branche maître.

### Eclipse Orion Web IDE
1. Sélectionnez les branches à fusionner.

2. Réservez la branche de destination. Pour plus d'informations, voir [ Utilisation d'une branche locale](#start_working_on_branch).

 <img class="screen-shot" src="./images/destinationbranch.png" alt="Réservation d'une branche de destination">

1. Cliquez sur la liste **Référence**, développez **local** et cliquez sur le nom de la branche source. Les modifications de la branche source
s'affichent dans la section Entrant.

  <img class="screen-shot" src="./images/sourcebranch.png" alt="Modifications de la branche source affichées dans la section Entrant">

1. Dans la section Entrant, cliquez sur l'icône **Fusionner** <img  class="inline" src="./images/mergeicon.png" alt="Icône de fusion dans la section Entrant">

1. Dans la liste **Référence**, cliquez sur l'icône de réservation situé en regard de la branche dans laquelle vous venez de faire fusionner les modifications.

1. Si vous souhaitez distribuer les modifications, cliquez sur **Insérer**. Sinon, vous pouvez maintenant créer un déploiement test afin de vous assurer que
tout fonctionne comme prévu.

### Terminal Git
1. Sélectionnez les branches à fusionner.

2. Réservez la branche de destination. Pour plus d'informations, voir [ Utilisation d'une branche locale](#start_working_on_branch).

3. Entrez `git merge <nom_source>` et appuyez sur Entrée.


## Résolution d'un conflit de fusion
{: #resolve_a_merge_conflict}

### Eclipse Orion Web IDE
1. Dans le panneau Fichiers modifiés, consultez la liste des fichiers contenant des conflits.

2. Dans l'interface Web IDE, ouvrez chaque fichier contenant des conflits.

3. Résolvez chaque modification créant un conflit.

  **Remarque :** supprimez tout le texte que vous ne souhaitez pas conserver. Chaque conflit a le format suivant :

		<<<<<<< EN-TETE
		Texte dans la branche réservée.
		=======
		Texte dans la branche fusionnée.
		>>>>>>> ID_validation_de_branche_fusionnée
4. Pour chaque fichier en conflit, cochez la case. Entrez un message de validation de fusion et cliquez sur **Valider**.

### Terminal Git
1. Passez en revue le message Git pour connaître le nom des fichiers contenant des conflits.

2. Dans un éditeur de texte, ouvrez un fichier contenant des conflits.

3. Résolvez chaque modification créant un conflit, puis enregistrez le fichier.

  **Remarque :** supprimez tout le texte que vous ne souhaitez pas conserver. Chaque conflit a le format suivant :

		<<<<<<< EN-TETE
		Texte dans la branche réservée.
		=======
		Texte dans la branche fusionnée.
		>>>>>>> branche_fusionnée
4. Ajoutez le contenu de l'index de chaque fichier que vous avez modifié, puis validez la fusion. 

## Resynchronisation des branches
{: #rebase_branches}

### Eclipse Orion Web IDE
1. Sélectionnez les branches à resynchroniser. Vous allez resynchroniser le contenu de la branche source dans la branche de destination. 

2. Réservez la branche de destination. Pour plus d'informations, voir [ Utilisation d'une branche locale](#start_working_on_branch).

1. Cliquez sur la liste **Référence**.

1. Cliquez sur le nom de de la branche source.

1. Dans la section Entrant, cliquez sur l'icône de resynchronisation <img  class="inline" src="./images/rebase.png" alt="Icône de resynchronisation">.

5. Si vous rencontrez des conflits, [résolvez-les](#resolve_a_rebase_conflict).

6. Répétez l'étape précédente autant de fois que nécessaire afin de finaliser l'opération de resynchronisation.

1. Cliquez sur la liste **Référence**, développez **origine** et cliquez sur le nom de la branche source.

1. Cliquez sur **Insérer**.

### Terminal Git
1. Réservez la branche à mettre à jour en tapant `git checkout <nom_branche_destination>` et en appuyant sur Entrée.

2. Entrez `git rebase <nom_branche_source>` et appuyez sur Entrée.

3. Si vous rencontrez des conflits, [résolvez-les](#resolve_a_rebase_conflict).

5. Répétez l'étape précédente autant de fois que nécessaire afin de finaliser l'opération de resynchronisation.

  **Remarque :** Pour arrêter l'opération de resynchronisation, entrez `git rebase --abort` et appuyez sur Entrée.

## Résolution d'un conflit de resynchronisation
{: #resolve_a_rebase_conflict}

### Eclipse Orion Web IDE
1. Dans la section Modifications du répertoire de travail, passez en revue la liste des fichiers en conflit.

2. Dans l'interface Web IDE, ouvrez chaque fichier contenant des conflits.

3. Résolvez chaque modification créant un conflit.

  **Remarque :** supprimez tout le texte que vous ne souhaitez pas conserver. Chaque conflit a le format suivant :

		<<<<<<< EN-TETE
		Texte dans la branche réservée.
		=======
		Texte dans la branche fusionnée.
		>>>>>>> ID_validation_de_branche_fusionnée
4. Dans le panneau de resynchronisation, cochez la case de tous les fichiers corrigés et cliquez sur **Continuer**.

### Terminal Git
1. Passez en revue le message Git pour connaître le nom des fichiers contenant des conflits.

2. Dans un éditeur de texte, ouvrez un fichier contenant des conflits.

3. Résolvez chaque modification créant un conflit, puis enregistrez le fichier.

  **Remarque :** supprimez tout le texte que vous ne souhaitez pas conserver. Chaque conflit a le format suivant :

		<<<<<<< EN-TETE
		Texte dans la branche réservée.
		=======
		Texte dans la branche fusionnée.
		>>>>>>> branche_fusionnée
4. Ajoutez le contenu de l'index de chaque fichier que vous avez modifié.

5. Reprenez l'opération de resynchronisation en tapant `git rebase --continue`, puis en appuyant sur Entrée.
