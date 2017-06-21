---

copyright:
  years: 2017
lastupdated: "2017-03-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Conditions requises pour Delivery Insights
{: #prereqs}

Pour afficher des informations provenant de vos serveurs IBM UrbanCode Deploy dans {{site.data.keyword.DRA_short}}, vous devez héberger une instance de DevOps Connect sur un système qui peut se connecter à vos serveurs IBM UrbanCode Deploy. Ce système peut être un ordinateur physique ou une machine virtuelle. 
{:shortdesc}

Le système qui héberge DevOps Connect doit satisfaire les conditions requises suivantes :
- Le système doit disposer d'un environnement JRE (Java Runtime Environment) version 8 ou ultérieure.
- La variable `PATH` du système doit inclure l'emplacement du JRE.
- Le système doit autoriser DevOps Connect à créer des connexions sortantes vers IBM Bluemix.

Pour installer DevOps Connect et l'utiliser avec Delivery Insights, ouvrez le service DevOps Insights et cliquez sur **Settings > Delivery Insights Setup**.
