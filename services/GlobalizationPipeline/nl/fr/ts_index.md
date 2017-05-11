---

copyright:
  years: 2015, 2017
lastupdated: "2016-08-30"

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Traitement des incidents liés à {{site.data.keyword.GlobalizationPipeline_short}}
{: #globalizationpipelinets}


Voici quelques réponses aux questions fréquemment posées au sujet de l'utilisation de {{site.data.keyword.GlobalizationPipeline_short}}. 
{:shortdesc}


## Le nom de mon application n'a pas été correctement traduit
{: #problem1}

Les traductions générées pour certaines chaînes ne correspondent pas à celles que vous aviez prévues.
{:shortdesc}

Lorsqu'un fichier de ressources est traduit, il est possible que les chaînes contenant des noms de produit ou d'autres noms propres ne soit pas correctement traduites.
{: tsSymptoms}

Il arrive souvent que les noms de produit ou les noms propres ne soient pas correctement traduits, surtout si le nom contient des mots réels. Lorsque ces types de mots et de phrases sont traduits, selon la signification de ces mots dans une langue donnée, le texte traduit peut avoir une signification différente de celle du nom anglais.
{: tsCauses}

Testez la traduction des noms de produit avant de les utiliser, et si vous constatez des problèmes, modifiez le texte ou la traduction en conséquence. Pour obtenir des conseils en matière de style rédactionnel lorsque vous utilisez la traduction automatique, consultez [Conseils en matière de traduction automatique](./tips.html#globalizationpipeline_tips).
{: tsResolve}



## Je ne parviens pas à télécharger un fichier de ressources
{: #problem2}

Le fichier de ressources que j'essaie de télécharger n'est pas accepté.
{:shortdesc}

Lorsque j'ajoute un fichier de ressources à un nouveau bundle de traduction ou que je mets à jour un fichier de ressources existant à traduire, je reçois une erreur.
{: tsSymptoms}

{{site.data.keyword.GlobalizationPipeline_short}} n'accepte que les fichiers de ressources des types suivants : .properties Java, JSON et AMD I18N.
{: tsCauses}

Assurez-vous que le fichier de ressources en cours de téléchargement est de l'un des types ci-dessous.
{: tsResolve}
* .properties Java
* JSON
* AMD I18N



## Je ne parviens pas à télécharger mon fichier de ressources car il est trop gros
{: #problem3}

Le fichier de ressources que j'essaie de télécharger n'est pas accepté.
{:shortdesc}

Lorsque j'ajoute ou que je mets à jour un fichier de ressources dans un projet de traduction, une erreur se produit car une partie du fichier est trop volumineuse.
{: tsSymptoms}

{{site.data.keyword.GlobalizationPipeline_short}} accepte uniquement les fichiers de ressources qui sont conformes à des exigences de taille bien définies.
{: tsCauses}

Assurez-vous que le fichier de ressource est conforme aux instructions suivantes :
{: tsResolve}
* Chaque clé peut comporter 256 caractères maximum.
* Chaque valeur peut comporter 2048 caractères maximum.
* Chaque projet de traduction peut contenir 500 paires clé/valeur maximum.
* La taille d'un fichier de ressources ne peut pas dépasser 2 Mo.




## L'espacement autour des variables contenues dans des chaînes n'est pas cohérent
{: #problem5}

L'espacement utilisé autour des variables après la traduction n'est pas toujours le même.
{:shortdesc}

L'espacement utilisé autour des variables contenues dans des chaînes n'est pas toujours cohérent d'une langue à l'autre après la traduction.
{: tsSymptoms}

Les moteurs de traduction automatique sont conçus pour fonctionner avec une langue naturelle et ils ne reconnaissent pas toujours ou ne savent pas toujours comment gérer une syntaxe spécifique utilisée par les langages de programmation. Par conséquent, le traitement d'une syntaxe qui est mélangée avec du texte brut peut varier.
{: tsCauses}

Actuellement, {{site.data.keyword.GlobalizationPipeline_short}} reconnaît le pattern "{}" fréquemment utilisé pour représenter des variables et préserve le format d'origine de leur contenu.
{: tsResolve}
