---

copyright:
  years: 2016

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}

# Exemple de capteur de terminal mobile

L'exemple de capteur de terminal mobile utilise JavaScript pour connecter votre téléphone à {{site.data.keyword.iot_full}} et publier des données de capteur sur votre organisation {{site.data.keyword.iot_short}}.
{:shortdesc}

La bibliothèque client Python de {{site.data.keyword.iot_short}} vous permet de vous abonner afin de recevoir des commandes et visualiser les données de capteur publiées par votre téléphone. La visualisation de données est présentée sur un site Web intégré dans l'infrastructure WSGI (Web Server Gateway Interface). 

Cette application illustre une approche permettant de contrôler l'accès des utilisateurs aux données de capteur à partir de certains terminaux. Lorsque vous cliquez sur **Let's Play**, l'application crée un enregistrement utilisateur dans une base de données {{site.data.keyword.cloudantfull}} et appelle l'API de gestion de terminaux {{site.data.keyword.iot_short}} pour l'enregistrement du terminal. 

## Conditions préalables

Avant de déployer cet exemple :

- Créez un compte {{site.data.keyword.bluemix_notm}} et connectez-vous. Pour plus d'informations sur {{site.data.keyword.bluemix_notm}}, voir [Begin your free trial](https://apps.admin.ibmcloud.com/manage/trial/bluemix.html).
- Téléchargez et installez l'interface de ligne de commande Cloud Foundry. Cette interface vous permet de modifier et déployer des instances de service sur {{site.data.keyword.bluemix_notm}}. Pour plus d'informations, voir [Commencer le codage à l'aide de l'interface de ligne de commande cf](https://www.ng.bluemix.net/docs/#starters/install_cli.html). 

## Déploiement de cet exemple

Pour déployer votre propre copie de cet exemple dans {{site.data.keyword.bluemix_notm}}, procédez comme suit :

1. Créez une nouvelle application Python dans {{site.data.keyword.bluemix_notm}}.
  a. Dans votre tableau de bord {{site.data.keyword.bluemix_notm}}, cliquez sur **Créer une application**, puis sur **Web**.
  b. Sélectionnez **Python**, puis cliquez sur **Continuer**.
  c. Choisissez un nom d'application, puis cliquez sur **Terminer**.
  Votre application Python est maintenant en cours de reconstitution. 
2. Créez une instance du service {{site.data.keyword.cloudant_short_notm}} NoSQL DB.
a. Dans votre tableau de bord {{site.data.keyword.bluemix_notm}}, cliquez sur **Utiliser des services ou des API**.
  b. Sélectionnez **Données et analyses** dans le menu, puis cliquez sur **Cloudant NoSQL DB**.
  c. Cliquez sur **Créer**.
3. Liez votre instance de {{site.data.keyword.cloudant_short_notm}} NoSQL DB et votre instance de {{site.data.keyword.iot_short}} à votre application Python.
a. Cliquez sur **Lier un service ou une API**.
  b. Sélectionnez votre service {{site.data.keyword.cloudant_short_notm}} NoSQL DB et votre instance {{site.data.keyword.iot_short}}, puis cliquez sur **Ajouter**.
4. Clonez le [{{site.data.keyword.iot_short}}référentiel Python Github](https://github.com/ibm-messaging/iot-python.git). Pour cloner le référentiel à partir d'une interface de ligne de commande, accédez au répertoire destiné à accueillir le clone de référentiel et exécutez la commande suivante : 
```
$ git clone https://github.com/ibm-messaging/iot-python.git
```
5. Dans l'interface de ligne de commande, changez de répertoire pour l'exemple de capteur de terminal mobile à l'aide de la commande suivante : 
```
$ cd iot-python/samples/bluemixZoneDemo
```
6. Insérez votre application dans {{site.data.keyword.bluemix_notm}} à l'aide de la commande suivante en remplaçant `app_name` par le nom de votre application Python :
```
$ cf push app_name -m 32M -b https://github.com/cloudfoundry/cf-buildpack-python.git -c "python server.py"
```
7. Ouvrez `http://app_name.mybluemix.net/` dans un navigateur Web sur votre téléphone. Une page doit s'afficher.

Une page s'affiche illustrant de quelle manière les données d'accéléromètre sont envoyées depuis votre téléphone à l'aide de la messagerie MQTT sur
<keyword conref="cloudoeconrefs.dita#cloudoeconrefs/iot_short"/> et de quelle façon une application 
<keyword conref="cloudoeconrefs.dita#cloudoeconrefs/bluemix_short"/> utilise ces données pour reproduire vos mouvements.
Entrez votre ID terminal, cliquez sur <uicontrol>Connexion</uicontrol>, puis lancez-vous et essayez de déplacer votre téléphone.
