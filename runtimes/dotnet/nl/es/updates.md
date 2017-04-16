---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-06"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Últimas actualizaciones para el paquete de compilación de ASP.NET Core
{: #latest_updates}


Una lista de las últimas actualizaciones del paquete de compilación de aspnet.

## 10 de octubre de 2016: Se ha actualizado el paquete de compilación de ASP.NET Core v1.0.1-20161005-1225

* Adición de soporte para .NET Core 1.0.1
* Arreglo de un problema intermitente que hacía que el despliegue fallada cuando se almacenaba en la memoria caché paquetes NuGet

## 31 de agosto de 2016: Se ha actualizado el paquete de compilación de ASP.NET Core v1.0-20160826-1345

* Añada soporte para ejecutar scripts previos y posteriores a la compilación utilizando NPM y Bower para instalar bibliotecas css y javascript de interfaz de usuario.
* Mueva el paquete de compilación del estado Beta al estado GA

## 11 de julio de 2016: Se ha actualizado el paquete de compilación de ASP.NET Core v0.9-20160706-1603

Esta versión del paquete de compilación incluye los siguientes cambios:

* Esta versión del paquete de compilación da soporte a la compilación de la Vista previa 2 de .NET CLI 1.0 y a .NET Core 1.0 RTM
* El paquete de compilación sigue dando soporte a la Vista previa 1 de .NET CLI 1.0 y a .NET Core 1.0 RC2
* La versión predeterminada de .NET CLI que se instalará es ahora 1.0.0-preview2-003121

## 10 de junio de 2016: Se ha actualizado el paquete de compilación de ASP.NET Core v0.8.1-20160526-0957

Esta versión del paquete de compilación incluye los siguientes cambios:

* El nombre del tiempo de ejecución se cambia de ASP.NET 5 a ASP.NET Core.
* El número de versión del paquete de compilación se incluye en el resultado del script de detección.
* Esta versión del paquete de compilación elimina el soporte de aplicaciones basadas en DNX que utilizan CoreCLR RC1 y más bajo.
* Esta versión del paquete de compilación da soporte a .NET CLI y .NET Core RC2.
* El paquete de compilación detecta proyectos con un archivo project.json o archivos *.runtimeconfig.json de la salida de publicación.

## 22 de octubre de 2015: Se ha actualizado el paquete de compilación de ASP.NET 5 v0.7-20151022-1257

* Esta versión del paquete de compilación elimina Mono y, en su lugar, soporta la versión Beta 8 CoreCLR.

## 18 de septiembre de 2015: Se ha actualizado el paquete de compilación de ASP.NET 5 v0.6-20150916-1220

* Esta versión del paquete de compilación admite los cambios de Beta 7 DNX, y puede ejecutar aplicaciones dependientes de releases beta anteriores con el siguiente mandato de inicio personalizado:

```
   dnx src/dotnetstarter kestrel --server.urls http://${VCAP_APP_HOST}:${PORT}
```
{: codeblock}

* El uso del servidor web Nowin se ha eliminado del paquete de compilación y en su lugar se utiliza el servidor web [Kestrel]{https://github.com/aspnet/KestrelHttpServer}.

# rellinks
{: #rellinks}
## general
{: #general}
* [Tiempo de ejecución de núcleo de Dotnet](index.html)
