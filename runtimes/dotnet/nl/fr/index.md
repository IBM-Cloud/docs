---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-06"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# ASP.NET Core
{: #dotnet_core}

L'environnement d'exécution ASP.NET Core sur {{site.data.keyword.Bluemix}} utilise la technologie du pack de construction ASP.NET Core. ASP.NET Core est une infrastructure open source modulaire permettant de créer des applications Web .NET.
.Net Core est un petit environnement d'exécution multiplateforme qui peut être ciblé par des applications ASP.NET Core.
Elles sont combinées pour activer des applications Web modernes basées sur le cloud.
{: shortdesc}

## Détection
{: #detection}
Le pack de construction Bluemix ASP.NET Core est utilisé si l'application comporte un ou plusieurs dossiers contenant à la fois un fichier project.json et au moins un fichier .cs, ou si l'application est envoyée par push depuis le répertoire de sortie de la commande *dotnet publish*.

## Application de démarrage
{: #starter_application}

{{site.data.keyword.Bluemix}} fournit une application de démarrage ASP.NET Core.  L'application de démarrage ASP.NET Core est une application simple qui fournit un modèle que vous pouvez utiliser. Vous pouvez expérimenter cette application de démarrage et effectuer des modifications puis les envoyer par commande push vers l'environnement Bluemix.  Voir [Utilisation des applications de démarrage](/docs/cfapps/starter_app_usage.html) pour obtenir de l'aide.

## Versions d'environnement d'exécution
{: #runtime_versions}

### versions prises en charge
{: #supported_versions}
Ce pack de construction prend en charge les versions suivantes (les versions
indiquées comme obsolètes seront supprimées dans une édition ultérieure du pack
de construction). Consultez la [déclaration Microsoft de support pour les éditions LTS (Long Term Support) et les éditions actuelles](https://www.microsoft.com/net/core/support) (document en anglais).

#### Outillage project.json (déprécié)

| Version de .NET SDK        | Par défaut |
|-------------------------|---------|
| 1.0.0-preview2-003156   |   Non    |
| 1.0.0-preview2-1-003177 |   Non    |

#### Outillage MSBuild SDK

| Version de .NET SDK        | Par défaut |
|-------------------------|---------|
| 1.0.0-preview4-004233   |   Non    |
| 1.0.1                   |   Oui   |

#### Versions de l'exécution .NET Core

| Version de l'exécution .NET Core | Type d'édition | Par défaut |
|---------------------------|--------------|---------|
| 1.0.0                     | LTS          |   Non    |
| 1.0.1                     | LTS          |   Non    |
| 1.0.3                     | LTS          |   Non    |
| 1.0.4                     | LTS          |   Oui    |
| 1.1.0                     | Actuel       |   Non    |
| 1.1.1                     | Actuel       |   Non    |

### Spécification de la version de .NET SDK

Contrôlez la version de .NET SDK avec un fichier global.json optionnel placé dans le répertoire racine de l'application. Par exemple :
```
   {
      "projects": [ "src" ],
      "sdk": {
        "version": "1.0.1"
      }
   }
```
{: codeblock}

S'il n'est pas spécifié, l'outillage MSBuild utilisé est celui de l'exécution LTS (Long-term-support) la plus récente. Pour utiliser l'outillage project.json, vous pouvez spécifier l'une des versions de project.json listées plus haut, mais gardez à l'esprit que
ces versions sont amenées à disparaître dans le futur.

## Personnalisation des sources de package NuGet
{: #customizing_nuget_package_sources}

Contrôlez l'emplacement à partir duquel les dépendances de votre application sont téléchargées dans le fichier NuGet.Config du répertoire racine de l'application. Par exemple :
```
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
   <packageSources>
      <add key="NuGet.org" value="https://api.nuget.org/v3/index.json"/>
   </packageSources>
   </configuration>
```
{: codeblock}

## Développement d'applications en local
{: #developing_locally}

Pour plus d'informations sur l'exécution locale d'une application ASP.NET Core, consultez [Getting Started with ASP.NET](http://docs.asp.net/en/latest/getting-started/index.html).
Pour coller le plus possible au mode d'exécution de l'application dans Bluemix, suivez les instructions pour .NET Core ; sachez que le développement de l'application sur Linux n'est pas obligatoire.

L'outil Yeoman peut être utilisé pour générer de nouveaux modèles de projet, comme indiqué dans [Building Projects with Yeoman](http://docs.asp.net/en/latest/client-side/yeoman.html).

Pour plus d'informations sur un développement local via Visual Studio, voir [Developing with Visual Studio](/docs/starters/deploy_vs.html){: new_window}.

## Envoi par commande push d'une application publiée
{: #pushing_published_app}

Si votre application doit contenir tous ses fichiers binaires requis et éviter ainsi que le pack de construction ne télécharge des fichiers binaires externes, vous pouvez la pousser sous forme d'application *autonome* publiée. Consultez [.NET Core App Types](https://docs.microsoft.com/en-us/dotnet/articles/core/app-types){: new_window} pour plus d'informations sur les applications autonomes.

Pour publier une application, exécutez une commande telle que la suivante :
```
  dotnet publish -r ubuntu.14.04-x64
```
{: codeblock}

Les applications autonomes peuvent ensuite être poussées à partir de
```
  bin/<Debug|Release>/<framework>/<runtime>/publish
```
{: codeblock}
.

Les applications portables peuvent être poussées à partir de
```
  bin/<Debug|Release>/<framework>/publish
```
{:codeblock}
.

En outre, si vous utilisez un fichier manifest.yml dans votre application, vous pouvez spécifier le chemin d'accès au dossier de sortie de la publication dans votre fichier manifest.yml.  Ensuite, il n'est pas nécessaire de se placer dans ce dossier lors de l'envoi par commande push de l'application.

## Déploiement d'applications comportant plusieurs projets
{: #developing_apps_with_multiple_projects}

Pour déployer une application qui contient plusieurs projets, vous devez spécifier le projet que le pack de construction doit exécuter comme projet principal. Pour ce faire, créez un fichier .deployment dans le dossier racine de la solution qui définit le chemin d'accès vers le projet principal. Le chemin d'accès au projet principal peut être spécifié comme dossier de projet ou comme fichier de projet (.xproj ou .csproj).

Par exemple, si une solution contient trois projets, *MyApp.DAL*, *MyApp.Services* et *MyApp.Web* dans le dossier *src*, et si *MyApp.Web* est le projet principal, le format du fichier .deployment doit être le suivant :
```
  [config]
  project = src/MyApp.Web/MyApp.Web.csproj
```
{: codeblock}

Dans cet exemple, le pack de construction compile automatiquement les projets *MyApp.DAL* et *MyApp.Services* s'ils sont répertoriés en tant que dépendances dans le fichier project.json pour *MyApp.Web*, mais le pack de construction tente uniquement d'exécuter le projet principal, *MyApp.Web*, avec dotnet run -p src/MyApp.Web.

## Configuration de l'application
{: #application_configuration}

### Configuration de votre application pour écouter sur le port adéquat
{: #configuring_listen_proper_port}

Le pack de construction exécutera votre application avec la commande *dotnet run* et lui passera l'argument de ligne de commande suivant
```
  --server.urls http://0.0.0.0:${PORT}
```
{: codeblock}

Votre application devra passer cet argument à kestrel afin que celui-ci écoute sur le port correct.

Pour implémenter le passage de cet argument, quelques modifications doivent être apportées à la fois aux
exemples fournis dans le référentiel cli-samples et aux modèles fournis par Visual Studio, et ce avant leur
déploiement sur Bluemix.

Des modifications doivent être apportées à la méthode Main comme indiqué par les commentaires dans l'exemple suivant :

<pre>
  public static void Main(string[] args)
  {
    var config = new ConfigurationBuilder() //AJOUTEZ CES TROIS LIGNES AU DEBUT DE LA METHODE MAIN
        .AddCommandLine(args)
        .Build();

    var host = new WebHostBuilder()
        .UseKestrel()
        .UseConfiguration(config) //AJOUTEZ CETTE LIGNE AVANT 'UseStartup'
        .UseStartup&lt;Startup&gt;()
        .Build();
    host.Run();
}
</pre>
{: codeblock}

Dans le cas de l'outillage project.json, ajoutez cette ligne à votre fichier project.json :
```
  "Microsoft.Extensions.Configuration.CommandLine": "1.0.1",
```
{: codeblock}

Dans le cas de l'outillage MSBuild, ajoutez cette ligne à votre fichier .csproj :
```
  <PackageReference Include="Microsoft.Extensions.Configuration.CommandLine" Version="1.0.1" />
```
{:codeblock}

Ajoutez une instruction *using* au fichier qui contient votre méthode Main :
```
  using Microsoft.Extensions.Configuration;
```
{: codeblock}

### Veillez à ce que votre application ait tous les fichiers nécessaires dans le dossier de sortie de construction
{: #configure_output_files}

#### Utilisation de l'outillage project.json

Ajoutez la propriété suivante dans la section `buildOptions` du fichier project.json :
```
  "copyToOutput": {
    "include": [
      "wwwroot",
      "Areas/**/Views",
      "Views",
      "appsettings.json"
    ]
  }
```
{: codeblock}

Dans la méthode `Startup` de Startup.cs, retirez la ligne suivante :
```
  .SetBasePath(env.ContentRootPath)
```
{: codeblock}

Dans la méthode `Main` de Program.cs, retirez la ligne suivante :
```
  .UseContentRoot(Directory.GetCurrentDirectory())
```
{: codeblock}

Ces changements doivent permettre à .NET CLI de trouver les `Vues` de votre application, car elles sont maintenant copiées dans la sortie de la génération lorsque la commande `dotnet run` est exécutée. Si votre application a besoin d'autres fichiers au moment de son exécution (par exemple, des fichiers de configuration json), vous devez les ajouter à la section `include` de `copyToOutput` dans le fichier project.json de votre projet.

#### Utilisation de l'outillage MSBuild

Ajoutez un élément `<Content>` à l'élément `<ItemGroup>` de votre fichier .csproj :
```
  <ItemGroup>
    <Content Include="wwwroot/**/*;Areas/**/Views/*;Views/*;appsettings.json">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
      <CopyToPublishDirectory>Always</CopyToPublishDirectory>
    </Content>
  </ItemGroup>
```
{: codeblock}

Dans la méthode `Startup` de Startup.cs, retirez la ligne suivante :
```
  .SetBasePath(env.ContentRootPath)
```
{: codeblock}

Dans la méthode `Main` de Program.cs, retirez la ligne suivante :
```
  .UseContentRoot(Directory.GetCurrentDirectory())
```
{: codeblock}

Ces changements doivent permettre à .NET CLI de trouver les `Vues` de votre application, car elles sont maintenant copiées dans la sortie de la génération lorsque la commande `dotnet publish` est exécutée. Si votre application a besoin d'autres fichiers au moment de son exécution (par exemple, des fichiers de configuration json), vous devez aussi les ajouter, en les séparant par des points-virgules, à la propriété `Include` de l'élément `Content` dans le fichier .csproj de votre projet.

## Compilation de votre application en configuration Release (MSBuild uniquement)
{: #compiling_in_release_configuration}

Les projets basés sur MSBuild sont à présent publiés en utilisant la commande `dotnet publish` durant le passage en préproduction (staging). Par défaut, le pack de construction publiera votre application en configuration `Debug`. Pour qu'elle soit publiée en configuration `Release`, mettez à `true` la variable d'environnement `PUBLISH_RELEASE_CONFIG`. 

Vous pouvez pour cela utiliser la commande suivante avec le client de ligne de commande pour Cloud Foundry :

```shell
  cf set-env <app_name> PUBLISH_RELEASE_CONFIG true
```

Vous pouvez aussi définir la variable dans le fichier manifest.yml de votre application :

```yml
---
applications:
- name: sample-aspnetcore-app
  memory: 512M
  env:
    PUBLISH_RELEASE_CONFIG: true
```

## Désactivation du cache de packages NuGet
{: #disabling_the_nuget_package_cache}

Dans certains cas, il est nécessaire d'effacer le cache de packages NuGet de votre application. Cela aura pour effet d'effacer du cache tous les packages NuGet existants, mais aussi d'empêcher le pack de construction d'en mémoriser d'autres.

A cet effet, vous pouvez mettre à `false` la variable d'environnement `CACHE_NUGET_PACKAGES` en utilisant le client de ligne de commande pour Cloud Foundry : 

```shell
  cf set-env <app_name> CACHE_NUGET_PACKAGES false
```

Vous pouvez aussi mettre à `false` la variable d'environnement `CACHE_NUGET_PACKAGES` dans le fichier manifest.yml de votre application : 

```yml
---
applications:
- name: sample-aspnetcore-app
  memory: 512M
  env:
    CACHE_NUGET_PACKAGES: false
```

## Utilisation de bibliothèques natives personnalisées
{: #using_custom_native_libraries}

Il est parfois nécessaire d'utiliser à la fois un package NuGet et certaines bibliothèques natives (fichiers .so). Dans ce cas, pour que ces bibliothèques soient utilisables avec le pack de construction, vous devez les placer dans un dossier nommé "ld_library_path", sous le dossier racine de votre application. Le pack de construction ajoutera automatiquement ce chemin à la variable d'environnement `LD_LIBRARY_PATH` lors du passage en préproduction (staging). Vous pouvez sinon spécifier la variable d'environnement `LD_LIBRARY_PATH` dans le fichier `manifest.yml` de votre application ou utiliser la commande `cf set-env` pour spécifier un nom de dossier autre que "ld_library_path". Dans ce cas, le pack de construction ajoutera le chemin spécifique à la variable `LD_LIBRARY_PATH` qu'il générera. 

## Foire aux questions sur le dépannage
{: #troubleshooting_faq}

**Q** : Le déploiement de mon application échoue avec le message : `API/0App instance exited ... payload: {... "reason"=>"CRASHED", "exit_status"=>-1, ...}`.  Qu'est-ce que cela signifie ?

**R** : Si vous recevez un message similaire lors de l'envoi de votre application par commande push, il est fort probable que l'application dépasse les limites de quota de mémoire ou de disque.  Vous pouvez résoudre ce problème en augmentant les quotas pour votre application.

**Q** : Le déploiement de mon application échoue avec le message : `Failed to compress droplet: signal: broken pipe` ou `No space left on device`. Comment puis-je résoudre ce problème ?

**R** : Les projets poussés à partir d'un code source comprenant de nombreuses dépendances de packages NuGet provoquent parfois cette erreur lorsque la mise en cache des packages NuGet est activée. Pour désactiver la mise en cache, mettez à `false` la variable d'environnement `CACHE_NUGET_PACKAGES`. 

# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
* [NuGet](https://docs.nuget.org/Consume/Overview){: new_window}
* [Présentation d'ASP.NET Core](http://docs.asp.net/en/latest/conceptual-overview/aspnet.html){: new_window}
