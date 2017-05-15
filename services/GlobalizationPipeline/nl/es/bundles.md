---

copyright:
  years: 2015, 2017
lastupdated: "2016-08-30"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Cómo trabajar con paquetes
{: #globalizationpipeline_workingwithbundles}

Cada paquete que cree contiene los pares clave valor del archivo de recursos y el conjunto completo de traducciones que se han generado.
{:shortdesc}

Los archivos de recursos que suba pueden ser de cualquiera de los formatos siguientes y deben tener contenido en el formato de pares clave/valor que representan las series de interfaz de usuario de la app.


* Tipo de archivo: *archivos Properties de Java™ (.properties)*<br>
Ejemplo:
```js
logout=Logout 
back=Back 
examples=Menu 
home=Home 
web=Web 
enterprise=Enterprise 
extra=Resources 
about=About 
settings=Settings 
help=Help 
support=Support 
topics=Topics 
appExitMsg=Are you sure you want to quit the application?
```
* Tipo de archivo: *AMD I18N (.js)*<br>
Ejemplo:
```js
define({
    "root": {
       logout: "Logout",
       back: "Back",
       examples: "Menu",
       home: "Home",
       web: "Web",
       enterprise: "Enterprise",
       extra: "Resources",
       about: "About",
       settings: "Settings",
       help: "Help",
       support: "Support",
       topics: "Topics",
       appExitMsg: "Are you sure you want to quit the application?"
    }
});
``` 
* Tipo de archivo: *JSON (.json)*<br>
Ejemplo:
```js
{
  "logout": "Logout",
  "back": "Back",
  "examples": "Menu",
  "home": "Home",
  "web": "Web",
  "enterprise": "Enterprise",
  "extra": "Resources",
  "about": "About",
  "settings": "Settings",
  "help": "Help",
  "support": "Support",
  "topics": "Topics",
  "appExitMsg": "Are you sure you want to quit the application?"
}
``` 

Además, un archivo de recursos también se debe ajustar a estas directrices:
* Cada clave puede tener un máximo de 255 caracteres.
* Cada valor puede tener un máximo de 8191 caracteres.
* Cada paquete puede tener un máximo de 500 pares clave/valor.


## Traducción de un paquete
{: #globalizationpipeline_translatingabundle}

Solo se traducirán los archivos de recursos subidos. Puede subir un archivo de recursos al [crear un paquete](index.html#globalizationpipeline_creatingbundles) o al [modificar con detalles del paquete](bundles.html#globalizationpipeline_modifyingbundles).

Después de subir un archivo de recursos, puede traducir su contenido a cualquiera de los idiomas proporcionados por el motor de traducción automática predeterminado. Opcionalmente, puede elegir un motor de traducción automática alternativo tal como se describe en la sección [Configuración de la traducción automática](managing_translations.html#globalizationpipeline_service_to_service). El motor predeterminado da soporte a los siguientes idiomas de destino

<table>
<thead>
<tr>
<th>Idiomas de destino</th>
</tr>
</thead>
<tbody>
<tr>
<td>Chino (simplificado)</td>
</tr>
<tr>
<td>Chino (tradicional)</td>
</tr>
<tr>
<td>Francés</td>
</tr>
<tr>
<td>Alemán</td>
</tr>
<tr>
<td>Italiano</td>
</tr>
<tr>
<td>Japonés</td>
</tr>
<tr>
<td>Coreano</td>
</tr>
<tr>
<td>Portugués (de Brasil)</td>
</tr>
<tr>
<td>Español</td>
</tr>
</tbody>
</table>

**Nota:** El motor de traducción automática predeterminado de {{site.data.keyword.GlobalizationPipeline_short}} solo proporciona soporte para inglés como idioma de origen. Sin embargo, los motores de traducción automática alternativos disponibles para configurar dentro de {{site.data.keyword.GlobalizationPipeline_short}} dan soporte a la traducción de otras combinaciones de idiomas distintas del inglés.

A medida que cree paquetes, estos se irán añadiendo al separador **Paquetes** para que sean fácilmente accesibles. Desde allí, se pueden realizar tareas adicionales en las traducciones.


## Selección de un paquete con el que trabajar
{: #globalizationpipeline_selectingabundle}

1. Pulse el separador **Paquetes** para ver todos los paquetes que ha creado.
2. Pulse un **ID de paquete** de la lista para ver más detalles acerca de dicho paquete, o pulse el icono **Ver el detalle de paquetes** ![Seleccione el icono Ver el detalle de paquetes para abrir un paquete y trabajar con sus traducciones](images/viewProjectDetailIcon.png) en la columna Acciones.

![Ver todos los paquetes disponibles desde el separador Paquetes.](images/translationBundles.png)

Después de seleccionar un paquete con el que trabajar, puede ver el estado de sus traducciones, añadir o eliminar idiomas, editar las traducciones o proporcionar actualizaciones para el archivo de recursos.

Si ya no necesita un paquete, puede suprimirlo desde el separador **Paquetes**. Todas las traducciones asociadas con el paquete también se suprimirán.

## Modificación de detalles de paquetes
{: #globalizationpipeline_modifyingbundles}

Cuando abra un paquete, puede ver todos los detalles sobre el mismo. Todos los idiomas de destino que se encuentran en el paquete están enumerados, junto con el estado de traducción actual para cada uno.

![La página de detalles de paquetes muestra información sobre un paquete y sus traducciones.](images/bundleDetails.png)

El estado para cada idioma del paquete puede ser En curso, Error o Traducido:

| Estado | Descripción |
|--------|-------------|
| En curso | La traducción automática aún está en curso. |
| Error | Se ha producido un error mientras que el archivo de recursos se estaba traduciendo al idioma de destino. |
| Traducido | La traducción al idioma de destino está completa. |

Puede actualizar el archivo de recursos que utiliza el paquete, añadir un idioma de destino a un paquete, suprimir un idioma de destino desde un paquete y descargar las traducciones generadas para un idioma de destino.

### Actualización del archivo de recursos utilizado por el paquete

1. Junto al idioma de origen, pulse el icono **Subir recursos** ![Seleccione este icono para subir un nuevo archivo de recursos](images/uploadIcon.png) en la columna Acciones.
2. Pulse **Examinar** y seleccione el nuevo archivo de recursos que se subirá.
3. Seleccione el tipo de archivo de recursos que está subiendo
 * Archivo Properties de Java
 * AMD I18N
 * JSON
4. Pulse **Actualizar** para subir el nuevo archivo de recursos.

Los pares clave/valor que se encuentran en el archivo de recursos nuevo o actualizado se sincronizarán con los valores que ya se han subido. Solo se traducirá el contenido que sea nuevo o modificado.

### Adición de un idioma de destino a un paquete

1. Pulse el botón **Añadir idioma**.
2. Se mostrarán todos los idiomas de destino disponibles. Seleccione los idiomas que desee añadir al paquete.

La traducción para los idiomas seleccionados comenzará inmediatamente.

### Supresión de un idioma de destino desde un paquete

Cuando se suprime un idioma de destino de un paquete, elimine el idioma de destino y todas las traducciones asociadas desde el proyecto. En la columna Acciones del idioma de destino que se va a eliminar, pulse el icono **Eliminar este idioma de destino** ![Seleccione el icono de papelera Eliminar este idioma de destino](images/trashIcon.png).

### Descarga de las traducciones generadas para un idioma de destino

{{site.data.keyword.GlobalizationPipeline_short}} proporciona varias formas de incorporar la traducción para un idioma de destino en la aplicación. Puede descargar la traducción como un archivo de recursos e incluirla en la compilación de la aplicación. También puede hacer referencia a la traducción de forma dinámica desde {{site.data.keyword.GlobalizationPipeline_short}} utilizando uno de los [SDK](https://github.com/IBM-Bluemix/gp-common) de código abierto. 

<!-- For information on {{site.data.keyword.GlobalizationPipeline_full}} SDKs, see <link>. -->

Para descargar la traducción como un archivo de recursos: 

1. En la columna **Acciones** del idioma de destino o de origen para descargar, pulse el icono **Descargar las traducciones** ![Seleccione el icono de descarga para descargar las claves de origen o las traducciones para un idioma de destino](images/downloadIcon.png).
2. Seleccione un formato de archivo.
3. Pulse **Descargar**.
