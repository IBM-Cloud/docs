---

copyright:
  years: 2014, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Types d'accès

Les utilisateurs {{site.data.keyword.objectstorageshort}} peuvent être ou non des administrateurs. Les listes de contrôle d'accès sont activées par les administrateurs au niveau conteneur.
{: shortdesc}

<table>
<caption> Table 1. Rôles utilisateur définis </caption>
  <tr>
    <th> Utilisateurs administrateur (admin) </th>
    <th> Utilisateurs non administrateur (membre) </th>
  </tr>
  <tr>
    <td> Gèrent le contrôle d'accès </td>
    <td> Par défaut, n'ont pas d'accès au service ou à ses conteneurs </td>
  </tr>
  <tr>
    <td> Peuvent créer et supprimer des conteneurs </td>
    <td> Peuvent exécuter des actions basées sur les listes de contrôle d'accès en lecture/écriture des conteneurs </td>
  </tr>
  <tr>
    <td> Peuvent lire et écrire dans les conteneurs </td>
    <td> Peuvent effectuer les actions, comme défini par l'administrateur </td>
  </tr>
</table>


Vous pouvez gérer les utilisateurs {{site.data.keyword.objectstorageshort}} via l'interface utilisateur {{site.data.keyword.Bluemix_notm}}, l'API Cloud Foundry API ou l'interface de ligne de commande Cloud Foundry.
