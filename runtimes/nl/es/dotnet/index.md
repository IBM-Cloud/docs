---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# ASP.NET Core 
{: #dotnet_core}
*Última actualización: 30 de mayo de 2016*

El tiempo de ejecución de ASP.NET en {{site.data.keyword.Bluemix}} está basado en el paquete de compilación de ASP.NET Core.
ASP.NET Core es una infraestructura de código abierto modular para crear aplicaciones web .NET.
.Net Core es un tiempo de ejecución pequeño multiplataforma que puede ser objetivo de las aplicaciones de ASP.NET Core. Se combinan para habilitar aplicaciones web modernas basadas en la nube.
{: shortdesc}

## Detección
{: #detection}
El paquete de compilación ASP.NET Core de Bluemix se utiliza si hay uno o más archivos project.json en cualquier lugar de la aplicación, o si la aplicación se recibe del directorio de salida del mandato *dotnet publish*.

## Aplicación de inicio
{: #starter_application}

{{site.data.keyword.Bluemix}} proporciona una aplicación de inicio de ASP.NET Core.  La aplicación de inicio de ASP.NET Core es una app sencilla que proporciona una plantilla que puede utilizar.
Puede experimentar con la app de inicio, y realizar y enviar los cambios por push al entorno de Bluemix.  Consulte [Utilización de las aplicaciones de inicio](../../cfapps/starter_app_usage.html) para obtener ayuda con el uso de la aplicación de inicio.

## Versiones de tiempo de ejecución
{: #runtime_versions}

### Especificación de la versión de .NET CLI

Controle la versión de .NET CLI con un global.json opcional en el directorio raíz de la aplicación. Por ejemplo:
```
   {
      "projects": [ "src" ],
      "sdk": {
        "version": "1.0.0-preview1-002702"
      }
   }
```
{: codeblock}

Si no se especivca, se utiliza el Release Candidate más estable actualmente.

### Personalización de las fuentes de paquetes de NuGet

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
Para coincidir más a fondo con cómo se ejecuta la aplicación Bluemix, siga las intrucciones de Linux para .NET Core, auque el desarrollo de la aplicación en Linux no es necesario. 

La herramienta Yeoman puede utilizarse para generar nuevas plantillas de proyecto tal como se describen en
[Creación de proyectos con Yeoman](http://docs.asp.net/en/latest/client-side/yeoman.html).

## Envío por push de una aplicación publicada

Si desea que la aplicación contenga todos sus binarios necesarios de modo que el paquete de compilación no descargue ningún binario externo, puede enviar por push una aplicación *autocontenida* publicada.
Consulte [Tipos de portabilidad en .Net Core](http://dotnet.github.io/docs/core-concepts/app-types.html){: new_window} para obtener más información sobre las aplicaciones autocontenidas.


Para publicar un problema de aplicación, emita un mandato como el siguiente:
```
  dotnet publish -r ubuntu.14.04-x64 
```
{: codeblock}
  
La app podrá enviar por push desde el directorio 
```
  bin/<Debug|Release>/<framework>/<runtime>/publish
```
{: codeblock}
.

Tenga en cuenta que si utiliza un archivo manifest.yml en la aplicación, puede especificar la vía de acceso a la carpeta de salida de publicación en manifest.yml. Después no tendrá que estar en esa carpeta cuando envíe por push la aplicación. 

## Despliegue de apps con varios proyectos

Para desplegar una app que contiene varios proyectos, será necesario especificar qué proyecto desea que el paquete de compilación ejecute como proyecto principal. Esto puede llevarse a cabo creando un archivo .deployment en la carpeta raíz de la solución que establece la vía de acceso al proyecto principal. La vía de acceso al proyecto principal puede especificarse como carpeta de proyecto o el archivo de proyecto (.xproj o .csproj).

Por ejemplo, si una solución que contiene tres proyectos, *MyApp.DAL*, *MyApp.Services* y *MyApp.Web* en la carpeta *src*, y *MyApp.Web* es el proyecto principal, el formato del archivo .deployment sería el siguiente:
```
  [config]
  project = src/MyApp.Web
```
{: codeblock}

En este ejemplo, el paquete de compilación compila automáticamente los proyectos *MyApp.DAL* y *MyApp.Services* si están listados como dependencias en el archivo project.json para *MyApp.Web*, pero el paquete de compilación sólo intentará ejecutar el proyecto principal, *MyApp.Web*, con dotnet run -p src/MyApp.Web. La vía de acceso a *MyApp.Web*, suponiendo que este proyecto es yn proyecto xproj, también podría especificarse como 
```
  project = src/MyApp.Web/MyApp.Web.xproj 
```
{: codeblock}

## Utilización de ejemplos del repositorio cli-samples y la plantilla de Visual Studio

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

Añada la siguiente dependencia a project.json: 
```
  "Microsoft.Extensions.Configuration.CommandLine": "1.0.0-rc2-final",
```
{: codeblock}

Añada una sentencia *using* al archivo que contiene su método principal: 
```
  using Microsoft.Extensions.Configuration;
```
{: codeblock}

# rellinks
{: #rellinks}
## general
{: #general}
* [Últimas actualizaciones para el paquete de compilación de ASP.NET Core](updates.html)
* [NuGet](https://docs.nuget.org/Consume/Overview){: new_window}
* [Visión general de ASP.NET Core](http://docs.asp.net/en/latest/conceptual-overview/aspnet.html){: new_window}
