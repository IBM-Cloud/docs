---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-09"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

#Modificación de la aplicación de inicio a {{site.data.keyword.Bluemix_short}}
{: #modifying_starter_app}

Puede modificar la aplicación de inicio y luego volverla a desplegar en {{site.data.keyword.Bluemix_short}} para ver los resultados.{:shortdesc}


Una modificación sencilla consiste en aumentar o eliminar el límite de sucesos en la aplicación de inicio para que se ejecute más tiempo.

1. Abra app.js en un editor de texto o entorno de desarrollo.
2. Modifique la variable eventTarget o suprima esta línea para eliminar por completo el límite de sucesos.
	 <pre><code>var eventTarget = 100;</code></pre>
3. Si desea eliminar el límite de sucesos, también tiene que suprimir la siguiente sentencia if:
	 <pre><code>  
if (eventCount >= eventTarget) {
status_step[3] = "Completed";
		    console.log("\nSe ha alcanzado el recuento de sucesos de destino. El servicio de Geospatial Analytics se detendrá.\n");
callback(null, null);
		    } 
	</code></pre> 
4. Vuelva a desplegar la aplicación modificada en {{site.data.keyword.Bluemix_short}} con el mandato cf push.
	 <pre><code>  
	cf push myapp
	</code></pre>
5. Especifique el URL de la aplicación o "route" en el navegador o iníciela desde el panel de control de {{site.data.keyword.Bluemix_short}}.
