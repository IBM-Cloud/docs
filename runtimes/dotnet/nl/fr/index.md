---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-14"
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

# versions prises en charge
{: #supported_versions}
Ce pack de construction prend en charge les versions suivantes (les versions
indiquées comme obsolètes seront supprimées dans une édition ultérieure du pack
de construction) :

1. .NET Core 1.0.0-rc2-final (bêta) (obsolète)
2. .NET Core 1.0.0
3. .NET Core 1.0.1

## Détection
{: #detection}
Le pack de construction Bluemix ASP.NET Core est utilisé si l'application comporte un ou plusieurs dossiers contenant à la fois un fichier project.json et au moins un fichier .cs, ou si l'application est envoyée par push depuis le répertoire de sortie de la commande *dotnet publish*.

## Application de démarrage
{: #starter_application}

{{site.data.keyword.Bluemix}} fournit une application de démarrage ASP.NET Core.  L'application de démarrage ASP.NET Core est une application simple qui fournit un modèle que vous pouvez utiliser. Vous pouvez expérimenter cette application de démarrage et effectuer des modifications puis les envoyer par commande push vers l'environnement Bluemix.  Voir [Utilisation des applications de démarrage](/docs/cfapps/starter_app_usage.html) pour obtenir de l'aide.

## Versions d'environnement d'exécution
{: #runtime_versions}

### Spécification de la version .NET CLI

Contrôlez la version .NET CLI à l'aide d'un fichier global.json facultatif contenu dans le répertoire racine de l'application. Par exemple :
```
   {
      "projects": [ "src" ],
      "sdk": {
        "version": "1.0.0-preview2-003121"
      }
   }
```
{: codeblock}

Pour obtenir la liste des versions de l'interface de ligne de commande prises en charge, voir [Dernières mises à jour apportées au pack de construction ASP.NET Core](/docs/runtimes/dotnet/updates.html). Si aucune valeur n'est spécifiée, le candidat de l'édition stable est utilisé.

### Personnalisation des sources de package NuGet

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

Pour plus d'informations sur l'exécution d'une application ASP.NET Core en local, voir [Getting Started with ASP.NET](http://docs.asp.net/en/latest/getting-started/index.html).
Pour coller le plus possible au mode d'exécution de l'application dans Bluemix, suivez les instructions pour .NET Core ; sachez que le développement de l'application sur Linux n'est pas obligatoire.

L'outil Yeoman peut être utilisé pour générer de nouveaux modèles de projet, comme indiqué dans [Building Projects with Yeoman](http://docs.asp.net/en/latest/client-side/yeoman.html).

Pour plus d'informations sur un développement local via Visual Studio, voir [Developing with Visual Studio](/docs/starters/deploy_vs.html){: new_window}.

## Envoi par commande push d'une application publiée
{: #pushing_published_app}

Si votre application doit contenir tous ses fichiers binaires requis et éviter ainsi que le pack de construction ne télécharge des fichiers binaires externes, vous pouvez envoyer par commande push une application *autonome* publiée.  Voir [.NET Core App Types](https://docs.microsoft.com/en-us/dotnet/articles/core/app-types){: new_window} pour plus d'informations sur les applications autonomes,

Pour publier une application, exécutez une commande telle que la suivante :
```
  dotnet publish -r ubuntu.14.04-x64 
```
{: codeblock}
  
L'application peut ensuite être envoyée par commande push envoyé à partir du répertoire
```
  bin/<Debug|Release>/<framework>/<runtime>/publish
```
{: codeblock}
.

En outre, si vous utilisez un fichier manifest.yml dans votre application, vous pouvez spécifier le chemin d'accès au dossier de sortie de la publication dans votre fichier manifest.yml.  Ensuite, il n'est pas nécessaire de se placer dans ce dossier lors de l'envoi par commande push de l'application.

## Déploiement d'applications comportant plusieurs projets
{: #developing_apps_with_multiple_projects}

Pour déployer une application qui contient plusieurs projets, vous devez spécifier le projet que le pack de construction doit exécuter comme projet principal. Pour ce faire, créez un fichier .deployment dans le dossier racine de la solution qui définit le chemin d'accès vers le projet principal. Le chemin d'accès au projet principal peut être spécifié comme dossier de projet ou comme fichier de projet (.xproj ou .csproj).

Par exemple, si une solution contient trois projets, *MyApp.DAL*, *MyApp.Services* et *MyApp.Web* dans le dossier *src*, et si *MyApp.Web* est le projet principal, le format du fichier .deployment doit être le suivant :
```
  [config]
  project = src/MyApp.Web
```
{: codeblock}

Dans cet exemple, le pack de construction compile automatiquement les projets *MyApp.DAL* et *MyApp.Services* s'ils sont répertoriés en tant que dépendances dans le fichier project.json pour *MyApp.Web*, mais le pack de construction tente uniquement d'exécuter le projet principal, *MyApp.Web*, avec dotnet run -p src/MyApp.Web. Le chemin d'accès à *MyApp.Web*, si ce projet figure dans un projet xproj, peut également être spécifié comme suit : 
```
  project = src/MyApp.Web/MyApp.Web.xproj 
```
{: codeblock}

## Configuration de votre application pour écouter sur le port adéquat
{: #configuring_listen_proper_port}

Le pack de construction va exécuter votre application avec la commande *dotnet run* et transmettre l'argument de ligne de commande qui suit :
```
  --server.urls http://0.0.0.0:${PORT}
```
{: codeblock}

Votre application devra transmettre cet argument à kestrel pour s'assurer que kestrel est en mode écoute sur le port approprié.

L'implémentation de la transmission de cet argument nécessite que les exemples fournis dans le répertoire cli-samples et les modèles fournis par Visual Studio soient légèrement modifiés avant d'être déployés vers Bluemix.

Des modifications doivent être apportées à la méthode principale, comme indiqué par les commentaires dans l'exemple suivant :

<pre>
  public static void Main(string[] args)
  {
    var config = new ConfigurationBuilder() //ADD THESE 3 LINES AT THE TOP OF THE MAIN METHOD
        .AddCommandLine(args)
        .Build();

    var host = new WebHostBuilder()
        .UseKestrel()
        .UseConfiguration(config) //ADD THIS LINE BEFORE 'UseStartup'
        .UseStartup&lt;Startup&gt;()
        .Build();
    host.Run();
}
</pre>
{: codeblock}

Ajoutez la dépendance suivante à project.json : 
```
  "Microsoft.Extensions.Configuration.CommandLine": "1.0.0",
```
{: codeblock}

Ajoutez la propriété suivante dans la section `buildOptions` du fichier project.json
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

Ajoutez une instruction *using* au fichier qui contient votre méthode principale : 
```
  using Microsoft.Extensions.Configuration;
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

Ces changements doivent permettre à .NET CLI de trouver les éléments `Vues` de votre application car ils sont copiés dans le résultat de la génération quand la commande `dotnet run` s'exécute.  Si votre application dispose d'autres fichiers, comme des fichiers de configuration json, qui sont requis au moment de l'exécution, vous devez les ajouter à la section `include` de `copyToOutput` dans le fichier project.json.

## Foire aux questions liée au traitement des incidents
{: #troubleshooting_faq}

**Q** : Le déploiement de mon application échoue avec le message : `API/0App instance exited ... payload: {... "reason"=>"CRASHED", "exit_status"=>-1, ...}`.  Qu'est-ce que cela signifie ?

**R** : Si vous recevez un message similaire lors de l'envoi de votre application par commande push, il est fort probable que l'application dépasse les limites de quota de mémoire ou de disque. Vous pouvez résoudre ce problème en augmentant les quotas pour votre application.

# rellinks
{: #rellinks}
## general
{: #general}
* [Dernières mises à jour apportées au pack de construction ASP.NET Core](updates.html)
* [NuGet](https://docs.nuget.org/Consume/Overview){: new_window}
* [Présentation d'ASP.NET Core](http://docs.asp.net/en/latest/conceptual-overview/aspnet.html){: new_window}
