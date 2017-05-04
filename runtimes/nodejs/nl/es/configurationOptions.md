---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Opciones de configuración
{: #configuration_options}
{: shortdesc}

Dispone de diversas opciones para configurar el paquete de compilación sdk-for-nodejs.

## Scripts NPM
{: #npm_scripts}
NPM proporciona un recurso de creación de scripts que le permite ejecutar scripts, incluidos los scripts **previos a la instalación** y **posteriores a la instalación** que se aplican antes y después de que estén instalados los node_modules.  Consulte [npm-scripts ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://docs.npmjs.com/misc/scripts) para ver más detalles.

## Comportamiento de la memoria caché
{: #cache_behavior}
{{site.data.keyword.Bluemix}} mantiene un directorio de memoria caché por aplicación de nodo, que es persistente entre las compilaciones. La memoria caché almacena dependencias resueltas para que no se descargue ni se instale cada vez que se despliegue la app.  Por ejemplo, suponga que myapp depende de **express**.  A continuación, la primera vez que se despliegue myapp, se descargará el módulo **express**.  En los despliegues posteriores de myapp, se utilizará la instancia en memoria caché de **express**. El comportamiento predeterminado es almacenar en memoria caché todos los node_modules instalados por NPM y los bower_components instalados por bower.

Utilice la variable NODE_MODULES_CACHE para determinar si el paquete de compilación de nodos utiliza o no tiene en cuenta la memoria caché desde compilaciones anteriores. El valor predeterminado es true.  Para inhabilitar el almacenamiento en memoria caché del conjunto NODE_MODULES_CACHE en false, por ejemplo a través de la línea de mandatos de cf:
```
    $ cf set-env myapp NODE_MODULES_CACHE false
```
{: codeblock}

Tenga en cuenta que los node_modules que se incluyen en la aplicación no se almacenan en la memoria caché.

Puede utilizar una matriz **cacheDirectories** en el **package.json** de nivel superior para conseguir un control específico a través de los módulos que se almacenan en la memoria caché.  Cuando el elemento **cacheDirectories** ya se encuentra presente en el **package.json**, solo se almacenarán en la memoria caché los módulos que se encuentren en la matriz **cacheDirectories**.  En el ejemplo siguiente, solo se almacenan en la memoria caché los node_modules y bower_components.
```
{
  "cacheDirectories": ["node_modules","bower_components"],
  ...
}
```
{: codeblock}
