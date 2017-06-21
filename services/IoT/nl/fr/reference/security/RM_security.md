---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-17"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Gestion des risques et de la sécurité
{: #RM_security}

Vous pouvez améliorer la sécurité pour activer la création, l'application et la génération de rapports sur la sécurité de connexion des terminaux. Avec cette sécurité avancée, les certificats et l'authentification TLS (Transport Layer security) sont utilisés, en plus des ID utilisateur et des jetons utilisés par {{site.data.keyword.iot_short_notm}}, pour déterminer comment et où les terminaux se connectent à la plateforme. Lorsque des certificats sont activés, lors de la communication entre les terminaux et le serveur, tous les terminaux ne disposant pas de certificats valides, tels que configurés dans les paramètres de sécurité, se voient refuser l'accès, même s'ils utilisent des ID utilisateur et des mots de passe valides.

## Certificats client
{: #certificates}

Pour configurer les certificats client et l'accès au serveur pour les terminaux, l'opérateur système importe les certificats d'autorité de certification (AC) associés et les certificats de serveur de messagerie dans la plateforme {{site.data.keyword.iot_short_notm}}. L'analyste de sécurité configure ensuite les règles de sécurité de connexion afin que les connexions par défaut entre les terminaux et la plateforme utilisent les niveaux de sécurité Certificats seulement ou Certificats avec jetons d'authentification. L'analyste peut ajouter différentes règles pour différents types de terminaux.

Pour plus d'informations sur la configuration des certificats, voir [Configuration des certificats](set_up_certificates.html).

## Plans d'organisation et règles de sécurité
Les règles de sécurité améliorées permettent aux organisations de déterminer la façon dont ils souhaitent que les terminaux se connectent et soient authentifiés sur la plateforme en utilisant des règles de connexion et des règles de liste noire et de liste blanche. Les options de règle de sécurité qui sont disponibles sur une organisation dépendent du type de plan de l'organisation, comme suit :

**Plan standard :**
- Les opérateurs système peuvent configurer des règles de connexion à l'aide des options suivantes :
    - TLS facultatif 
    - TLS avec authentification par jeton
    - TLS avec authentification par jeton et par certificat client

**Plan de sécurité avancée ou plan léger :** 
- Les opérateurs système peuvent configurer des règles de connexion à l'aide des options suivantes :
    - TLS facultatif 
    - TLS avec authentification par jeton
    - TLS avec authentification par certificat client
    - TLS avec authentification par jeton et par certificat client
    - TLS avec certificat client ou jeton
- Les opérateurs système peuvent configurer des listes noires ou des listes blanches.

## Règles de connexion
{: #connect_policy}

Les règles de connexion contrôlent le mode de connexion des terminaux à la plateforme. Vous pouvez configurer des règles de connexion par défaut pour tous les types de terminaux et créer des paramètres personnalisés pour des types de terminaux spécifiques. Les règles peuvent être configurées pour autoriser des connexions non chiffrées, pour appliquer uniquement les connexions de sécurité de couche de transport (TLS) et pour permettre aux terminaux de s'authentifier avec des certificats côté client.

Pour plus d'informations sur la configuration des règles de sécurité de connexion, voir [Configuration des règles de sécurité](set_up_policies.html).

La sécurité de connexion peut également être configurée pour que les opérateurs système puissent utiliser leur propre certificat de serveur de messagerie au lieu du certificat par défaut fourni. L'utilisation d'un certificat de serveur de messagerie personnalisé peut être utile si les terminaux des utilisateurs seront authentifiés auprès du serveur pendant l'établissement de connexion TLS. Seuls les certificats de serveur de messagerie personnalisé qui utilisent le même domaine que le serveur de messagerie IoTP d'origine (<orgId>.messaging.internetofthings.ibmcloud.com) sont pris en charge.

## Règles de liste noire et de liste blanche
{: #wl_bl}

Les règles de liste noire et de liste blanche permettent de contrôler les emplacements à partir desquels les terminaux sont autorisés à se connecter au compte de l'organisation. Une liste noire identifie toutes les adresses IP, CIDR ou pays auxquels l'accès au serveur est refusé, tandis qu'une liste blanche donne un accès explicite à des adresses IP spécifiques.

Pour plus d'informations sur la configuration des règles de liste noire et de liste blanche, voir [Configuration des listes noires et des listes blanches](set_up_policies.html#config_black_white).

## Tableau de bord de gestion des risques et de la sécurité
{: #dashboard}

Enfin, l'opérateur système et l'analyste de sécurité peuvent utiliser le tableau de bord de Gestion des risques et de la sécurité pour afficher l'état de sécurité global. Les cartes du tableau de bord peuvent leur fournir une vue d'ensemble complète de la conformité, ainsi que l'état de connexion des terminaux.
