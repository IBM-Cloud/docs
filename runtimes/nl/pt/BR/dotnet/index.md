---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# ASP.NET Core 
{: #dotnet_core}
*Última atualização: 30 de maio de 2016*

O tempo de execução ASP.NET Core no {{site.data.keyword.Bluemix}} é desenvolvido com o buildpack ASP.NET Core. O ASP.NET Core
é uma estrutura de software livre modular para a construção de aplicativos da web .NET.
O .Net Core é um tempo de execução pequeno de plataforma cruzada que pode ser direcionado pelos aplicativos ASP.NET Core.
Eles combinam para permitir aplicativos da web modernos, baseados em nuvem.
{: shortdesc}

## Detecção
{: #detection}
O buildpack do Bluemix ASP.NET Core será usado se houver um ou mais arquivos project.json em qualquer lugar no aplicativo,
 ou se o aplicativo for enviado por push do diretório de saída do comando *dotnet publish*.

## Aplicativo iniciador
{: #starter_application}

O {{site.data.keyword.Bluemix}} fornece um aplicativo iniciador do ASP.NET Core. O aplicativo iniciador do ASP.NET Core é um app simples que fornece um modelo que pode ser usado. É possível experimentar o app iniciador e fazer mudanças e enviá-las por push para o ambiente do Bluemix.  Consulte [Usando os aplicativos iniciadores](../../cfapps/starter_app_usage.html) para obter ajuda sobre o uso
do aplicativo iniciador.

## Versões de tempo de execução
{: #runtime_versions}

### Especificando a versão da CLI .NET

Controle a versão da CLI .NET com um global.json opcional no diretório raiz do aplicativo. Por exemplo:
```
   {
      "projects": [ "src" ],
      "sdk": {
        "version": "1.0.0-preview1-002702"
      }
   }
```
{: codeblock}

Se não for especificado, o Candidato a Liberação estável mais atual será usado.

### Customizando fontes de pacote NuGet

Controle de onde as dependências do seu aplicativo são transferidas por download no arquivo NuGet.Config no diretório raiz do aplicativo. Por exemplo:
```
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
   <packageSources>
      <add key="NuGet.org" value="https://api.nuget.org/v3/index.json"/>
   </packageSources>
   </configuration>
```
{: codeblock}

## Desenvolvendo aplicativos localmente
{: #developing_locally}

Para obter mais informações sobre a execução de um aplicativo ASP.NET Core localmente, consulte
[Introdução ao ASP.NET](http://docs.asp.net/en/latest/getting-started/index.html).
Para corresponder com mais exatidão como o aplicativo é executado no Bluemix, siga as instruções do Linux para .NET Core, mas o desenvolvimento do aplicativo no Linux não é necessário.

A ferramenta Yeoman pode ser usada para gerar novos modelos de projeto, conforme descrito em
[Construindo projetos com o Yeoman](http://docs.asp.net/en/latest/client-side/yeoman.html).

## Enviando por push um aplicativo publicado

Se você quiser que seu aplicativo contenha todos os binários necessários para que o buildpack não faça download de
qualquer binário externo, será possível enviar por push um aplicativo *autocontido* publicado. Consulte [Tipos de portabilidade no .Net Core](http://dotnet.github.io/docs/core-concepts/app-types.html){: new_window}
para obter mais informações sobre aplicativos autocontido.

Para publicar um aplicativo, emita um comando como:
```
  dotnet publish -r ubuntu.14.04-x64 
```
{: codeblock}
  
O app, então, pode ser enviado por push do diretório
```
  bin/<Debug|Release>/<framework>/<runtime>/publish
```
{: codeblock}
específico.

Observe também que se você estiver usando um arquivo manifest.yml em seu
aplicativo, será possível especificar o caminho para a pasta de saída de publicação no
manifest.yml. Assim, não é necessário estar nessa pasta quando enviar o aplicativo por
push.

## Implementando apps com diversos projetos

Para implementar um app que contém diversos projetos, você precisará especificar
qual projeto deseja que o buildpack execute como projeto principal. Isso pode ser feito
criando um arquivo .deployment na pasta raiz da solução que configura o caminho para
o projeto principal. O caminho para o projeto principal pode ser especificado como a
pasta ou o arquivo do projeto (.xproj ou .csproj).

Por exemplo, se uma solução contendo três projetos,
*MyApp.DAL*, *MyApp.Services* e *MyApp.Web* na
pasta *src*, e *MyApp.Web* for o projeto principal, o formato
do arquivo .deployment será este:
```
  [config]
  project = src/MyApp.Web
```
{: codeblock}

Neste exemplo, o buildpack compilaria automaticamente os projetos
*MyApp.DAL* e *MyApp.Services* se eles estivessem listados como
dependências no arquivo project.json para *MyApp.Web*, mas o buildpack
somente tentaria executar o projeto principal, *MyApp.Web*, com dotnet run
-p src/MyApp.Web. O caminho para *MyApp.Web*, supondo que
este seja um projeto xproj, também poderia ser especificado como 
```
  project = src/MyApp.Web/MyApp.Web.xproj 
```
{: codeblock}

## Usando amostras do repositório de amostras da cli e modelo do Visual Studio

O buildpack executará seu aplicativo com o comando *dotnet run* e
passará o argumento de linha de comandos da seguinte forma
```
  --server.urls http://0.0.0.0:${PORT}
```
{: codeblock}

Seu aplicativo precisará passar este argumento ao kestrel para assegurar que o kestrel esteja atendendo na porta correta.

Para implementar a passagem desse argumento, as amostras fornecidas no repositório
de amostras da cli e nos modelos fornecidos pelo Visual Studio requerem pequenas
modificações antes da implementação no Bluemix.

São necessárias modificações no método Main, conforme observado pelos comentários no exemplo a seguir:

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

Inclua a dependência a seguir no project.json: 
```
  "Microsoft.Extensions.Configuration.CommandLine": "1.0.0-rc2-final",
```
{: codeblock}

Inclua uma instrução *using* no arquivo que contém seu método Main: 
```
  using Microsoft.Extensions.Configuration;
```
{: codeblock}

# rellinks
{: #rellinks}
## geral
{: #general}
* [Atualizações mais recentes para o buildpack do ASP.NET Core](updates.html)
* [NuGet](https://docs.nuget.org/Consume/Overview){: new_window}
* [Visão geral do ASP.NET Core](http://docs.asp.net/en/latest/conceptual-overview/aspnet.html){: new_window}
