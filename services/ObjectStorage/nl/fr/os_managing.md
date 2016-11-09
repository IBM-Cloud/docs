---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Gestion d'{{site.data.keyword.objectstorageshort}} dans les différentes régions{: #multi-regions}
*Dernière mise à jour : 19 octobre 2016*
{: .last-updated}

Le service {{site.data.keyword.objectstorageshort}} prend en charge les régions de stockage Dallas et Londres. Ces régions de stockage sont indépendantes de la région {{site.data.keyword.Bluemix_notm}} (Sud des Etats-Unis ou Royaume-Uni, par exemple) dans laquelle l'instance de service {{site.data.keyword.objectstorageshort}} est créée. Si vous créez une instance dans la région {{site.data.keyword.Bluemix_notm}} Sud des Etats-Unis, vous pouvez lire et écrire des données dans l'une des deux régions de stockage, Dallas ou Londres.
{: shortdesc}

Pour la région {{site.data.keyword.Bluemix_notm}} Sud des Etats-Unis, la région de stockage Dallas est le paramètre par défaut. Pour la région {{site.data.keyword.Bluemix_notm}} Royaume-Uni, la région de stockage par défaut est Londres.  L'interface utilisateur {{site.data.keyword.objectstorageshort}} se lance toujours sur la région de stockage par défaut de la région {{site.data.keyword.Bluemix_notm}} utilisée. Pour changer de région, cliquez sur la liste déroulante Région {{site.data.keyword.objectstorageshort}} et choisissez une autre région.

**Remarque :** le service {{site.data.keyword.objectstorageshort}} NE prend PAS en charge la réplication sur différentes régions de stockage.

### Accès multi-région

Pour utiliser le service {{site.data.keyword.objectstorageshort}}, vous devez [vous authentifier auprès
d'OpenStack Keystone](../ObjectStorage/os_security.html#keystone-authentication){: new_window}. Une fois authentifié, un jeton X-Subject-Token et des noeuds finaux {{site.data.keyword.objectstorageshort}} seront disponibles dans la réponse. Chaque région de stockage dispose d'un [point d'accès](../ObjectStorage/os_api.html#access-points) différent.


Ainsi, pour créer un conteneur intitulé `my_container` dans la région de stockage Dallas, spécifiez un point d'accès Dallas dans la commande curl, comme suit :

  ```
  curl -i https://dal.objectstorage.open.softlayer.com/v1/AUTH_3c9c89a2edbb458da74a9e81e215da9e/my_container -X PUT -H "Content-Length: 0" -H "X-Auth-Token: gAABAABWlw4mwttbb_6G3LnTiGusyoOSEFMG7oTnDYWN1vBZB6XAxUEhe4ehGkdw6Qm_I9ZFFXr8fwcc2KaEbpWbQoglhAvrYTXbrkn8MvErLdnbcT0XK2t5L7lEZyyKQlsgmQWcrch9VOO_OiSKKToORZR7luI-2TrR_JIVZm-8AAS7hLhl9"
  ```
  {: pre}
Vous recevez le code suivant en sortie :

  ```
  HTTP/1.1 201 Created
  Content-Length: 0
  Content-Type: text/html; charset=UTF-8
  X-Trans-Id: tx4a640ca81c7240ea8f812-00569712fc
  Date: Thu, 14 Jan 2016 03:16:13 GMT
  ```
  {: screen}

Pour créer un conteneur intitulé `my_container` dans la région de stockage Londres, spécifiez un point d'accès Londres dans la commande curl, comme suit :

  ```
  curl -i https://lon.objectstorage.open.softlayer.com/v1/AUTH_3c9c89a2edbb458da74a9e81e215da9e/my_container -X PUT -H "Content-Length: 0" -H "X-Auth-Token: gAABAABWlw4mwttbb_6G3LnTiGusyoOSEFMG7oTnDYWN1vBZB6XAxUEhe4ehGkdw6Qm_I9ZFFXr8fwcc2KaEbpWbQoglhAvrYTXbrkn8MvErLdnbcT0XK2t5L7lEZyyKQlsgmQWcrch9VOO_OiSKKToORZR7luI-2TrR_JIVZm-8AAS7hLhl9"
  ```
  {: pre}
Vous recevez le code suivant en sortie :

  ```
  HTTP/1.1 201 Created
  Content-Length: 0
  Content-Type: text/html; charset=UTF-8
  X-Trans-Id: tx4a640ca81c7240ea8f812-00569712fc
  Date: Thu, 14 Jan 2016 03:16:13 GMT
  ```
  {: screen}

**Remarque :** le jeton `X-Subject-Token` acquis depuis Keystone, libellé en tant que `X-Trans-ID` dans l'exemple, fonctionne dans les différentes régions de stockage.
