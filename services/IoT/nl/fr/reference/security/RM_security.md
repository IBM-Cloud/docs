---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-07"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Gestion des risques et de la sécurité
{: #RM_security}

 Le module complémentaire de gestion des risques et de la sécurité permet aux organisations d'améliorer la sécurité d'{{site.data.keyword.iot_full}} en créant, en appliquant et en signalant la sécurité des connexions des terminaux. Avec ce module complémentaire, les certificats et l'authentification TLS (Transport Layer security) sont utilisés, en plus des ID utilisateur et des jetons utilisés par {{site.data.keyword.iot_short_notm}}, pour déterminer comment et où les terminaux se connectent à la plateforme. Lors de la communication entre les terminaux et le serveur, tous les terminaux ne disposant pas de certificats valides avec accès au serveur, tels que configurés dans le module complémentaire Gestion des risques et de la sécurité, se voient refuser l'accès, même s'ils utilisent des ID utilisateur et des mots de passe valides.

## Règles de sécurité des connexions
{: #connect_policy}

Les règles de sécurité des connexions appliquent la façon dont les terminaux se connectent à la plateforme. Vous pouvez définir des règles de connexion par défaut pour tous les types de terminaux, ainsi que des paramètres personnalisés pour des types de terminaux spécifiques. Les règles peuvent être configurées pour autoriser des connexions non chiffrées, pour appliquer uniquement les connexions de sécurité de couche de transport (TLS) et pour permettre aux terminaux de s'authentifier avec des certificats côté client. Lorsque des certificats côté client sont utilisés, les règles de sécurité offrent une option supplémentaire consistant à n'utiliser que le certificat pour l'authentification client ou à utiliser une combinaison d'un certificat client et d'un ID client et d'une paire de jetons d'authentification.

Pour plus d'informations sur la configuration des règles de sécurité de connexion, voir [Configuration des règles de sécurité](set_up_policies.html).

La sécurité de connexion peut également être configurée pour que les clients utilisent leur propre certificat côté serveur au lieu du certificat par défaut fourni. Cela peut être utile, par exemple, si les terminaux des utilisateurs vont s'authentifier auprès du serveur pendant l'établissement de connexion TLS. Dans cette première version du module Gestion des risques et de la sécurité, le nom de domaine du serveur {{site.data.keyword.iot_short_notm}} ne peut pas être modifié et doit être utilisé tel quel dans le certificat du serveur.

## Certificats client
{: #certificates}

Pour configurer les certificats client et l'accès au serveur pour les terminaux, l'opérateur système importe les certificats d'autorité de certification (AC) associés et les certificats de serveur de messagerie dans la plateforme {{site.data.keyword.iot_short_notm}}. L'analyste de sécurité configure ensuite les règles de sécurité de connexion afin que les connexions par défaut entre les terminaux et la plateforme utilisent les niveaux de sécurité Certificats seulement ou Certificats avec jetons d'authentification. L'analyste peut ajouter différentes règles pour différents types de terminaux.

Pour plus d'informations sur la configuration des certificats, voir [Configuration des certificats](set_up_certificates.html).

## Règles de liste noire et de liste blanche
{: #wl_bl}

Les règles de liste noire et de liste blanche permettent de contrôler les emplacements à partir desquels les terminaux sont autorisés à se connecter au compte de l'organisation. Une liste noire identifie toutes les adresses IP, CIDR ou pays auxquels l'accès au serveur est refusé, tandis qu'une liste blanche donne un accès explicite à des adresses IP spécifiques.

Pour plus d'informations sur la configuration des règles de liste noire et de liste blanche, voir [Configuration des listes noires et des listes blanches](set_up_policies.html#config_black_white).

## Tableau de bord de gestion des risques et de la sécurité
{: #dashboard}

Enfin, l'opérateur système et l'analyste de sécurité peuvent utiliser le tableau de bord de Gestion des risques et de la sécurité pour afficher l'état de sécurité global. Les cartes du tableau de bord peuvent leur fournir une vue d'ensemble complète de la conformité, ainsi que l'état de connexion des terminaux.
