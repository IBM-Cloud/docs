---

 

copyright:

  years: 2015, 2016

 

---
{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}


# CLI en modalidad de desarrollo
{: #devmodecli}

*Última actualización: 25 de febrero de 2016*

La Modalidad de desarrollo (dev_mode) es una característica de Bluemix que puede utilizar para trabajar con sus apps mientras se están ejecutando en la nube. La
modalidad
de desarrollo incluye la interfaz de línea de mandatos dev_mode. La CLI de dev_mode está creada como un plug-in de CLI cf y soporta tanto apps Liberty como IBM Node.js.

La CLI de dev_mode ofrece las siguientes características:
- Conmute su app entre la modalidad de desarrollo y la modalidad normal.
- Actualice archivos de aplicación de forma incremental sin un nuevo envío push.
- Inicie, detenga o reinicie la app en el contenedor existente.

## Introducción
**Requisito previo:** Antes de empezar, instale la CLI de Cloud Foundry. Consulte [Empiece a escribir código con la interfaz de línea de mandatos de Cloud Foundry](https://github.com/cloudfoundry/cli) para obtener detalles. 


Utilice uno de los siguientes métodos para instalar la herramienta de línea de mandatos dev_mode.
- Instale localmente.
  1. Descargue el plug-in de dev_mode para su plataforma desde el [Repositorio de plug-ins de CLI de IBM Bluemix](http://plugins.ng.bluemix.net).
  2. Instale el plug-in dev_mode utilizando el mandato cf install-plugin:
  
        ```
        cf install-plugin dev_mode-linux_amd64
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

## Uso
**Para visualizar todos los mandatos de la CLI de dev_mode, utilice el siguiente mandato:**

```
cf plugins
```

### Mandatos de dev_mode

### mode

```
cf mode <nombre_app> <dev|normal>
```

Cambia la modalidad de la app.

### status

```
cf status <nombre_app>
```

Muestra la modalidad de la app y el estado de tiempo de ejecución.

### update-file

```
cf update-file <vía_acceso_remota> <vía_acceso_local> [opciones_mandato]
```

Actualiza los archivos de aplicación en la nube.

Opciones de mandato:

**expand**

Indica si los archivos cargados se deben extraer del archivo zip.

**restart**

Reinicia el tiempo de ejecución de la app después de que se hayan actualizado los archivos.
  
### delete-file

```
cf delete-file <vía_acceso_remota> [opciones_mandato]
```

Suprime los archivos de aplicación en la nube.

Opciones de mandato:

**restart**

Reinicia el tiempo de ejecución de la app después de que se hayan suprimido los archivos.

### start-inplace

```
cf start-inplace <nombre_app>
```

Inicia la app en el contenedor existente.

### stop-inplace

```
cf stop-inplace <nombre_app>
```

Detiene la app en el contenedor existente.

### restart-inplace

```
cf restart-inplace <nombre_app>
```

Reinicia la app en el contenedor existente.



### help

```
cf help <nombre_mandato>
```
Muestra la ayuda sobre un mandato.
