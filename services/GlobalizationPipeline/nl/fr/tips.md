---

copyright:
  years: 2015, 2017
lastupdated: "2016-07-12"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Conseils en matière de traduction automatique
{: #globalizationpipeline_tips}

*Dernière mise à jour : 12 juillet 2016*
{: .last-updated}

La traduction automatique peut s'avérer efficace lorsqu'il s'agit de proposer une traduction approximative de la signification du texte source. En revanche, la qualité et la pertinence de la traduction automatique varient considérablement selon la langue cible et le moteur de traduction automatique que vous utilisez. La qualité de la traduction automatique repose en grande partie sur la qualité du texte source lui-même. Il est fort probable qu'un texte source contenant beaucoup d'expressions familières, de phrases incomplètes, de ponctuations incorrectes et de termes et d'expressions ambigus ne soit pas traduit correctement.
{:shortdesc}

Lorsque vous créez votre interface utilisateur d'application {{site.data.keyword.Bluemix_notm}}, suivez quelques instructions de rédaction de base afin d'améliorer non seulement la qualité de votre langue source, mais également la qualité de la traduction automatique.

De plus, demandez à des interlocuteurs natifs de la langue cible de réviser et d'éditer la traduction automatique. Collectez également des commentaires auprès des utilisateurs de votre application, car ils sont probablement les mieux placés pour juger de la pertinence et de l'exactitude de la traduction.

## Conseils en matière de style rédactionnel
{: #writingstyletips}

* **Rédigez des phrases simples courte ou moyenne (entre 5 et 20 mots) :** Les moteurs de traduction automatique ont souvent des difficultés à traduire des phrases composées et complexes, y compris des phrases comportant des point-virgule. Transmettez une idée par phrase. Si une phrase contient deux verbes actifs pour transmettre deux idées, fractionnez-la en deux. Les moteurs de traduction automatique ont également des difficultés à effectuer l'analyse syntaxique des phrases qui sont trop courtes pour fournir suffisamment de contexte.
* **Evitez les expressions : ** Dans la mesure du possible, utilisez des phrases complètes. Les expressions sont admises pour les titres et les sous-titres, mais évitez d'utiliser un style télégraphique. Utilisez des phrases complètes pour introduire des listes.
* **Evitez les dictons, l'argot et le jargon : ** Remplacez les expressions dont la traduction littérale n'a aucun sens. Par exemple, remplacez "on the fly" par "dynamic," "on the other hand" par "alternatively" et "keep in mind" par "remember."
* **Evitez les traits d'humour et de sarcasme, les expressions familières, les émoticônes et les métaphores.**
* **Soyez succinct :** Supprimez tout texte inutile ou redondant. Par exemple, remplacez "It is useful to remember that large values increase the response time" par "Large values increase the response time."
* **Evitez d'écrire des phrases entières en majuscules :** La mise en majuscules fournit des indications sur la signification du mot. Par exemple, si vous écrivez "BILL", le moteur de traduction automatique ne peut pas déterminer s'il s'agit du nom "Bill" ou du mot "bill."
* **Evitez les mots ambigus :** Par exemple, n'utilisez pas "once" à la place de "after" ou "when." N'utilisez pas "while" à la place de "although" ou "whereas." N'utilisez pas "may" lorsque vous voulez dire "might" ou "can."
* **Evitez les pronoms :** Répétez les noms ou les groupes nominaux chaque fois que vous le pouvez. Le pronom "it" pose particulièrement problème.
* **Utilisez la voix active dans la mesure du possible :** Les phrases actives sont généralement plus claires que les phrases passives. Par exemple, écrivez "The utility determines which path is most efficient" au lieu de "The most efficient path is determined."
* **Evitez les informations d'ordre culturel.**
* **Gardez à l'esprit que les moteurs de traduction automatique sont susceptibles de traduire les noms de produit :** De nombreux pays conservent les noms de produit anglais d'origine, mais les moteurs de traduction automatique sont susceptibles d'essayer de traduire les noms de produit, en particulier si ces noms comportent des mots réels. Avant d'utiliser un nom de produit, testez sa traduction. Si vous constatez des problèmes, modifiez le texte ou la traduction en conséquence.
* **Assurez-vous que toutes les informations sont écrites dans une seule langue : ** Les moteurs de traduction automatique peuvent considérer que toutes les informations sont écrites dans une seule langue, même si le texte inclut un ou deux mots dans une autre langue. Par exemple, si le texte comporte l'expression "en route", le moteur de traduction automatique va tout de même essayer de traduire ces mots comme s'il s'agissait de mots anglais.
* **Evitez les slogans marketing :** Les slogans marketing reposent souvent sur la compréhension d'une culture spécifique de la part d'un public donné. Evitez ces types de slogan car les moteurs de traduction automatique ont souvent des difficultés à les traduire correctement.
* **Assurez-vous que les éléments de liste sont complets et parallèles : ** Par exemple, si un élément commence par un verbe, assurez-vous que tous les autres éléments commencent également par un verbe.
* **Evitez les termes please et thank you :** Ces mots peuvent sembler déplacés voir même condescendants dans certaines cultures.
* **Ecrivez les dates dans un format non numérique :** Les formats de date numériques varient selon les pays. Ecrivez le nom du mois, le jour et l'année. Par exemple, utilisez 1er septembre 2003 au lieu de 9/01/03, car cette représentation peut être interprétée par 1er septembre 2003 ou 9 janvier 2003.

## Conseils en matière de grammaire
{: #grammartips}

* **Utilisez la ponctuation adéquate : ** Le fait d'omettre des points et des virgules peut entraîner une mauvaise interprétation des informations de la part d'un moteur de traduction automatique.
* **Assurez-vous que les accords entre les sujets et les verbes sont respectés :** Assurez-vous que les verbes sont accordés au pluriel ou au singulier respectivement avec des sujets au pluriel ou au singulier.
* **Utilisez le présent simple : ** De nombreuses langues ne sont pas dotées des propriétés verbales de l'anglais, telles que les voix et les temps. Dans la mesure du possible, évitez d'avoir recours au futur et au passé. Par exemple, vous pouvez remplacer "If you run this program, DB2® will return an error message" par "If you run this program, DB2 returns an error message."
* **Assurez-vous que les accords entre les pronoms et les antécédents sont respectés : ** Par exemple, "A user should first determine their tasks" pourrait être remplacé par "Users should first determine their tasks.".
* **Evitez les modificateurs détachés : ** Placez correctement les modificateurs pour qu'ils modifient le nom approprié. Par exemple, "While typing in commands, the program does not send any messages to you" pourrait être remplacé par "While typing in commands, you do not receive any messages from the program."
* **Evitez les double négations :** Par exemple, "Do not omit the date" pourrait être remplacé par "Include the date."
* **Evitez l'emploi de l'infinitif, du participe présent et du participe passé pour les verbes placés en début de phrase : ** Ces formes verbales sont souvent ambiguës et difficiles à traduire.
* **Evitez les chaînes nominales : ** Limitez les groupes nominaux composés, tels que "special filter factor estimate considerations," à trois mots maximum.
* **Evitez d'utiliser des mots associés à plusieurs catégories grammaticales : ** En anglais, de nombreux mots, tels que "default," peuvent être un nom ou un verbe. Cette structure n'existe pas dans un grand nombre d'autres langues. Soyez cohérent dans la façon dont vous utilisez chaque mot. Par exemple, utilisez toujours "default" comme un nom.
* **Assurez-vous que les éléments énumérés dans une phrase sont parallèles :** Par exemple, n'utilisez que des noms ou que des verbes pour les éléments énumérés dans une phrase ; ne mélangez pas des noms et des verbes.
* **N'omettez pas les mots qui sont nécessaires :** Par exemple, à la place de "The file names are displayed in uppercase characters and the file extensions in lowercase," utilisez "The file names are displayed in uppercase characters and the file extensions are displayed in lowercase characters." Utilisez le mot "that" pour apporter une clarification si besoin est. Par exemple, remplacez "If you determine the problem is a missing file" par "If you determine that the problem is a missing file."
* **N'utilisez pas un tiret pour marquer une pause :** Par exemple, n'écrivez pas "When you get to this point - the point when all data has been loaded - you need to test the system." Remplacez les tirets par des virgules ou reformulez la phrase.
 
## Conseils en matière de terminologie
{: #terminologytips}

* **Utilisez une terminologie cohérente : ** Evitez d'avoir recours à plusieurs termes pour désigner la même chose. Evitez d'utiliser un seul terme pour faire référence à plusieurs choses.
* **Ajoutez des explications pour les termes spécialisés.**
* **Evitez d'utiliser des termes qui ont des significations différentes dans d'autres environnements et contextes :** Ces termes sont notamment "billion," "domestic," et "foreign."
* **Adoptez une ligne cohérente et normalisée pour la mise en majuscules, l'emploi des traits d'union et la formation des mots :** Par exemple, écrivez "fix pack" au lieu de "fix pack".
* **Utilisez des minuscules sauf pour les noms propres.**
* **Evitez les symboles spéciaux :** Si vous devez utiliser le symbole #, n'employez pas le signe dièse. Utilisez plutôt le symbole du numéro (#).
* **Evitez les abréviations :** Les moteurs de traduction automatique sont susceptibles de reconnaître les abréviations courantes, telles qu'IBM et DB2, mais ils ne peuvent pas toutes les reconnaître. Dans la mesure du possible, évitez d'avoir recours aux abréviations. N'utilisez pas les abréviations latines, telles que "i.e." et "etc."

## Conseils en matière de ponctuation
{: #punctuationtips}

* **Evitez d'utiliser une barre oblique pour signifier "and or" :** Reformulez la phrase pour indiquer la signification exacte. Par exemple, vous pouvez reformuler "You can view the draft copy and/or the review copy" par "You can view the draft copy, the review copy, or both."
* **N'indiquez pas de pluriel en ajoutant (s) :** Utilisez l'expression "one or more" ou utilisez le pluriel uniquement.
* **N'utilisez pas de perluète (&) pour signifier "and".**
* **Utilisez des virgules pour séparer les éléments énumérés dans une phrase et placez une virgule avant la conjonction : ** Par exemple, "Select your company, location, and profession."

## Conseils en matière d'orthographe
{: #spellingtips}

* **Vérification orthographique :** Les mots mal orthographiés peuvent entraîner des erreurs de traduction. Vérifiez toujours que vous n'avez pas fait de fautes d'orthographe.
* **Utilisez une orthographe cohérente :** Assurez-vous que les termes, acronymes et noms propres sont toujours orthographiés de la même manière, y compris pour l'emploi des majuscules et des minuscules.

## Conseils en matière de présentation visuelle
{: #visualtips}

* **Evitez d'insérer du texte dans les graphiques.**
* **Evitez d'utiliser un formatage pour la mise en évidence.**

