---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-15"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Configuration des règles de sécurité
{: #set_up_policies.md}

Lorsqu'un plan de sécurité avancée est utilisé pour une organisation, un analyste de sécurité peut configurer des règles de sécurité de connexion et des listes noires ou des listes blanches. Lorsqu'un plan standard est utilisé, l'analyste peut configurer des règles de connexion, avec moins d'options, et ne peut pas configurer des listes noires ou des listes blanches.

## Configuration des règles de connexion pour une sécurité avancée
{: #config_connect}

Vous pouvez définir le niveau de sécurité par défaut qui est appliqué à tous les terminaux. Vous pouvez ensuite ajouter des paramètres de sécurité personnalisés pour des terminaux spécifiques.

1. Sur la page **Règles**, cliquez sur **Configurer** en regard de **Sécurité de connexion**.
2. Sous **Sécurité d connexion par défaut**, sélectionnez le niveau de sécurité de connexion par défaut dans la liste déroulante. La valeur que vous sélectionnez ici s'applique à tous les terminaux, à l'exception des terminaux dotés de paramètres de connexion personnalisés. Ces règles affectent la façon dont les terminaux se connectent au serveur - elles ne modifient aucun paramètre sur le terminal même ou n'envoient aucun message sur le terminal. Vous pouvez sélectionner l'un des niveaux de sécurité suivants par défaut :
    - TLS facultatif
    - TLS avec authentification par jeton
    - TLS avec authentification par certificat client
    - TLS avec authentification par jeton et par certificat client
    - TLS avec certificat client ou jeton
3. Si nécessaire, cliquez sur **Ajouter une connexion personnalisée** et sélectionnez les types de terminaux et les niveaux de sécurité personnalisés. 
3. Cliquez sur **Actualiser la conformité**. En fonction du niveau de sécurité sélectionné, le tableau actualisé indique le nombre de terminaux concernés et le niveau de conformité prévu au niveau de sécurité défini.
4. Cliquez sur **Sauvegarder**.  

**Remarque :** Vous pouvez également accéder aux paramètres de sécurité de connexion sur la page **Général** sous **Paramètres**. Cliquez sur **Ouvrir la règle de sécurité de connexion**.

## Configuration des règles de connexion pour une sécurité standard
{: #config_connect}

Pour les organisations qui utilisent une sécurité standard, vous modifiez les paramètres de sécurité sur la page **Général** sous **Paramètres**. Vous pouvez définir le niveau de sécurité par défaut qui est appliqué à tous les terminaux.

1. Sous **Paramètres**, sélectionnez **Général**.
2. Sous **Sécurité de connexion**, sélectionnez le niveau de sécurité de connexion par défaut dans la liste déroulante. La valeur que vous sélectionnez ici s'applique à tous les terminaux. Ces règles affectent la façon dont les terminaux se connectent au serveur - elles ne modifient aucun paramètre sur le terminal même ou n'envoient aucun message sur le terminal. Vous pouvez sélectionner l'un des niveaux de sécurité suivants par défaut :
    - TLS facultatif
    - TLS avec authentification par jeton
    - TLS avec authentification par jeton et par certificat client
4. Cliquez sur **Sauvegarder**.  

## Configuration des listes noires et des listes blanches
{: #config_black_white}

Les organisations qui ont utilisé une sécurité avancée peuvent limiter l'accès au serveur à partir de certains terminaux à l'aide d'une liste noire, mais elles peuvent aussi utiliser une liste blanche pour accorder au serveur l'accès à certains terminaux. Vous pouvez utiliser une liste noire ou une liste blanche - elles ne peuvent pas être utilisées ensemble.

### Configuration d'une liste noire
{: #config_blacklist}

1. Sur la page **Règles** de sécurité, dans la section **Liste noire**, cliquez sur **Configurer**.
2. Sur la page **Liste noire**, cliquez sur **Ajouter à la liste noire**.
3. Dans la fenêtre **Ajouter à la liste noire**, effectuez l'une des opérations suivantes :
    - Dans l'onglet **Adresse IP/plage**, saisissez les adresses IP que vous souhaitez bloquer ou les plages d'adresses IP pour plusieurs terminaux consécutifs.
    - Dans l'onglet **CIDR**, entrez un bloc noté Classless Inter-Domain Routing (CIDR).
    - Dans l'onglet **Pays**, entrez ou sélectionnez les pays dont vous souhaitez bloquer tous les terminaux.
4. Dans la fenêtre **Ajouter à la liste noire**, cliquez sur **Sauvegarder**.
5. Consultez la liste des terminaux bloqués. Tous les terminaux figurant dans la liste, en fonction de l'adresse IP, du routage CIDR ou du pays, ne peuvent pas se connecter au serveur {{site.data.keyword.iot_short_notm}}.
6. Cliquez sur **Sauvegarder**.
7. Activez la liste noire. Si une liste blanche était activée, elle est désactivée.

### Configuration d'une liste blanche
{: #config_whitelist}

1. Sur la page **Règles** de sécurité, cliquez sur **Configurer** en regard de **Liste blanche**.
2. Sur la page **Liste blanche**, cliquez sur **Ajouter à la liste blanche**.
3. Dans la fenêtre **Ajouter à la liste blanche**, effectuez l'une des opérations suivantes :
    - Dans l'onglet **Adresse IP/plage**, saisissez les adresses IP dont vous souhaitez autoriser l'accès ou les plages d'adresses IP pour plusieurs terminaux consécutifs.
    - Dans l'onglet **CIDR**, entrez un bloc noté Classless Inter-Domain Routing (CIDR).
    - Dans l'onglet **Pays**, entrez ou sélectionnez les pays dont vous souhaitez autoriser l'accès de tous les terminaux.
4. Dans la fenêtre **Ajouter à la liste blanche**, cliquez sur **Sauvegarder**.
5. Consultez la liste des terminaux autorisés. Tous les terminaux figurant dans la liste, en fonction de l'adresse IP, du routage CIDR ou du pays, sont autorisés à se connecter au serveur {{site.data.keyword.iot_short_notm}}.
6. Cliquez sur **Sauvegarder**.
7. Activez la liste blanche. Si une liste noire était activée, elle est désactivée.
