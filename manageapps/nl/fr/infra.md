---

 

copyright:

  2016

 

---

{:shortdesc: .shortdesc}

#  Couches de l'infrastructure Bluemix

*Dernière mise à jour : 15 mars 2016*

{{site.data.keyword.Bluemix_notm}} fait abstraction des couches du système d'exploitation et de
l'infrastructure et les masque pour que vous n'ayez pas à les gérer. Toutefois, il se peut que vous souhaitiez en savoir plus sur le système d'exploitation et le
middleware utilisés pour votre application.
{:shortdesc}

## Affichage des couches de l'infrastructure Bluemix
{:viewinfra}

Vous pouvez exécuter la commande cf stacks pour afficher les piles, ou systèmes de fichiers racine, disponibles dans lesquelles vos applications
seront déployées. Vous pouvez aussi spécifier la pile lorsque vous utilisez la commande cf push avec l'option *-s* et l'argument
*nom_pile*, où nom_pile est le système de fichiers racine, par exemple `lucid64` ou `cflinuxfs2`:
```
cf push nom_app -s nom_pile
```
Vous pouvez utiliser la commande `cf buildpacks` pour afficher les composants de middleware, par exemple le profil WebSphere Liberty et
SDK for Node.js, qui sont
disponibles en tant que contextes d'exécution dans lesquels votre application peut s'exécuter. De plus, vous pouvez spécifier l'environnement d'exécution pour votre application avec la commande
suivante :
```
cf push nom_app -b nom_pack_construction
```
