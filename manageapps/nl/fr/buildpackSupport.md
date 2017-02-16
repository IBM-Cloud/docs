---

copyright:
  years: 2016, 2017
lastupdated: "2016-10-10"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Déclaration de support pour les packs de construction
{: #buildpack_support_statement}


## Packs de construction IBM intégrés
{: #built-in_ibm_buildpacks}

Pour [Liberty for Java](/docs/runtimes/liberty/index.html), [SDK for Node.js](/docs/runtimes/nodejs/index.html) et [ASP.NET Core](/docs/runtimes/dotnet/index.html), IBM prend en charge deux versions (n et n - 1), par exemple IBM Liberty Buildpack version 1.22 et IBM Liberty Buildpack version 1.21. Chaque pack de construction fournit et prend en charge une ou plusieurs versions principales de son contexte d'exécution correspondant, en fonction des besoins, par exemple IBM SDK, Java Technology Edition version 7 édition 1 et version 8. En général, les packs de construction sont actualisés une fois par mois avec la version secondaire disponible la plus récente du contexte d'exécution.

Pour [IBM Bluemix Runtime for Swift](/docs/runtimes/swift/index.html), IBM prend en charge le pack de construction qui correspond à la version la plus récente de Swift disponible sur [Swift.org](http://swift.org). Les mises à jour du pack de construction sont synchronisées avec la version publiée de Swift la plus récente disponible.

Les problèmes ou questions que vous pourriez avoir peuvent être signalés pour toute version du pack de construction IBM intégré actuellement pris en charge dans {{site.data.keyword.Bluemix_notm}}. Toutefois, leur pertinence dans la version la plus récente devra être vérifiée. Si un incident est trouvé, IBM fournira un correctif dans un niveau ultérieur du contexte d'exécution et du pack de construction correspondant. Elle ne fournira pas de correctif pour les versions principales et secondaires antérieures (N-1, n-1). Elle n'assurera pas non plus le support des contextes d'exécution de communauté, même s'ils utilisent des packs de construction IBM, comme par exemple Open JDK avec le pack de construction Liberty. La même stratégie de support que pour les packs de construction de communauté intégrés ci-dessous s'applique à ces contextes d'exécution de communauté.

## Packs de construction de communauté intégrés
{: #built-in_community_buildpacks}

Les packs de construction de communauté intégrés suivants sont mis à disposition par la communauté Cloud Foundry :

* [Java](/docs/runtimes/tomcat/index.html)
* [Node.js](https://github.com/cloudfoundry/nodejs-buildpack)
* [PHP](/docs/runtimes/php/index.html)
* [Ruby](/docs/runtimes/ruby/index.html)
* [Python](/docs/runtimes/python/index.html)
* [Go](/docs/runtimes/go/index.html)

La mise à jour de ces packs de construction est effectuée lorsque {{site.data.keyword.Bluemix_notm}} est mis à niveau vers une nouvelle version de Cloud Foundry. Les problèmes ou questions liés à ces contextes d'exécution dans {{site.data.keyword.Bluemix_notm}} peuvent être signalés à IBM ; nous aiderons à déterminer si {{site.data.keyword.Bluemix_notm}} est la source
du problème. Pour les problèmes liés à {{site.data.keyword.Bluemix_notm}}, IBM fournira un correctif. Cependant, pour les incidents survenant dans le pack de construction ou le
contexte d'exécution lui-même, IBM vous aidera à les signaler à la communauté appropriée. IBM ne fournira pas de correctif pour ces packs de
construction et ces contextes d'exécution.

## Packs de construction externes
{: #external_buildpacks}


IBM n'assure pas le support des packs de construction externes. Il peut être nécessaire de contacter la communauté Cloud Foundry pour obtenir de
l'aide.
