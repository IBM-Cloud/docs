---

copyright:
  years: 2015,2016

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Gestion des risques et de la sécurité
{: #RM_security}
Dernière mise à jour : 15 novembre 2016
{: .last-updated}

Le module complémentaire de gestion des risques et de la sécurité permet aux organisations d'améliorer la sécurité d'IBM Watson IoT Platform en créant, appliquant et en signalant la sécurité des connexions des terminaux. Avec ce module complémentaire, les certificats et l'authentification TLS (Transport Layer security) sont utilisés, en plus des ID utilisateur et des jetons utilisés par Watson IoT Platform, pour déterminer comment et où les terminaux se connectent à la plateforme. Lors de la communication entre les terminaux et le serveur, tous les terminaux ne disposant pas de certificats valides avec accès au serveur, tels que configurés dans le module complémentaire Gestion des risques et de la sécurité, se voient refuser l'accès, même s'ils utilisent des ID utilisateur et des mots de passe valides.

**Remarque :** Pour vous inscrire et activer le programme bêta de gestion des risques et de la sécurité d'IBM Watson IoT Platform, accédez à https://developer.ibm.com/iotplatform/2016/11/02/experience-the-latest-iot-security-capabilities-sign-up-to-our-november-beta-today/.

## Règles de sécurité des connexions

Les règles de sécurité des connexions appliquent la façon dont les terminaux se connectent à la plateforme. Vous pouvez définir des règles de connexion par défaut pour tous les types de terminaux, ainsi que des paramètres personnalisés pour des types de terminaux spécifiques. Les règles peuvent être configurées pour autoriser des connexions non chiffrées, pour appliquer uniquement les connexions de sécurité de couche de transport (TLS) et pour permettre aux terminaux de s'authentifier avec des certificats côté client. Lorsque des certificats côté client sont utilisés, les règles de sécurité offrent une option supplémentaire consistant à n'utiliser que le certificat pour l'authentification client ou à utiliser une combinaison d'un certificat client et d'un ID client et d'une paire de jetons d'authentification.   

La sécurité de connexion peut également être configurée pour que les clients utilisent leur propre certificat côté serveur au lieu du certificat par défaut fourni. Cela peut être utile, par exemple, si les terminaux des utilisateurs vont authentifier le serveur pendant l'établissement de connexion TLS. Dans cette première version du module Gestion des risques et de la sécurité, le nom de domaine du serveur Watson IoT Platform ne peut pas être modifié et doit être utilisé tel quel dans le certificat du serveur.

## Certificats client

Pour configurer les certificats client et l'accès au serveur pour les terminaux, l'opérateur système importe les certificats d'autorité de certification (AC) associés et les certificats de serveur de messagerie dans la plateforme Watson IoT. L'analyste de sécurité configure ensuite les règles de sécurité de connexion afin que les connexions par défaut entre les terminaux et la plateforme utilisent les niveaux de sécurité Certificats seulement ou Certificats avec jetons d'authentification. L'analyste peut ajouter différentes règles pour différents types de terminaux.

## Règles de liste blanche et de liste noire

Les règles de liste blanche et de liste noire permettent de contrôler les emplacements à partir desquels les terminaux sont autorisés à se connecter au compte de l'organisation. Une liste noire identifie toutes les adresses IP, CIDR ou pays auxquels l'accès au serveur est refusé, tandis qu'une liste blanche donne un accès explicite à des adresses IP spécifiques.

## Tableau de bord de gestion des risques et de la sécurité

Enfin, l'opérateur système et l'analyste de sécurité peuvent utiliser le tableau de bord de Gestion des risques et de la sécurité pour afficher l'état de sécurité global. Les cartes du tableau de bord peuvent leur fournir une vue d'ensemble complète de la conformité, ainsi que l'état de connexion des terminaux.
