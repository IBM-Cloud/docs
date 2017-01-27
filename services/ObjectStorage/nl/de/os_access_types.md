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


# Zugriffstypen

{{site.data.keyword.objectstorageshort}}-Benutzer können Benutzer mit Administratorberechtigungen oder Benutzer ohne Administratorberechtigungen sein. Zugriffssteuerungslisten werden durch Administratorbenutzer auf der Containerebene aktiviert.
{: shortdesc}

<table>
<caption> Tabelle 1. Definierte Benutzerrollen</caption>
  <tr>
    <th> Benutzer mit Administratorberechtigungen (admin) </th>
    <th> Benutzer ohne Administratorberechtigungen (member) </th>
  </tr>
  <tr>
    <td> Zugriffssteuerung verwalten </td>
    <td> Standardmäßig kein Zugriff auf den Service oder seine Container </td>
  </tr>
  <tr>
    <td> Container erstellen und löschen </td>
    <td> Aktionen abhängig von den Lese-/Schreibzugriffssteuerungslisten der Container </td>
  </tr>
  <tr>
    <td> Containerinhalt lesen und schreiben </td>
    <td> Durch den Administrator festgelegte Aktionen </td>
  </tr>
</table>


Sie können {{site.data.keyword.objectstorageshort}}-Benutzer über die {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle, die Cloud Foundry-API oder die Cloud Foundry CLI verwalten.
