---

 

copyright:

  years: 2015, 2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:download: .download}

# Empezar a escribir código con Git
*Última actualización: 2 de marzo de 2016*  

Puede crear un repositorio
Git alojado que se desplegará automáticamente en {{site.data.keyword.Bluemix}}. A continuación, puede modificar el código que se ejecuta en la app enviando los cambios al repositorio Git. 
{:shortdesc}

1. Para empezar, en la página de visión general de la app, pulse **Añadir repositorio Git y conducto**, o en
{{site.data.keyword.Bluemix_notm}} Classic Experience, pulse **ADD GIT**. 
2. En la ventana que se abre, asegúrese de que el recuadro de selección **Rellenar el repositorio con el paquete de apps del iniciador y habilitar el conducto (Build & Deploy)** está marcado. Se crea el repositorio Git. Si el código del iniciador está disponible,
se carga en el repositorio. Además, el servicio de Delivery Pipeline que se ejecuta en {{site.data.keyword.jazzhub}} despliega la app.  
3. Para actualizar la app puede utilizar la línea de mandatos o Web IDE.  
   **Si utiliza la línea de mandatos:**
   a. Clone el repositorio Git desde el URL de Git en la página Visión general de la app.  
   b. En su editor favorito, actualice el código.  
   c. En la interfaz de línea de mandatos de Git, envíe los cambios.  
	    
   **Si utiliza Web IDE:**  
   a. En la página Visión general de la app, pulse **Editar código**. El proyecto se abrirá en Web IDE.  
   b. Realice los cambios necesarios y, a continuación, envíelos con el soporte Git integrado.  
		
La app actualizada se vuelve a desplegar para {{site.data.keyword.Bluemix_notm}}.  

Para ver instrucciones paso a paso, consulte [Configuración de la integración de Git y despliegue automático en DevOps Services](https://hub.jazz.net/tutorials/jazzeditor/#git_integration_and_autodeployment).  

## ¿Ha añadido Git? Pruebe {{site.data.keyword.Bluemix_notm}} Live Sync  

Si va a crear una app Node.js, puede utilizar {{site.data.keyword.Bluemix_notm}} Live Sync para actualizar rápidamente la instancia de la app en {{site.data.keyword.Bluemix_notm}} y desarrollarla como lo haría en el escritorio.  

Para obtener más información sobre {{site.data.keyword.Bluemix_notm}} Live Sync, consulte [{{site.data.keyword.Bluemix_notm}} Live Sync](../develop/bluemixlive.html). Para obtener más detalles sobre los mandatos, consulte la documentación de la CLI de [{{site.data.keyword.Bluemix_notm}} Live Sync](../cli/reference/bl/index.html). Para utilizar {{site.data.keyword.Bluemix_notm}} Live Sync con Web IDE, consulte [Edición en directo](../develop/bluemixlive.html).  

1. Descargue e instale la línea de mandatos bl de {{site.data.keyword.Bluemix_notm}} Live Sync. 

<p>
<a class="xref" href="http://livesyncdownload.ng.bluemix.net/downloads/blive_setup.msi" target="_blank" title="(se abre en un separador o ventana nueva)"><img class="image" src="images/bl_gs_icons_windows_b.svg" alt="Botón Descargar la línea de mandatos bl de Windows" /> </a> <a class="xref" href="http://livesyncdownload.ng.bluemix.net/downloads/BluemixLive.pkg" target="_blank" title="(se abre en un separador o ventana nueva)"><img class="image" src="images/bl_gs_icons_mac-osx_b.svg" alt="Botón Descargar la línea de mandatos bl de Mac" /> </a>
</p>

**Importante:** La herramienta de línea de mandatos bl solo está disponible para Windows 7 y 8 y Mac OS X versión 10.9 o posterior. 

2. En una línea de mandatos, inicie sesión con el mandato siguiente. Se le solicitará su ID y contraseña de IBM®. 
```
bl login
```

3. Consulte la lista de proyectos disponibles para sincronizar {{site.data.keyword.Bluemix_notm}} Live Sync introduciendo el siguiente mandato: 
```
bl projects
```
Busque el nombre de proyecto en la lista que coincida con la app. El nombre del proyecto tiene el formato de su *alias* | *nombre app*. 

4. Sincronice el entorno local con el proyecto en {{site.data.keyword.Bluemix_notm}} especificando
el siguiente mandato. Si es el propietario del proyecto, solo debe especificar nombre-app para nombreProyecto. 
<!--- this command needs italicized parameters projectName localDirectory and yellow on 'local' -->
```
bl sync nombre_proyecto -d directorio_local --verbose
```
Este mandato seguirá ejecutándose (y la sincronización continuará) hasta que se especifique una "q". La opción --verbose muestra la información de estado e inicio de sesión. Si alguno de los argumentos contiene un espacio,
deberá escribir el nombre entre comillas. 

5. En otra ventana de la línea de mandatos del directorio local,
despliegue la app en {{site.data.keyword.Bluemix_notm}} en la
modalidad de edición en directo especificando el siguiente mandato:
```
bl start
```  

Cuando cambie los archivos en su directorio local, los cambios
se propagarán automáticamente en la app que se ejecuta
en {{site.data.keyword.Bluemix_notm}} y
en el espacio de trabajo de la nube del proyecto. Si tiene que reiniciar la app Node
puede utilizar el siguiente mandato:
```
bl start --restart 
```
