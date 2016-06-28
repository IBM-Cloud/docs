---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Dernières mises à jour apportées au pack de construction ASP.NET Core
{: #latest_updates}

*Dernière mise à jour : 10 juin 2016*

Liste des dernières mises à jour apportées au pack de construction aspnet.

## 10 juin 2016 : Pack de construction ASP.NET Core v0.8.1-20160526-0957 mis à jour

Cette version du pack de construction inclut les modifications suivantes : 

* Le nom de l'environnement d'exécution, ASP.NET 5, est devenu ASP.NET Core.
* Le numéro de version du pack de construction est inclus dans le script de sortie de détection.
* Cette version du pack de construction retire la prise en charge des applications basées sur DNX à l'aide de CoreCLR RC1 et version antérieure. 
* Cette version du pack de construction prend en charge .NET CLI et .NET Core RC2.
* Le pack de construction détecte des projets avec un fichier project.json ou des fichiers *.runtimeconfig.json issus de la sortie de publication. 

## 22 octobre 2105 : Pack de construction ASP.NET 5 v0.7-20151022-1257 mis à jour

* Cette version du pack de construction retire Mono et prend en charge la version bêta 8 de CoreCLR à la place. 

## 18 septembre 2105 : Pack de construction ASP.NET 5 v0.6-20150916-1220 mis à jour

* Cette version du pack de construction prend en charge les modifications de l'environnement DNX 7 bêta. De plus, elle peut exécuter des applications
qui dépendent d'éditions bêta plus anciennes avec la commande de démarrage personnalisée suivante :


```
   dnx src/dotnetstarter kestrel --server.urls http://${VCAP_APP_HOST}:${PORT}
```
{: codeblock}

* L'utilisation du serveur Web Nowin a été retirée de ce pack de construction et le serveur Web [Kestrel]{https://github.com/aspnet/KestrelHttpServer} est utilisé à la place. 

# rellinks
{: #rellinks}
## general
{: #general}
* [Environnement d'exécution Dotnet Core](index.html)
