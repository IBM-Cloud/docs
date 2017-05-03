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

El tiempo de ejecución de ASP.NET en {{site.data.keyword.Bluemix}} está basado en el paquete de compilación de ASP.NET Core. ASP.NET Core es una infraestructura de código abierto modular para crear aplicaciones web .NET.
.Net Core es un tiempo de ejecución pequeño multiplataforma que puede ser objetivo de las aplicaciones de ASP.NET Core.
Se combinan para habilitar aplicaciones web modernas basadas en la nube.
{: shortdesc}

## Detección
{: #detection}
El paquete de compilación de ASP.NET Core de Bluemix se utiliza si hay una o más carpetas que contienen un project.json y al menos un archivo .cs en cualquier lugar de la aplicación, o si la aplicación se envía por push desde el directorio de salida del mandato *dotnet publish*.

## Aplicación de inicio
{: #starter_application}

{{site.data.keyword.Bluemix}} proporciona una aplicación de inicio de ASP.NET Core.  La aplicación de inicio de ASP.NET Core es una app sencilla que proporciona una plantilla que puede utilizar. Puede experimentar con la app de inicio, y realizar y enviar los cambios por push al entorno de Bluemix.  Consulte [Utilización de las aplicaciones de inicio](/docs/cfapps/starter_app_usage.html) para obtener ayuda con el uso de la aplicación de inicio.

## Versiones de tiempo de ejecución
{: #runtime_versions}

### Versiones soportadas
{: #supported_versions}
Este paquete de compilación da soporte a las versiones siguientes; las marcadas como en desuso se eliminará en un futuro release del paquete de compilación.  Consulte [Declaración de soporte de Microsoft para LTS y releases actuales](https://www.microsoft.com/net/core/support).

#### Herramientas project.json (en desuso)

| Versión de .NET SDK        | Valor pred. |
|-------------------------|---------|
| 1.0.0-preview2-003156   |   No    |
| 1.0.0-preview2-1-003177 |   No    |

#### Herramientas MSBuild SDK

| Versión de .NET SDK        | Valor pred. |
|-------------------------|---------|
| 1.0.0-preview4-004233   |   No    |
| 1.0.1                   |   Sí   |

#### Versiones de .NET Core Runtime

| Versión de .NET Core Runtime | Tipo de release | Valor pred. |
|---------------------------|--------------|---------|
| 1.0.0                     | LTS          |   No    |
| 1.0.1                     | LTS          |   No    |
| 1.0.3                     | LTS          |   No    |
| 1.0.4                     | LTS          |   Sí   |
| 1.1.0                     | Actual      |   No    |
| 1.1.1                     | Actual      |   No    |

### Especificación de la versión de .NET SDK

Controle la versión de .NET SDK con un global.json opcional en el directorio raíz de la aplicación. Por ejemplo:
```
   {
      "projects": [ "src" ],
      "sdk": {
        "version": "1.0.1"
      }
   }
```
{: codeblock}

Si no se especifica, se utilizan las herramientas MSBuild correspondientes al tiempo de ejecución de soporte a largo plazo (LTS) más reciente.  Para utilizar herramientas project.json, puede especificar una de las versiones de project.json arriba mencionadas, pero tenga en cuenta que estas versiones se retirarán en el futuro.

## Personalización de las fuentes de paquetes de NuGet
{: #customizing_nuget_package_sources}

Controle donde se descargan las dependencias de la aplicación en el archivo NuGet.Config en el directorio raíz de la aplicación. Por ejemplo:
```
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
   <packageSources>
      <add key="NuGet.org" value="https://api.nuget.org/v3/index.json"/>
   </packageSources>
   </configuration>
```
{: codeblock}

## Desarrollo de aplicaciones localmente
{: #developing_locally}

Para obtener más información sobre la ejecución de una aplicación de ASP.NET Core localmente, consulte
[Iniciación a ASP.NET](http://docs.asp.net/en/latest/getting-started/index.html).
Para coincidir más a fondo con cómo se ejecuta la aplicación Bluemix, siga las instrucciones de Linux para .NET Core, aunque el desarrollo de la aplicación en Linux no es necesario.

La herramienta Yeoman puede utilizarse para generar nuevas plantillas de proyecto tal como se describen en
[Creación de proyectos con Yeoman](http://docs.asp.net/en/latest/client-side/yeoman.html).

Para más información sobre cómo desarrollar localmente utilizando Visual Studio, consulte [Desarrollo con Visual Studio](/docs/starters/deploy_vs.html){: new_window}.

## Envío por push de una aplicación publicada
{: #pushing_published_app}

Si desea que la aplicación contenga todos sus binarios necesarios de modo que el paquete de compilación no descargue ningún binario externo, puede enviar por push una aplicación *autocontenida* publicada.  Consulte [Tipos de app de .NET Core ](https://docs.microsoft.com/en-us/dotnet/articles/core/app-types){: new_window} para obtener más información sobre aplicaciones autocontenidas.

Para publicar un problema de aplicación, emita un mandato como el siguiente:
```
  dotnet publish -r ubuntu.14.04-x64
```
{: codeblock}

Para aplicaciones autocontenidas, la app se podrá enviar por push desde el directorio
```
  bin/<Debug|Release>/<framework>/<runtime>/publish
```
{: codeblock}
.

Para aplicaciones portables, la app se podrá enviar por push desde el directorio
```
  bin/<Debug|Release>/<framework>/publish
```
{:codeblock}
.

Tenga en cuenta que si utiliza un archivo manifest.yml en la aplicación, puede especificar la vía de acceso a la carpeta de salida de publicación en manifest.yml.  Después no tendrá que estar en esa carpeta cuando envíe por push la aplicación.

## Despliegue de apps con varios proyectos
{: #developing_apps_with_multiple_projects}

Para desplegar una app que contiene varios proyectos, será necesario especificar qué proyecto desea que el paquete de compilación ejecute como proyecto principal. Esto puede llevarse a cabo creando un archivo .deployment en la carpeta raíz de la solución que establece la vía de acceso al proyecto principal. La vía de acceso al proyecto principal puede especificarse como carpeta de proyecto o el archivo de proyecto (.xproj o .csproj).

Por ejemplo, si una solución que contiene tres proyectos, *MyApp.DAL*, *MyApp.Services* y *MyApp.Web* en la carpeta *src*, y *MyApp.Web* es el proyecto principal, el formato del archivo .deployment sería el siguiente:
```
  [config]
  project = src/MyApp.Web/MyApp.Web.csproj
```
{: codeblock}

En este ejemplo, el paquete de compilación compila automáticamente los proyectos *MyApp.DAL* y *MyApp.Services* si están listados como dependencias en el archivo project.json para *MyApp.Web*, pero el paquete de compilación sólo intentará ejecutar el proyecto principal, *MyApp.Web*, con dotnet run -p src/MyApp.Web.

## Configuración de la aplicación
{: #application_configuration}

### Configuración de la aplicación para que escuche en el puerto correcto
{: #configuring_listen_proper_port}

El paquete de compilación ejecutará la aplicación con el mandato *dotnet run* y pasará el argumento de línea de mandato como se indica a continuación
```
  --server.urls http://0.0.0.0:${PORT}
```
{: codeblock}

La aplicación necesitará pasar este argumento a kestrel para asegurarse de que kestrel esté escuchando en el puerto correcto.

Para implementar que este argumento se pase, los ejemplos proporcionados en el repositorio cli-samples y las plantillas proporcionadas por Visual Studio requieren ligeras modificaciones antes de desplegarse en Bluemix.

Son necesarias modificaciones en el método principal tal como se indican en los comentarios del siguiente ejemplo:

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

Para herramientas project.json, añada esta línea a su archivo project.json:
```
  "Microsoft.Extensions.Configuration.CommandLine": "1.0.1",
```
{: codeblock}

Para herramientas MSBuild, añada esta línea a su archivo .csproj:
```
  <PackageReference Include="Microsoft.Extensions.Configuration.CommandLine" Version="1.0.1" />
```
{:codeblock}

Añada una sentencia *using* al archivo que contiene su método principal:
```
  using Microsoft.Extensions.Configuration;
```
{: codeblock}

### Asegúrese de la aplicación tenga todos los archivos necesarios en la carpeta de salida de la compilación
{: #configure_output_files}

#### Utilización de herramientas project.json

Añada la siguiente propiedad a la sección `buildOptions` de project.json:
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

En el método `Startup` de Startup.cs, elimine la siguiente línea:
```
  .SetBasePath(env.ContentRootPath)
```
{: codeblock}

En el método `Main` de Program.cs, elimine la siguiente línea:
```
  .UseContentRoot(Directory.GetCurrentDirectory())
```
{: codeblock}

Estos cambios deben permitir que .NET CLI encuentre las `Vistas` de la aplicación porque ahora se copiarán en la salida de la compilación cuando se ejecute el mandato `dotnet run`.  Si la aplicación tiene otros archivos, como los archivos de configuración json, que son necesarios en el tiempo de ejecución, también deberá añadirlos a la sección `include` de `copyToOutput` del archivo project.json correspondiente a su proyecto.

#### Utilización de herramientas MSBuild

Añada un elemento `<Content>` al elemento `<ItemGroup>` del archivo .csproj:
```
  <ItemGroup>
    <Content Include="wwwroot/**/*;Areas/**/Views/*;Views/*;appsettings.json">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
      <CopyToPublishDirectory>Always</CopyToPublishDirectory>
    </Content>
  </ItemGroup>
```
{: codeblock}

En el método `Startup` de Startup.cs, elimine la siguiente línea:
```
  .SetBasePath(env.ContentRootPath)
```
{: codeblock}

En el método `Main` de Program.cs, elimine la siguiente línea:
```
  .UseContentRoot(Directory.GetCurrentDirectory())
```
{: codeblock}

Estos cambios deben permitir que .NET CLI encuentre las `Vistas` de la aplicación porque ahora se copiarán en la salida de la compilación cuando se ejecute el mandato `dotnet publish`.  Si la aplicación tiene otros archivos, como los archivos de configuración json, que son necesarios en el tiempo de ejecución, también deberá añadirlos a la propiedad `Include` del elemento `Content` del archivo project.json correspondiente a su proyecto, separados por signos de punto y coma.

## Compilación de la aplicación en la configuración del Release (solo MSBuild)
{: #compiling_in_release_configuration}

Los proyectos que se basan en MSBuild ahora se publican utilizando el mandato `dotnet publish` durante la transferencia.  De forma predeterminada, el paquete de compilación publicará la aplicación en la configuración `Debug`.
Para publicar la aplicación en la configuración `Release`, establezca la variable de entorno `PUBLISH_RELEASE_CONFIG` en `true`.

Puede hacerlo con la CLI de CloudFoundry con el siguiente mandato:

```shell
  cf set-env <app_name> PUBLISH_RELEASE_CONFIG true
```

Como alternativa, puede establecer la variable en el archivo manifest.yml de la aplicación:

```yml
---
applications:
- name: sample-aspnetcore-app
  memory: 512M
  env:
    PUBLISH_RELEASE_CONFIG: true
```

## Inhabilitación de la memoria caché del paquete NuGet
{: #disabling_the_nuget_package_cache}

En algunas situaciones puede ser necesario borrar la memoria caché del paquete NuGet para la aplicación.  Esto borrará los paquetes NuGet existentes en memoria caché e impedirá que el paquete de compilación almacene en memoria caché paquetes nuevos.

Puede hacerlo estableciendo la variable de entorno `CACHE_NUGET_PACKAGES` en `false` con la CLI de CloudFoundry:

```shell
  cf set-env <app_name> CACHE_NUGET_PACKAGES false
```

Como alternativa, puede establecer la variable de entorno `CACHE_NUGET_PACKAGES` en `false` en el archivo manifest.yml de la aplicación:

```yml
---
applications:
- name: sample-aspnetcore-app
  memory: 512M
  env:
    CACHE_NUGET_PACKAGES: false
```

## Utilización de bibliotecas nativas personalizadas
{: #using_custom_native_libraries}

Algunas bibliotecas pueden requerir que utilice un paquete NuGet y algunos archivos de bibliotecas nativas ( archivos .so).  Para utilizar estas bibliotecas con el paquete de compilación, debe colocarlas en una carpeta denominada "ld_library_path" en la carpeta raíz de la aplicación.
El paquete de compilación añadirá automáticamente esta vía de acceso a la variable de entorno `LD_LIBRARY_PATH` durante la transferencia.  Como alternativa, puede especificar la variable de entorno `LD_LIBRARY_PATH` en el archivo `manifest.yml` de la aplicación o mediante el mandato `cf set-env` para que utilice un nombre de carpeta que no sea "ld_library_path".  En este caso, el paquete de compilación añadirá esta vía de acceso personalizada a la variable `LD_LIBRARY_PATH` generada por el paquete de compilación.

## Preguntas más frecuentes (FAQ) de resolución de problemas
{: #troubleshooting_faq}

**P**: Mi aplicación no se despliega y aparece el mensaje: `API/0App instance exited ... payload: {... "reason"=>"CRASHED", "exit_status"=>-1, ...}`.  ¿Qué significa?

**R**: Si recibe un mensaje parecido cuando envía la aplicación, lo más probable es que se deba que la aplicación supera los límites de cuota de memoria o de disco.  Se puede solucionar aumentando las cuotas para la aplicación.

**P**: Mi aplicación no se puede desplegar con el mensaje: `Failed to compress droplet: signal: broken pipe` o `No space left on device`.  ¿Cómo lo puedo solucionar?

**R**: Los proyectos enviados por push desde el código fuente que contienen un gran número de dependencias de paquetes NuGet pueden generar este error cuando la memoria caché de paquetes NuGet está habilitada.  establezca la variable de entorno `CACHE_NUGET_PACKAGES` en `false` para inhabilitar la memoria caché.

# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
* [NuGet](https://docs.nuget.org/Consume/Overview){: new_window}
* [Visión general de ASP.NET Core](http://docs.asp.net/en/latest/conceptual-overview/aspnet.html){: new_window}
