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

O tempo de execução ASP.NET Core no {{site.data.keyword.Bluemix}} é desenvolvido com o buildpack ASP.NET Core. O ASP.NET Core
é uma estrutura de software livre modular para a construção de aplicativos da web .NET.
O .Net Core é um tempo de execução pequeno de plataforma cruzada que pode ser direcionado pelos aplicativos ASP.NET Core.
Eles combinam para permitir aplicativos da web modernos, baseados em nuvem.
{: shortdesc}

## Detecção
{: #detection}
O buildpack Bluemix ASP.NET Core será usado se houver uma ou mais pastas contendo um arquivo project.json e pelo menos um arquivo .cs em qualquer lugar no aplicativo
ou se o aplicativo for enviado por push do diretório de saída do comando *dotnet publish*.

## Aplicativo iniciador
{: #starter_application}

O {{site.data.keyword.Bluemix}} fornece um aplicativo iniciador do ASP.NET Core.  O aplicativo iniciador do ASP.NET Core é um app simples que fornece um modelo que pode ser usado. É possível experimentar o app iniciador e fazer mudanças e enviá-las por push para o ambiente do Bluemix.  Consulte [Usando os aplicativos iniciadores](/docs/cfapps/starter_app_usage.html) para obter ajuda sobre o uso
do aplicativo iniciador.

## Versões de tempo de execução
{: #runtime_versions}

### Versões suportadas
{: #supported_versions}
Esse buildpack suporta as versões a seguir; aquelas marcadas como descontinuadas serão removidas em uma liberação de buildpack futura. Veja [Instrução de suporte da Microsoft para liberações LTS e atuais](https://www.microsoft.com/net/core/support).

#### Conjunto de ferramentas project.json (descontinuado)

| Versão SDK .NET        | Padrão |
|-------------------------|---------|
| 1.0.0-preview2-003156   |   Não    |
| 1.0.0-preview2-1-003177 |   Não    |

#### Conjunto de ferramentas SDK MSBuild

| Versão SDK .NET        | Padrão |
|-------------------------|---------|
| 1.0.0-preview4-004233   |   Não    |
| 1.0.1                   |   Sim   |

#### Versões de runtime do .NET Core

| Versão do runtime do .NET Core | Tipo de Release | Padrão |
|---------------------------|--------------|---------|
| 1.0.0                     | LTS          |   Não    |
| 1.0.1                     | LTS          |   Não    |
| 1.0.3                     | LTS          |   Não    |
| 1.0.4                     | LTS          |   Sim   |
| 1.1.0                     | Atual      |   Não    |
| 1.1.1                     | Atual      |   Não    |

### Especificando a versão SDK .NET

Controle a versão .NET SDK com um global.json opcional no diretório raiz do aplicativo. Por exemplo:
```
   {
      "projects": [ "src" ],
      "sdk": {
        "version": "1.0.1"
      }
   }
```
{: codeblock}

Se não especificado, o conjunto de ferramentas MSBuild para o tempo de execução Long-term-support (LTS) mais recente será usado. Para usar o conjunto de ferramentas project.json, é possível especificar uma das versões project.json listadas acima, mas também será necessário lembrar-se de que essas versões serão removidas no futuro.

## Customizando fontes de pacote NuGet
{: #customizing_nuget_package_sources}

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

Para obter informações sobre como desenvolver localmente usando o Visual Studio,
consulte [Desenvolvendo com o Visual Studio](/docs/starters/deploy_vs.html){: new_window}.

## Enviando por push um aplicativo publicado
{: #pushing_published_app}

Se você quiser que seu aplicativo contenha todos os binários necessários para que o buildpack não faça download de
qualquer binário externo, será possível enviar por push um aplicativo *autocontido* publicado.  Consulte
[Tipos de
app .NET Core](https://docs.microsoft.com/en-us/dotnet/articles/core/app-types){: new_window} para obter mais informações sobre
aplicativos autocontidos.

Para publicar um aplicativo, emita um comando como:
```
  dotnet publish -r ubuntu.14.04-x64
```
{: codeblock}

Para aplicativos autocontidos, o app poderá então ser enviado por push do diretório
```
  bin/<Debug|Release>/<framework>/<runtime>/publish
```
{: codeblock}
específico.

Para aplicativos móveis, o app poderá ser enviado por push do diretório
```
  bin/<Debug|Release>/<framework>/publish
```
{:codeblock}
específico.

Observe também que se você estiver usando um arquivo manifest.yml em seu
aplicativo, será possível especificar o caminho para a pasta de saída de publicação no
manifest.yml.  Assim, não é necessário estar nessa pasta quando enviar o aplicativo por
push.

## Implementando apps com diversos projetos
{: #developing_apps_with_multiple_projects}

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
  project = src/MyApp.Web/MyApp.Web.csproj
```
{: codeblock}

Neste exemplo, o buildpack compilaria automaticamente os projetos
*MyApp.DAL* e *MyApp.Services* se eles estivessem listados como
dependências no arquivo project.json para *MyApp.Web*, mas o buildpack
somente tentaria executar o projeto principal, *MyApp.Web*, com dotnet run
-p src/MyApp.Web.

## Configuração do Aplicativo
{: #application_configuration}

### Configurando seu aplicativo para atender na porta adequada
{: #configuring_listen_proper_port}

O buildpack executará seu aplicativo com o comando *dotnet run* e
passará o argumento de linha de comandos da seguinte forma
```
  --server.urls http://0.0.0.0:${PORT}
```
{: codeblock}

Seu aplicativo precisará passar este argumento ao kestrel para assegurar que o kestrel esteja atendendo na porta correta.

Para implementar a passagem desse argumento, as amostras fornecidas no repositório de amostras da CLI e os modelos fornecidos pelo Visual Studio
requererão pequenas modificações antes da implementação no Bluemix.

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

Para o conjunto de ferramentas project.json, inclua esta linha no arquivo project.json:
```
  "Microsoft.Extensions.Configuration.CommandLine": "1.0.1",
```
{: codeblock}

Para o conjunto de ferramentas MSBuild, inclua esta linha no arquivo .csproj:
```
  <PackageReference Include="Microsoft.Extensions.Configuration.CommandLine" Version="1.0.1" />
```
{:codeblock}

Inclua uma instrução *using* no arquivo que contém seu método Main:
```
  using Microsoft.Extensions.Configuration;
```
{: codeblock}

### Assegure-se de que seu aplicativo tenha todos os arquivos necessários na pasta de saída de construção
{: #configure_output_files}

#### Usando o conjunto de ferramentas project.json

Inclua a propriedade a seguir na seção `buildOptions` de project.json:
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

No método Startup.cs `Startup`, remova a linha a seguir:
```
  .SetBasePath(env.ContentRootPath)
```
{: codeblock}

No método Program.cs `Main`, remova a linha a seguir:
```
  .UseContentRoot(Directory.GetCurrentDirectory())
```
{: codeblock}

Essas mudanças devem permitir que a CLI .NET localize as `Views`
do seu aplicativo, uma vez que elas agora serão copiadas na saída de construção quando o
comando `dotnet run` for executado.  Se o seu aplicativo tiver quaisquer outros arquivos, como arquivos de configuração json, que são necessários no tempo de execução, também será necessário incluí-los na seção de `include` de `copyToOutput` no arquivo project.json de seu projeto.

#### Usando o conjunto de ferramentas MSBuild

Inclua um elemento `<Content>` no elemento `<ItemGroup>` do arquivo .csproj:
```
  <ItemGroup>
    <Content Include="wwwroot/**/*;Areas/**/Views/*;Views/*;appsettings.json">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
      <CopyToPublishDirectory>Always</CopyToPublishDirectory>
    </Content>
  </ItemGroup>
```
{: codeblock}

No método Startup.cs `Startup`, remova a linha a seguir:
```
  .SetBasePath(env.ContentRootPath)
```
{: codeblock}

No método Program.cs `Main`, remova a linha a seguir:
```
  .UseContentRoot(Directory.GetCurrentDirectory())
```
{: codeblock}

Essas mudanças devem permitir que a CLI de .NET localize as `Visualizações` de seu aplicativo, uma vez que elas agora serão copiadas na saída de construção quando o comando `dotnet publish` for executado. Se o seu aplicativo tiver quaisquer outros arquivos, como arquivos de configuração json, que são necessários no tempo de execução, também será necessário incluí-los na propriedade de `Include` do elemento `Content` no arquivo .csproj de seu projeto, separados por pontos e vírgulas.

## Compilando seu aplicativo na configuração de liberação (apenas MSBuild)
{: #compiling_in_release_configuration}

Os projetos baseados em MSBuild são agora publicados usando o comando `dotnet publish` durante a preparação. Por padrão, o buildpack publicará seu aplicativo na configuração de `Depuração`.
Para publicar seu aplicativo na configuração de `Liberação`, configure a variável de ambiente `PUBLISH_RELEASE_CONFIG` como `true`.

Isso pode ser feito com o CloudFoundry CLI com o comando a seguir:

```shell
  cf set-env <app_name> PUBLISH_RELEASE_CONFIG true
```

Como alternativa, é possível configurar a variável no arquivo manifest.yml do aplicativo:

```yml
---
applications:
- name: sample-aspnetcore-app
  memory: 512M
  env:
    PUBLISH_RELEASE_CONFIG: true
```

## Desativando o cache de pacotes NuGet
{: #disabling_the_nuget_package_cache}

Em algumas situações, pode ser necessário limpar o cache de pacotes NuGet de seu aplicativo. Fazer isso limpará quaisquer pacotes NuGet em cache existentes e evitará que o buildpack armazene em cache quaisquer novos pacotes.

Isso pode ser feito configurando a variável de ambiente `CACHE_NUGET_PACKAGES` como `false` usando o CloudFoundry CLI:

```shell
  cf set-env <app_name> CACHE_NUGET_PACKAGES false
```

Como alternativa, é possível configurar a variável de ambiente `CACHE_NUGET_PACKAGES` como `false` no arquivo manifest.yml do aplicativo:

```yml
---
applications:
- name: sample-aspnetcore-app
  memory: 512M
  env:
    CACHE_NUGET_PACKAGES: false
```

## Usando bibliotecas nativas customizadas
{: #using_custom_native_libraries}

Algumas bibliotecas podem requerer o uso de um pacote NuGet e alguns arquivos de biblioteca nativa (arquivos .so). Para usar essas bibliotecas com o buildpack, é necessário colocá-las em uma pasta chamada "ld_library_path" na pasta raiz do aplicativo. O buildpack incluirá automaticamente esse caminho na variável de ambiente `LD_LIBRARY_PATH` durante a preparação. Como alternativa, é possível especificar a variável de ambiente `LD_LIBRARY_PATH` no arquivo `manifest.yml` do aplicativo ou usando o comando `cf set-env` para usar um nome de pasta diferente de "ld_library_path". Nesse caso, o buildpack anexará esse caminho customizado ao `LD_LIBRARY_PATH` gerado pelo buildpack.

## FAQ de resolução de problemas
{: #troubleshooting_faq}

**Q**: o aplicativo falha ao implementar com a mensagem: `API/0App instance exited ... payload: {... "reason"=>"CRASHED", "exit_status"=>-1, ...}`.  O que isso significa?

**A**: se você estiver recebendo uma mensagem semelhante ao enviar por push seu
aplicativo, provavelmente seu aplicativo está excedendo os limites de cota de memória ou de disco.  Isso pode ser resolvido aumentando as cotas para seu aplicativo.

**Q**: ao ser implementado, meu aplicativo falha com a mensagem: `Falha ao compactar droplet: sinal: canal interrompido` ou `Sem espaço no dispositivo`. Como posso corrigir isso?

**A**: os projetos enviados por push do código-fonte que contêm um grande número de dependências de pacotes NuGet podem, às vezes, causar esse erro quando o cache de pacote NuGet está ativado. Configure a variável de ambiente `CACHE_NUGET_PACKAGES` como `false` para desativar o cache.

# rellinks
{: #rellinks notoc}
## geral
{: #general notoc}
* [NuGet](https://docs.nuget.org/Consume/Overview){: new_window}
* [Visão geral do ASP.NET Core](http://docs.asp.net/en/latest/conceptual-overview/aspnet.html){: new_window}
