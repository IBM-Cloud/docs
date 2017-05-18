---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-13"

---

<!-- Attribute definitions -->
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

#{{site.data.keyword.streaminganalyticsshort}} traitement des incidents 
{: #ts_StreamingAnalytics}

Vous pouvez trouver des réponses aux questions courantes sur la façon d'utiliser {{site.data.keyword.streaminganalyticsshort}} sur {{site.data.keyword.Bluemix_short}}.
{:shortdesc}

##Quand je lance le service, il m'est demandé d'entrer des données d'identification pour me connecter à la console
{: #log_in_console}

Lorsque vous lancez {{site.data.keyword.streaminganalyticsshort}}, vous êtes invité à indiquer vos donnée d'identification pour la connexion à la console de service.
{:shortdesc}

Vous lancez un service {{site.data.keyword.streaminganalyticsshort}} que vous aviez créé précédemment, mais à la place d'un accès direct à la console de service, une page de connexion s'afficher, dans laquelle des données d'identification vous sont demandées.
{: tsSymptoms}

L'infrastructure de service a été mise à jour et le cache de votre navigateur empêche le service de récupérer la mise à jour.
{: tsCauses}

Effacez le cache de votre navigateur pour être sûr d'obtenir la dernière version de la console de service.
{: tsResolve}

##Mon application est défaillante
{: #app_unhealthy}

Vous ne pouvez exécuter correctement votre application si son état de santé est `défaillant`.
{:shortdesc}

Vous soumettez une application à l'instance de service, l'application démarre puis échoue immédiatement après, avec un état de santé à `défaillant`. L'erreur suivante apparaît dans le fichier journal : `/lib64/libc.so.6: version GLIBC_2.14 not found`.
{: tsSymptoms}

Vous n'avez pas compilé l'application en utilisant le système d'exploitation RHEL 6.5 ou une version CentOS équivalente.
{: tsCauses}

Vous devez recompiler votre application sous Red Hat Enterprise Linux (RHEL) 6.5 ou une version CentOS équivalente, utilisant des processeurs Intel.Soumettez à nouveau votre application à votre instance de service.
{: tsResolve}
