---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-21"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Utilisation du package Alarm
{: #openwhisk_catalog_alarm}

Le package `/whisk.system/alarms` peut être utilisé pour exécuter un déclencheur à une fréquence spécifiée. Il peut être utile pour configurer des tâches ou des travaux récurrents, comme l'appel d'une action de sauvegarde du système toutes les heures.

Le package inclut le flux ci-dessous.

| Entité | Type | Paramètres | Description |
| --- | --- | --- | --- |
| `/whisk.system/alarms` | package | - | Alarmes et utilitaire périodique |
| `/whisk.system/alarms/alarm` | flux | cron, trigger_payload, maxTriggers | Exécuter un événement déclencheur régulièrement |


## Exécution régulière d'un événement déclencheur
{: #openwhisk_catalog_alarm_fire}

Le flux `/whisk.system/alarms/alarm` configure le service Alarm pour exécuter un événement déclencheur à une fréquence spécifiée. Les paramètres sont les suivants :

- `cron` : chaîne basée sur la syntaxe crontab UNIX, qui indique quand déclencher la tâche périodique (en temps universel coordonné). Il s'agit d'une séquence de cinq zones séparées par un espace : `X X X X X`.
Pour plus d'informations sur l'utilisation de la syntaxe cron, voir : http://crontab.org. Voici quelques exemples de la fréquence indiquée par la chaîne :

  - `* * * * *` : au début de chaque minute.
  - `0 * * * *` : au début de chaque heure.
  - `0 */2 * * *` : toutes les 2 heures (c'est-à-dire 02:00:00,
04:00:00, ...)
  - `0 9 8 * *` : à 9:00:00 du matin (UTC) le huitième jour de chaque mois.

- `trigger_payload` : la valeur de ce paramètre devient le contenu du déclencheur à chaque fois que le déclencheur est exécuté.

- `maxTriggers` : l'exécution de déclencheurs s'arrête lorsque cette limite est atteinte. La valeur par défaut est 1 000 000. Vous pouvez définir cette limite sur l'infini (-1).

Voici un exemple de création de déclencheur qui sera exécuté toutes les 2 minutes avec les valeurs `name` et `place` dans l'événement déclencheur :

  ```
  wsk trigger create periodic \
    --feed /whisk.system/alarms/alarm \
    --param cron "*/2 * * * *" \
    --param trigger_payload "{\"name\":\"Odin\",\"place\":\"Asgard\"}"
  ```
  {: pre}

Chaque événement généré inclut sous forme de paramètres les propriétés spécifiées dans la valeur `trigger_payload`. Dans ce cas, chaque événement déclencheur possède les paramètres `name=Odin` et `place=Asgard`.

**Remarque** : Le paramètre `cron` prend également en charge une syntaxe personnalisée de six zones, dans laquelle la sixième zone représente les secondes. 
Pour plus de détails sur l'utilisation de cette syntaxe cron personnalisée, voir : https://github.com/ncb000gt/node-cron. 
Voici un exemple d'utilisation de la notation sur six zones :
  - `*/30 * * * * *` : toutes les trente secondes.

