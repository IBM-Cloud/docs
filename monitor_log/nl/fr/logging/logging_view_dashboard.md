---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-27"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Analyse de journaux depuis la console Bluemix
{: #analyzing_logs_bmx_ui}

Dans {{site.data.keyword.Bluemix}}, vous pouvez visualiser, filtrer et analyser des journaux via l'onglet Journaux disponible pour chaque application Cloud Foundry ou conteneur Docker.
{:shortdesc}

L'environnement {{site.data.keyword.Bluemix_notm}} Public inclut des capacités de journalisation intégrées. Par exemple, lorsque vous exécutez vos applications dans Cloud Foundry (CF), les données de journal sont capturées depuis les composants système qui interagissent avec votre application, ceux de votre application, et même au sein de votre application, lorsque vous utilisez les flux stdout et stderr.

Prenez en compte les informations suivantes sur la disponibilité des données de journal pour analyse et sur la conservation des journaux :

* Dans {{site.data.keyword.Bluemix_notm}} Public, les données de journal sont conservées par défaut pendant 7 jours. 
* Vous pouvez stocker jusqu'à 1 Go de données par jour. 
* Par défaut, les journaux disponibles pour analyse depuis la console {{site.data.keyword.Bluemix_notm}} sont celles des dernières 24 heures.

**Conseil :** pour analyser des données pour une période personnalisée antérieure aux dernières 24 heures, voir [Analyse de journal avancée avec Kibana](logging_analyzing_logs_Kibana.html#analyzing_logs_Kibana). 

##  Accès aux journaux d'une application Cloud Foundry
{: #launch_logs_tab_bmx_ui_cf}

Pour consulter les journaux de déploiement ou d'exécution d'une application Cloud Foundry, procédez comme suit :

1. Dans le tableau de bord Applications, cliquez sur le nom de votre application Cloud Foundry. 
    
2. Dans la page des informations d'application détaillées, cliquez sur **Journaux**.
    
    Depuis l'onglet **Journaux**, vous pouvez visualiser les journaux récents de votre application ou suivre des journaux en temps réel. De plus, vous pouvez filtrer les journaux par composant (type de journal), par ID d'instance d'application et par erreur.
    

##  Accès aux journaux d'un conteneur Docker
{: #launch_logs_tab_bmx_ui_containers}

Pour consulter les journaux de déploiement ou d'exécution d'un conteneur Docker, procédez comme suit :

1. Dans le tableau de bord Applications, cliquez sur le nom du conteneur unique ou du groupe de conteneurs. 
    
2. Dans la page des informations d'application détaillées, cliquez sur **Surveillance et journaux**.

3. Sélectionnez l'onglet **Journalisation**.
    
    Depuis l'onglet **Journalisation**, vous pouvez visualiser les journaux récents de votre conteneur ou suivre des journaux en temps réel. 

## Format de journal d'application CF
{: #log_format_cf}

Les journaux des applications {{site.data.keyword.Bluemix_notm}} Cloud Foundry sont affichés sous un format fixe, similaire au schéma suivant :

<code><var class="keyword varname">Component</var>/<var class="keyword varname">ID_instance</var>/<var class="keyword varname">message</var>/<var class="keyword varname">horodatage</var></code>

Chaque entrée de journal comporte les zones suivantes :

| Zone | Description |
|-------|-------------|
| Horodatage | Date et heure de l'instruction de journal. L'horodatage est défini à la milliseconde près. |
| Composant | Composant qui génère le journal. Pour la liste des différents composants, voir [Sources de journal pour les applications CF](logging_cf_apps.html#logging_bluemix_cf_apps_log_sources). <br> Chaque type de composant est suivi d'une barre oblique et d'un chiffre qui indique l'instance d'application. 0 est le chiffre attribué à la première instance, 1 est le chiffre attribué à la  deuxième instance, etc. |
| Message | Message émis par le composant. Il varie selon le contexte. |
{: caption="Tableau 1. Zones d'entrée de journal d'une application CF" caption-side="top"}


## Format des journaux de conteneur
{: #log_format_containers}

Les journaux des conteneurs sont affichés dans un format fixe, similaire au schéma suivant :

<code><var class="keyword varname">horodatage</var>/<var class="keyword varname">machine</var>/<var class="keyword varname">message</var>  </code>

Chaque entrée de journal comporte les zones suivantes :

| Zone | Description |
|-------|-------------|
| Date/Heure | Date et heure de l'instruction de journal. L'horodatage est défini à la milliseconde près. |
| Machine | Nom de l'hôte sur lequel s'exécute le conteneur. |
| Message | Message émis. Varie selon le contexte. |
{: caption="Tableau 2. Zones d'entrée de journal de conteneur Docker" caption-side="top"}

