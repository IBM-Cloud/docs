---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Tipi di accesso.

Gli utenti {{site.data.keyword.objectstorageshort}} possono essere sia amministrativi che non amministrativi. Gli elenchi del controllo dell'accesso vengono abilitati dagli utenti amministrativi al livello del contenitore.
{: shortdesc}

<table>
<caption> Tabella 1. Ruoli utente definiti </caption>
  <tr>
    <th> Utenti amministrativi (ammin) </th>
    <th> Utenti non amministrativi (membro) </th>
  </tr>
  <tr>
    <td> Gestisci il controllo dell'accesso </td>
    <td> Per impostazione predefinita, non si dispone dell'accesso al servizio o ai relativi contenitori </td>
  </tr>
  <tr>
    <td> Puoi creare e eliminare i contenitori </td>
    <td> Puoi eseguire azioni in base alle ACL di lettura/scrittura dei contenitori </td>
  </tr>
  <tr>
    <td> Puoi leggere e scrivere nei contenitori </td>
    <td> Puoi eseguire azioni come determinato dall'amministratore </td>
  </tr>
</table>


Puoi gestire gli utenti {{site.data.keyword.objectstorageshort}} tramite l'interfaccia utente {{site.data.keyword.Bluemix_notm}}, l'API o la CLI Cloud Foundry.
