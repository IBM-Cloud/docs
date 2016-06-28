---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# ASP.NET Core 
{: #dotnet_core}
*Dernière mise à jour : 30 mai 2016*

L'environnement d'exécution ASP.NET Core sur {{site.data.keyword.Bluemix}} utilise la technologie du pack de construction ASP.NET Core. ASP.NET Core est une infrastructure open source modulaire permettant de créer des applications Web .NET.
.Net Core est un petit environnement d'exécution multiplateforme qui peut être ciblé par des applications ASP.NET Core.
Elles sont combinées pour activer des applications Web modernes basées sur le cloud.
{: shortdesc}

## Détection
{: #detection}
Le pack de construction Bluemix ASP.NET Core est utilisé si un ou plusieurs fichiers project.json figurent dans l'application, ou si l'application est propagée depuis le répertoire de sortie de la commande *dotnet publish*. 

## Application de démarrage
{: #starter_application}

{{site.data.keyword.Bluemix}} fournit une application de démarrage ASP.NET Core. L'application de démarrage ASP.NET Core est une application simple qui fournit un modèle que vous pouvez utiliser. Vous pouvez expérimenter cette application de démarrage et effectuer des modifications puis les envoyer par commande push vers l'environnement Bluemix.  Voir [Utilisation des applications de démarrage](../../cfapps/starter_app_usage.html) pour obtenir de l'aide.

## Versions d'environnement d'exécution
{: #runtime_versions}

### Spécification de la version .NET CLI

Contrôlez la version .NET CLI à l'aide d'un fichier global.json facultatif contenu dans le répertoire racine de l'application. Par exemple :
```
   {
      "projects": [ "src" ],
      "sdk": {
        "version": "1.0.0-preview1-002702"
      }
   }
```
{: codeblock}

Si aucune valeur n'est spécifiée, le candidat de l'édition stable est utilisé. 

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

## Envoi par commande push d'une application publiée 

Si votre application doit contenir tous ses fichiers binaires requis et éviter ainsi que le pack de construction ne télécharge des fichiers binaires externes, vous pouvez envoyer par commande push une application *autonome* publiée. Pour plus d'informations sur les applications autonomes, voir [Types of portability in .Net Core](http://dotnet.github.io/docs/core-concepts/app-types.html){: new_window}.


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

## Utilisation d'exemples à partir du répertoire cli-samples et du modèle Visual Studio

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
    var config = new ConfigurationBuilder() //AJOUTER CES 3 LIGNES EN HAUT DE LA METHODE PRINCIPALE
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
  "Microsoft.Extensions.Configuration.CommandLine": "1.0.0-rc2-final",
```
{: codeblock}

Ajoutez une instruction *using* au fichier qui contient votre méthode principale : 
```
  using Microsoft.Extensions.Configuration;
```
{: codeblock}

# rellinks
{: #rellinks}
## general
{: #general}
* [Dernières mises à jour apportées au pack de construction ASP.NET Core](updates.html)
* [NuGet](https://docs.nuget.org/Consume/Overview){: new_window}
* [Présentation d'ASP.NET Core](http://docs.asp.net/en/latest/conceptual-overview/aspnet.html){: new_window}
