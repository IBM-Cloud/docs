---

 

copyright:

  years: 2015，2016

 

---

{:shortdesc: .shortdesc}

# Services VCAP

*Dernière mise à jour : 15 mars 2016*


La variable d'environnement VCAP_SERVICES est un objet JSON qui contient des informations que vous pouvez utiliser pour interagir avec une
instance de service dans {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}


## Extraction de la valeur de la variable d'environnement VCAP_SERVICES
{:retrieving}

La variable d'environnement VCAP_SERVICES est un objet JSON qui contient des informations que vous pouvez utiliser pour interagir avec une
instance de service dans {{site.data.keyword.Bluemix_notm}}. Ces informations incluent le nom de l'instance de service et l'adresse URL de connexion à l'instance de service. Les valeurs sont remplies dans la variable d'environnement VCAP_SERVICES lorsque votre application est liée à une instance de service dans
{{site.data.keyword.Bluemix_notm}}.

La valeur de la variable d'environnement VCAP_SERVICES n'est disponible que lorsque vous liez une instance de service à votre application. Vous pouvez afficher les variables d'environnement de l'application avec la commande suivante :
```
cf env NOM_APP
```
