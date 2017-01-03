---

copyright:
  years: 2014, 2016
lastupdated: "2016-12-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Retrait de l'accès

Vous pouvez retirer l'accès qui a été accordé à un conteneur ou à un objet en utilisant les listes de contrôle d'accès.
{: shortdesc}

Pour retirer d'un conteneur une liste de contrôle d'accès en lecture, exécutez l'une des commandes suivantes :

Commande Swift :

  <codeblock>swift post <nom_conteneur> --read-acl “”</codeblock>

Commande cURL :

```
curl -i <URL_STOCKAGE_SE> -X POST -H "Content-Length: 0" -H "X-Container-Read: " -H "X-Auth-Token: <JETON_AUTH_SE>"
```
{: pre}

Pour retirer d'un conteneur une liste de contrôle d'accès en écriture, exécutez l'une des commandes suivantes :

    Commande Swift :

    ```
    swift post <nom_conteneur> --write-acl “”
    ```
    {: pre}

    Commande cURL :

    ```
    curl -i <URL_STOCKAGE_SE> -X POST -H "Content-Length: 0" -H "X-Container-Write: " -H "X-Auth-Token: <JETON_AUTH_SE>"
    ```
    {: pre}

Pour vérifier que vous avez retiré une liste de contrôle d'accès, exécutez l'une des commandes suivantes.

    Commande Swift :

    ```
    swift stat <nom_conteneur>
    ```
    {: pre}

    La sortie exemple suivante affiche des listes de contrôle d'accès vierges (Read ACL et Write ACL), ce qui indique que l'accès a été retiré.

    ```
             Account: AUTH_c727d7e248b448f6b268f31a1bd8691e
       Container: Test
         Objects: 1
           Bytes: 31512
        Read ACL:
       Write ACL:
         Sync To:
        Sync Key:
   Accept-Ranges: bytes
X-Storage-Policy: standard
     X-Timestamp: 1462818314.11220
      X-Trans-Id: txf04968bc9ef8431982b77-005772e34b
    Content-Type: text/plain; charset=utf-8
    ```
    {: screen}

    Commande cURL :
    ```
    curl -i <URL_STOCKAGE_SE> -I -H "X-Auth-Token:<JETON_AUTH_SE>"
    ```
    {: pre}
