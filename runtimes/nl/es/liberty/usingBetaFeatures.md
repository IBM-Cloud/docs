---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Utilización de las características beta
{: #using_beta_features}

*Última actualización: 10 de junio de 2016*
{: .last-updated}

Las funciones beta de Liberty proporcionan un acceso previo a las nuevas funciones y modelos de programación que quizás se incluyan en un futuro release de Liberty. La mayoría de las funciones beta también se pueden utilizar en las aplicaciones desplegadas en Bluemix.

**Importante**: Las funciones beta están pensadas para entornos de desarrollo y prueba y no se deben utilizar en producción. Para ver las condiciones de uso completas, consulte el [ acuerdo de licencia beta ](http://public.dhe.ibm.com/ibmdl/export/pub/software/websphere/wasdev/downloads/wlp/beta/lafiles/en.html).

Características beta de Liberty disponibles en Bluemix
<table>
<tr>
<th align="left">Característica</th>
<th align="left">Característica</th>
<th align="left">Característica</th>
<th align="left">Característica</th>
</tr>

<tr>
<td>bluemixLogCollector-1.1</td>
<td>cloudant-1.0</td>
<td>httpWhiteboard-1.0</td>
<td>logstashCollector-1.1</td>
</tr>

<tr>
<td>osgiBundle-1.0</td>
<td>passwordUtilities-1.0</td>
<td></td>
<td></td>
<td></td>
</tr>

</table>

Para poder utilizar las funciones beta de Liberty en Bluemix, debe hacer lo siguiente:

1. [Desplegar un directorio del servidor o un servidor empaquetado](optionsForPushing.html) con una o varias funciones beta habilitadas en el archivo server.xml como en el ejemplo siguiente:
```
    <server>
        <featureManager>
            <feature>jsp-2.3</feature>
            <feature>passwordUtilities-1.0</feature>
        </featureManager>
    </server>
```
{: #codeblock}

2.  Establezca la variable de entorno **IBM_LIBERTY_BETA** en **true**. Esta variable indica al paquete de compilación de Liberty que instale y habilite las funciones beta para la aplicación.  Por ejemplo:
  * utilizando la herramienta de línea de mandatos cf:
```
       $ cf set-env <nombre_aplicación> IBM_LIBERTY_BETA true
```
{: #codeblock}

  * o bien, utilizando el archivo manifest.yml:
```
      env:
          IBM_LIBERTY_BETA: "true"
```

3. Establezca la variable de entorno **JBP_CONFIG_LIBERTY** en **"version: +"**. Esta variable habilita el [tiempo de ejecución beta de Liberty](buildpackDefaults.html#liberty_versions) que da soporte a funciones beta. Por ejemplo:
  * utilizando la herramienta de línea de mandatos cf:
```
       $ cf set-env <yourappname> JBP_CONFIG_LIBERTY "version: +"
```
{: #codeblock}

  * o bien, utilizando el archivo manifest.yml:
```
      env:
          JBP_CONFIG_LIBERTY: "version: +"
```

Si está habilitando funciones beta en una aplicación existente, no olvide volver a transferir la aplicación después de establecer las variables de entorno. 

{: #codeblock}

# rellinks
{: #rellinks}
## general
{: #general}
* [Tiempo de ejecución de Liberty](index.html)
* [Visión general del perfil de Liberty](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
