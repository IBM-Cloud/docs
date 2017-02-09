---



copyright:

  years: 2015，2017

lastupdated: "2017-01-12"



---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# (En desuso) CLI en modalidad de desarrollo
{: #devmodecli}

**Esta CLI ha quedado en desuso:** En lugar de utilizar la CLI del modo de desarrollo (dev_mode), utilice IBM Eclipse Tools for Bluemix o DevOps Web IDE. Puede seguir utilizando la CLI dev_mode hasta el 30 de junio 2016.

Con la interfaz de línea de mandatos de modalidad de desarrollo de Bluemix (CLI de dev_mode), puede actualizar las apps mientras las apps se están ejecutando en la nube. La CLI de dev_mode está creada como un plug-in de CLI cf y soporta tanto apps Liberty como IBM Node.js.
{: shortdesc}


Puede llevar a cabo las siguientes tareas con la CLI de dev_mode:
- Conmute su app entre la modalidad de desarrollo y la modalidad normal.
- Actualice archivos de aplicación de forma incremental sin un nuevo envío push.
- Inicie, detenga o reinicie la app en el contenedor existente.

## Instalación del plug-in dev_mode
**Requisito previo:** Antes de empezar, instale la CLI de Cloud Foundry. Consulte [Empiece a escribir código con la interfaz de línea de mandatos de Cloud Foundry](https://github.com/cloudfoundry/cli) para obtener detalles.


Utilice uno de los siguientes métodos para instalar la herramienta de línea de mandatos dev_mode:
- Instale localmente.
  1. Descargue el plug-in de dev_mode para su plataforma desde el [Repositorio de plug-ins de CLI de IBM Bluemix](http://plugins.ng.bluemix.net).
  2. Vaya a la carpeta en la que se ha guardado el complemento dev_mode e instale dicho complemento utilizando el mandato cf install-plugin. Por ejemplo:

        ```
        cf install-plugin dev_mode-linux64
        ```

- Instale desde el repositorio de CLI de Bluemix.
  1. Añada el repositorio bluemix-repo en los repositorios de la CLI de Cloud Foundry utilizando el siguiente mandato:

        ```
        cf add-plugin-repo bluemix-repo http://plugins.ng.bluemix.net
        ```

  2. Escriba cf repo-plugins. El plug-in dev_mode aparecerá en el repositorio bluemix-repo.

		```
        cf repo-plugins
        ```

  3. Instale el plug-in dev_mode en los plug-ins de la CLI de Cloud Foundry utilizando el siguiente mandato:

        ```
        cf install-plugin dev_mode -r bluemix-repo
        ```

## Visualización de mandatos dev_mode

Para visualizar todos los mandatos de CLI dev_mode, utilice el siguiente mandato:

```
cf plugins
```

## Índice de mandatos de CLI de dev_mode
{: #dev_mode_cmds_index}

Utilice el índice en la siguiente tabla para hacer referencia a los mandatos de CLI dev_mode utilizados con frecuencia:

<table summary="Índice de mandatos de dev_mode">
 <caption>Tabla 1. Mandatos de dev_mode</caption>
 <thead>
 <th colspan="4">Mandatos de dev_mode</th>
 </thead>
 <tbody>
 <tr>
 <td>[help](#help)</td>
 <td>[mode](#mode)</td>
 <td>[status](#status)</td>
 <td>[update-file](#update_file)</td>
 </tr>
 <tr>
 <td>[delete-file](#delete_file)</td>
 <td>[start-inplace](#start_inplace)</td>
 <td>[stop-inplace](#stop_inplace)</td>
 <td>[restart-inplace](#restart_inplace)</td>
 </tr>
  </tbody>
 </table>


## help
{: #help}

Muestra la ayuda sobre un mandato.

```
cf help <nombre_mandato>
```


## mode
{: #mode}

Cambia la modalidad de la app.

```
cf mode <nombre_app> <dev|normal>
```
<strong>Opciones de mandato</strong>:

   <dl>
   <dt>dev</dt>
   <dd>Modalidad de desarrollo.</dd>
   <dt>normal</dt>
   <dd>Modalidad de producción.</dd>
   </dl>


## status
{: #status}

Muestra la modalidad de la app y el estado de tiempo de ejecución.
```
cf status <nombre_app>
```



## update-file
{: #update_file}

Actualiza los archivos de aplicación en la nube.

```
cf update-file <vía_acceso_remota> <vía_acceso_local> [opciones_mandato]
```


<strong>Opciones de mandato</strong>:

   <dl>
   <dt>expand</dt>
   <dd>Indica si los archivos cargados se deben extraer del archivo zip.</dd>
   <dt>restart</dt>
   <dd>Reinicia el tiempo de ejecución de la app después de que se hayan actualizado los archivos.</dd>
   </dl>



## delete-file
{: #delete_file}

Suprime los archivos de aplicación en la nube.

```
cf delete-file <vía_acceso_remota> [opciones_mandato]
```


<strong>Opciones de mandato</strong>:
 <dl>
   <dt>restart</dt>
   <dd>Reinicia el tiempo de ejecución de la app después de que se hayan actualizado los archivos.</dd>
  </dl>


## start-inplace
{: #start_inplace}
Inicia la app en el contenedor existente.

```
cf start-inplace <nombre_app>
```



## stop-inplace
{: #stop_inplace}
Detiene la app en el contenedor existente.

```
cf stop-inplace <nombre_app>
```



## restart-inplace
{: #restart_inplace}

Reinicia la app en el contenedor existente.

```
cf restart-inplace <nombre_app>
```



# Enlaces relacionados
{: #rellinks}

## Enlaces relacionados
{: #general}
* [CLI de modalidad de desarrollo ![icono de enlace externo](../../../icons/launch-glyph.svg)](http://clis.ng.bluemix.net/ui/repository.html#cf-plugins){:new_window}
* [DevOps Web IDE ![icono de enlace externo](../../../icons/launch-glyph.svg)](https://hub.jazz.net/docs/deploy/){:new_window}
